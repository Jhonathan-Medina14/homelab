# 01 — Planificación y Hardware

> Fase: **diseño previo a la instalación** · Estado: ✅ completado
> Fecha de redacción: 2026-09-17

## 1. Contexto y motivación

Quería un entorno donde pudiera autoalojar mis servicios personales (fotos, contraseñas, documentos) y del negocio (página web, contabilidad), sin depender de suscripciones en la nube y con control total sobre mis datos. La solución: convertir un mini PC en un servidor de virtualización con Proxmox VE.

Criterios de selección del equipo:
- **Consumo eléctrico bajo** (mini PC 24/7 vs. PC tradicional).
- **Potencia suficiente** para varias VMs simultáneas con margen de crecimiento.
- **Dos puertos Ethernet 2.5GbE** para segmentación futura de red.
- **Precio accesible** frente a un servidor usado (consumo y ruido).

## 2. Verificación de hardware

Inventario validado sobre el equipo real (salida de `systeminfo` en Windows 11 Pro):

```yaml
hardware:
  equipo: GMKtec M5 Ultra
  cpu: AMD Ryzen AI Max+ 395 (Family 25, Model 80)
  nucleos_fisicos: 16
  hilos: 32
  ram_total: 32 GB
  slots_m2: 2 (NVMe) — 1 ocupado con Windows 11 Pro
  red:
    ethernet: 2x Realtek 2.5GbE
    wifi: RZ616 Wi-Fi 6E (reservado para clientes/guests, nunca para el host)
  bios: M5 Ultra 1.06 — SVM (virtualización AMD) ya activo
```

**Lección aprendida**: antes de comprar o instalar nada, verifiqué la compatibilidad con las herramientas del sistema (`systeminfo`, BIOS). La virtualización (SVM) ya venía activa, lo que evitó un paso extra.

## 3. Riesgo identificado: licencia Windows OEM

El equipo trae Windows 11 Pro con licencia **OEM digital vinculada al hardware**. Al instalar Proxmox, Windows se borra.

**Mitigación (Fase 0):**
- Vincular la licencia a una cuenta Microsoft *antes* de tocar el disco.
- Crear USB de recuperación de Windows 11.
- Respaldar el informe de sistema y exportar drivers.
- (Nota: si en el futuro virtualizo Windows, la reactivación de una licencia OEM puede requerir atención especial por estar ligada al hardware físico.)

## 4. Presupuesto de recursos

Con 16 núcleos físicos y 32 GB de RAM, distribuí los recursos de forma **conservadora (ratio 1:1 en vCPUs, sin overcommit inicial)**:

| Máquina | vCPU | RAM | Rol |
|---|---|---|---|
| Proxmox host | — | ~4 GB (reserva) | Solo orquestación |
| VM Principal | 8 | 12 GB (ballooning min 8) | Servicios privados: Immich, Vaultwarden, Portainer |
| VM Expuesta | 2 | 4 GB | Todo lo que toca Internet: NPM, sitio web |
| VM Pruebas/IA/Monitoreo | 6 | 8 GB (ballooning min 6) | Grafana, Zabbix, experimentos IA |
| **Total asignado** | **16** | **28 GB máx.** | Margen ~4 GB para ZFS ARC y picos |

**Decisiones técnicas y su porqué:**
- `cpu_type: host` en todas las VMs → expone instrucciones AVX del Ryzen necesarias para cargas de IA.
- Ballooning en VMs grandes → la RAM se devuelve al host cuando no se usa.
- `qemu-guest-agent` obligatorio en todas las VMs → apagado limpio y ballooning funcional.
- Si más adelante el uso es ligero, se puede elevar la VM principal a 12 vCPUs.

## 5. Plan de red y acceso

```yaml
red:
  ip_lan_host: 192.168.1.10 (estática / DHCP reservado)
  admin_proxmox: https://192.168.1.10:8006 (solo LAN + Tailscale)
  acceso_remoto: Tailscale en cada VM — sin abrir puertos de servicios privados
  exposicion_publica: solo 80/443 → VM expuesta (NPM + Let's Encrypt)
```

**Regla de seguridad fijada**: Vaultwarden e Immich nunca se exponen directamente a Internet; acceso solo vía VPN (Tailscale) o reverse proxy endurecido.

## 6. Decisiones de diseño registradas

| Decisión | Elección | Alternativa descartada | Motivo |
|---|---|---|---|
| Hipervisor | Proxmox VE | VMware ESXi, Hyper-V | Open source, comunidad, familiaridad |
| SO de las VMs | Debian 12 / Ubuntu Server (sin GUI) | Con escritorio | Menor consumo, enfoque servidor |
| Acceso remoto | Tailscale (VPN mesh) | Abrir puertos en el router | Seguridad, sin configuración de NAT |
| Exposición pública | VM dedicada + NPM + SSL | Exponer servicios privados | Aislamiento de la superficie de ataque |
| Almacenamiento de VMs | NVMe interno | Disco USB externo | Latencia y fiabilidad (el USB es solo para backups) |

## 7. Compras planeadas

| Prioridad | Ítem | Uso |
|---|---|---|
| 1 | SSD NVMe interno 512 GB | Segundo datastore (crecimiento) |
| 2 | Disco externo USB 1 TB | Backups (vzdump + pg_dump) |

## 8. Próximos pasos

- [ ] Ejecutar Fase 0 (respaldo de Windows y licencia)
- [ ] Ejecutar Fase 1 (prueba en vivo de Proxmox desde USB, sin tocar el disco)
- [ ] Documentar la Fase 2 en `docs/02-instalacion-proxmox.md`

---

*Principio rector: la VM es la frontera de aislamiento; el hipervisor solo orquesta.*

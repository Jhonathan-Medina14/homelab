# 02 — Instalación y post-instalación de Proxmox VE

> Fase: **1-2** · Estado: ⬜ Pendiente
> Fecha de ejecución: *(pendiente)*

## 1. Resumen de la fase

*(En 2-3 líneas: qué se hizo en esta fase y qué validó el resultado.)*

## 2. Preparación (Fase 0 — respaldo de Windows)

| Tarea | Estado | Notas |
|---|---|---|
| Licencia Windows vinculada a cuenta Microsoft | ⬜ | |
| USB de recuperación de Windows 11 creado | ⬜ | |
| Drivers exportados (Double Driver) | ⬜ | Opcional |
| Product ID anotado y systeminfo respaldado | ⬜ | Guardar en lugar seguro, NO subir al repo |

**Lección aprendida:** *(¿algo salió distinto a lo esperado?)*

## 3. Prueba en vivo desde USB (Fase 1)

- ISO utilizada: Proxmox VE ___ (enlace a la versión)
- Herramienta de booteo: balenaEtcher
- Resultados de la verificación en vivo:
  - [ ] Ambos NVMe reconocidos
  - [ ] Red 2.5GbE funcional (ping al router)
  - [ ] RAM completa visible (32 GB)
- Decisión: ¿proceder con la instalación? ¿Por qué?

## 4. Instalación de Proxmox (Fase 2)

### 4.1 Configuración de BIOS previa
- SVM: activo (confirmado)
- Memory Integrity / Credential Guard: *(estado y motivo)*

### 4.2 Instalación
- Sistema de archivos elegido: *(ext4 / ZFS — y por qué)*
- IP estática: 192.168.1.10/24 · Gateway: 192.168.1.1 · DNS: ___
- Capturas de pantalla: *(subir a assets/)*

### 4.3 Post-instalación (comandos y resultados)

```bash
# Cambiar repositorios a no-subscription
# (documentar comandos ejecutados)

# Actualización del sistema
apt update && apt dist-upgrade -y
```

- [ ] Repositorio enterprise deshabilitado + no-subscription agregado
- [ ] Sistema actualizado
- [ ] Usuario admin no-root creado
- [ ] Almacenamiento local-zfs (o ext4) configurado
- [ ] NTP y zona horaria configurados (America/Bogota)

## 5. Problemas encontrados y cómo se resolvieron

*(Este es el apartado más valioso del documento. Formato sugerido:)*

| # | Síntoma | Causa | Solución | Tiempo invertido |
|---|---|---|---|---|
| 1 | | | | |

## 6. Estado al cierre de la fase

- Acceso a la interfaz web: https://192.168.1.10:8006 ✅/❌
- Próxima fase: VM Principal → `docs/03-vm-principal.md`

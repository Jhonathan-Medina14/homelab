# HomeLab — GMKtec M5 Ultra

Proyecto personal de infraestructura de laboratorio casero sobre **Proxmox VE**, orientado al autoalojamiento de servicios, aprendizaje de virtualización, redes, Docker y despliegue seguro de aplicaciones web.

> Documentación viva: cada fase, decisión técnica y problema resuelto queda registrado aquí como evidencia de aprendizaje y portafolio profesional.

---

## Objetivo

Construir desde cero un entorno de producción casero que autoaloje mis servicios personales y del negocio, aplicando buenas prácticas de arquitectura, seguridad y operación:

- **Privacidad**: reemplazar servicios en la nube (Google Fotos, gestores de contraseñas) por alternativas autoalojadas.
- **Aprendizaje**: dominar Proxmox, redes, Docker, reverse proxy, SSL, monitoreo y backups.
- **Demostrable**: documentar todo el proceso para evidenciar habilidades en IT.

## Servicios objetivo

| Servicio | Propósito |
|---|---|
| Immich | Google Fotos privado (requiere Postgres + Redis) |
| Vaultwarden | Gestor de contraseñas |
| Stirling PDF | Editor/convertidor PDF ligero |
| Nginx Proxy Manager | Reverse proxy + certificados SSL (Let's Encrypt) |
| Sitio web del negocio | Exposición pública controlada |
| Grafana + Prometheus | Monitoreo de infraestructura |
| Tailscale | Acceso remoto privado sin abrir puertos |

## Arquitectura (resumen)

```
                    Internet (solo 80/443)
                          │
                   ┌──────▼──────┐
                   │ VM Expuesta │  2 vCPU / 4 GB — Debian 12 minimal
                   │   (NPM)     │  Página web del negocio + SSL
                   └──────┬──────┘
                          │
        ┌─────────────────┼──────────────────┐
        │                 │                  │
 ┌──────▼──────┐   ┌──────▼──────┐    ┌──────▼──────┐
 │ VM Principal │   │ VM Pruebas  │    │  Tailscale  │
 │ 12 GB/8 vCPU │   │ 8 GB/6 vCPU │    │  (acceso    │
 │ Immich,      │   │ IA, Grafana │    │  remoto en  │
 │ Vaultwarden, │   │ Zabbix      │    │  todas las  │
 │ Portainer    │   │             │    │  VMs)       │
 └─────────────┘   └─────────────┘    └─────────────┘
                          │
              ┌───────────▼───────────┐
              │  Proxmox VE 8.x host  │  Reserva ~4 GB
              │  (solo orquesta)      │
              └───────────────────────┘
```

**Reglas de arquitectura adoptadas:**
- La VM es la frontera de aislamiento; el contenedor es la unidad de aplicación.
- El hipervisor nunca corre aplicaciones, solo orquesta.
- Solo la VM expuesta toca Internet (puertos 80/443). Nada privado se expone sin VPN o reverse proxy endurecido.

## Hardware base

- **Equipo**: GMKtec M5 Ultra (mini PC)
- **CPU**: AMD Ryzen AI Max+ 395 — 16 núcleos / 32 hilos
- **RAM**: 32 GB
- **Red**: 2× Ethernet 2.5GbE (el host siempre por cable; Wi-Fi solo para clientes)
- **Almacenamiento**: 1 NVMe interno (Windows 11 Pro actualmente) + segundo NVMe 512 GB (planeado) + disco externo USB 1 TB para backups (en compra)

## Estado del proyecto

| Fase | Descripción | Estado |
|---|---|---|
| 0 | Respaldo de Windows 11 + licencia | ⬜ Pendiente |
| 1 | Prueba en vivo de Proxmox (sin tocar disco) | ⬜ Pendiente |
| 2 | Instalación y post-instalación de Proxmox | ⬜ Pendiente |
| 3 | VM Principal (12 GB / 8 vCPU) + servicios core | ⬜ Pendiente |
| 4 | VM Expuesta (4 GB / 2 vCPU) + acceso público | ⬜ Pendiente |
| 5 | VM Pruebas / IA / Monitoreo (8 GB / 6 vCPU) | ⬜ Pendiente |
| 6 | Backups y operación continua | ⬜ Pendiente |

## Documentación

- [docs/01-planificacion-y-hardware.md](docs/01-planificacion-y-hardware.md) — Decisión del hardware, justificación de recursos y plan de red
- `docs/02-instalacion-proxmox.md` — *(próximamente)*
- `docs/03-vm-principal.md` — *(próximamente)*
- `docs/04-vm-expuesta.md` — *(próximamente)*
- `docs/05-vm-pruebas-y-monitoreo.md` — *(próximamente)*
- `docs/06-backups.md` — *(próximamente)*
- `docs/07-problemas-y-soluciones.md` — *(bitácora de errores y aprendizajes)*

## Lo aprendido hasta ahora

- Diseño de arquitectura de VMs con presupuesto de recursos (ratio 1:1 de vCPUs sin overcommit).
- Principios de segmentación de red y exposición mínima a Internet.
- *(Se irá completando con cada fase)*

---

*Zona horaria: UTC-5 · Documentación en español — English summary available on request.*

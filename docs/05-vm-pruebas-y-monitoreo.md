# 05 — VM Pruebas / IA / Monitoreo

> Fase: **5** · Estado: ⬜ Pendiente
> Fecha de ejecución: *(pendiente)*

## 1. Resumen de la fase

*(Objetivo: zona de experimentos con dominio de fallo separado — romper aquí nunca afecta las VMs de producción.)*

## 2. Configuración de la VM

| Parámetro | Valor |
|---|---|
| SO | Debian 12 / Ubuntu Server |
| vCPU | 6 (cpu_type: host) |
| RAM | 8 GB (ballooning: min 6 / max 8) |
| Disco | 100 GB |

## 3. Stack de monitoreo

**Ruta elegida:** *(Grafana + Prometheus + node_exporter — ligera / Zabbix — completa. Documentar por qué se eligió una.)*

### 3.1 Despliegue

- [ ] Stack de monitoreo levantado con Compose
- [ ] node_exporter instalado en las 3 VMs (y PVE exporter en el host, si aplica)
- [ ] Grafana accesible (puerto 3000) vía Tailscale

### 3.2 Dashboards

- [ ] Dashboard de CPU/RAM/disco de las VMs
- [ ] Dashboard del host Proxmox
- Capturas: *(subir a assets/)*

## 4. Experimentos de IA

- Modelo/herramienta probada: ___
- Consumo de RAM real observado: ___
- Limitación encontrada: *(8 GB compartidos con monitoreo limitan modelos grandes — documentar)*
- Estado: ⬜

## 5. Problemas encontrados y cómo se resolvieron

| # | Síntoma | Causa | Solución | Tiempo invertido |
|---|---|---|---|---|
| 1 | | | | |

## 6. Lo aprendido en esta fase

*(Conceptos: métricas, exporters, dashboards, observabilidad, límites de recursos para IA local.)*

## 7. Próxima fase

Backups y operación continua → `docs/06-backups.md`

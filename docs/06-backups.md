# 06 — Backups y operación continua

> Fase: **6** · Estado: ⬜ Pendiente
> Fecha de ejecución: *(pendiente)*
> Dependencia: disco externo USB comprado e identificado

## 1. Resumen de la fase

*(Objetivo: garantizar que cualquier fallo — disco, VM corrupta, error humano — sea recuperable. Un backup no probado no existe.)*

## 2. Preparación del disco externo

- Disco: ___ (capacidad, modelo)
- Identificación en el host: `/dev/sdX` *(documentar cómo se verificó que NO es un NVMe — `lsblk`)*
- Formato: ext4/xfs con etiqueta `backups`
- Punto de montaje: ___
- [ ] Montaje persistente configurado (fstab, con nofail)

## 3. Estrategia de backups

**Opción elegida:** *(A: vzdump programado directo al externo / B: Proxmox Backup Server)*

### 3.1 Backups de VMs (vzdump)

- Frecuencia: semanal + antes de cualquier cambio grande
- VMs incluidas: principal / expuesta / pruebas
- Retención: ___
- Horario programado: ___

```bash
# Comandos de configuración (Datacenter → Backup o cron)
```

### 3.2 Backup de datos de Immich

- Fotos: volumen copiado al externo (ruta destino: ___)
- Base de datos: `pg_dump` periódico al externo
- Frecuencia: ___

## 4. Prueba de restauración REAL

> Esta es la parte más importante de todo el documento.

- [ ] VM de prueba restaurada en almacenamiento temporal
- [ ] Arranque verificado
- [ ] Servicio dentro de la VM verificado
- Fecha de la prueba: ___
- Tiempo total de restauración: ___
- Lecciones: *(¿qué mejorar del proceso?)*

## 5. Documentación operativa

*(Registrar aquí, sin secretos: puertos, volúmenes, rutas. Las credenciales van en la bóveda de contraseñas, no en este repo.)*

## 6. Rutina mensual de mantenimiento

- [ ] `apt update && apt upgrade` en host y las 3 VMs
- [ ] Revisión SMART de discos
- [ ] Verificación de espacio en disco de backups
- [ ] Revisión de logs y alertas de Grafana/Zabbix

## 7. Problemas encontrados y cómo se resolvieron

| # | Síntoma | Causa | Solución | Tiempo invertido |
|---|---|---|---|---|
| 1 | | | | |

## 8. Lo aprendido en esta fase

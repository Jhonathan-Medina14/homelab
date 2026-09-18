# 03 — VM Principal: servicios privados internos

> Fase: **3** · Estado: ⬜ Pendiente
> Fecha de ejecución: *(pendiente)*

## 1. Resumen de la fase

*(Qué se desplegó en esta VM y para qué sirve en el ecosistema del HomeLab.)*

## 2. Configuración de la VM

| Parámetro | Valor |
|---|---|
| SO | Debian 12 netinst / Ubuntu Server 24.04 |
| vCPU | 8 (cpu_type: host) |
| RAM | 12 GB (ballooning: min 8 / max 12) |
| Disco | ___ GB |
| Red | vmbr0 |

**Justificación de la configuración:** *(¿por qué estos valores? Referenciar el presupuesto de recursos del doc 01.)*

## 3. Instalación del SO base

- [ ] SO instalado sin entorno gráfico
- [ ] qemu-guest-agent instalado y funcionando
- [ ] Red configurada (IP: ___, gateway, DNS)
- [ ] Acceso SSH funcionando (por Tailscale, no por LAN si es posible)

## 4. Docker y gestión

```bash
# Documentar comandos exactos ejecutados (instalación de Docker, plugin compose)
```

- [ ] Docker + Compose instalados
- [ ] Portainer CE levantado (puerto 9000)
- [ ] Tailscale instalado y la VM unida a la tailnet

## 5. Servicios desplegados

### 5.1 Vaultwarden
- Imagen: `vaultwarden/server:latest`
- Puerto host: 8222
- Configuración relevante: *(volúmenes, variables de entorno)*
- Estado: ⬜

### 5.2 Stirling PDF
- Imagen: `frooodle/s-pdf:latest`
- Puerto host: 8080
- Estado: ⬜

### 5.3 Immich (compose: app + ml + redis + postgres)
- Puerto host: 2283
- Estructura del compose: *(pegar docker-compose.yml clave o enlazarlo)*
- Volúmenes de datos separados del sistema: *(rutas de fotos y DB)*
- Estado: ⬜

### 5.4 App de contabilidad
- Stack elegido: ___
- Estado: ⬜

## 6. Pruebas de funcionamiento

*(Cómo verificaste que cada servicio funciona: acceso desde la LAN, desde Tailscale, subida de una foto de prueba a Immich, creación de una entrada en Vaultwarden, etc.)*

## 7. Problemas encontrados y cómo se resolvieron

| # | Síntoma | Causa | Solución | Tiempo invertido |
|---|---|---|---|---|
| 1 | | | | |

## 8. Lo aprendido en esta fase

*(Conceptos nuevos dominados: redes de Docker, volúmenes, compose, etc.)*

## 9. Próxima fase

VM Expuesta → `docs/04-vm-expuesta.md`

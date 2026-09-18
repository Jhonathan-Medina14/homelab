# 04 — VM Expuesta: acceso público seguro

> Fase: **4** · Estado: ⬜ Pendiente
> Fecha de ejecución: *(pendiente)*

## 1. Resumen de la fase

*(Objetivo: exponer SOLO lo necesario a Internet — la página web del negocio — manteniendo todo lo privado aislado.)*

## 2. Configuración de la VM

| Parámetro | Valor |
|---|---|
| SO | Debian 12 minimal |
| vCPU | 2 (cpu_type: host) |
| RAM | 4 GB |
| Disco | 40 GB |

## 3. Docker + Nginx Proxy Manager

- [ ] Docker + Compose instalados
- [ ] NPM levantado (puertos 80/443/81)
- [ ] Acceso a la interfaz web de NPM funcionando

## 4. Sitio web del negocio

- Stack elegido: *(nginx puro / según necesidad del sitio)*
- Contenedor: ___
- Dominio: *(documentar cuál, sin exponer credenciales)*
- Estado: ⬜

## 5. Exposición a Internet

- [ ] Redirección de puertos en el router: 80/443 → esta VM **únicamente**
- [ ] Certificado SSL con Let's Encrypt desde NPM
- [ ] Renovación automática del certificado verificada

## 6. Endurecimiento

- [ ] fail2ban instalado y configurado
- [ ] Actualizaciones automáticas de seguridad (unattended-upgrades)
- [ ] SSH solo con clave (acceso por contraseña deshabilitado)
- [ ] **Regla verificada: ningún servicio privado apunta a esta VM**

## 7. Pruebas de seguridad

*(Qué verificaste: ¿la IP del host responde en 8006 desde Internet? Debe dar timeout. ¿Acceso a servicios privados por dominio público? Debe fallar.)*

## 8. Problemas encontrados y cómo se resolvieron

| # | Síntoma | Causa | Solución | Tiempo invertido |
|---|---|---|---|---|
| 1 | | | | |

## 9. Lo aprendido en esta fase

*(Conceptos: reverse proxy, DNS, certificados TLS, superficie de ataque, hardening básico.)*

## 10. Próxima fase

VM Pruebas / IA / Monitoreo → `docs/05-vm-pruebas-y-monitoreo.md`

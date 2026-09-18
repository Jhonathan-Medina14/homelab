# 07 — Bitácora de problemas y soluciones

> Documento transversal: aquí se consolidan los errores más relevantes de todo el proyecto, con fecha y contexto. En una entrevista, esta es la evidencia de capacidad de diagnóstico.

*(Reglas del documento: 1 síntoma = 1 entrada. Incluir el error exacto, no solo "no funcionaba". Orden cronológico, más reciente arriba.)*

---

## Plantilla de entrada

```
### [FECHA] — Título corto del problema
- **Contexto:** en qué fase/servicio ocurría
- **Síntoma:** mensaje de error exacto o comportamiento observado
- **Diagnóstico:** cómo se aisló la causa (comandos, logs consultados)
- **Causa raíz:** qué era realmente
- **Solución:** pasos exactos aplicados
- **Prevención:** qué se hizo/hará para que no se repita
- **Tiempo de resolución:** ___
```

---

## Entradas

### [AAAA-MM-DD] — (ejemplo) Docker no arrancaba tras reiniciar la VM
- **Contexto:** Fase 3, VM Principal
- **Síntoma:** `Failed to start docker.service`
- **Diagnóstico:** `journalctl -u docker` mostró...
- **Causa raíz:** ...
- **Solución:** ...
- **Prevención:** ...
- **Tiempo de resolución:** 45 min

---

*(Añadir nuevas entradas arriba de esta línea)*

# Seguimiento del proyecto: entrenador de maratón con Claude + Garmin

**Objetivo:** Maratón de Badajoz (marzo 2027) en 3h30, con Claude como entrenador. Lee mis datos de Garmin a través de Intervals.icu y sube los entrenamientos a mi fenix 7.

**Plan publicado:** [juanruizrodrig.github.io/plan-maraton](https://juanruizrodrig.github.io/plan-maraton/)

**Última actualización:** 17 nov 2026

```
Reloj Garmin ⇄ Garmin Connect ⇄ Intervals.icu ⇄ Servidor MCP (Cloudflare) ⇄ Claude (claude.ai)
```

---

## Estado general

| Pieza | Estado |
|---|---|
| Servidor MCP en Cloudflare | ✅ Funcionando |
| Conector "Garmin Coach" en claude.ai | ✅ Conectado |
| Leer actividades | ✅ Probado |
| Crear y borrar entrenamientos hasta el reloj | ✅ Probado de punta a punta |
| Datos de salud (HRV, sueño, FC en reposo) | ✅ Llegan desde el 16–17 nov 2026 (HRV, FC en reposo, sueño, VO2máx) |
| Conector usable también desde Claude Code | ✅ Comprobado el 17 nov |
| Página del plan en el móvil | ✅ Publicada |
| Recordatorio de la revisión del domingo | ✅ Evento el 22 nov a las 21:00 en Google Calendar |
| Historial en Intervals.icu | ⏳ Compartido en Garmin el 17 nov. Revisado de nuevo ese día: solo 12 actividades, todas desde el 8 nov |
| Zonas de FC | ⚠️ FC máxima mal configurada (170) |
| Proyecto "Entrenador running" en claude.ai | ✅ Creado y configurado el 17 nov |

---

## Pendiente ahora (en orden)

### Intervals.icu
- [x] Activar la descarga de **wellness** (HRV, sueño, FC en reposo). Llega desde el 17 nov
- [x] Compartir los **datos históricos** de Garmin con Intervals.icu (17 nov)
- [ ] Comprobar que llega el historial anterior al 8 nov. Si no aparece en 24–48 h, seguir con E1
- [ ] Settings → Sports → Run: corregir la **FC máxima** y revisar zonas
- [ ] Dormir con el fenix puesto para que mida el HRV nocturno

### claude.ai
- [x] Crear el Proyecto **"Entrenador running"** y pegar las instrucciones (17 nov)
- [x] Subir al conocimiento del Proyecto el plan (`index.html`) y el documento **Bitácora**
- [x] Activar Garmin Coach en los chats del Proyecto y hacer el primer chat de prueba
- [ ] Primera **revisión semanal**: domingo 22 nov, 21:00 (evento en Google Calendar)

### Móvil
- [ ] Instalar la app **Claude** (Anthropic) e iniciar sesión
- [ ] Añadir la página del plan a la pantalla de inicio

### Con Claude Code (recomendado antes de usarlo a fondo)
- [ ] **E3: reducir lo que devuelve `getRecentActivities`.** Con solo 12 actividades ya devuelve ~53.000 caracteres. Al pedir 8–12 semanas en una revisión puede saturar la conversación

---

## Evolutivos (mejoras futuras)

| # | Mejora | Por qué | Estado |
|---|---|---|---|
| E1 | **Cargar mi historial de Garmin en Intervals.icu** a partir de la exportación completa de datos de Garmin | Con meses de historial, la forma y la fatiga (CTL/ATL), las zonas y el volumen habitual pasan a ser reales, y el plan se calibra mejor | 🟡 Exportación solicitada el 17 nov 2026. Falta recibirla y subir los archivos de actividades (FIT) a Intervals.icu |
| E2 | Herramienta `getActivityIntervals` en el servidor | Ver cada serie por separado, no solo la media de la sesión, para ajustar bien los ritmos | ⏳ Propuesta |
| E3 | Filtrar los campos que devuelve `getRecentActivities` | Poder analizar muchos meses sin saturar la conversación. Hoy 12 actividades ocupan ~53.000 caracteres | ⚠️ Recomendado pronto |
| E4 | Seguridad de la página de login del conector: XSS en `state` y límite de intentos | Riesgo bajo, pero conviene cerrarlo | ⏳ Opcional |
| E5 | Actualizar dependencias con avisos de seguridad (`agents`, MCP SDK) | 4 avisos altos que requieren subir de versión mayor | ⏳ Opcional |
| E6 | Casillas de completado sincronizadas entre dispositivos, o marcadas solas a partir de Intervals.icu | Hoy solo se guardan en el navegador del móvil | ⏳ Idea |

### E1: pasos previstos
1. Esperar el correo de Garmin con el enlace de descarga. Puede tardar días.
2. Descomprimir la exportación y localizar los archivos de actividades (`.fit`).
3. Subirlos a Intervals.icu desde la opción de subir archivos de actividades. Admite varios a la vez.
4. Comprobar en Intervals.icu que aparecen los meses antiguos y que la forma (CTL) ya no está cerca de 0.
5. Recalibrar el plan con Claude: *"Inicio de bloque: analiza mis últimas 12 semanas…"*.

---

## Rutina en marcha

| Cuándo | Dónde | Qué |
|---|---|---|
| Cada día | Reloj y esta página | Entrenar y marcar la casilla |
| Si no puedo un día | Proyecto en claude.ai | "Hoy [día] no puedo por [motivo]. Reajusta la semana" |
| Domingo, 21:00 (evento en Google Calendar) | Proyecto en claude.ai | "Revisión semanal", pegar el bloque en la Bitácora y aprobar la semana siguiente |
| Si cambian semanas futuras | Claude Code | Actualizar `index.html` y la página |

---

## Historial

| Fecha | Hito |
|---|---|
| 8 nov 2026 | Servidor MCP desplegado en Cloudflare y revisión de seguridad hecha |
| 8 nov 2026 | Cuestionario de perfil e instrucciones del Proyecto escritas |
| 16 nov 2026 | Plan de 17 semanas publicado en GitHub Pages, con tiempos estimados y descanso el sábado |
| 16 nov 2026 | Reglas de reajuste semanal y bitácora añadidas a las instrucciones |
| 16 nov 2026 | Nueva `MCP_PASSWORD` y conector Garmin Coach añadido en claude.ai |
| 16 nov 2026 | Probado de punta a punta: lectura, creación y borrado de entrenamientos hasta el fenix 7 |
| 16 nov 2026 | Primer análisis real: rodajes suaves demasiado rápidos y wellness vacío |
| 17 nov 2026 | Solicitada la exportación completa de datos de Garmin (evolutivo E1) |
| 17 nov 2026 | Compartidos los datos históricos de Garmin con Intervals.icu. El wellness ya llega (HRV 85, FC en reposo 41, sueño 6h36). El historial antiguo todavía no |
| 17 nov 2026 | Creado en Google Calendar el evento del domingo 22 nov (montar el Proyecto + primera revisión semanal) |
| 17 nov 2026 | Repaso de estado: el historial sigue sin llegar y E3 pasa a ser recomendado pronto |
| 17 nov 2026 | Proyecto "Entrenador running" creado en claude.ai, con instrucciones, conocimiento (plan y Bitácora) y conector |

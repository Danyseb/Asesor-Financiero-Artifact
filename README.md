# Asesor Financiero

Tablero personal de finanzas hecho como artefacto de Claude, más una skill del mismo asesor que verifica información en internet.

## Contenido

| Ruta | Qué es |
|---|---|
| `index.html` | El artefacto completo (una sola página, sin dependencias salvo Google Fonts). |
| `skill/asesor-financiero/SKILL.md` | La skill del asesor para el chat de Claude, con búsqueda web. |

## El tablero

Ocho secciones:

- **Resumen**: ingresos, gastos, ahorro neto, fondo de emergencia, ritmo de gasto por categoría, proyección al cierre y gráficas de 6 meses.
- **Movimientos**: captura rápida en lenguaje natural, importación de CSV con detección de duplicados y bandeja *Por revisar* que aprende reglas.
- **Metas**: ahorro necesario por mes y por quincena, retraso al ritmo real y propuesta de dónde sacar la diferencia.
- **Cuentas y pagos**: calendario de cortes y límites, alertas a 7 y 2 días.
- **Mi plan**: diagnóstico inicial, escalera de prioridades, dinero realmente invertible, reparto de ingresos extra y bitácora de decisiones.
- **Negocios**: margen, punto de equilibrio, tres escenarios, recuperación, ROI y validación.
- **Inversiones**: fichas con evaluación de 11 puntos, calculadora de posición y bitácora de operaciones.
- **Asesor**: chat que lee los datos del tablero.

Incluye switch de modo claro (blanco y azul) y oscuro (negro y naranja).

Además: editar categorías y presupuestos, buscador y filtros de movimientos, descarga en CSV, deshacer en todo lo que se borra, guía de primeros pasos y ayuda breve.

## Cómo funciona dentro de Claude

Publicado como artefacto, usa capacidades de la plataforma:

- `db` + `user`: guarda los datos en un espacio privado del dueño.
- `sample`: chat del asesor, captura rápida y categorización con IA.
- `downloads`: respaldo en `.json`.

Abierto fuera de Claude (por ejemplo, el archivo local en un navegador), arranca con datos de ejemplo y guarda solo en ese navegador; el chat y la IA no están disponibles.

## Cómo actualizarlo

1. Edita `index.html`.
2. Pídele a Claude que lo publique en el mismo artefacto (conserva el enlace y los datos).
3. Haz commit aquí para tener el historial.

## Robustez de los datos

- No guarda nada hasta que tus datos cargan bien; si la carga falla, muestra un error en vez del ejemplo.
- Migra automáticamente datos de versiones anteriores sin descartar registros.
- Detecta cambios hechos en otro dispositivo antes de guardar, para no sobrescribirlos.
- Solo reescribe las secciones que cambiaron; un año con muchos movimientos se reparte en varios documentos.

## Seguridad

- No guarda números completos de tarjeta: solo los últimos 4 dígitos.
- No hay llaves ni contraseñas en el código.
- Los análisis de inversión son educativos; no es asesoría financiera certificada.

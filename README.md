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
- **Inversiones**: registro de acciones (empresa, ticker validado, bolsa, en cartera o en observación, posición y ganancia/pérdida), análisis profesional técnico y fundamental con historial por acción, evaluación de 11 puntos, calculadora de posición y bitácora de operaciones.
- **Asesor**: chat que lee los datos del tablero.

Incluye switch de modo claro (blanco y azul) y oscuro (negro y naranja).

Además: editar categorías y presupuestos, buscador y filtros de movimientos, descarga en CSV, deshacer en todo lo que se borra, guía de primeros pasos y ayuda breve.

### Análisis de acciones

La página no puede buscar en internet, así que **Analizar** arma un bloque que empieza con "Contexto de mi tablero Asesor Financiero". Se pega en un chat con Claude (la skill `asesor-financiero` busca datos actuales con fuente y fecha) y la respuesta se pega de vuelta para guardarla. El tablero solo muestra precios que traen fuente y fecha, y nunca ejecuta ni simula órdenes.

### Monitor de oportunidades

Revisa todas las acciones contra un umbral de caída configurable por acción (por defecto −5 % contra el máximo de 30 días o el precio de compra). **Generar revisión** arma un bloque para el chat con Claude; la respuesta termina con una línea `MONITOR:` por acción que el tablero lee.

Regla principal: proteger el capital primero. El tablero aplica sus reglas encima del análisis y solo puede bajar un veredicto, nunca subirlo:

- Sin precio con fuente y hora → **Sin datos**.
- No cruzó el umbral o está subiendo → **Esperar**, con precio de reentrada.
- Cruzó por deterioro del negocio → **Evitar**.
- **Oportunidad** solo con caída sana, zona de entrada, stop y riesgo/beneficio de al menos 1:2; siempre muestra la pérdida si falla y el tamaño máximo (10 % de la cartera por defecto).

Incluye banner de oportunidades nuevas, historial de alertas con el precio al aviso y el texto fijo "Análisis informativo; no garantiza resultados." Nunca ejecuta ni simula órdenes.

## Diseño

Un solo matiz por tema (azul en claro, naranja en oscuro) en una escala de tonos con significado:

- Lienzo de la página y barra de pestañas: el tono más tenue.
- Títulos de sección: el tono más profundo; subtítulos y etiquetas, tono medio-profundo.
- Marco superior de cada recuadro según su función: consultar (suave), capturar datos (medio), asesor o análisis de Claude (fuerte).
- Acciones y progreso (botón principal, pestaña activa, barras): el acento puro.
- Verde, ámbar y rojo solo indican estados.

Tipografía IBM Plex Sans y Plex Mono; espaciado en escala 4/8/12/16/24/32/48 px; contraste WCAG AA en ambos temas.

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

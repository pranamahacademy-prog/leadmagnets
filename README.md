# Lead magnets · Método Pranamah

## Test interactivo — «Las 12 señales de que no duermes mal por estrés»

`index.html` es el test de 8 preguntas que lleva a la comunidad de WhatsApp.

Es **un único archivo autocontenido**: no carga nada de fuera (las tipografías van
incrustadas en el propio HTML). Se puede abrir con doble clic, subir por FTP,
publicar en Netlify / Vercel / GitHub Pages o incrustar en un `<iframe>`.

### Recorrido

1. **Portada** — titular, promesa y botón de inicio.
2. **8 preguntas** — una por pantalla, con barra de progreso y avance automático
   al responder. Se puede volver atrás y las respuestas se guardan en el
   navegador, así que si alguien cierra a mitad, retoma donde lo dejó.
3. **Cálculo** — dos segundos de espera antes del resultado.
4. **Resultado** — puntuación sobre 24, uno de los tres perfiles y sus señales.
5. **Únete a la comunidad** — CTA final al grupo de WhatsApp.

### Diseño

**Paleta** (de la referencia de marca):

| Color | Uso |
|---|---|
| `#f6f1eb` | fondo de página |
| `#f8f8f3` | tarjetas |
| `#d6bfae` | filetes, bordes y detalles |
| `#a3b18a` | acento: progreso, opción elegida, CTA de WhatsApp |
| `#2c3e50` | texto y bloque final |
| `#bdc3c7` | reservado para grises secundarios |

Se usa además `#9c5f6b`, el rosa de la palabra en cursiva de la referencia
tipográfica, y solo para eso: la palabra destacada de cada titular.

**Tipografías** — Playfair Display para los titulares (con su cursiva) y Lato
para texto y interfaz. Subset latino, que cubre todo el español.

### Cómo editarlo

Todo lo editable está al principio del `<script>`, al final del archivo:

- **Enlace de WhatsApp** → la constante `WHATSAPP`.
- **Preguntas** → el array `QUESTIONS`. Cada opción lleva un valor `v` de 0 a 3
  (0 = ninguna señal, 3 = señal clara). Si añades o quitas preguntas, el máximo
  se recalcula solo; revisa entonces los cortes de `PROFILES`.
- **Resultados** → el array `PROFILES`, ordenado por el `max` de puntos de cada
  perfil: 0–7, 8–15 y 16–24.

### Accesibilidad

Navegable con teclado (teclas `1`–`4` para responder, flechas para moverse,
`Retroceso` para volver), roles `radiogroup`/`radio`, avisos por `aria-live` y
respeto de `prefers-reduced-motion`.

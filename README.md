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
4. **Resultado + comunidad** — bienestar del sueño sobre 10, perfil y acceso al
   grupo, todo en la misma pantalla.

## Publicarlo y compartirlo por enlace

El destino previsto es **GitHub Pages**, que sirve este repositorio tal cual y
gratis. La rama por defecto ya es la de trabajo y `index.html` está en la raíz,
así que solo falta activarlo:

1. En GitHub: **Settings → Pages**.
2. En *Build and deployment*, *Source*: **Deploy from a branch**.
3. Rama: la que aparece por defecto; carpeta: **/ (root)**. Guardar.

En un par de minutos el test queda en:

    https://pranamahacademy-prog.github.io/leadmagnets/

Ese es el enlace que se manda por mensaje. Si prefieres un dominio propio
(`test.tudominio.com`), se añade en esa misma pantalla de Pages y se crea un
CNAME en el DNS; en ese caso hay que cambiar las tres URL absolutas de las
metaetiquetas `og:url`, `og:image` y `canonical`, al principio del HTML.

### La tarjeta de previsualización

Cuando el enlace llega por privado, Instagram y WhatsApp muestran una tarjeta
con imagen, título y descripción. La imagen es `og.png` (1200×630, 99 KB, por
debajo del límite a partir del cual WhatsApp deja de mostrar previsualización
grande) y se genera con el mismo diseño y las mismas tipografías que la portada.

Si cambias el titular o la imagen, las redes guardan la versión antigua en
caché durante días. Para forzar el refresco, pasa la URL por el
[depurador de Facebook](https://developers.facebook.com/tools/debug/) y pulsa
*Scrape Again*.

### Notas para la automatización de Instagram

- El enlace tiene que ser público: nada de páginas con login por delante.
- Instagram abre los enlaces en su navegador interno. Por eso el botón final
  navega en la misma pestaña en lugar de abrir una nueva: así el móvil pasa el
  enlace a la app de WhatsApp en vez de quedarse atrapado en el navegador.
- Se pueden añadir parámetros al enlace sin romper nada
  (`…/leadmagnets/?utm_source=instagram&utm_campaign=test-sueno`), útil si más
  adelante añades analítica. La página los ignora.
- La página no carga nada de fuera ni instala cookies, así que no necesita
  banner de consentimiento.

### Sin scroll

**En escritorio (a partir de 900 px de ancho) ninguna pantalla hace scroll.**
Portada, preguntas y resultado se encuadran dentro del alto de la ventana, y
todas las medidas — titulares, opciones, márgenes — escalan con `svh`, así que
se ajustan solas. Comprobado de 1280×620 a 1920×1080.

En móvil hacen scroll, como es natural, las preguntas más largas; la que nunca
lo hace es la última.

### La pantalla final

Entra entera en el viewport en cualquier tamaño, con el botón de WhatsApp
siempre a la vista. Para conseguirlo se adapta al espacio disponible:

- **A partir de 900 px de ancho** el diagnóstico y el bloque de comunidad van en
  dos columnas, así que la altura es la del más alto y caben también las tres
  señales del perfil.
- **En móvil**, apilados, no hay sitio para las tres señales además del acceso a
  la comunidad, así que se ocultan: mandan la puntuación, el perfil y el botón.

Comprobado sin scroll de 360×640 a 1440×900.

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

### Las dos escalas

Por dentro se suman **señales**: de 0 a 24, donde más es peor. Lo que se enseña
es lo contrario, el **bienestar del sueño de 0 a 10**, donde 10 es un descanso
excelente. La conversión está en la función `bienestar()`:

    nota = 10 - redondeo(señales / 24 × 10)

El aro se rellena en proporción a la nota, así que un aro lleno es buena señal.
Los tres perfiles siguen calculándose con los puntos crudos.

### Accesibilidad

Navegable con teclado (teclas `1`–`4` para responder, flechas para moverse,
`Retroceso` para volver; los atajos funcionan aunque no se anuncien en pantalla),
roles `radiogroup`/`radio`, avisos por `aria-live` y respeto de
`prefers-reduced-motion`.

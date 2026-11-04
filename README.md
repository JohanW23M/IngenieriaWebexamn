# Guía de estudio – Ingeniería Web (UTPL)

> Docente: Mgtr. Ramiro Ramírez
> Temas del examen: **1) Arquitecturas web · 2) Desarrollo con HTML · 3) Desarrollo con CSS**
> Fuentes: diapositivas de clase (Interfaces web, Arquitecturas Web, HTML5 Fundamentos, Clase 2) y el gist de prácticas (`index.html`, `style.css`, `login.html`).
>
> Leyenda: 🟦 = viene de las diapositivas · 🟩 = viene del código de la práctica · 🟨 = complemento teórico mío (no está en tus diapositivas, pero encaja con lo que el profesor pide).

---

## Índice

1. [Mapa del proyecto de práctica](#1-mapa-del-proyecto-de-práctica)
2. [Arquitecturas web](#2-arquitecturas-web)
3. [Desarrollo con HTML](#3-desarrollo-con-html)
4. [Práctica 1: `index.html` (página principal) línea por línea](#4-práctica-1-indexhtml-línea-por-línea)
5. [Práctica 2: `login.html` línea por línea](#5-práctica-2-loginhtml-línea-por-línea)
6. [Desarrollo con CSS](#6-desarrollo-con-css)
7. [`style.css` explicado bloque por bloque](#7-stylecss-explicado-bloque-por-bloque)
8. [Tabla maestra: HTML ↔ CSS (cómo se referencia cada elemento)](#8-tabla-maestra-html--css)
9. [Errores y malas prácticas del código (típico "encuentre el error")](#9-errores-y-malas-prácticas-del-código)
10. [Autoevaluación](#10-autoevaluación)

---

## 1. Mapa del proyecto de práctica

🟩 Por las rutas del código, la estructura de carpetas es esta:

```
proyecto/
├── index.html          ← página principal (gistfile1.txt)
├── html/
│   └── login.html      ← página de login
└── css/
    └── style.css       ← hoja de estilos compartida (gistfile2.txt)
```

**Por qué importa:** las rutas cambian según dónde esté el archivo.

| Archivo | Cómo enlaza el CSS | Explicación |
|---|---|---|
| `index.html` (raíz) | `href="css/style.css"` | Entra directo a la carpeta `css`. |
| `login.html` (dentro de `html/`) | `href="../css/style.css"` | `../` = "sube una carpeta" y luego entra a `css`. |

> **Idea clave:** una sola hoja de estilos (`style.css`) sirve para varias páginas. Cada página activa sus estilos mediante **clases** (`class="..."`). Por ejemplo, `<body class="bodylogin">` activa solo los estilos del login.

---

## 2. Arquitecturas web

### 2.1 Concepto 🟦

- La **arquitectura web** es la **estructura conceptual de la World Wide Web (WWW)**.
- La web es un medio en constante cambio que permite:
  - la **comunicación** entre usuarios, y
  - la **interacción técnica (interoperabilidad)** entre distintos sistemas y subsistemas.

### 2.2 Por qué es importante (SEO y experiencia de usuario) 🟦

- Una buena arquitectura permite que **usuarios y rastreadores de buscadores** se muevan fácilmente por el portal.
- En experiencia de usuario ayuda a responder: **"¿qué hago aquí?"** y **"¿a dónde voy ahora?"**.
- Una arquitectura optimizada ayuda a las **arañas (crawlers)** de los buscadores a encontrar e indexar todas las páginas.
- Resultado: los usuarios encuentran lo que necesitan y la página gana **más autoridad**.

### 2.3 Tipos de arquitectura de la información 🟦

| Tipo | Cómo funciona | Para quién |
|---|---|---|
| **Vertical** | Todas las URLs se enlazan **directamente desde el dominio**. | Páginas muy especializadas en una temática, o webs que empiezan y tienen pocas URLs. |
| **SILO** (también llamada horizontal) | Se **agrupa semánticamente** el contenido y se organiza de forma **jerárquica según keywords**. | Sitios con mucho contenido que necesitan orden temático (mejor para SEO). |

### 2.4 Arquitecturas de desarrollo 🟦

> La más recomendada **depende del tipo de aplicación y de los requerimientos del proyecto**. No hay una "mejor" universal. Esto es clave para responder preguntas de caso.

#### a) Microservicios
- **Recomendada para:** aplicaciones grandes, escalables y distribuidas.
- **Características / ventajas:**
  - Se desarrollan, implementan y escalan componentes **de forma independiente**.
  - **Flexibilidad tecnológica**: cada equipo puede usar tecnologías distintas.
  - Mantenimiento y actualización **sin afectar todo el sistema**.
- **Ejemplos:** Netflix, Uber, Amazon.

#### b) Serverless (sin servidor)
- **Recomendada para:** aplicaciones con **demanda variable** que necesitan **escalado automático**.
- **Ventajas:**
  - El **proveedor en la nube** maneja la infraestructura; tú te centras en desarrollar.
  - **Escalado automático** según la demanda.
  - **Pagas solo por lo que usas**.
- **Ejemplos:** AWS Lambda, Google Cloud Functions, Azure Functions.

#### c) SPA (Single Page Application, aplicación de página única)
- **Recomendada para:** aplicaciones **interactivas y rápidas** (dashboards, sistemas internos).
- **Ventajas:**
  - Mejor experiencia: **evita recargas completas** de la página.
  - Uso intensivo de **React, Angular o Vue.js** para manipular el DOM y los estados.
- **Ejemplos:** Gmail, Trello, GitHub.

#### d) JAMstack (JavaScript, APIs y Markup)
- **Recomendada para:** sitios estáticos o dinámicos que buscan **velocidad, escalabilidad y seguridad**.
- **Ventajas:**
  - Contenido servido como **archivos estáticos** (muy rápido).
  - Mejor rendimiento y seguridad al **reducir el procesamiento en el servidor**.
  - Buena para **SEO**.
- **Ejemplos:** sitios web y blogs estáticos con contenido dinámico desde APIs.

#### e) MVC (Model-View-Controller)
- **Recomendada para:** aplicaciones **tradicionales y de tamaño medio**.
- **Ventajas:**
  - **Separa claramente**: lógica de negocio (**Modelo**), interfaz (**Vista**) e interacción del usuario (**Controlador**).
  - Facilita mantenimiento y desarrollo en **equipos grandes**.
- **Ejemplos:** Ruby on Rails, Django, ASP.NET.

#### f) Multitier (N-tier / varias capas)
- **Recomendada para:** aplicaciones **empresariales** que dividen presentación, lógica de negocio y datos.
- **Ventajas:**
  - **Define responsabilidades** por capa (mantenimiento y escalabilidad).
  - **Más seguridad** al aislar la capa de presentación de la lógica de negocio.
- **Ejemplos:** aplicaciones corporativas con bases de datos complejas, como **ERP o CRM**.

### 2.5 Resumen comparativo (para memorizar) 🟦

| Arquitectura | Palabra clave | Úsala cuando… |
|---|---|---|
| Microservicios | Independencia | App grande y distribuida, equipos separados |
| Serverless | Pago por uso | Demanda variable, no quieres administrar servidores |
| SPA | Sin recargas | Dashboards / apps muy interactivas |
| JAMstack | Estático + APIs | Velocidad, seguridad y SEO |
| MVC | Separación de responsabilidades | App tradicional de tamaño medio |
| Multitier | Capas | Sistema empresarial (ERP, CRM) |

### 2.6 Stacks de desarrollo 🟦

Las diapositivas muestran stacks para **PHP**, **Python** y **JS**, pero solo con imágenes. Revisa esas diapositivas en el PPT original y completa aquí:

- Stack PHP: _(completar desde la diapositiva 15)_
- Stack Python: _(completar desde la diapositiva 16)_
- Stack JS: _(completar desde la diapositiva 17)_

### 2.7 Otros conceptos de arquitectura que aparecen en clase

- **Control de acceso:** restricción por **IP/dominio** o por **usuario y clave**; archivo **`.htaccess`** (Apache) para configurar el comportamiento del servidor, por ejemplo ante errores como el **404**. 🟦
- **HTTPS:** protocolo seguro, la transferencia de datos va **cifrada**. 🟦
- **Webapp dinámica vs. HTML estático:** la webapp accede directamente a las **bases de datos**, así que ofrece información actualizada. 🟦

---

## 3. Desarrollo con HTML

### 3.1 Conceptos 🟦

- **HTML = HyperText Markup Language.**
- HTML5 es la **quinta versión** del estándar.
- **No es un lenguaje de programación: es un lenguaje de marcado.** (Pregunta muy típica.)
- Sirve para **estructurar el contenido** de la web.
- HTML5 introduce: **etiquetas semánticas, multimedia nativa, formularios mejorados y APIs.**

### 3.2 Estructura básica de un documento HTML5 🟨

```html
<!DOCTYPE html>                       <!-- 1. Declara que es HTML5 -->
<html lang="es">                      <!-- 2. Elemento raíz; lang = idioma -->
<head>                                <!-- 3. Metadatos (no se ven en la página) -->
  <meta charset="utf-8">              <!--    Codificación de caracteres (tildes, ñ) -->
  <meta name="viewport"
        content="width=device-width, initial-scale=1">  <!-- Responsive -->
  <title>Título de la pestaña</title>
  <link rel="stylesheet" href="css/style.css">          <!-- Enlaza el CSS -->
</head>
<body>                                <!-- 4. Contenido visible -->
  ...
</body>
</html>
```

### 3.3 Etiquetas semánticas 🟦

| Etiqueta | Función |
|---|---|
| `<header>` | Encabezado de la página o de una sección |
| `<nav>` | Menú de navegación |
| `<main>` | Contenido principal |
| `<section>` | Sección temática |
| `<article>` | Contenido **independiente** (noticia, entrada de blog) |
| `<aside>` | Contenido lateral o complementario |
| `<footer>` | Pie de página |

> **Cómo distinguir `section` de `article`:** si el bloque tiene sentido **por sí solo** (una noticia que podrías copiar a otro sitio) → `article`. Si es una **parte temática** de la página → `section`. En tu práctica, la sección de noticias es una `section` y cada noticia es un `article`.

**Por qué usar semánticas en vez de `<div>`:** el código se entiende solo, mejora el SEO y la accesibilidad (lectores de pantalla). 🟨

### 3.4 Formularios HTML5 🟦

Nuevos tipos de `input`: `email`, `date`, `number`, `range`, `color`, `search`, `url`.
(Más los clásicos que usas en el login: `text`, `password`, `checkbox`.)

```html
<input type="email"  placeholder="correo@utpl.edu.ec">   <!-- valida formato de correo -->
<input type="date">                                       <!-- selector de fecha -->
<input type="number" min="1" max="10">                    <!-- solo números -->
<input type="range">                                      <!-- barra deslizante -->
<input type="color">                                      <!-- selector de color -->
<input type="search">                                     <!-- campo de búsqueda -->
<input type="url">                                        <!-- valida que sea una URL -->
```

### 3.5 Multimedia HTML5 🟦

- Ya **no se necesita Flash**: hay soporte **nativo** para video y audio.
- Atributos: `controls`, `autoplay`, `loop`, `muted`.

```html
<video src="video.mp4" controls autoplay muted loop></video>
<audio src="audio.mp3" controls></audio>
```

| Atributo | Qué hace |
|---|---|
| `controls` | Muestra los botones de reproducción |
| `autoplay` | Se reproduce solo al cargar |
| `loop` | Se repite en bucle |
| `muted` | Empieza sin sonido |

### 3.6 Buenas prácticas 🟦

1. Usar **etiquetas semánticas**.
2. Mantener **indentación clara**.
3. Incluir **`alt`** en las imágenes.
4. **Validar** el código con el **W3C Validator**.
5. **Separar HTML, CSS y JS** (archivos distintos).
6. Usar **`meta viewport`** para diseño responsive.

### 3.7 Accesibilidad web (Clase 1) 🟦

- Que personas con discapacidad puedan **percibir, entender, navegar e interactuar** con la web.
- Organismo: **W3C**, grupo de trabajo **WAI**.
- Ejemplos de casos a considerar: daltonismo, ceguera, Parkinson, fracturas.
- Herramientas: contrast-ratio.com (contraste de colores), paletton.com (paletas), TAW (tawdis.net), validator.w3.org/checklink.

---

## 4. Práctica 1: `index.html` línea por línea

🟩 Código del gist (`gistfile1.txt`). Cada bloque indica **qué hace** y **cómo se referencia desde el CSS**.

### 4.1 Cabecera del documento

```html
<!DOCTYPE html>
```
Declara que el documento es **HTML5**. Siempre va en la primera línea.

```html
<html>
```
**Elemento raíz.** Todo el documento va dentro. (Buena práctica: `<html lang="es">`.)

```html
<head>
<meta charset="utf-8">
```
`<head>` agrupa **metadatos**. `charset="utf-8"` permite mostrar tildes y la ñ correctamente.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```
Hace que la página sea **responsive** en móviles: el ancho se adapta al del dispositivo.

```html
<title>Ejemplo de CSS</title>
```
Texto que aparece en la **pestaña** del navegador.

```html
<link rel="stylesheet" type="text/css" href="css/style.css">
```
**Conecta el HTML con el CSS.**
- `rel="stylesheet"` → la relación es "hoja de estilos".
- `href="css/style.css"` → ruta **relativa** del archivo.
</head>

### 4.2 Encabezado (`header`)

```html
<body>
<header class="mainHeader">
```
- `<body>`: todo lo visible.
- `<header>`: etiqueta semántica del encabezado.
- `class="mainHeader"`: **nombre de clase** para estilizarlo.
- **Se referencia en CSS como:** `header.mainHeader` (etiqueta `header` **con** la clase `mainHeader`, sin espacio).

```html
<h2 class="logotipo">LOGOTIPO</h2>
```
- `<h2>`: título de nivel 2.
- **Se referencia como:** `header.mainHeader h2` (cualquier `h2` **dentro** del header; hay un espacio = descendiente).
- ⚠️ La clase `logotipo` está puesta pero **el CSS no la usa**; el estilo se aplica por la etiqueta `h2`.

```html
<nav class="mainNav">
<a href="">INICIO</a>
<a href="">PROTAFOLIO</a>
<a href="">CONTACTOS</a>
<a href="">REGISTRO</a>
</nav>
```
- `<nav>`: menú de navegación.
- `<a href="">`: **enlace** (hipervínculo). `href` es el destino; vacío = no va a ningún lado.
- **Se referencia como:** `header.mainHeader nav` (el menú) y `header.mainHeader nav a` (cada enlace). Con hover: `header.mainHeader nav a:hover`.
- ⚠️ Typo: "PROTAFOLIO" debería ser "PORTAFOLIO".

### 4.3 Slider

```html
<section class="mainSlider">
<h2>Slider de la pagina</h2>
</section>
```
- `<section>`: sección temática (aquí, el banner principal).
- **Se referencia como:** `section.mainSlider` y su título como `section.mainSlider h2`.

### 4.4 Noticias

```html
<section class="news">
  <article class="newsItem">
    <h2>Titulo de la noticia</h2>
    <img src="">
    <p>Esto es la informacion de la noticia</p>
    <button>Mas informacion</button>
  </article>
  ... (se repite 3 veces)
</section>
```
- `<section class="news">`: contenedor de las noticias. **CSS:** `section.news`.
- `<article class="newsItem">`: **cada noticia** es contenido independiente. **CSS:** `section.news .newsItem` (clase `newsItem` dentro de `section.news`).
- `<h2>`: título de la noticia.
- `<img src="">`: imagen (`src` = ruta de la imagen). ⚠️ Falta `alt`.
- `<p>`: párrafo de texto.
- `<button>`: botón.
- Las 3 noticias comparten la misma clase `newsItem`, por eso **un solo bloque de CSS estiliza las tres**. Esto es **reutilización con clases**.

### 4.5 Pie de página

```html
<footer class="mainFooter">
<h6>Derechos Reservados UTPL 2026, by: @rlramirez</h6>
</footer>
```
- `<footer>`: pie de página semántico. **CSS:** `footer.mainFooter`.
- `<h6>`: título de nivel 6 (el más pequeño), usado aquí para el texto de derechos.

---

## 5. Práctica 2: `login.html` línea por línea

🟩 Código del gist (`login.html`).

### 5.1 Cabecera

```html
<link rel="stylesheet" type="text/css" href="../css/style.css">
```
Usa **`../`** porque este archivo está dentro de la carpeta `html/` y el CSS está un nivel arriba, en `css/`.

```html
<link href="https://cdn.boxicons.com/3.0.8/fonts/basic/boxicons.min.css" rel="stylesheet">
```
Carga **Boxicons** desde un **CDN** (servidor externo): una librería de **íconos**. Sin esta línea, las etiquetas `<i class="bx ...">` no mostrarían nada.
> **CDN** = red de servidores que entrega archivos (CSS, JS, fuentes) sin que tú los tengas que descargar.

### 5.2 Cuerpo y contenedor

```html
<body class="bodylogin">
```
**Activa los estilos de login para el `body`.**
- **CSS:** `body.bodylogin` → fondo verde, y **Flexbox** para centrar todo en la pantalla.

```html
<section class="wrapper">
```
Contenedor (caja morada de 420px) que envuelve todo el formulario.
- **CSS:** `.wrapper` (selector de clase, sin la etiqueta delante).

```html
<form action="">
```
`<form>` agrupa los campos que se envían juntos. `action` = a qué URL se envían los datos (vacío = la misma página).

```html
<h1>LOGIN APP</h1>
```
Título principal. **CSS:** `.wrapper h1` (cualquier `h1` dentro de `.wrapper`).

### 5.3 Campos de entrada

```html
<div class="input-box">
  <input type="text" name="" placeholder="Username">
  <i class="bx bx-user"></i>
</div>
```
- `<div class="input-box">`: **caja contenedora** del input y su ícono. Sirve para posicionar el ícono encima del campo.
  **CSS:** `.wrapper .input-box`.
- `<input type="text">`: campo de texto. `placeholder="Username"` = texto de ayuda gris que desaparece al escribir.
  **CSS:** `.input-box input` y `.input-box input::placeholder`.
- `<i class="bx bx-user"></i>`: ícono de Boxicons. Dos clases: `bx` (base de la librería) + `bx-user` (el dibujo concreto).
  **CSS:** `.input-box i`.

```html
<div class="input-box">
  <input type="password" name="" placeholder="Pasword">
  <i class="bx bx-lock"></i>
</div>
```
Igual que el anterior. `type="password"` **oculta los caracteres** con puntos. Ícono: candado (`bx-lock`).

### 5.4 Recordarme y olvidé contraseña

```html
<div class="remember-forgot">
  <label>
    <input type="checkbox" name=""> Remember me
  </label>
  <a href="">Forgor Password</a>
</div>
```
- `<div class="remember-forgot">`: fila que contiene las dos cosas. **CSS:** `.wrapper .remember-forgot` (aquí se usa Flexbox con `space-between`).
- `<label>`: etiqueta de texto asociada al control. Al envolver el `input`, hacer clic en el texto marca el checkbox.
- `<input type="checkbox">`: casilla de verificación. **CSS:** `.remember-forgot label input`.
- `<a href="">`: enlace "olvidé mi contraseña". **CSS:** `.remember-forgot a` y `.remember-forgot a:hover`.
- ⚠️ Typo: "Forgor" → "Forgot".

### 5.5 Botón y registro

```html
<button type="submit" class="btn"> Login App</button>
```
- `type="submit"`: al hacer clic **envía el formulario**.
- **CSS:** `.wrapper .btn`.

```html
<div class="register-link">
  <p>Don't have acount <a href="">Register</a></p>
</div>
```
- `<div class="register-link">`: contenedor. **CSS:** `.wrapper .register-link`.
- `<p>` con un `<a>` dentro (enlace dentro de un párrafo). **CSS:** `.register-link p a` y `.register-link p a:hover`.
- ⚠️ Typo: "acount" → "account".

---

## 6. Desarrollo con CSS

### 6.1 Qué es y cómo se conecta 🟨

- **CSS = Cascading Style Sheets.** Define **cómo se ve** el HTML (colores, tamaños, posición, tipografías).
- **HTML = estructura. CSS = presentación.** (Por eso la buena práctica "separar HTML, CSS y JS".)
- Tres formas de aplicarlo (de mejor a peor práctica):
  1. **Externo** (tu práctica): `<link rel="stylesheet" href="css/style.css">`
  2. **Interno:** etiqueta `<style>` dentro del `<head>`.
  3. **En línea:** atributo `style="..."` dentro de una etiqueta.

### 6.2 Anatomía de una regla

```css
selector {            /* A QUÉ elementos se aplica */
  propiedad: valor;   /* QUÉ cambia y CÓMO */
}
```

```css
header.mainHeader h2 {     /* selector */
    padding: 30px;         /* propiedad: valor */
    width: 30%;
}
```

### 6.3 Tipos de selectores que usa tu práctica

| Selector | Ejemplo en tu código | Significado |
|---|---|---|
| **Universal** `*` | `* { ... }` | Todos los elementos |
| **Etiqueta** | `footer`, `h2` | Todos los elementos de ese tipo |
| **Clase** `.nombre` | `.wrapper`, `.btn` | Elementos con `class="nombre"` |
| **Etiqueta + clase** (sin espacio) | `header.mainHeader` | Un `header` **que tenga** la clase `mainHeader` |
| **Descendiente** (espacio) | `header.mainHeader h2` | Un `h2` **dentro de** `header.mainHeader` (a cualquier nivel) |
| **Lista de selectores** (coma) | `header.mainHeader, section.mainSlider, section.news` | Aplica **el mismo estilo a todos** los de la lista |
| **Pseudo-clase** `:hover` | `nav a:hover` | Cuando el mouse pasa por encima |
| **Pseudo-elemento** `::placeholder` | `.input-box input::placeholder` | Estiliza el texto de ayuda del input |

> **Diferencia que suelen preguntar:**
> `header.mainHeader` (sin espacio) = el `header` con esa clase.
> `header .mainHeader` (con espacio) = un elemento con esa clase **dentro de** un `header`.
> `.input-box input` = los `input` dentro de `.input-box`. `.input-box, input` = ambos por separado.

### 6.4 Especificidad (qué regla gana si hay conflicto) 🟨

Orden de menor a mayor peso: **`*` < etiqueta < clase < id < estilo en línea**.

**Ejemplo real de tu práctica:** el `*` define `font-family: "Roboto Condensed"` para todo, pero `header.mainHeader h2` define `font-family: "Imperial Script"`. **Gana la segunda** porque es más específica (etiqueta + clase + etiqueta pesa más que `*`).

### 6.5 Modelo de caja (box model) 🟨

Todo elemento es una caja con capas, de adentro hacia afuera:

```
┌──────────── margin (espacio EXTERIOR) ────────────┐
│  ┌──────────── border (borde) ────────────┐       │
│  │  ┌──────── padding (espacio INTERIOR) ┐│       │
│  │  │        contenido (content)         ││       │
│  │  └────────────────────────────────────┘│       │
│  └────────────────────────────────────────┘       │
└───────────────────────────────────────────────────┘
```

- `padding`: espacio **dentro** (entre contenido y borde).
- `margin`: espacio **fuera** (entre este elemento y los vecinos).
- `box-sizing: border-box`: el `width` **incluye** padding y borde. Sin esto, un `width: 100%` con padding se desbordaría. Por eso va en el reset `*`.

### 6.6 Unidades usadas en la práctica 🟨

| Unidad | Qué es | Dónde la usas |
|---|---|---|
| `%` | Porcentaje del elemento padre | `width: 80%`, `width: 30%` |
| `px` | Píxeles (fijo) | `width: 420px`, `padding: 30px` |
| `vh` | 1% del **alto de la pantalla** | `min-height: 100vh` (el body ocupa toda la pantalla) |

---

## 7. `style.css` explicado bloque por bloque

🟩 Código del gist (`gistfile2.txt`).

### 7.1 Importar fuentes

```css
@import url('https://fonts.googleapis.com/css2?family=Imperial+Script&family=Montserrat...&display=swap');
```
`@import` trae **fuentes de Google Fonts**. Se declaran tres familias: Imperial Script, Montserrat y Roboto Condensed. `display=swap` muestra primero una fuente de respaldo mientras carga la otra.

### 7.2 Reset global

```css
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: "Roboto Condensed", sans-serif;
}
```
| Línea | Qué hace |
|---|---|
| `*` | Aplica a **todos** los elementos |
| `padding: 0; margin: 0;` | Quita los espacios que el navegador pone por defecto |
| `box-sizing: border-box` | El ancho incluye padding y borde |
| `font-family: "Roboto Condensed", sans-serif` | Fuente por defecto; `sans-serif` es el **respaldo** si la primera falla |

### 7.3 Contenedores principales (página principal)

```css
header.mainHeader, section.mainSlider, section.news{
    width: 80%;
    background-color: #ccc;
    margin: 0 auto;
}
```
- **Selector con comas:** los **tres** bloques reciben el mismo estilo.
- `width: 80%`: ocupan el 80% del ancho del navegador.
- `background-color: #ccc`: gris claro (**código hexadecimal**: `#ccc` = `#cccccc`).
- `margin: 0 auto`: **centra horizontalmente** (0 arriba/abajo, `auto` a los lados reparte el espacio sobrante).
  - Truco: `margin: A B` → A = arriba y abajo, B = izquierda y derecha.

### 7.4 Cabecera

```css
header.mainHeader h2{
    padding: 30px;
    font-family: "Imperial Script";
    width: 30%;
    display: inline-block;
}
```
- `padding: 30px`: espacio interior.
- `font-family: "Imperial Script"`: fuente cursiva solo para el logo (sobrescribe el `*`).
- `display: inline-block`: **se coloca en línea** (junto a otros elementos) pero **acepta width/height**. Esto permite que el logo y el menú queden en la **misma fila**.

```css
header.mainHeader nav{
    width: 60%;
    display: inline-block;
    text-align: right;
}
```
- Logo 30% + menú 60% = 90%, caben en la misma fila.
- `text-align: right`: los enlaces se alinean a la **derecha**.

```css
header.mainHeader nav a{
    text-decoration: none;
    color: #ff0000;
    padding: 0 10px;
}
```
- `text-decoration: none`: quita el subrayado de los enlaces.
- `color: #ff0000`: **rojo** (ff = rojo máximo, 00 verde, 00 azul → formato `#RRGGBB`).
- `padding: 0 10px`: 0 arriba/abajo, 10px a los lados.

```css
header.mainHeader nav a:hover{
    background-color: #000;
    color: #fff;
    padding: 20px;
    border-radius: 15px;
}
```
- `:hover`: **solo cuando el mouse está encima**.
- Fondo negro, texto blanco, bordes redondeados (`border-radius: 15px`).
- ⚠️ El `padding` cambia de `0 10px` a `20px` al hacer hover, así que el enlace **crece** y puede mover el layout. Es un detalle que se puede preguntar.

### 7.5 Slider

```css
section.mainSlider{
    background-color: #ff3333;
}
```
Sobrescribe el gris `#ccc` de la regla compartida (7.3) con un rojo claro. **Gana esta** porque aparece **después** y es más específica.

```css
section.mainSlider h2{
    padding: 130px 0;
    text-align: center;
}
```
- `padding: 130px 0`: 130px arriba/abajo, 0 a los lados → da **altura** al banner.
- `text-align: center`: título centrado.

### 7.6 Noticias

```css
section.news{
    text-align: center;
}
```
Centra el contenido de la sección (incluye los `inline-block`).

```css
section.news .newsItem{
    width: 27%;
    display: inline-block;
    background-color: #cc3333;
    margin: 5px;
    padding: 20px;
}
```
- `.newsItem` dentro de `section.news`.
- `width: 27%` × 3 = 81% + márgenes → **caben 3 en una fila**.
- `display: inline-block`: se colocan lado a lado en vez de apilarse.
- `margin: 5px` (separación entre tarjetas), `padding: 20px` (aire interior).

### 7.7 Pie de página

```css
footer.mainFooter{
    background-color: #000;
    color: #ccc;
    text-align: center;
    padding: 20px 0;
}
```
Fondo negro, texto gris claro, centrado.

### 7.8 Estilos del login

```css
body.bodylogin{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: seagreen;
}
```
**Esto es Flexbox, un tema central.**

| Propiedad | Qué hace |
|---|---|
| `display: flex` | Convierte el `body` en contenedor flexible; sus hijos (`.wrapper`) son "ítems flex" |
| `justify-content: center` | Centra en el **eje horizontal** (eje principal) |
| `align-items: center` | Centra en el **eje vertical** (eje cruzado) |
| `min-height: 100vh` | El body mide **al menos todo el alto de la pantalla** (sin esto, no habría altura para centrar verticalmente) |
| `background: seagreen` | Color por **nombre** (también se puede en hex, rgb, etc.) |

```css
.wrapper{
    width: 420px;
    background-color: purple;
    color: #fff;
}
.wrapper h1{
    font-size: 36px;
    text-align: center;
}
```
Caja fija de 420px, fondo morado, texto blanco. El `h1` centrado y de 36px.

```css
.wrapper .input-box{
    position: relative;
    width: 100%;
    height: 50px;
    background-color: salmon;
    margin: 30px 0;
}
```
- `position: relative`: este contenedor pasa a ser el **punto de referencia** para posicionar elementos hijos con `absolute` (el ícono).
- `margin: 30px 0`: separación vertical entre campos.

```css
.input-box input{
    width: 100%;
    height: 100%;
    background: transparent;
    border: none;
    outline: none;
    border: 2px solid rgba(255, 255, 255, .2);
    border-radius: 40px;
    font-size: 16px;
    color: #ff;
    padding: 20px 45px 20px 20px;
}
```
| Línea | Qué hace |
|---|---|
| `width/height: 100%` | El input llena toda la caja `.input-box` |
| `background: transparent` | Sin fondo propio (se ve el salmón de atrás) |
| `border: none` luego `border: 2px solid rgba(...)` | La segunda **sobrescribe** a la primera; queda un borde de 2px blanco al 20% de opacidad. (`rgba(R,G,B,alfa)`; alfa 0 a 1) |
| `outline: none` | Quita el contorno que el navegador dibuja al hacer clic |
| `border-radius: 40px` | Bordes muy redondeados (forma de píldora) |
| `padding: 20px 45px 20px 20px` | **Orden: arriba, derecha, abajo, izquierda** (sentido de las agujas del reloj). Los 45px a la derecha dejan espacio para el ícono |
| `color: #ff` | ⚠️ **Valor inválido**: un hex debe tener 3 o 6 dígitos. El navegador lo ignora. Debería ser `#fff` |

```css
.input-box input::placeholder{
    color: #fff;
}
```
`::placeholder` (**pseudo-elemento**) estiliza el texto de ayuda ("Username"). Se ve blanco.

```css
.input-box i{
    position: absolute;
    right: 20px;
    top: 30%;
    transform: translate(-10px);
    font-size: 20px;
}
```
- `position: absolute`: saca el ícono del flujo y lo posiciona **respecto al contenedor `relative`** (`.input-box`).
- `right: 20px; top: 30%`: lo ubica a la derecha, casi centrado en vertical.
- `transform: translate(-10px)`: desplaza 10px a la izquierda (un solo valor = eje X).
- `font-size: 20px`: los íconos de Boxicons se escalan con font-size.

```css
.wrapper .remember-forgot{
    display: flex;
    justify-content: space-between;
    font-size: 15px;
    margin: -15px 0 15px;
}
```
- `display: flex` + `justify-content: space-between`: pone "Remember me" a la izquierda y "Forgot Password" a la derecha (**el espacio sobrante va entre ambos**).
- `margin: -15px 0 15px`: **margen superior negativo** (lo acerca al campo de arriba), 0 a los lados, 15px abajo.

```css
.remember-forgot label input{
    accent-color: #fff;
    margin-right: 10px;
}
```
`accent-color` cambia el **color del checkbox**. `margin-right` lo separa del texto.

```css
.remember-forgot a{
    color: #fff;
    text-decoration: none;
}
.remember-forgot a:hover{
    text-decoration: underline;
}
```
Enlace blanco sin subrayado; **subrayado solo al pasar el mouse**.

```css
.wrapper .btn{
    width: 100%;
    height: 45px;
    background: #fff;
    color: #333;
    border: none;
    outline: none;
    border-radius: 40px;
    box-shadow: 0 0 10px rgba(0, 0, 0, .3);
    cursor: pointer;
    font-size: 16px;
    font-weight: 600;
}
```
- `box-shadow: 0 0 10px rgba(0,0,0,.3)`: sombra (X=0, Y=0, desenfoque=10px, negro al 30%).
- `cursor: pointer`: el cursor se vuelve manito.
- `font-weight: 600`: semi-negrita.

```css
.wrapper .register-link{
    font-size: 14px;
    text-align: center;
    margin: 20px 0 15px;
}
.register-link p a{
    color: #fff;
    text-decoration: none;
    font-weight: 600;
}
.register-link p a:hover{
    text-decoration: underline;
}
```
Texto pequeño y centrado; enlace "Register" en blanco y negrita, con subrayado al pasar el mouse. (El `margin-top: 20px` comentado con `/* */` está desactivado; un comentario CSS **no se ejecuta**.)

---

## 8. Tabla maestra: HTML ↔ CSS

**Cómo se conecta cada elemento del HTML con su selector en el CSS.**

### Página principal

| Elemento en HTML | Atributo clave | Selector CSS que lo estiliza |
|---|---|---|
| `<header class="mainHeader">` | `class="mainHeader"` | `header.mainHeader` |
| `<h2 class="logotipo">` | (clase no usada) | `header.mainHeader h2` |
| `<nav class="mainNav">` | `class="mainNav"` | `header.mainHeader nav` |
| `<a>` dentro del nav | – | `header.mainHeader nav a` / `nav a:hover` |
| `<section class="mainSlider">` | `class="mainSlider"` | `section.mainSlider` y `section.mainSlider h2` |
| `<section class="news">` | `class="news"` | `section.news` |
| `<article class="newsItem">` | `class="newsItem"` | `section.news .newsItem` |
| `<footer class="mainFooter">` | `class="mainFooter"` | `footer.mainFooter` |

### Login

| Elemento en HTML | Atributo clave | Selector CSS que lo estiliza |
|---|---|---|
| `<body class="bodylogin">` | `class="bodylogin"` | `body.bodylogin` |
| `<section class="wrapper">` | `class="wrapper"` | `.wrapper` |
| `<h1>` | – | `.wrapper h1` |
| `<div class="input-box">` | `class="input-box"` | `.wrapper .input-box` |
| `<input>` en `.input-box` | `type`, `placeholder` | `.input-box input`, `.input-box input::placeholder` |
| `<i class="bx bx-user">` | clases `bx` + `bx-user` | `.input-box i` |
| `<div class="remember-forgot">` | `class="remember-forgot"` | `.wrapper .remember-forgot` |
| `<input type="checkbox">` en label | – | `.remember-forgot label input` |
| `<a>` en `.remember-forgot` | `href` | `.remember-forgot a` / `a:hover` |
| `<button class="btn">` | `type="submit"`, `class="btn"` | `.wrapper .btn` |
| `<div class="register-link">` | `class="register-link"` | `.wrapper .register-link` |
| `<a>` dentro del `<p>` | – | `.register-link p a` / `a:hover` |

### Regla mnemotécnica para "referenciar"

| Escribes en CSS | Significa |
|---|---|
| `p` | todos los `<p>` |
| `.caja` | todo lo que tenga `class="caja"` |
| `#caja` | lo que tenga `id="caja"` (único en la página) |
| `div.caja` | un `<div>` con clase `caja` (**pegado**) |
| `div .caja` | algo con clase `caja` **dentro** de un `<div>` (**con espacio**) |
| `a, p` | los `<a>` **y** los `<p>` |
| `a:hover` | los `<a>` cuando el mouse está encima |
| `input::placeholder` | el texto de ayuda de los `input` |

---

## 9. Errores y malas prácticas del código

> Muy típico en exámenes: "identifique los errores".

| # | Dónde | Problema | Corrección |
|---|---|---|---|
| 1 | `style.css` → `.input-box input` | `color: #ff;` es un valor **hexadecimal inválido** (2 dígitos) | `color: #fff;` |
| 2 | `style.css` → `.input-box input` | `border: none;` seguida de `border: 2px solid ...` → la primera es **redundante** (la segunda la anula) | Dejar solo una |
| 3 | `index.html` → `<img src="">` | Sin atributo **`alt`** y con `src` vacío (incumple la buena práctica de HTML5) | `<img src="foto.jpg" alt="Descripción">` |
| 4 | `login.html` → `<input ... name="">` | `name` **vacío**: sin `name`, el dato **no se envía** con el formulario | `name="username"`, `name="password"` |
| 5 | `login.html` | Los campos usan solo `placeholder`, sin `<label>` asociado (accesibilidad) | Añadir `<label for="user">` e `id="user"` en el input |
| 6 | `index.html`/`login.html` | `<html>` sin `lang` | `<html lang="es">` |
| 7 | `index.html` → `<a href="">` | Enlaces **vacíos** (no navegan) | `href="login.html"`, etc. |
| 8 | `index.html` → `class="logotipo"` / `mainNav` | Clases declaradas pero **no usadas** en el CSS | Quitarlas o estilizarlas |
| 9 | Textos | "PROTAFOLIO", "Pasword", "Forgor", "acount" | PORTAFOLIO, Password, Forgot, account |
| 10 | `nav a:hover` | El `padding` cambia en hover y **mueve el diseño** | Mantener el mismo padding y cambiar solo color/fondo |
| 11 | `login.html` | Uso de `<section>` para el wrapper del login; sería más semántico `<main>` | `<main class="wrapper">` |
| 12 | Layout con `inline-block` | Entre elementos `inline-block` aparece un **pequeño espacio** por los saltos de línea del HTML | Usar **Flexbox** o **Grid** para layouts modernos |

---

## 10. Autoevaluación

**Arquitecturas web**
1. ¿Qué es una arquitectura web? ¿Qué dos cosas permite la WWW (comunicación e interoperabilidad)?
2. ¿Diferencia entre arquitectura **vertical** y **SILO**?
3. Un banco necesita separar presentación, lógica y datos con más seguridad. ¿Qué arquitectura eligiría? *(Multitier)*
4. Una app con tráfico muy irregular y pago solo por uso. *(Serverless)*
5. Un dashboard que no recarga la página. *(SPA)*
6. Un blog rápido y seguro con contenido desde APIs. *(JAMstack)*
7. Netflix, Uber y Amazon migraron a… *(Microservicios)*
8. ¿Qué significa cada letra de MVC?

**HTML**
9. ¿HTML es lenguaje de programación? Justifique. *(No, es de marcado.)*
10. Nombre las 7 etiquetas semánticas y su función.
11. ¿Cuándo uso `<article>` y cuándo `<section>`?
12. Escriba un formulario con un campo de correo, uno de fecha y un botón de envío.
13. Escriba una etiqueta de video con controles, silenciado y en bucle.
14. Nombre 4 buenas prácticas de HTML5.
15. ¿Para qué sirve `<meta name="viewport" ...>`?
16. ¿Qué hace `type="password"`? ¿Y `type="submit"`?
17. ¿Qué significa `../css/style.css`?

**CSS**
18. ¿Qué hace `margin: 0 auto`?
19. ¿Diferencia entre `header.mainHeader` y `header .mainHeader`?
20. ¿Qué hace `display: inline-block`?
21. Explique cómo se centra un elemento horizontal y verticalmente con Flexbox.
22. ¿Para qué sirve `min-height: 100vh`?
23. ¿Por qué el ícono usa `position: absolute` y el contenedor `position: relative`?
24. ¿Qué hace `box-sizing: border-box`?
25. En `padding: 20px 45px 20px 20px`, ¿qué valor corresponde a cada lado?
26. ¿Qué regla gana entre `*` y `header.mainHeader h2`? ¿Por qué?
27. ¿Qué hace `justify-content: space-between`?
28. Encuentre el error en `color: #ff;`.

---

### Pendientes para completar con tus apuntes

- [ ] Diapositivas 15–17 de Arquitecturas Web (stacks PHP, Python, JS).
- [ ] Si hubo más prácticas en el repositorio de GitHub (aparte del gist del login), pégalas para añadirlas a la sección 4/5/7.
- [ ] Confirmar con el profesor el formato (teoría, código o mixto).

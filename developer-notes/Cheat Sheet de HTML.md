# Cheat Sheet de HTML

Todo lo que aprendiste en los Pasos 1 a 7, con para qué sirve cada cosa, cómo se usa y una plantilla lista para copiar.

## 1. Esqueleto base y reglas de oro

Toda página HTML empieza con esta estructura. Cópiala siempre como punto de partida:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Título de la pestaña</title>
  </head>
  <body>
    <!-- Aquí va todo lo que se ve -->
  </body>
</html>
```

| Parte | Para qué sirve |
| --- | --- |
| `<!DOCTYPE html>` | Le dice al navegador que es HTML moderno |
| `<html lang="es">` | Envuelve todo; `lang` indica el idioma |
| `<head>` | Información invisible: título, codificación, estilos |
| `<meta charset="UTF-8">` | Para que se vean bien las tildes y la ñ |
| `<meta name="viewport" ...>` | Hace que la página se vea bien en el celular |
| `<title>` | Texto de la pestaña del navegador |
| `<body>` | Todo el contenido visible |

**Reglas de oro**

- Casi todas las etiquetas se abren y se cierran: `<p>` ... `</p>`.
- Las que no se cierran: `<img>`, `<input>`, `<br>`, `<meta>`.
- Los atributos van en la etiqueta de apertura: `<a href="...">`.
- Usa siempre comillas dobles en los valores: `src="foto.jpg"`.
- Usa sangría (2 espacios) para cada etiqueta hija: el código se lee mucho mejor.
- Nombres de archivo en minúsculas, sin espacios ni tildes: `mi-foto.jpg`.
- La página principal de un sitio se llama `index.html`.

## 2. Texto y listas

| Etiqueta | Para qué sirve | Ejemplo |
| --- | --- | --- |
| `<h1>` | Título principal (solo uno por página) | `<h1>Hola, soy María</h1>` |
| `<h2>` a `<h6>` | Subtítulos, de más a menos importante | `<h2>Sobre mí</h2>` |
| `<p>` | Párrafo | `<p>Texto aquí.</p>` |
| `<strong>` | Negrita (importante) | `<strong>muy importante</strong>` |
| `<em>` | Cursiva (énfasis) | `<em>cursiva</em>` |
| `<br>` | Salto de línea (no se cierra) | `Línea 1<br>Línea 2` |
| `<hr>` | Línea horizontal separadora | `<hr>` |
| `<ul>` + `<li>` | Lista con viñetas (el orden no importa) | ver abajo |
| `<ol>` + `<li>` | Lista numerada (el orden importa) | ver abajo |

```html
<ul>
  <li>Escuchar música</li>
  <li>Ver películas</li>
</ul>

<ol>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ol>
```

Una lista puede tener otra lista dentro de un `<li>` (listas anidadas):

```html
<ul>
  <li>Deportes
    <ul>
      <li>Fútbol</li>
      <li>Natación</li>
    </ul>
  </li>
</ul>
```

**Recuerda:** usa los títulos para dar estructura, no para hacer el texto más grande. Para eso está CSS.

## 3. Imágenes y enlaces

**Imagen** (no se cierra):

```html
<img src="foto.jpg" alt="Descripción de la foto" width="300">
```

- `src`: ruta del archivo (debe estar en tu carpeta, junto a `index.html` o en una subcarpeta como `img/foto.jpg`).
- `alt`: descripción en texto. Es obligatorio por accesibilidad y se muestra si la imagen no carga.
- `width` / `height`: tamaño en píxeles. Con solo `width`, el alto se ajusta solo.

**Enlace:**

```html
<a href="https://www.wikipedia.org">Visitar Wikipedia</a>
```

| Tipo de enlace | Cómo se escribe |
| --- | --- |
| Externo (otra web) | `<a href="https://google.com">Google</a>` |
| Pestaña nueva | `<a href="https://google.com" target="_blank">Google</a>` |
| Correo | `<a href="mailto:tucorreo@ejemplo.com">Escríbeme</a>` |
| Otra página tuya | `<a href="contacto.html">Contacto</a>` |
| Ancla en la misma página | `<a href="#contacto">Ir a contacto</a>` (y en el destino: `<section id="contacto">`) |
| Imagen como enlace | `<a href="https://google.com"><img src="foto.jpg" alt="Foto"></a>` |

**Recuerda:**

- Los enlaces externos siempre llevan `https://`. Sin eso, el navegador busca un archivo dentro de tu carpeta.
- Puedes meter `<p>`, `<h2>` o `<img>` dentro de un `<a>`, pero nunca otro `<a>` ni botones.
- El texto del enlace debe decir a dónde lleva: "Ver mi portafolio", no "haz clic aquí".
- Para enlaces con `target="_blank"` es buena práctica agregar `rel="noopener"` por seguridad.

## 4. Secciones semánticas

Estas etiquetas no cambian cómo se ve la página: describen **qué es** cada parte. Ayudan a Google, a los lectores de pantalla y a ti cuando lees tu código.

| Etiqueta | Para qué sirve | Cuántas veces |
| --- | --- | --- |
| `<header>` | Parte de arriba: título, logo, menú | Una por página (o una por sección) |
| `<nav>` | Menú con los enlaces principales | Las que necesites |
| `<main>` | Contenido principal de la página | **Solo una** |
| `<section>` | Bloque con un tema, normalmente con su `<h2>` | Varias |
| `<article>` | Contenido independiente (una entrada de blog, una tarjeta) | Varias |
| `<aside>` | Contenido lateral o secundario | Opcional |
| `<footer>` | Parte de abajo: derechos, contacto, redes | Una |
| `<div>` | Caja genérica sin significado, para agrupar y dar estilo | Todas las que necesites |
| `<span>` | Caja genérica en línea, dentro de un texto | Las que necesites |

```html
<body>
  <header>
    <h1>Mi sitio</h1>
    <nav>
      <a href="index.html">Inicio</a> |
      <a href="contacto.html">Contacto</a>
    </nav>
  </header>

  <main>
    <section>
      <h2>Sobre mí</h2>
      <p>Texto...</p>
    </section>
  </main>

  <footer>
    <p>&copy; 2026 María</p>
  </footer>
</body>
```

**Regla práctica:** si existe una etiqueta semántica que describe lo que es, úsala. Usa `<div>` solo cuando ninguna encaje.

## 5. Formularios

```html
<form>
  <label for="nombre">Nombre:</label>
  <input type="text" id="nombre" name="nombre" required placeholder="Tu nombre">
  <button type="submit">Enviar</button>
</form>
```

| Elemento | Para qué sirve |
| --- | --- |
| `<form>` | Envuelve todo el formulario |
| `<label for="x">` | Texto del campo; su `for` debe ser igual al `id` del campo |
| `<input type="text">` | Texto corto |
| `<input type="email">` | Correo (valida que tenga @) |
| `<input type="password">` | Contraseña (oculta lo escrito) |
| `<input type="number" min="1" max="120">` | Números, con límites |
| `<input type="date">` | Selector de fecha |
| `<input type="checkbox">` | Casilla de marcar / desmarcar |
| `<input type="radio">` | Elegir una sola opción (mismo `name` en el grupo) |
| `<textarea rows="5">` | Texto largo (mensaje) |
| `<select>` + `<option>` | Lista desplegable |
| `<button type="submit">` | Envía el formulario |

| Atributo | Qué hace |
| --- | --- |
| `id` | Identifica el campo (lo usa el `label`) |
| `name` | Nombre con el que viaja el dato al enviarlo |
| `required` | No deja enviar si está vacío |
| `placeholder` | Texto gris de ejemplo |
| `value` | Valor que se envía (en radios y opciones) |

**Select y radio, listos para copiar:**

```html
<label for="motivo">Motivo:</label>
<select id="motivo" name="motivo">
  <option value="pregunta">Tengo una pregunta</option>
  <option value="proyecto">Quiero proponerte un proyecto</option>
</select>

<input type="radio" id="correo" name="respuesta" value="correo">
<label for="correo">Por correo</label>
<input type="radio" id="tel" name="respuesta" value="telefono">
<label for="tel">Por teléfono</label>
```

**Recuerda:** solo con HTML el formulario se ve y valida, pero **no envía** el mensaje a ningún lado. Para recibirlo necesitas un servicio externo (por ejemplo Formspree o Netlify Forms) o programar un servidor. Con uno de esos servicios, solo cambias `<form>` por `<form action="URL-del-servicio" method="POST">`.

## 6. Comentarios y CSS básico

**Comentarios** (el navegador los ignora; sirven para explicar o "apagar" código):

```html
<!-- Esto es un comentario -->
<!-- <img src="foto.jpg" alt="Foto"> -->   (código apagado)
```

Atajo en VS Code: **Ctrl + /** (Mac: **Cmd + /**). No escribas contraseñas ni datos privados en comentarios: cualquiera puede verlos con "Ver código fuente".

**CSS dentro del `<head>`:**

```html
<head>
  <style>
    selector {
      propiedad: valor;
    }
  </style>
</head>
```

| Quiero... | CSS |
| --- | --- |
| Centrar el texto | `text-align: center;` |
| Columna centrada en la pantalla | `max-width: 700px; margin: 0 auto;` |
| Espacio interno | `padding: 20px;` |
| Espacio externo | `margin: 20px;` |
| Color de texto | `color: #333;` |
| Color de fondo | `background-color: #f5f5f5;` |
| Cambiar tipo de letra | `font-family: Arial, sans-serif;` |
| Tamaño de letra | `font-size: 18px;` |
| Bordes redondeados | `border-radius: 8px;` |
| Centrar solo una imagen | `display: block; margin: 0 auto;` |

**Cómo conectar un archivo CSS aparte** (lo mejor cuando el proyecto crece):

```html
<link rel="stylesheet" href="estilos.css">
```

Va dentro del `<head>`, y el archivo `estilos.css` contiene solo las reglas, sin la etiqueta `<style>`.

## 7. Plantilla de página profesional

Copia este código en `index.html`, cambia los textos y ya tienes una base limpia, centrada y que se ve bien en celular. Usa todo lo que aprendiste: estructura semántica, imágenes, enlaces, listas, formulario y CSS básico.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Mi página personal: quién soy y qué hago.">
  <title>María | Página personal</title>

  <style>
    /* ===== Estilos generales ===== */
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      color: #333;
      background-color: #f9f9f9;
      margin: 0;
    }

    /* Bloques con ancho máximo y centrados */
    header, main, footer {
      max-width: 700px;
      margin: 0 auto;
      padding: 20px;
    }

    header { text-align: center; }

    header img {
      border-radius: 50%;
      display: block;
      margin: 0 auto 10px;
    }

    nav a {
      margin: 0 10px;
      text-decoration: none;
      color: #0066cc;
    }
    nav a:hover { text-decoration: underline; }

    section { margin-bottom: 30px; }

    footer {
      text-align: center;
      font-size: 14px;
      color: #777;
      border-top: 1px solid #ddd;
    }

    button {
      background-color: #0066cc;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 6px;
      cursor: pointer;
    }
  </style>
</head>

<body>

  <!-- ===== Encabezado ===== -->
  <header>
    <img src="foto.jpg" alt="Foto de María" width="150">
    <h1>Hola, soy María</h1>
    <nav>
      <a href="#sobre-mi">Sobre mí</a>
      <a href="#hobbies">Hobbies</a>
      <a href="#contacto">Contacto</a>
    </nav>
  </header>

  <!-- ===== Contenido principal ===== -->
  <main>

    <section id="sobre-mi">
      <h2>Sobre mí</h2>
      <p>Tengo <strong>25 años</strong> y estoy aprendiendo a crear páginas web.</p>
    </section>

    <section id="hobbies">
      <h2>Mis hobbies</h2>
      <ul>
        <li>Escuchar música</li>
        <li>Ver películas</li>
        <li>Salir a caminar</li>
      </ul>
    </section>

    <section id="contacto">
      <h2>Contacto</h2>
      <form>
        <p>
          <label for="nombre">Nombre:</label><br>
          <input type="text" id="nombre" name="nombre" required>
        </p>
        <p>
          <label for="correo">Correo:</label><br>
          <input type="email" id="correo" name="correo" required>
        </p>
        <p>
          <label for="mensaje">Mensaje:</label><br>
          <textarea id="mensaje" name="mensaje" rows="5" required></textarea>
        </p>
        <button type="submit">Enviar</button>
      </form>
    </section>

  </main>

  <!-- ===== Pie de página ===== -->
  <footer>
    <p>&copy; 2026 María. Hecho con HTML.</p>
  </footer>

</body>
</html>
```

**Qué hace que se vea profesional**

- Ancho máximo y centrado: el texto no se estira por toda la pantalla.
- Poca variedad: una fuente, dos o tres colores.
- Espacio de sobra (`padding`, `margin`, `line-height`) entre elementos.
- Estructura semántica y títulos en orden (`h1`, luego `h2`).
- Todas las imágenes con `alt`.
- Se ve bien en celular gracias al `meta viewport`.

**Orden recomendado para un proyecto**

1. Escribe primero todo el HTML, sin estilos.
2. Comprueba que todo se ve, los enlaces llevan a donde deben y las imágenes cargan.
3. Agrega el CSS al final, de a poco, recargando con F5 cada vez.

## 8. Errores comunes y checklist

| Si pasa esto... | Revisa esto |
| --- | --- |
| La imagen no aparece | Nombre exacto (mayúsculas y extensión), que esté en la misma carpeta, sin espacios |
| Un enlace interno no abre | Que el archivo exista y el nombre coincida: `contacto.html` |
| Un enlace externo busca un archivo | Falta `https://` al inicio |
| Todo el texto es un enlace | Falta cerrar `</a>` |
| Todo desapareció después de un punto | Un comentario sin cerrar `-->` |
| Los cambios no se ven | Guardaste el archivo (Ctrl + S) y recargaste (F5) |
| Salen símbolos raros en lugar de tildes | Falta `<meta charset="UTF-8">` en el `<head>` |
| El formulario no envía nada | Es normal: HTML solo no envía; hace falta un servicio o servidor |
| Un campo de radio deja marcar varios | Todos los radios del grupo deben tener el mismo `name` |
| El layout se ve raro | Etiqueta mal cerrada o mal anidada: revisa la sangría |

**Anidar bien las etiquetas** (la que se abre al final se cierra primero):

```html
<!-- Correcto -->
<p>Texto <strong>importante</strong></p>

<!-- Incorrecto -->
<p>Texto <strong>importante</p></strong>
```

**Checklist antes de dar por terminada una página**

- [ ] Tiene `<!DOCTYPE html>`, `lang="es"`, `charset` y `<title>`
- [ ] Solo hay un `<h1>` y los títulos van en orden
- [ ] Cada `<img>` tiene `alt`
- [ ] Los enlaces llevan a donde dicen (pruébalos todos)
- [ ] Cada `<input>` tiene su `<label>` con `for` e `id` iguales
- [ ] Todas las etiquetas están cerradas y bien anidadas
- [ ] Nombres de archivo en minúsculas y sin espacios
- [ ] Probaste la página achicando la ventana (así se verá en celular)
- [ ] No dejaste comentarios con datos privados

**Próximos pasos para seguir aprendiendo**

1. CSS a fondo: colores, tipografías, `flexbox` para acomodar elementos.
2. Diseño responsive con `@media`.
3. JavaScript para hacer la página interactiva.
4. Publicar tu sitio gratis con GitHub Pages o Netlify.

Para practicar con documentación confiable: [MDN Web Docs en español](https://developer.mozilla.org/es/).

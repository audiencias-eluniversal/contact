# Contexto del proyecto

Repositorio de **landing pages de redirección** de El Universal (Audiencias). Cada página es un HTML estático que muestra una cuenta regresiva de 3 segundos y redirige al destino (normalmente WhatsApp). Sirve para medir el tráfico que llega desde El Universal hacia cada aliado/cliente.

Se publica con GitHub Pages: `https://audiencias-eluniversal.github.io/contact/<carpeta>/<archivo>.html`

## Estructura

Una carpeta por cliente/producto, con una o más páginas HTML:

| Carpeta | Páginas |
|---|---|
| `luchy-coach` | `neuro-reset.html` (plantilla base) |
| `magic-and-moments` | `despedida-de-soltera.html`, `pedida-de-mano.html` |
| `multydrink` | `multydrink.html` (destino: `http://yux.fi/Multydrink`, un enlace especial de WhatsApp) |
| `newport` | `newport.html` |
| `promotora-dirc` | `la-ramada-caribe.html`, `nuevo-ramada-caribe.html` |
| `PyM` | `hogar.html`, `salud.html`, `vehiculos.html` |
| `supergiros` | `soat-nov-2026.html` |

`pixel_meta.txt` contiene el snippet oficial del Pixel de Meta de El Universal.

## Anatomía de una página

Se crea copiando una existente (la plantilla base es `luchy-coach/neuro-reset.html`) y cambiando:

1. `<title>`, `description`, y las etiquetas Open Graph / Twitter (título, descripción, `og:url`).
2. `urlDestino` en el `<script>` (enlace de WhatsApp o enlace corto).
3. Textos visibles si aplica.

Se mantiene sin cambios: estilos, Font Awesome, cuenta regresiva y el script de **GoatCounter** (`https://audienciaseluniversal.goatcounter.com/count`) antes de `</body>`.

## Regla: Pixel de Meta obligatorio

**Cada vez que se cree una página nueva o se actualice una existente, verificar que el HTML tenga el Pixel de Meta** (buscar `fbq('init', '1778254566808591')`). Si no lo tiene, agregarlo:

- Copiar el contenido de `pixel_meta.txt` y pegarlo dentro de `<head>`, justo antes de `</head>`.
- No duplicarlo si ya está.

Nota: páginas anteriores a esta regla pueden no tenerlo todavía; añadirlo la próxima vez que se toquen.

## Convenciones

- Idioma: español (`lang="es"`).
- Commits en español, mensajes cortos (p. ej. "Creado Multydrink").
- Trabajo directo sobre `main`.

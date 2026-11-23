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

## Regla: evento de contacto (Meta + GoatCounter)

Toda página nueva o actualizada debe registrar el evento de contacto justo antes de redirigir al destino. Referencia: `multydrink/multydrink.html`.

- **Meta:** `fbq('track', 'Contact')` (evento estándar; se ve en la columna "Contactos" de Ads Manager si el pixel está asociado a la cuenta y el evento se atribuye a un anuncio).
- **GoatCounter:** `goatcounter.count({ path: 'contacto-<producto>-<destino>', title: '...', event: true })`. Ejemplo: `contacto-multydrink-yuxfi`.
- Ambos se disparan desde una función única (`irAlDestino()`), usada tanto por la cuenta regresiva como por el clic en el botón, con una bandera para no contar dos veces.
- Se espera 400 ms antes de cambiar `window.location.href` para que los eventos alcancen a enviarse.
- Cada llamada va en `try/catch` y verifica que `fbq` / `goatcounter` existan, para que un bloqueador no impida la redirección.
- El evento mide que el usuario fue enviado al destino, no que llegó ni que escribió.
- Al actualizar una página existente que no lo tenga, agregarlo.

Verificación: Events Manager > Probar eventos (Meta) y pestaña de eventos en GoatCounter.

## Convenciones

- Idioma: español (`lang="es"`).
- Commits en español, mensajes cortos (p. ej. "Creado Multydrink").
- Trabajo directo sobre `main`.

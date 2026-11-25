# Loren Ipsum · Prototipo funcional

Un solo archivo: `index.html` (HTML + CSS + JS, sin dependencias externas salvo Google Fonts).

## Pantallas (rutas)
| Ruta | Qué hace |
|---|---|
| `#/` | Landing de venta (hero, qué incluye, cómo funciona, todo incluido, testimonios, FAQ, oferta, cierre, footer legal) |
| `#/crear` | Editor en 5 pasos: nombres + fecha/hora + idioma → fotos (hasta 6, se comprimen) → canción (YouTube/Spotify) → carta (4 sugerencias) → revisar con vista previa |
| `#/pagar/ID` | Pago con Yape o Plin + envío del comprobante por WhatsApp. Pago con tarjeta si configuras `cardPaymentUrl` |
| `#/listo/ID` | QR, tarjeta imprimible (PNG 1080×1350), descarga de QR, compartir |
| `#/p/ID` | Página de la pareja: música, nombres, galería, contador en vivo, carta, 4 idiomas, compartir |
| `#/v/...` | La misma página, abierta desde el QR en cualquier celular |
| `#/demo` | Ejemplo |
| `#/mis-paginas` | Páginas creadas en el dispositivo (editar, pagar, ver QR, eliminar) |

## Configurar (bloque `CONFIG` al inicio del script)
- `price` y `priceNumber`, `whatsapp` (51 + número), datos de Yape y Plin (`qrImage` = URL de la imagen de tu QR).
- `cardPaymentUrl`: link de pago de tu pasarela. Valida en su documentación oficial cómo generarlo.
- `testMode: false` antes de publicar, para ocultar el botón "Simular pago aprobado".
- Colores: variables `:root` al inicio del CSS. Textos: dentro de `<template id="tpl-home">`.
- Meta Pixel y GA4: hay comentarios en el `<head>` donde pegarlos. Las UTM se guardan y se añaden a los mensajes de WhatsApp.
- Footer: reemplaza `[URL_TERMINOS]`, `[URL_PRIVACIDAD]`, `[URL_CAMBIOS]`, `[URL_LIBRO_RECLAMACIONES]`, la razón social y el RUC.
  El Libro de Reclamaciones virtual es obligatorio para una tienda online en Perú. Valídalo con un profesional.
- Testimonios: son espacios vacíos y deben llenarse con reseñas reales y autorizadas.

## Límites del prototipo (requieren servidor para producción)
1. **Datos locales:** las páginas se guardan en el navegador de quien las crea (IndexedDB).
2. **Fotos:** el QR lleva comprimidos los textos, la canción y la fecha, así que funciona en cualquier celular, pero **sin fotos**. Para mostrar fotos se necesita un backend (Supabase o Firebase) que guarde las imágenes y dé un enlace corto `/p/ID`. El objeto `Store` es el único punto que hay que reemplazar.
3. **Pagos:** la activación con Yape o Plin es manual. Para activar automáticamente se necesita una pasarela con confirmación en el servidor (webhook). El estado "pagado" nunca debe decidirse en el navegador.
4. **Cuentas:** el original pide cuenta y contraseña antes de crear. Aquí se omitió porque frena la conversión. En producción se puede pedir correo o WhatsApp al final, junto al pago.
5. **Carta con IA:** hoy son plantillas. La IA real va en el backend; nunca pongas claves de API en este archivo.

## Instalar
Sube `index.html` a cualquier hosting estático (Netlify, Vercel, Hostinger, cPanel). Debe servirse por **https** para que funcionen "copiar enlace" y "compartir".

## Qué probar
- **Celular:** el menú no se parte, la barra fija "Crear mi regalo" aparece al bajar, las fotos se suben desde la galería, la canción suena al tocar ▶ y el QR impreso se escanea bien.
- **PC:** se puede arrastrar y soltar fotos, la tarjeta se descarga y la navegación con teclado (Tab) funciona.

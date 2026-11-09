# Michael Monetiza Clips

Interfaz web responsive en español para preparar proyectos de clips a partir de videos grabados o transmisiones.

## Estado actual

**Prototipo de interfaz, no procesador de video.** La página permite elegir un archivo o introducir un enlace, seleccionar opciones de formato, duración, subtítulos y reencuadre, y guardar preferencias localmente. No sube archivos a ningún servidor ni produce MP4. La galería es demostrativa.

## Publicar con GitHub Pages

En el repositorio, abre **Settings → Pages → Build and deployment → Deploy from a branch**, selecciona **main** y **/(root)**, y guarda. GitHub Pages puede tardar unos minutos en publicar. La dirección esperada, una vez activado, es `https://michael400600-byte.github.io/michael-monetiza-clips/`.

## Próximas fases

1. Backend de procesamiento con FFmpeg y transcripción local (Faster-Whisper).
2. Extracción de clips, puntuación de segmentos y exportación de MP4.
3. Integración segura de enlaces compatibles y, después, directos.

GitHub Pages solo aloja contenido estático; no ejecuta Python ni FFmpeg. No guardar secretos, credenciales ni tokens en este repositorio público.

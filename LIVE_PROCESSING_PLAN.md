# Michael Monetiza Clips — procesamiento de directos (fase 1)

## Objetivo confirmado
- Plataforma web; procesamiento en servidor, no en el equipo del usuario.
- Entrada: enlace de YouTube Live autorizado.
- Analizar durante la transmisión, sin esperar al final.
- Detectar y generar candidatos automáticamente (30–60 segundos, 9:16, subtítulos).
- Mostrar vista previa y lista de candidatos; **el usuario selecciona y descarga manualmente**.
- Nunca publicar automáticamente.

## Arquitectura propuesta (aún NO desplegada)
1. Frontend estático existente en GitHub Pages.
2. API en servicio externo con HTTPS y CORS restringido al origen de Pages.
3. Cola de trabajos y trabajador de video con FFmpeg y transcripción.
4. Ingesta autorizada del live: verificar acceso y condiciones de YouTube; no eludir DRM ni controles de acceso.
5. Buffer por ventanas de 60–120 s; analizar audio y cortes de escena; puntuar candidatos con contexto.
6. Render 9:16 y subtítulos; guardar MP4 temporalmente en almacenamiento de objetos.
7. API para progreso, lista de clips, previsualización y enlaces de descarga temporales.

## API propuesta
- POST /api/jobs {url, clipDuration, subtitles} -> {jobId}
- GET /api/jobs/{jobId} -> {status, processedSeconds, error}
- GET /api/jobs/{jobId}/clips -> [{id, start, end, score, previewUrl, downloadUrl}]
- POST /api/jobs/{jobId}/stop -> {status}

## Antes de activar
- Elegir proveedor de servidor con capacidad de FFmpeg, almacenamiento y trabajos largos; los planes gratis pueden suspender procesos.
- Verificar que el enlace de prueba permita ingestión autorizada en vivo.
- Añadir controles de costo, límite de duración, eliminación automática y protección contra URLs internas (SSRF).
- Implementar y probar el backend; conectar frontend y desplegar.

**Estado:** especificación técnica únicamente. No procesa ni descarga videos reales todavía.

## Proveedor elegido (9 noviembre 2026)
Oracle Cloud Always Free como primera opción de prueba, sujeto a registro, verificación, disponibilidad de instancia ARM y cuotas. Mantener GitHub Pages para frontend. No existe todavía servidor desplegado ni conexión API; no afirmar que se generan clips reales. No solicitar credenciales ni tarjetas en el chat. Siguiente paso: usuario crea cuenta desde sitio oficial y confirma que llegó a la consola; después se prepara la instancia y se despliega el backend.

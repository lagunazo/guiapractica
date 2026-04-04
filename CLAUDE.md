# Guía Práctica de Limpieza de Lagunas — Proyecto Web

## Contexto del proyecto
Landing page de lanzamiento para la publicación "Guía Práctica de Limpieza de Lagunas" de Basura Cero Argentina y Punto Tach. Publicada en lagunasbasuracero.com.ar via GitHub Pages.

## Repositorio
- GitHub: https://github.com/lagunazo/guiapractica
- URL producción: https://lagunasbasuracero.com.ar
- URL GitHub Pages original: https://lagunazo.github.io/guiapractica/

## Stack técnico
- HTML estático + Tailwind CSS CDN (inline) + CSS propio (styles.css)
- Sin framework. Sin bundler. Sin npm.
- Hosting: GitHub Pages
- DNS: Cloudflare → NIC.ar (dominio .com.ar)

## Estructura de archivos
```
/
├── index.html          ← archivo principal
├── styles.css          ← CSS propio (NO Tailwind)
├── CNAME               ← contiene: lagunasbasuracero.com.ar
├── images/
│   ├── hero.png        ← fondo hero section
│   ├── mockup1.png     ← mockup del libro (versión actual)
│   ├── logo_ptach.svg  ← logo Punto Tach
│   ├── logo_basuracero.png ← logo Basura Cero Argentina
│   ├── og_imageA.jpg   ← imagen Open Graph (1200x630px)
│   ├── image_2.png     ← foto sección El Problema
│   ├── paso_1.png      ← foto Planificación
│   ├── paso_2.png      ← foto Ejecución
│   ├── paso_3.png      ← foto Evaluación
│   ├── destacada.png   ← foto galería principal
│   ├── foto_grilla_1.png
│   ├── foto_grilla_2.png
│   ├── foto_grilla_3.png
│   └── foto_grilla_4.png
└── pdf/
    └── Guia_PracticaOK2.pdf  ← PDF descargable (versión actual)
```

## REGLA CRÍTICA — Dos sistemas de estilos coexisten
**SIEMPRE verificar antes de cualquier cambio:**
- El `<header id="hero">` usa EXCLUSIVAMENTE clases Tailwind inline. NUNCA agregar CSS externo para el hero.
- El navbar usa EXCLUSIVAMENTE clases propias en styles.css (.custom-navbar, .navbar-logos, etc.)
- El resto de secciones mezcla ambos sistemas.

## Colores de marca
```
#1a4b6e  azul profundo (primario)
#2d6a4f  verde bosque (secundario)
#e86f51  coral/naranja (acento, CTAs)
#f8f6f1  blanco roto (fondo)
```

## Servicios externos integrados
| Servicio | Uso | Credencial |
|----------|-----|------------|
| Formspree | Formulario contacto | https://formspree.io/f/xdawjgzr |
| Supabase | Contador de descargas | URL: https://yjzgkmiwhxjncofrtuuq.supabase.co |
| Google Analytics 4 | Estadísticas | ID: G-0MZ62JBKH7 |
| Cloudflare | DNS | Panel: cloudflare.com |

## Supabase — estructura de la tabla contador
```sql
tabla: contador
columnas: id (bigint, PK, auto), valor (bigint, default 0)
fila actual: id=1, valor=N (se incrementa con cada descarga)
políticas RLS: SELECT y UPDATE habilitados para anon
```

## Secciones del index.html (en orden)
1. `<nav class="custom-navbar" id="main-nav">` — navbar fijo
2. `<header id="hero">` — hero Tailwind puro
3. `<section id="problema">` — El Problema
4. `<section id="guia">` — La Guía
5. `<section id="metodologia">` — 3 Pasos
6. `<section data-purpose="impact-stats">` — Cifras de impacto
7. `<section data-purpose="target-audience">` — Para quién
8. `<section id="autores">` — Autoras
9. `<section id="galeria">` — Galería
10. `<section data-purpose="final-cta">` — CTA descarga
11. `<section id="share-redes">` — Botones compartir (STANDALONE)
12. `<section id="contacto">` — Formulario
13. `<section id="privacidad">` — Política privacidad
14. `<footer>` — Footer

## ADVERTENCIA IMPORTANTE — share-section
La sección `#share-redes` es STANDALONE e independiente.
NUNCA debe estar dentro del div flex del CTA final.
Si se rompe: moverla fuera del div `class="flex flex-col sm:flex-row..."`.

## PDF descargable
- Ruta: `pdf/Guia_PracticaOK2.pdf`
- URL: https://lagunasbasuracero.com.ar/pdf/Guia_PracticaOK2.pdf
- GitHub Pages es case-sensitive: respetar mayúsculas exactas del nombre

## Open Graph
- Imagen: `images/og_imageA.jpg`
- URL canónica: https://lagunasbasuracero.com.ar/
- Twitter/X: @puntotach

## Google Analytics — eventos personalizados configurados
- `pdf_download` — clic en Descargar PDF
- `share` — clic en botones de compartir (method: whatsapp/facebook/twitter/instagram)
- `form_submit` — envío exitoso del formulario de contacto

## Flujo Git para actualizar el sitio
```bash
git pull origin main --rebase   # SIEMPRE primero
# ... hacer cambios ...
git add .
git commit -m "descripción del cambio"
git push origin main
```
Si hay archivos subidos manualmente desde la web de GitHub,
siempre hacer pull --rebase antes de push para evitar el error "rejected".

## Trabajo pendiente / próximas mejoras identificadas
- Feed de Instagram embebido (@puntotach + @basuracero.argentina)
- Mapa interactivo de jornadas realizadas (Leaflet.js + OpenStreetMap)
- Sección de testimonios de participantes
- FAQ en acordeón con preguntas frecuentes
- Migración de Formspree a Web3Forms (más estable, sin límite de envíos)
- Gamificación y comunidad (módulo de app)
- App móvil de limpieza de lagunas (esquema completo disponible en el historial del chat)

## Módulos de app planificados (esquema completo)
1. Registro de jornadas
2. Planilla digital de censo (reemplaza Anexo 1 de la guía)
3. Pesaje y cómputo de datos
4. Mapa de cuerpos de agua
5. Registro fotográfico
6. Dashboard de datos e impacto
7. Gamificación y comunidad
8. Convocatoria y difusión
9. Monitor ambiental (cianosemáforo)

## Organizaciones involucradas
- **Punto Tach** (Trama Activa Chascomunense) — Chascomús, Buenos Aires
  - Email: puntotach@gmail.com
  - Instagram: @puntotach
  - Facebook: https://www.facebook.com/profile.php?id=61587699427923
- **Basura Cero Argentina**
  - Instagram: @basuracero.argentina
  - Facebook: https://www.facebook.com/profile.php?id=100082586721318

## Autoras de la guía
- Paula Andrea Ramírez Ramírez — Administradora Ambiental, vocal Basura Cero Argentina
- Luciana Laura Schoj — activista, Punto Tach
- Camila Sánchez — Punto Tach
- Fotografías: Inés Otero (@inesotero_envuelolibre)

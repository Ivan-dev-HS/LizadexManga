# Subir Tomo a GitHub Pages

Esta carpeta ya está lista para publicarse tal cual: contiene `index.html`, tu icono en varios tamaños y el `manifest.json` para que se instale con tu icono.

## Pasos

1. Ve a github.com → **New repository**. Nómbralo, por ejemplo, `tomo-manga`. Puede ser público (necesario para GitHub Pages gratis).
2. Sube estos 6 archivos a la raíz del repositorio (arrastra y suelta en la web de GitHub, o con git):
   - `index.html`
   - `manifest.json`
   - `icon-192.png`
   - `icon-512.png`
   - `apple-touch-icon.png`
   - `favicon-32.png`
3. Ve a **Settings → Pages** dentro del repositorio.
4. En "Branch", elige `main` (o `master`) y carpeta `/ (root)`. Guarda.
5. Espera 1-2 minutos. GitHub te dará una URL como:
   `https://tu-usuario.github.io/tomo-manga/`

## Instalar en el móvil
1. Abre esa URL en el navegador del móvil.
2. iOS (Safari): botón compartir → **Añadir a pantalla de inicio**.
3. Android (Chrome): menú ⋮ → **Instalar app** (o "Añadir a pantalla de inicio").

En ambos casos el icono que verás en la pantalla de inicio será el tuyo (el logo azul y naranja), y la app se abrirá a pantalla completa, sin barra de navegador.

## Actualizaciones futuras
Cada vez que quieras cambiar algo en la app, solo sustituye `index.html` en el repositorio (o súbelo de nuevo con el mismo nombre) y GitHub Pages se actualiza solo.

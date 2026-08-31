# BiblioBP17 — PWA

Sube **el contenido de esta carpeta** a la raíz de tu repositorio de GitHub y activa GitHub Pages
(Settings → Pages → Deploy from a branch → `main` / `root`). La PWA necesita https: GitHub Pages ya lo da.

Archivos:

| Archivo | Para qué |
| --- | --- |
| `index.html` | La aplicación completa (HTML+CSS+JS autocontenido, sin dependencias) |
| `manifest.json` | Manifiesto PWA (nombre BiblioBP17, iconos, standalone) — enlazado desde el HTML |
| `sw.js` | Service worker: la app funciona sin conexión; el Excel se pide siempre a la red primero |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | Iconos de instalación (recorte de la foto de la balda) |
| `bibliotecaBP17.xlsx` | El catálogo. **Este es el archivo que actualizas en GitHub** |

## Instalar en Chrome

Abre `https://<usuario>.github.io/<repo>/` → menú ⋮ → *Instalar aplicación*
(o el botón «Instalar aplicación» de la cabecera, que aparece cuando Chrome lo permite).

## Cómo se manejan los datos

- Primer arranque: la app lee `bibliotecaBP17.xlsx` del repositorio y lo guarda en el dispositivo.
- A partir de ahí trabaja siempre sobre la copia local, así que las ediciones, altas y bajas persisten
  aunque estés sin conexión.
- Pantalla **Datos**: traer del repositorio *sustituyendo* todo, traer *fusionando* solo los libros
  nuevos (comparando título+autor), cargar un `.xlsx` del dispositivo, exportar CSV o copia `.json`,
  restaurar copia y vaciar los datos locales.
- Si cambias el Excel en GitHub, basta con «Traer del repositorio»; el service worker no cachea el
  `.xlsx` por delante de la red.

## Al cambiar el HTML

Sube el número de versión en `sw.js` (`const CACHE = 'bibliobp17-v1'` → `v2`) para que Chrome
descarte la copia antigua.

## Columnas del Excel

Se reconocen por el nombre del encabezado (sin distinguir mayúsculas ni acentos): Título, Autor,
Librería, Estante, Sección, Ubicación, Género, Resumen, Saga, Nº en la saga, Idioma, Editorial,
Año de publicación, Palabras clave. Si no reconoce al menos cinco, usa ese mismo orden de columnas.

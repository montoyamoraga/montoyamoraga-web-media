# montoyamoraga-web-media

Repositorio de imágenes para los proyectos web de montoyamoraga.

## Estructura de carpetas

Cada proyecto vive en su propia carpeta en la raíz del repositorio, con el nombre:

```text
AAAA-proyecto
```

Dentro de cada carpeta de proyecto, las imágenes se organizan en subcarpetas según su formato:

```text
AAAA-proyecto/
  jpg/   fotos originales en jpg (00.jpg, 01.jpg, ...)
  png/   imágenes originales en png (00-portada.png, ...)
  webp/  previews en formato webp, generadas automáticamente a partir de jpg/ y png/
```

Los archivos se nombran con números de dos dígitos empezando en `00`, opcionalmente seguidos de una descripción (por ejemplo `00-portada.png`). Cada `.webp` mantiene el mismo nombre que su original.

Excepción: en las colecciones de videos fechados, los archivos se nombran solo con su fecha (`AAAA-MM-DD.mp4`), y la fecha define el orden. Por ejemplo `2026-callese-hombre/mp4/2026-09-16.mp4`.

## Fotos de cursos

Las fotos de los cursos de enseñanza de montoyamoraga.github.io van en una carpeta por curso, `ensenanza-<curso>/jpg/`. Mantienen su nombre de archivo original, que identifica a les autores de cada trabajo (por ejemplo `ensenanza-dis8636/jpg/dis8636-theo-rios.jpg`), y se listan por ese nombre en `datos/ensenanza.yaml` del sitio. El sitio muestra la versión de `webp/`.

Las fotos deben quedar derechas en sus píxeles: `cwebp` ignora la orientación EXIF de las fotos de celular, así que una foto que solo se ve derecha gracias a EXIF queda girada en `webp/`.

## GIF animados

Los GIF animados van en una subcarpeta `gif/` dentro de la carpeta del proyecto, con la misma numeración que el resto de las imágenes. No se convierten a webp: el sitio los muestra directamente desde `gif/`.

```text
AAAA-proyecto/
  gif/    animaciones en formato .gif
```

## SVG

Las imágenes vectoriales van en una subcarpeta `svg/` dentro de la carpeta del proyecto, con la misma numeración que el resto de las imágenes. Tampoco se convierten a webp: el sitio las muestra directamente desde `svg/`. Por ejemplo, los paneles de los módulos de VCV Rack en `2026-menatron/svg/`.

```text
AAAA-proyecto/
  svg/    imágenes vectoriales en formato .svg
```

## Modelos 3D

Los modelos 3D van en una subcarpeta `glb/` dentro de la carpeta del proyecto:

```text
AAAA-proyecto/
  glb/    modelos 3D en formato .glb
```

Por ejemplo, el escaneo 3D de la página de inicio de montoyamoraga.github.io está en `2026-escaneo-3d/glb/montoyamoraga-2026-08.glb`, y se carga desde:

```text
https://cdn.jsdelivr.net/gh/montoyamoraga/montoyamoraga-web-media@main/2026-escaneo-3d/glb/montoyamoraga-2026-08.glb
```

## Previstas

La carpeta `previstas/` tiene las imágenes que se muestran al compartir un enlace de montoyamoraga.github.io en WhatsApp o redes sociales (etiqueta `og:image`). Cada prevista mide 1200×630 y pesa menos de 300 KB, porque WhatsApp no muestra imágenes más pesadas.

```text
previstas/
  sitio.jpg               prevista por defecto del sitio
  ensenanza-<curso>.jpg   prevista de cada curso, por ejemplo ensenanza-dis8636.jpg
```

## Generación de previews webp

Las imágenes en `webp/` se generan automáticamente a partir de las que están en `jpg/` y `png/`, usando [`scripts/generar-webp.sh`](scripts/generar-webp.sh) y `cwebp`.

Esto corre solo, mediante el GitHub Action [`generar-webp.yml`](.github/workflows/generar-webp.yml): cada vez que se sube una imagen nueva a una carpeta `jpg/` o `png/` en `main`, el workflow genera los `.webp` correspondientes y los commitea de vuelta al repositorio.

También se puede correr a mano desde la raíz del repositorio:

```sh
scripts/generar-webp.sh
```

Esto requiere tener `cwebp` instalado (en macOS: `brew install webp`). El script recorre todas las carpetas `jpg/` y `png/` del repositorio y genera los `.webp` que falten o estén desactualizados en la carpeta `webp/` correspondiente.

# montoyamoraga-web-media

Repositorio de imágenes para los proyectos web de montoyamoraga.

## Estructura de carpetas

Cada proyecto vive en su propia carpeta en la raíz del repositorio, con el nombre:

```text
AAAA-proyecto
```

Dentro de cada carpeta de proyecto, las fotos se organizan en dos subcarpetas:

```text
AAAA-proyecto/
  jpg/    fotos originales (00.jpg, 01.jpg, ...)
  webp/   previews en formato webp, generadas automáticamente a partir de jpg/
```

Los archivos dentro de `jpg/` y `webp/` se nombran con números de dos dígitos empezando en `00`, en el mismo orden que las fotos originales.

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

## Generación de previews webp

Las imágenes en `webp/` se generan automáticamente a partir de las que están en `jpg/`, usando [`scripts/generar-webp.sh`](scripts/generar-webp.sh) y `cwebp`.

Esto corre solo, mediante el GitHub Action [`generar-webp.yml`](.github/workflows/generar-webp.yml): cada vez que se sube una foto nueva a una carpeta `jpg/` en `main`, el workflow genera los `.webp` correspondientes y los commitea de vuelta al repositorio.

También se puede correr a mano desde la raíz del repositorio:

```sh
scripts/generar-webp.sh
```

Esto requiere tener `cwebp` instalado (en macOS: `brew install webp`). El script recorre todas las carpetas `jpg/` del repositorio y genera los `.webp` que falten o estén desactualizados en la carpeta `webp/` correspondiente.

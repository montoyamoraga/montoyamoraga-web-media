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

## Generación de previews webp

Las imágenes en `webp/` se generan automáticamente a partir de las que están en `jpg/` y `png/`, usando [`scripts/generar-webp.sh`](scripts/generar-webp.sh) y `cwebp`.

Esto corre solo, mediante el GitHub Action [`generar-webp.yml`](.github/workflows/generar-webp.yml): cada vez que se sube una imagen nueva a una carpeta `jpg/` o `png/` en `main`, el workflow genera los `.webp` correspondientes y los commitea de vuelta al repositorio.

También se puede correr a mano desde la raíz del repositorio:

```sh
scripts/generar-webp.sh
```

Esto requiere tener `cwebp` instalado (en macOS: `brew install webp`). El script recorre todas las carpetas `jpg/` y `png/` del repositorio y genera los `.webp` que falten o estén desactualizados en la carpeta `webp/` correspondiente.

# Procesador de palabras - UNIR

Aplicación de línea de comandos para leer palabras de un fichero de texto, ordenarlas alfabéticamente e imprimirlas. Cada línea del fichero se trata como una palabra. Se puede elegir si se eliminan las palabras duplicadas antes de imprimir el resultado.

Si el fichero indicado no existe, la aplicación muestra un aviso y procesa una lista de palabras de ejemplo.

## Ejecución

### Requisitos

- Python 3 para ejecutar el programa localmente.
- GNU Make para usar los comandos del Makefile.
- Docker para ejecutar el programa en un contenedor.

Los comandos del Makefile están pensados para Linux y macOS. En Windows, ejecútalos en una máquina virtual Linux o adapta los comandos a las herramientas disponibles.

### Ejecución local

Desde la raíz del repositorio, ejecuta:

```sh
make run-local
```

Este target procesa `words.txt` y elimina duplicados. Para elegir otro fichero u opción, invoca el script directamente:

```sh
python3 main.py <filename> <yes|no>
```

- `filename`: ruta al fichero que contiene una palabra por línea.
- `yes`: elimina palabras duplicadas antes de imprimirlas.
- `no`: conserva las palabras duplicadas.

La opción no distingue mayúsculas y minúsculas.

### Ejecución con Docker

```sh
make run
```

Este target ejecuta el programa dentro de un contenedor `python:3.6-slim` y monta el directorio del repositorio en el contenedor. No es necesario construir una imagen propia.

Para ejecutarlo con valores personalizados, usa Docker desde la raíz del repositorio:

```sh
docker run --rm --volume "$PWD:/opt/app" --workdir /opt/app python:3.6-slim python3 main.py words.txt no
```

En el ejemplo, `words.txt` es el fichero procesado y `no` conserva los duplicados. El contenedor es temporal (`--rm`): al finalizar, se elimina y no queda un servicio ejecutándose. El repositorio no incluye configuración para desplegar la aplicación como servicio permanente.

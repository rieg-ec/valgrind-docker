# Valgrind en Docker

## Pasos para instalar

1. Instala Docker y docker-compose. En macOS basta con instalar [docker desktop](https://docs.docker.com/desktop/mac/install/).
2. Verifica que tienes docker instalado con `docker -v`
3. Clona este repositorio: `git clone https://github.com/rieg-ec/valgrind-docer && cd valgrind-docker`. corre `docker compose up -d` dentro del directorio clonado.

## Cómo usar

1. Busca el id del contenedor con `docker ps`. El contenedor será el que empiece con `valgrind-docker_valgrind`. Copia el id.
2. En la consola ejecuta `docker compose exec <id del contenedor> /bin/bash`, con eso ingresaras al contenedor. En tu terminal deberia salir `root@0<id del contenedor>:/#`.
3. Corre `cd ~/volume` para ir a la carpeta con tu codigo. Si ahora corres `ls`, deberia haber un archivo `Makefile` y `hola.c`
4. Compila el codigo de prueba con `make`.
5. Ejecuta el binario resultante: `./hola`
6. Si el output es `funciona bien :)`, estas list@.
7. Tus archivos de C deben ir dentro de la carpeta `volume/`.

## Consideraciones importantes

- El contenedor de docker y tu computador _comparten_ la carpeta `/volumes`, por lo tanto puedes modificar cualquier archivo desde afuera del contenedor y los cambios se veran reflejados adentro también.

- Lo unico importante es siempre compilar tu codigo _desde adentro del contenedor_. Preocupate de seguir el 2do paso en la seccion `Cómo usar` para entrar al contenedor. Si compilas tu codigo desde afuera, puede ser que el binario resultante sea distinto y te arroje errores al ejecutarlo dentro del contenedor.

- El compilador y valgrind vienen instalados, no debes instalarlos tu. Puedes probar que valgrind esté funcionando: `valgrind ./hola`. Si crees que algo más debiera estar instalado por defecto avisame :)

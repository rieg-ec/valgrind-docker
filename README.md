# Valgrind y C en Docker

## Pasos para instalar

1. Instala Docker y docker-compose. En macOS basta con instalar [docker desktop](https://docs.docker.com/desktop/mac/install/).
2. Verifica que tienes docker instalado con `docker -v`
3. Clona este repositorio: `git clone https://github.com/rieg-ec/valgrind-docker && cd valgrind-docker`. corre `docker compose up -d` dentro del directorio clonado.
(Ojo. Es nescesario ejecutar `docker compose up -d` cada vez que quieras utilizar esto, aunque solo se demorara la primera vez)

## Cómo usar

1. En la consola ejecuta `docker compose run mycontainer /bin/bash`, con eso ingresaras al contenedor. En tu terminal deberia salir algo similar a `root@0<id del contenedor>:/#`.
2. Corre `cd ~/volume` para ir a la carpeta con tu codigo. 
3. desde aca puedes utilizar la consola como quieras, para compilar, ejecutar o utilizar valgrind.

Por ejemplo si tienes la carpeta
```
 │volume
    └───code
    │   └───src
    │   │
    │   └───tests
    │   │
    │   └Makefile
```

los comandos son ejecutados *Dentro* del container (con el comando mencionado anteriormente)

```
cd ~/volume # ir a carpeta volume (Importante)
cd code/ # entrar a la carpeta que deseamos
make
./program # ejecutar ejecutar el ejecutable 
valgrind ./program #ejecutar valgrind
```



## Consideraciones importantes

- El contenedor de docker y tu computador _comparten_ la carpeta `/volumes`, por lo tanto puedes modificar cualquier archivo desde afuera del contenedor y los cambios se veran reflejados adentro también.

- Lo unico importante es siempre compilar tu codigo _desde adentro del contenedor_. Preocupate de seguir el 2do paso en la seccion `Cómo usar` para entrar al contenedor. Si compilas tu codigo desde afuera, puede ser que el binario resultante sea distinto y te arroje errores al ejecutarlo dentro del contenedor.

- El compilador y valgrind vienen instalados, no debes instalarlos tu. Puedes probar que valgrind esté funcionando: `valgrind ./program`. Si crees que algo más debiera estar instalado por defecto avisame :)

- Si deseas cambiarle el nombre al container, basta con cambiarlo en el archivo `docker-compose.yml`

- La primera vez que ejecutes `docker-compose up -d` tomara algun tiempo ya que ha de descargar todos los archivos nescesarios.
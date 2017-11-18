![Docker][img-dockerhead]
***

> La siguiente información sobre [_Docker_](https://docs.docker.com/) tiene exclusivamente carácter didáctico personal, como respaldo de mis apuntes, notas y pequeñas prácticas. Sirviendo como fuente de consulta, tanto para mí como para cualquiera a quien pudiera interesar. 


# Introducción a DOCKER
### Secciones del curso:
##### Primer bloque
- [01 - Introducción a contenedores y Docker][s1]
- [02 - Instalar Docker][s2]
- [03 - Primeros pasos con Docker][s3]
- [04 - Rutinas diarias con imagenes y contenedores][s4]

##### Segundo bloque
- [05 - Construyendo imagenes][s5]
- [06 - Volúmenes en Docker][s6]
- [07 - Publicar servicios][s7]
- [08 - Publicar imagenes en Docker Cloud][s8]
- [09 - Publicar imagenes desde Github][s9]

##### Tercer bloque
- [10 - Desplegar en producción][s10]
- [11 - Conectando contenedores][s11]
- [12 - Registros privados en Docker][s12]
- [13 - Conclusiones y resultados][s13]
- [14 - Ejercicios y actividades][s14]
---
#### Requisitos:
- Comandos básicos en Linux
- Editores de texto - vi, vim, nano..,
- Ordenador con conexión a Internet
- Sistema de virtualización instalado, VirtualBox, VMWare...

#### Objetivos:
- Dominar la plataforma de Docker
- Adaptar Docker a nuestra infraestructura
- Crear y desplegar servicios con Docker
- Orquestar y escalar los servicios
- Crear registros privados de Docker
---
### Primer bloque
##### _Sección 01_
### Introducción a contenedores y Docker.
- [Comportamiento distinto en función del entorno][s1s1s1]
- [¿Qué son los contenedores y las imagenes?][s1s2s2]
- [¿Qué es Docker?][s1s3s3]
- [Productos y herramientas][s1s4s4]
- [Los Contenedores no son máquinas virtuales][s1s5s5]

#

---
>***Comportamiento distinto en función del entorno***
---
Empaquetando la aplicación con todas las dependencias que son necesarias para que sea autónoma (librerías, OS, servidor) podríamos evitar problemas de comportamientos distintos entre las máquinas utilizadas para el desarrollo de software respecto a las máquinas de despliegue.
| App
|-
| bin/libs
| OS
| Infraestructura

#

---
> ***¿Qué son los contenedores y las imagen |imagenes?***
Unidad de software estandarizada
---
Un ***contenedor*** es un paquete ejecutable, ligero y autónomo con todo lo necesario para su ejecución. (App, servidor de la app, bibliotecas y componentes, configuraciones, OS *sólo los ficheros necesarios...). 
Es ***portable***, al conservar todos los elementos de una máquina a otra. 
Funcionan de forma ***aislada***, sin necesitar de otros procesos para su ejecución ni entrar en conflicto con dependencias de otros contenedores desplegados en el mismo servidor, dado que los contenedores ***son estancos***.

 Las ***Imagenes*** son el resultado del empaquetado y el ***Contenedor*** es la ejecución de la imagen. 
- De una imagen pueden ejecutarse muchos contenedores.
- Una imagen no tiene estado, sólo es el empaquetado. 
- Un contenedor puede tener distintos estados (Iniciado - Detenido/Pausado - Terminado)

![docker][img-docker]

#

---
> ***¿Qué es Docker?***
---
Plataforma para la gestión de contenedores y, a su vez, una tecnología para desplegar aplicaciones.

Utilizado por ***Programadores & Administradores***
- Reduce el tiempo de instalación y configuración.
- Evita problemas de compatibilidad al utilizar múltiples versiones en nuestros sistemas. 
- Rápido empaquetado y despliegue.
- Permite escalar aplicaciones en tiempo real.
- Garantiza el correcto funcionamiento en múltiples entornos.

#

---
> ***Productos y herramientas*** 
---
Utilizados para la gestión de los contenedores e imagenes:

| Logo | Herramienta | 
| ------ | ------ | 
|![logoLite] [img-docker_lite] | ***Docker:***  Motor principal para la gestión de contenedores. Encargado de crear, obtener y publicar imagenes, así como el despliegue, ejecución y parada de los contenedores.
| ![][img-compose]  | ***Docker-Compose:*** Ayuda para gestionar múltiples contenedores y servicios al mismo tiempo a través de sencillas configuraciones. |
| ![][img-swarm] | ***Docker-Swarm:*** Ayuda para gestionar las imagenes y contenedores, no solo en un nodo, sino a través de clusteres. |
| ![][img-jubernates] | **Ver Kubernates:*** El producto de Google sustituye a Docker-Swarm . |
| ![][img-machine] | ***Docker-Machine:*** Ayuda para gestionar las imagenes y contenedores, no solo en un nodo, sino a través de clusteres. |
| ![][img-registry] | ***Docker-Registry:*** Permite Almacenar y gestio |

#

---
> ***Los Contenedores no son máquinas virtuales***
---
- ***Las máquinas virtuales:*** (Casa)
- - Son totalmente independientes y ofrecen protección.
- - Tiene su propia infraestructura, (tuberías, desagües, electricidad)
- - Tienen los mismos recursos, (habitación,cocina,baño...)

Si nuestra intención es disponer de un estudio en lugar de toda una casa, estaremos malgastando recursos por algo que no necesitamos.

- ***El contenedor:*** (Apartamento en un edificio)
- - El edificio de apartamentos representa nuestra instalación de Docker en la máquina.
- - El contenedor representa uno de los apartamentos del edificio. 
- - Comparten arquitectura (tuberías, electricidad, desagües...)
- - Ventaja de diferentes tamaños de apartamentos en función de las necesidades.

<> La construcción de las imagenes con Docker parten de lo más básico y van adicionando sólo lo necesario.
<> La construcción de máquinas virtuales se realiza al inverso, parten de una instalación de todo el sistema operativo y, dependiendo de la aplicación, se van instalando los componentes necesarios.
![][img-docker_vm]

***Combinando máquinas virtuales y contenedores***
Es posible que coexistan MV y Contenedores a la vez. Esta mezcla, bien combinada, puede darnos la receta perfecta para nuestra infraestructura. Veamos un ejemplo:
![][img-docker+vm]

#

---
##### _Sección 02_
### Instalando Docker.
- Plataformas disponibles para la instalación de Docker
- Crear MV para la instalación de Ubuntu
- Instalar Docker en Ubutu
- Nuestro primer Contenedor

#

---
> ***Plataformas disponibles para la instalación de Docker***
---
- El ***sistema principal de Docker*** (motor/engine) se encuentra disponible para instalarlo sobre plataformas con ***Sistemas Operativos*** basados en el ***Kernel de ***Linux***.*** 
- Docker también permite instalarlo sobre plataformas ***Windows*** gracias a `Kitmatic`. Es un programa que contiene las herramientas Docker a través de una interfaz gráfica. Al ser necesario un OS basado en Linux, para solucionarlo, éste programa crea una máquina virtual ligera para instalar _Ubuntu Server_ como sistema operativo sobre el que  montará el motor de Docker. 
- De la misma forma, Docker, facilita `Kitematic` para sistemas ***OSX***. 

#

---
> ***Crear MV para la instalación de Ubuntu***
---
- Para el ejemplo, instalaremos el motor de Docker sobre un sistema basado en Linux que instalaremos en una máquina virtual. Generalizando de este modo la instalación, en lugar de instalaciones específicas en función del sistema operativo que estemos utilizando. (Windows,OSX..). 
- Otra razón es, la mayoría de las infraestructuras empresariales utilizan sistemas basados en Linux (redhat,ubuntu). Por lo que puede ser más oportuno conocer cómo realizar la instalación en estos entornos. 
- Para recrear un escenario empresarial, con una infraestructura de máquinas basadas en Linux, comenzaremos creando una máquina virtual ***Host***(Infraestructura), a la que instalaremos un ***Host-OS***  basado en Linux, (Ubuntu Server), sobre la que instalaremos el ***Docker Engine***.

***Comenzándo:***
- ***Descargamos*** [Ubuntu Server](https://www.ubuntu.com/download/server)
- ***Creamos una máquina virtual*** con VirtualBox con las siguientes características:
- - 2GB RAM
- - 10 GB HDD dinámico
- - Configuraciones predeterminadas sobre el sistema de archivos, particiones.
- - Configurar el arranque montando en la unidad de CD la imagen de Ubuntu descargada.
- - Configurar nombre de máquina/usuario/pass => `ubuntu/ubuntu/ubuntu`
- - Instalación del módulo _OpenSSH_ (opción durante instalación)
- - Reiniciamos y fin instalación
- ***Habilitamos puerto para la comunicación SSH***.
Desde la interface de VBox, entramos en  `Setting->Network->Advance->Reenvio de Puertos` de la máquina creada, publicamos el `HostPort` -> ***22*** al  `GuestPort` ->***2222***.
La conexión SSH desde un invitado por el puerto 2222 será encaminado al puerto 22 de la máquina creada. 
- ***Conectamos a la máquina***  por el puerto 2222 desde un cliente SSH,(MobaXterm,Putty..):
***`$ ssh ubuntu@localhost -p 2222`***

![][img-docker_vm]

#

---
> ***Instalar Docker en Ubutu***
---
***Paso 1 — Instalación de Docker***
Primero, vamos a actualizar la base de datos de paquetes:
```
$ sudo apt-get update
```
Agregue la clave GPG para el repositorio oficial de Docker al sistema:
```
$ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```
Agregue el repositorio Docker a fuentes APT:
```
$ sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'
```
Actualice la base de datos de paquetes, con los paquetes Docker desde el repositorio recién agregado:
```
$ sudo apt-get update
```
Asegúrese de que está a punto de instalar desde el repositorio de Docker en lugar del repositorio predeterminado de Ubuntu 16.04:
```
$ apt-cache policy docker-engine
```
Debería ver una salida similar a la siguiente:
```
docker-engine:
  Installed: (none)
  Candidate: 1.11.1-0~xenial
  Version table:
     1.11.1-0~xenial 500
        500 https://apt.dockerproject.org/repo ubuntu-xenial/main amd64 Packages
     1.11.0-0~xenial 500
        500 https://apt.dockerproject.org/repo ubuntu-xenial/main amd64 Packages
```
Observe que docker-engine no está instalado, pero el candidato para la instalación es del repositorio de Docker para Ubuntu 16.04. El número de versión de docker-engine puede ser diferente.

Por último, instale Docker:
```
$ sudo apt-get install -y docker-engine
```
Docker ahora debe estar instalado, el daemon iniciado, y el proceso habilitado para iniciar en el arranque. Compruebe que se está ejecutando:
```
$ sudo systemctl status docker
```
La salida debe ser similar a la siguiente, mostrando que el servicio está activo y en ejecución:
```
Output
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2016-05-01 06:53:52 CDT; 1 weeks 3 days ago
     Docs: https://docs.docker.com
 Main PID: 749 (docker)
```
La instalación de Docker ahora le ofrece no sólo el servicio Docker (daemon), sino también la utilidad de línea de comandos docker o el cliente Docker. Exploraremos cómo utilizar el comando docker más adelante en este tutorial.

#

***Paso 2 — Ejecutar el Comando Docker Sin Sudo (Opcional)***
De forma predeterminada, ejecutar el comando docker requiere privilegios de root, es decir, tiene que prefijar el comando con sudo. También puede ser ejecutado por un usuario en el grupo docker, que se crea automáticamente durante la instalación de Docker. Si intenta ejecutar el comando docker sin prefijarlo con sudo o sin estar en el grupo docker, obtendrá una salida como esta:
```
Output
docker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
See 'docker run --help'.
```
Si desea evitar escribir sudo cada vez que ejecute el comando docker, añada su nombre de usuario al grupo docker:
```
$ sudo usermod -aG docker $(whoami)
```
Deberá cerrar la sesión del Droplet y regresar como el mismo usuario para habilitar este cambio.

Si necesita agregar un usuario al grupo docker en el que no ha iniciado sesión, declare explícitamente el nombre de usuario utilizando:
```
$ sudo usermod -aG docker username
```
El resto de este artículo asume que está ejecutando el comando docker como un usuario en el grupo de usuario docker. Si opta por no hacerlo, por favor agregue los comandos con sudo.

#

---
> ***Nuestro primer contenedor***
---
Los contenedores Docker se ejecutan desde imagenes de Docker. De forma predeterminada, extrae estas imagenes de Docker Hub, un registro de Docker administrado por Docker, la compañía detrás del proyecto Docker. Cualquier persona puede construir y alojar sus imagenes Docker en Docker Hub, por lo que la mayoría de las aplicaciones y distribuciones Linux que necesitará para ejecutar contenedores Docker tienen imagenes alojadas en Docker Hub.

Para comprobar si puede acceder y descargar imagenes de Docker Hub, escriba:
```
$ docker run hello-world
```
La salida, que debe incluir lo siguiente, debe indicar que Docker está trabajando correctamente:
```
Output
Hello from Docker.
This message shows that your installation appears to be working correctly.
```

#

---
##### _Sección 03_
#### Primeros pasos con Docker.
- Estructura de comandos
- Imagenes y Contenedores
- Docker Store
- Imagenes oficiales de Docker en GitHub

#

---
> ***Estructura de comandos***
---
***Paso 3 — Uso del Comando Docker***
Con Docker instalado y funcionando, ahora es el momento de familiarizarse con la utilidad de la línea de comandos. El uso de docker consiste en pasarle una cadena de opciones y comandos seguidos de argumentos. La sintaxis toma esta forma:
```
$ docker [option] [command] [arguments]
```
Para ver todos los subcomandos disponibles, ingrese:
```
$ docker --help | more
```
En Docker version 17.05.0-ce, la lista completa de los subcomandos disponibles incluye:

```
ubuntu@ubuntu:~$ docker
Usage:  docker COMMAND
A self-sufficient runtime for containers
Options:
      --config string      Location of client config files (default
                           "/home/ubuntu/.docker")
  -D, --debug              Enable debug mode
      --help               Print usage
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level
                           ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default
                           "/home/ubuntu/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default
                           "/home/ubuntu/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default
                           "/home/ubuntu/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  container   Manage containers
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.
```
Para ver los modificadores disponibles para un comando específico, escriba:
```
$ docker docker-subcommand --help
```
Comandos relacionados con el sistema:
```
$ docker system --help
```
Para ver información sobre Docker en todo el sistema, utilice:
```
$ docker info
```

#

---
> ***Imagenes y Contenedores***
---
Algunas acciones con Imagenes y Contenedores: 
| Imagenes | Contenedores | 
| ------ | ------ | 
| pull | run | 
| push | stop | 
| build | restart | 
| save | inspect | 
| load | stats | 
Para ver todos los comandos disponibles, inscribimos:
```
$ docker image --help
$ docker container --help
```

***Analizando los pasos realizados por Docker al ejecutar el comando `docker run hello-world:`***
- 1º - Comprueba si la imagen está en el repositorio local
- 2º - Se descarga la imagen del repositorio remoto DockerHub si no existe en local
- 3º - Inicia el contenedor con la imagen descargada. Solo lo arranca.
- 4º - La imagen contendrá todo lo necesario para ejecutarse, si lo necesita.

#

---
> ***Docker Store***
https://store.docker.com/
---

Plataforma donde obtener información sobre las imagenes que tiene Docker.
Con el buscador web de Docker Store podemos encontrar imagenes oficiales y de la comunidad, aplicar filtros por categorías, ver descripción, información de descarga y utilización sobre las imagenes.

***Desde la terminal de comandos***, también podemos realizar búsquedas de imagenes: 
Puede buscar imagenes disponibles en Docker Hub utilizando el comando docker con el subcomando search. Por ejemplo, para buscar la imagen de Ubuntu, escriba:
```
$ docker search ubuntu
```
El script rastreará Docker Hub y devolverá una lista de todas las imagenes cuyo nombre coincida con la cadena de búsqueda. En este caso, la salida será similar a esto:

```
Output

NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                            Ubuntu is a Debian-based Linux operating s...   3808      [OK]       
ubuntu-upstart                    Upstart is an event-based replacement for ...   61        [OK]       
torusware/speedus-ubuntu          Always updated official Ubuntu docker imag...   25                   [OK]
rastasheep/ubuntu-sshd            Dockerized SSH service, built on top of of...   24                   [OK]
ubuntu-debootstrap                debootstrap --variant=minbase --components...   23        [OK]       
nickistre/ubuntu-lamp             LAMP server on Ubuntu                           6                    [OK]
nickistre/ubuntu-lamp-wordpress   LAMP on Ubuntu with wp-cli installed            5                    [OK]
nuagebec/ubuntu                   Simple always updated Ubuntu docker images...   4                    [OK]
nimmis/ubuntu                     This is a docker images different LTS vers...   4                    [OK]
maxexcloo/ubuntu                  Docker base image built on Ubuntu with Sup...   2                    [OK]
admiringworm/ubuntu               Base ubuntu images based on the official u...   1                    [OK]
```

En la columna OFICIAL, OK indica una imagen creada y apoyada por la empresa detrás del proyecto. Una vez que haya identificado la imagen que desea utilizar, puede descargarla a su computadora mediante el subcomando pull, así:
```
$ docker pull ubuntu
```
Después de descargar una imagen, puede ejecutar un contenedor usando la imagen descargada con el subcomando run. Si no se ha descargado una imagen cuando se ejecuta docker con el subcomando run, el cliente Docker descargará primero la imagen y luego ejecutará un contenedor utilizando:
```
$ docker images
```
La salida debería ser algo similar a esto:
```
Output
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              c5f1cf30c96b        7 days ago          120.8 MB
hello-world         latest              94df4f0ce8a4        2 weeks ago         967 B
```
Como veremos más adelante, las imagenes que utilice para ejecutar contenedores pueden modificarse y utilizarse para generar nuevas imagenes, que luego pueden cargarse (pushed es el término técnico) a Docker Hub u otros registros de Docker.



***Descargar una versión específica***
Lo indicaremos a través de las `TAG de la siguiente forma
image:tag

```
ubuntu@ubuntu:~$ docker pull ubuntu:17.04
17.04: Pulling from library/ubuntu
8b23367590c3: Pull complete
d18b5715fdd4: Pull complete
5ba295b2a11b: Pull complete
31ace8c1d433: Pull complete
95434b428ba1: Pull complete
Digest: sha256:0537ec6ef3bdcc490db2aec99ed84c28b9e5cafd4f810f46a6314dee930d1051
Status: Downloaded newer image for ubuntu:17.04

ubuntu@ubuntu:~$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              17.04               5e9fde03a0de        7 days ago          94.7MB
hello-world         latest              725dcfab7d63        8 days ago          1.84kB
ubuntu@ubuntu:~$
```

#

---
> ***Imagenes oficiales de Docker en GitHub***
---
A través de _GitHub_, podremos consultar las versiones de cada imagen oficial, junto a su documentación técnica. Por ejemplo, las distintas versiones disponibles de [Ubuntu](https://github.com/docker-library/docs/tree/master/ubuntu).
https://github.com/docker-library

#

---
##### _Sección 04_
#### Rutinas con imagenes y contenedores.
- Iniciar y listar los contenedores
- Mostrar los logs
- Eliminar imagenes y contenedores locales
- Salvar y cargar imagenes

#

---
> ***Iniciar y listar contenedores***
---
Vamos a consultar la ayuda sobre el comando que utiliza Docker para iniciar los contenedores:
***`$ docker run --help | more`***
```
Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container

Options:
      --add-host list                  Add a custom host-to-IP mapping (host:ip)
  -a, --attach list                    Attach to STDIN, STDOUT or STDERR
      --blkio-weight uint16            Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0)
```

- ***Listar el directorio raíz de un contenedor a partir de una imagen:***
***`$ docker container run ubuntu:17.04 ls -la /`***
docker [comandos contenedores] [inicia] [contenedor con imagen] [lista directorio raíz del contenedor]
```
ubuntu@ubuntu:~$ docker container run ubuntu:17.04 ls -la /
total 72
drwxr-xr-x  34 root root 4096 Nov 12 02:17 .
drwxr-xr-x  34 root root 4096 Nov 12 02:17 ..
-rwxr-xr-x   1 root root    0 Nov 12 02:17 .dockerenv
drwxr-xr-x   2 root root 4096 Sep 15 08:42 bin
drwxr-xr-x   2 root root 4096 Apr 10  2017 boot
drwxr-xr-x   5 root root  340 Nov 12 02:17 dev
drwxr-xr-x  35 root root 4096 Nov 12 02:17 etc
drwxr-xr-x   2 root root 4096 Apr 10  2017 home
drwxr-xr-x   8 root root 4096 Feb 16  2017 lib
drwxr-xr-x   2 root root 4096 Sep 15 08:42 lib64
drwxr-xr-x   2 root root 4096 Sep 15 08:42 media
drwxr-xr-x   2 root root 4096 Sep 15 08:42 mnt
drwxr-xr-x   2 root root 4096 Sep 15 08:42 opt
dr-xr-xr-x 121 root root    0 Nov 12 02:17 proc
drwx------   2 root root 4096 Sep 15 08:42 root
drwxr-xr-x   5 root root 4096 Nov  4 09:45 run
drwxr-xr-x   2 root root 4096 Nov  4 09:45 sbin
drwxr-xr-x   2 root root 4096 Sep 15 08:42 srv
dr-xr-xr-x  13 root root    0 Nov 12 02:17 sys
drwxrwxrwt   2 root root 4096 Sep 15 08:42 tmp
drwxr-xr-x  11 root root 4096 Sep 15 08:42 usr
drwxr-xr-x  13 root root 4096 Sep 15 08:42 var
```
***Listar contenedores***
Podemos ver nuestro contenedor generado:
Contenedores activos:
***`$ docker container ls`***
Todos los contenedores:
***`$ docker container ls -a`***
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
70cbce8d1a56        ubuntu:17.04        "ls -la /"          8 minutes ago       Exited (0) 8 minutes ago                       jolly_engelbart
c6305720e5bd        hello-world         "/hello"            2 hours ago         Exited (0) 2 hours ago                         flamboyant_archimedes
```

#

---
>***Mostrar los logs***
---
***Listar procesos***
El agente de Docker se mantendrá mostrando los logs que generen nuestros procesos del sistema asociados al contenedor indicado:
***`$ docker container run ubuntu:17.04 top -b`***
_`Cntrl + c`_ para detener el contenedor y la inspección del agente.
```
ubuntu@ubuntu:~$ docker container run ubuntu:17.04 top -b
top - 02:33:17 up  5:32,  0 users,  load average: 0.00, 0.00, 0.00
Tasks:   1 total,   1 running,   0 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.3 us,  0.1 sy,  0.1 ni, 99.4 id,  0.2 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  2048268 total,  1271904 free,   101632 used,   674732 buff/cache
KiB Swap:  2093052 total,  2093052 free,        0 used.  1790160 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
    1 root      20   0   38912   3208   2832 R  0.0  0.2   0:00.03 top
```

El flag `--detach` permite que los procesos que se ejecutan de este contenedor no estén anclados a esta terminal, permitiéndonos no detener el contenedor y seguir haciendo otras actividades:
***`$ docker container run --detach ubuntu:17.04 top -b`***
Podemos ver cómo en la salida nos devuelve un identificador único, indicando que el comando se ha ejecutado:
```
$ docker container run --detach ubuntu:17.04 top -b
c089a58bed9ea2277b0adc2801ca10593709cc0e75b97b79eedae882bcef8173
```
Ahora podemos buscar el contenedor y ver q sigue ejecutándose, además de comprobar que tienen el mismo identificador:
```
$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
c089a58bed9e        ubuntu:17.04        "top -b"            9 seconds ago       Up 9 seconds                            blissful_boyd
ubuntu@ubuntu:~$
```

#

 ***Ver el proceso del contenedor desligado de la terminal que ejecutó el comando***
 
Podemos conultar cómo se usa este comando con:
***`$ docker container logs --help`***
Usage:  docker container logs [OPTIONS]

Vamos a buscar los logs de un contenedor específico por su _NAME_:
***`$ docker container logs blissful_boyd`***
```
ubuntu@ubuntu:~$ docker container logs blissful_boyd
top - 02:46:22 up  5:45,  0 users,  load average: 0.00, 0.00, 0.00
Tasks:   1 total,   1 running,   0 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.3 us,  0.1 sy,  0.0 ni, 99.4 id,  0.1 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  2048268 total,  1278536 free,    94708 used,   675024 buff/cache
KiB Swap:  2093052 total,  2093052 free,        0 used.  1797088 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
    1 root      20   0   38912   3188   2816 R  0.0  0.2   0:00.03 top
```
-Utilizamos el flag `--follow` para mantener el seguimiento en la terminal de logs que se van generando: 
***`$ docker container logs --follow blissful_boyd`***

#

---
>***Eliminar imagenes y contenedores locales***
---

***Borrando un contenedor:*** (Si está arrancado debemos detenerlo previamente)
***`$ docker container rm [OPTIONS] CONTAINER-NAME [CONTAINER...]`***
```
ubuntu@ubuntu:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                         PORTS               NAMES
9d3d846ebdf6        ubuntu:17.04        "top -b"            About an hour ago   Exited (0) About an hour ago                       elated_northcutt

$ docker container rm elated_northcutt
```
Si intentamos borrar un contenedor en ejecución, Docker nos informará con un mensaje de error.  
Es posible forzar el borrado utilizando el flag `-f`, pero es preferible que nos aseguremos qué estamos borrando.

***Borrando una imagen:***
***`$ docker image rm [OPTIONS] IMAGE-NAME [IMAGE...]`***
Listamos las imagenes:
```
ubuntu@ubuntu:~$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              17.04               5e9fde03a0de        7 days ago          94.7MB
hello-world         latest              725dcfab7d63        8 days ago          1.84kB
```
Borramos la que deseemos, indicando el nombre, y si se repite el nombre de imagen, indicamos el TAG o ID:
```
$ docker image rm hello-world
$ docker image rm ubuntu:17.04
```

---
>***Salvar y cargar imagenes***
***`$ docker image save [OPTIONS] IMAGE [IMAGE...]`***
---

Permiten transportar de una máquina a otra sin necesidad de utulizar Docker Store.
Veamos primero un ejemplo de creación de un fichero a partir de una imagen.
Posteriormente, realizaremos el proceso inverso, cargar la imagen a partir del fichero generado.

***Salvando la imagen:***
***1º - Identificar la imagen que queremos salvar***
```
ubuntu@ubuntu:~$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              17.04               5e9fde03a0de        8 days ago          94.7MB
hello-world         latest              725dcfab7d63        8 days ago          1.84kB
```
***2º - Salvar la imagen deseada***
Especificar con el _flag_ _`--output`_ el nombre del fichero resultante seguido del nombre de la imagen elegida.
```
$ docker image save --output ubuntu-17.04 ubuntu:17.04
```
***3º - Localizar el fichero generado tras la imagen***
Se encontrará en nuestro directirio `/home/$(whoami)/`
```
ubuntu@ubuntu:~$ ls -la
total 95984
drwxr-xr-x 3 ubuntu ubuntu     4096 nov 12 15:10 .
drwxr-xr-x 3 root   root       4096 nov 11 21:35 ..
-rw------- 1 ubuntu ubuntu     1940 nov 12 04:57 .bash_history
-rw-r--r-- 1 ubuntu ubuntu      220 nov 11 21:35 .bash_logout
-rw-r--r-- 1 ubuntu ubuntu     3771 nov 11 21:35 .bashrc
drwx------ 2 ubuntu ubuntu     4096 nov 11 21:37 .cache
-rw-r--r-- 1 ubuntu ubuntu      655 nov 11 21:35 .profile
-rw-r--r-- 1 ubuntu ubuntu        0 nov 11 21:45 .sudo_as_admin_successful
-rw------- 1 ubuntu ubuntu 98251264 nov 12 15:10 ubuntu-17.04
-rw------- 1 ubuntu ubuntu      156 nov 12 14:48 .Xauthority
```

***Cargando una imagen a partir de un fichero***
Pasemos a realizar el proceso inverso, borraremos la imagen original del repositorio local para  poseteriormente genera una imagen cargándola desde el fichero creado anteriormente:

***1º*** - Eliminaremos la imagen de nuestro repositorio local de imagenes para realizar el proceso inverso: 
```
$ docker image rm ubuntu:17.04
```
_(*) ***Error response from daemon:***_
- Si nos muestra un error indicando que no podemos borrar la imagen debido a que está corriendo en un contenedor, y al verificar el contenedor vemos que está detenido-EXITED, es posible que pudiera haberse quedado referenciado en el _DOCKER-DAEMON_ erróneamente por un apagado del sistema incorrecto. 
- Para solucionarlo podemos forzar el borrado de la imagen con el flag _`-f`_ o _`--force`_ y posterior y opcionalmente podemos borrar el contenedor referenciado a esa imagen.
```
ubuntu@ubuntu:~$ docker image rm ubuntu:17.04
Error response from daemon: conflict: unable to remove repository reference "ubuntu:17.04" (must force) - container 70cbce8d1a56 is using its referenced image 5e9fde03a0de
ubuntu@ubuntu:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                    PORTS               NAMES
c089a58bed9e        ubuntu:17.04        "top -b"            12 hours ago        Exited (0) 11 hours ago                       blissful_boyd
9d3d846ebdf6        ubuntu:17.04        "top -b"            12 hours ago        Exited (0) 12 hours ago                       elated_northcutt
70cbce8d1a56        ubuntu:17.04        "ls -la /"          12 hours ago        Exited (0) 12 hours ago                       jolly_engelbart
c6305720e5bd        hello-world         "/hello"            14 hours ago        Exited (0) 14 hours ago                       flamboyant_archimedes
ubuntu@ubuntu:~$ docker container stop jolly_engelbart
jolly_engelbart

## Detenemos el contenedor:
ubuntu@ubuntu:~$ docker container stop 70cbce8d1a56
70cbce8d1a56

## Intentamos nuevamente borrar la imagen:
ubuntu@ubuntu:~$ docker image rm ubuntu:17.04
Error response from daemon: conflict: unable to remove repository reference "ubuntu:17.04" (must force) - container 70cbce8d1a56 is using its referenced image 5e9fde03a0de

## Forzamos el borrado de la imagen:
ubuntu@ubuntu:~$ docker image rm -f ubuntu:17.04
Untagged: ubuntu:17.04
Untagged: ubuntu@sha256:0537ec6ef3bdcc490db2aec99ed84c28b9e5cafd4f810f46a6314dee930d1051
Deleted: sha256:5e9fde03a0de0865b769b9dee0118941ad73110f681b66158129edfdf9a6fdd2
ubuntu@ubuntu:~$ docker image ls -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              725dcfab7d63        8 days ago          1.84kB

## Podemos borramos el contenedor que no se detenía:
ubuntu@ubuntu:~$ docker container rm jolly_engelbart
jolly_engelbart
```

#

***2º*** - Una  vez eliminada la imagen, vamos a ver cómo cargar imagenes desde archivos.
***`$ docker image load [OPTIONS] IMAGE`***
```
ubuntu@ubuntu:~$ docker image load --input ubuntu-17.04
Loaded image: ubuntu:17.04

## Podemos verificar que se ha generado una imagen en nuestro repositorio local.
ubuntu@ubuntu:~$ docker image ls -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              17.04               5e9fde03a0de        8 days ago          94.7MB
hello-world         latest              725dcfab7d63        8 days ago          1.84kB
```



---
## _Segundo bloque_
##### _Sección 05_
#### Construyendo imagenes.

[- Introducción a Dockerfile]
[- Construcción de la primera imagen]
[- Instrucciones en DockerFile]
[- Buenas prácticas en DockerFile]

#

---
> ***Introducción a Dockerfile***
---
Docker construye las imagenes a partir de las instrucciones definidas en el fichero de texto Dockerfile.
Dockefile define la estructura necesaria para que nuestra aplicación funcione correctamente.
- Dependencias del sistema operativo.
- Programas (servidor, bbdd...).
- Configuraciones del sistema. 
- Dependencias/librerías para la aplicación.
- Código fuente.

Una vez que definido nuestro Dockerfile, podemos lanzar desde la línea de comandos el comando _`build`_, encargado de leer y procesar el fichero Dockerfile para llevar a cabo la construcción de la imagen.
Las imagenes construidas ***se estructuran en capas***. Cada línea del fichero dockerfile representa una capa.

---
> ***Construcción de la primera imagen***
---

Vamos a construir una imagen de ejemplo donde el objetivo será escribir por consola un mensaje,
- Creamos un directorio donde guardar los ficheros necesarios para construir nuestra imagen.
- Creamos dentro del directorio nuestro fichero dockerfile.
***`$ vim Dockerfile`***

```
FROM ubuntu:17.04

ENTRYPOINT echo "Mensaje de bienvenida"
```
Con la etiqueta _`FROM`_ establecemos la imagen base.
_`ENTRYPOINT`_ le indicará qué comando debe ejecutar cuando inicie.

Una vez que tenemos el fichero creado, pasamos a construir la imagen con el comando ***_build_***:
```
$ docker images build --tag img-welcome .
```
Con el flag _`--Tag`_ indicamos el nombre que tendrá nuestra imagen.
El punto separado por el espacio indica que el fichero dockerfile se encuentra en el directorio actual:
`img-welcome` ***`.`***

```
ubuntu@ubuntu:~/mydockerfiles$ vim Dockerfile
ubuntu@ubuntu:~/mydockerfiles$ ls
Dockerfile
ubuntu@ubuntu:~/mydockerfiles$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              17.04               5e9fde03a0de        10 days ago         94.7MB
hello-world         latest              725dcfab7d63        10 days ago         1.84kB

ubuntu@ubuntu:~/mydockerfiles$ docker image build --tag imag-welcome .
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM ubuntu:17.04
 ---> 5e9fde03a0de
Step 2/2 : ENTRYPOINT echo "Bienvenido al Curso de Docker"
 ---> Running in b81a9ed9d25c
 ---> 7b155699c350
Removing intermediate container b81a9ed9d25c
Successfully built 7b155699c350
Successfully tagged imag-welcome:latest
ubuntu@ubuntu:~/mydockerfiles$
```

En la salida observamos que Docker ha realizado dos pasos, cada paso con un identificador único:
- Step 1/2: Primera capa con la imagen de ubuntu-17.04, (id 5e9fde03a0de)
- Step 2/2: Segunda capa (id 7b155699c350)
- Al resultado de la construcción le asigna como _`IMAGE ID`_ el último ID generado, (id 7b155699c350).

Verificamos que se ha creado la imagen y probamos su ejecución:
```
ubuntu@ubuntu:~/mydockerfiles$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
imag-welcome        latest              7b155699c350        9 minutes ago       94.7MB
ubuntu              17.04               5e9fde03a0de        10 days ago         94.7MB
hello-world         latest              725dcfab7d63        10 days ago         1.84kB

ubuntu@ubuntu:~/mydockerfiles$ docker container run imag-welcome
Bienvenido al Curso de Docker
```

***Comando asociados a las imagenes de Docker:***
***_$ docker image history --help_***
El comando _`history`_ nos permite conocer el conjunto de instrucciones realizadas para la creación de una imagen.

Como podemos ver, la única diferencia entre la imagen creada y la imagen base utilizada de ubuntu:17.04, es la instrucción _ENTRYPOINT_ que hemos realizado en la nueva imagen.
Por lo que este comando nos sirve para ratificar los pasos que se han realizado, donde no se ha añadido ningún otro fichero durante la construcción y la imagen resultante debe tener el mismo tamaño que la imagen base.
```
ubuntu@ubuntu:~/mydockerfiles$ docker image history imag-welcome
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
7b155699c350        29 minutes ago      /bin/sh -c #(nop)  ENTRYPOINT ["/bin/sh" "...   0B
5e9fde03a0de        10 days ago         /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>           10 days ago         /bin/sh -c mkdir -p /run/systemd && echo '...   7B
<missing>           10 days ago         /bin/sh -c sed -i 's/^#\s*\(deb.*universe\...   2.74kB
<missing>           10 days ago         /bin/sh -c rm -rf /var/lib/apt/lists/*          0B
<missing>           10 days ago         /bin/sh -c set -xe   && echo '#!/bin/sh' >...   745B
<missing>           10 days ago         /bin/sh -c #(nop) ADD file:4e2e1f8336bcc64...   94.7MB

ubuntu@ubuntu:~/mydockerfiles$ docker image history ubuntu:17.04
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
5e9fde03a0de        10 days ago         /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>           10 days ago         /bin/sh -c mkdir -p /run/systemd && echo '...   7B
<missing>           10 days ago         /bin/sh -c sed -i 's/^#\s*\(deb.*universe\...   2.74kB
<missing>           10 days ago         /bin/sh -c rm -rf /var/lib/apt/lists/*          0B
<missing>           10 days ago         /bin/sh -c set -xe   && echo '#!/bin/sh' >...   745B
<missing>           10 days ago         /bin/sh -c #(nop) ADD file:4e2e1f8336bcc64...   94.7MB
```

#

---
> ***Instrucciones en DockerFile***
---
Vamos a modificar el fichero Dockerfile creado anteriormente y añadirle algunas instrucciones:

```
FROM ubuntu:17.04
LABEL Descripción="Esta es una imagen de ejemplo" Autor="JMC" Versión="v1.0.0"

COPY datos/ejemplo

ENTRYPOINT cat /datos/ejemplo/texto
```
***LABEL***: Crea etiqueta de metadatos como clave-valor separados por un espacio.
***COPY***: Copia ficheros desde nuestra máquina a la estructura de ficheros que estamos creando.
`origen /destino` => `datos /ejemplo`
En este caso, copia el contenido del directorio de nuestra máquina `datos` al nuevo directorio `/ejemplo` ubicado en la raíz de la imagen que estamos creando.
La siguiente instrucción es `ENTRYPOINT`, acción que realizará al ejecutar la imagen, donde recibe el comando `cat` para leer el archivo de texto que vamos a copiar de `data` a `/ejemplo`

```
ubuntu@ubuntu:~/mydockerfiles$ mkdir datos
ubuntu@ubuntu:~/mydockerfiles$ ls
datos  Dockerfile
ubuntu@ubuntu:~/mydockerfiles$ cd datos/
ubuntu@ubuntu:~/mydockerfiles/datos$ nano texto
ubuntu@ubuntu:~/mydockerfiles/datos$ ls
texto
ubuntu@ubuntu:~/mydockerfiles$ ls
datos  Dockerfile

ubuntu@ubuntu:~/mydockerfiles$ cat Dockerfile
FROM ubuntu:17.04
LABEL Descripción="Esta es una imagen de ejemplo" Autor="JMC" Versión="v1.0.0"

COPY datos /ejemplo

ENTRYPOINT cat /ejemplo/texto


ubuntu@ubuntu:~/mydockerfiles$ docker image build -t ejemplo .
Sending build context to Docker daemon  3.584kB
Step 1/4 : FROM ubuntu:17.04
 ---> 5e9fde03a0de
Step 2/4 : LABEL Descripción "Esta es una imagen de ejemplo" Autor "JMC" Versión "v1.0.0"
 ---> Running in c24618e57e76
 ---> 33466cedbd6e
Removing intermediate container c24618e57e76
Step 3/4 : COPY datos /ejemplo
 ---> 42241fa6a952
Removing intermediate container d0acf62f7621
Step 4/4 : ENTRYPOINT cat /ejemplo/texto
 ---> Running in 30a3fb8a0396
 ---> cff6c019fb4f
Removing intermediate container 30a3fb8a0396
Successfully built cff6c019fb4f
Successfully tagged ejemplo:latest

ubuntu@ubuntu:~/mydockerfiles$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ejemplo             latest              cff6c019fb4f        16 seconds ago      94.7MB
imag-welcome        latest              7b155699c350        2 days ago          94.7MB
ubuntu              17.04               5e9fde03a0de        12 days ago         94.7MB
hello-world         latest              725dcfab7d63        12 days ago         1.84kB

ubuntu@ubuntu:~/mydockerfiles$ docker run ejemplo
Bienvenido al curso Dockerfile!!!
```


***Modificar el comportamiento del contenedor al iniciarse:***
Podemos sobrescribir las acciones definidas en el archivo Dockerfile, modificando así el comportamiento, si las definimos al lanzar el comando de ejecución de la imagen.
***`$ docker run --entrypoint "/bin/ls" ejemplo -la`***

`--entrypoint "/bin/ls"` => modifica-sobrescribe la acción definida en Dockerfile indicando que liste el directorio raíz de nuestra imagen ejemplo.

```
ubuntu@ubuntu:~/mydockerfiles$ docker run --entrypoint "/bin/ls" ejemplo -la
total 76
drwxr-xr-x  35 root root 4096 Nov 16 22:45 .
drwxr-xr-x  35 root root 4096 Nov 16 22:45 ..
-rwxr-xr-x   1 root root    0 Nov 16 22:45 .dockerenv
drwxr-xr-x   2 root root 4096 Sep 15 08:42 bin
drwxr-xr-x   2 root root 4096 Apr 10  2017 boot
drwxr-xr-x   5 root root  340 Nov 16 22:45 dev
drwxr-xr-x   2 root root 4096 Nov 16 22:17 ejemplo
drwxr-xr-x  35 root root 4096 Nov 16 22:45 etc
drwxr-xr-x   2 root root 4096 Apr 10  2017 home
drwxr-xr-x   8 root root 4096 Feb 16  2017 lib
drwxr-xr-x   2 root root 4096 Sep 15 08:42 lib64
drwxr-xr-x   2 root root 4096 Sep 15 08:42 media
drwxr-xr-x   2 root root 4096 Sep 15 08:42 mnt
drwxr-xr-x   2 root root 4096 Sep 15 08:42 opt
dr-xr-xr-x 125 root root    0 Nov 16 22:45 proc
drwx------   2 root root 4096 Sep 15 08:42 root
drwxr-xr-x   5 root root 4096 Nov  4 09:45 run
drwxr-xr-x   2 root root 4096 Nov  4 09:45 sbin
drwxr-xr-x   2 root root 4096 Sep 15 08:42 srv
dr-xr-xr-x  13 root root    0 Nov 16 22:45 sys
drwxrwxrwt   2 root root 4096 Sep 15 08:42 tmp
drwxr-xr-x  11 root root 4096 Sep 15 08:42 usr
drwxr-xr-x  13 root root 4096 Sep 15 08:42 var
ubuntu@ubuntu:~/mydockerfiles$

ubuntu@ubuntu:~/mydockerfiles$ docker run --entrypoint "/bin/ls" ejemplo -la /ejemplo
total 12
drwxr-xr-x  2 root root 4096 Nov 16 22:17 .
drwxr-xr-x 35 root root 4096 Nov 16 22:47 ..
-rw-rw-r--  1 root root   34 Nov 16 22:13 texto

```

#

---
> ***Buenas prácticas en DockerFile***
---
- Intentar no instalar paquetes no necesarios.
- Cada contenedor debe cumplir sólo un propósito. (orientación a microservicios)
- Minimizar el número de capas
- Escribir líneas cortas de instrucciones y utilizar \ para mejor entendimiento
backslash nos permite concatenar instrucciones generando una única capa como resultado.
```
RUN apt-get update && apt-get install -y \
bzr\
cvs\
git\
mercurial\
subversion\
```
- Mantener nuestros Dockerfile en un control de versiones nos permite conocer todos los cambios realizados.

#

---
##### _Sección 06_
#### Volúmenes.
---
> ***¿Qué son los volúmenes?***
---
- Docker gestiona los datos utilizando volúmenes.
- Son estructura de archivos incluidos en uno o varios contenedores.
- Su objetivo es persistir la información de forma independiente al ciclo de vida de los contenedores.

Para incorporar la estructura de archivos a nuestra imagen, como en el ejemplo anterior `datos/texto` a `/ejemplo` debemos realizarlo al crear la imagen.

Si la información que tenemos en el directorio `datos/` varía constantemente, sería poco práctico tener que generar un contenedor cada ocasión.

Veamos como convertir nuestro directorio `data/` en un volumen para incorporar la la estructura de ficheros en dos contenedores:

- En el contenedor A se montaron en el directorio raíz del sistema de archivos.
- - Contenedor A => home/ubuntu/datos:/
- En el contenedor B se montaron en el directorio var.
- - Contenedor B => home/ubuntu/datos:/var

No nos obliga a incorporar la estructura de ficheros en una ubicación específica.

 ***Características de los volúmenes***
- Son creados cuando se inician los contenedores.
- Pueden ser utilizados entre varios contenedores. (ejemplo anterior)
- Los cambios en los datos de los volúmenes son reflejados en los contenedores automáticamente.
- Al actualizar las imagenes, no se modifica la información en los volúmenes.
- La información contenida en el volumen no se elimina al eliminar los contenedores.

***Formas de uso de los volúmenes***
- Volúmenes de datos.   
- Contenedores como volúmenes de datos.

#

---
> ***Utilizar volúmenes de datos***
---
Iniciar un contenedor a partir de la imagen de base de Ubuntu que venimos utilizando.
Al iniciarlos, vamos a montar un volumen en el contenedor con datos/texto del host.
El volumen de datos/ será montado en la raíz del contenedor en el directorio /ejemplo

Vamos a mostrar el contenido del fichero `/ejemplo/texto` una vez que el volumen ha sido montando dentro del contenedor.

Nueva habilidad- Iniciar el contenedor de forma interactiva. Implica que una vez iniciado nos quedaremos dentro de la estructura del contenedor para poder trabajar desde dentro.

***`$ docker run --name ejemplo-volum -v /home/ubuntu/mydockerfiles/datos:/ejemplo -it ubuntu:17.04 /bin/bash`***

`--name ejemplo-volum` => asignamos un nombre al contenedor, en lugar de delegar en Docker
`-v /home/ubuntu/mydockerfiles/datos:/ejemplo` => Indicamos que monte un volumen con /data en el directorio raíz del contenedor creando la carpeta /ejemplo
`-it ubuntu:17.04 /bin/bash` => Iniciar de forma interactiva, creando un contenedor a partir de la imagen de ubuntu:17.04 y dejándonos en una línea de comandos bash, para poder interactuar dentro del contenedor.


```
ubuntu@ubuntu:~/mydockerfiles$ docker run --name ejemplo-volum -v /home/ubuntu/mydockerfiles/datos:/ejemplo -it ubuntu:17.04 /bin/bash
root@a344bd936442:/# ls -la
total 76
drwxr-xr-x  35 root root 4096 Nov 17 00:08 .
drwxr-xr-x  35 root root 4096 Nov 17 00:08 ..
-rwxr-xr-x   1 root root    0 Nov 17 00:08 .dockerenv
drwxr-xr-x   2 root root 4096 Sep 15 08:42 bin
drwxr-xr-x   2 root root 4096 Apr 10  2017 boot
drwxr-xr-x   5 root root  360 Nov 17 00:08 dev
drwxrwxr-x   2 1000 1000 4096 Nov 16 22:13 ejemplo
drwxr-xr-x  35 root root 4096 Nov 17 00:08 etc
drwxr-xr-x   2 root root 4096 Apr 10  2017 home
drwxr-xr-x   8 root root 4096 Feb 16  2017 lib
drwxr-xr-x   2 root root 4096 Sep 15 08:42 lib64
drwxr-xr-x   2 root root 4096 Sep 15 08:42 media
drwxr-xr-x   2 root root 4096 Sep 15 08:42 mnt
drwxr-xr-x   2 root root 4096 Sep 15 08:42 opt
dr-xr-xr-x 126 root root    0 Nov 17 00:08 proc
drwx------   2 root root 4096 Sep 15 08:42 root
drwxr-xr-x   5 root root 4096 Nov  4 09:45 run
drwxr-xr-x   2 root root 4096 Nov  4 09:45 sbin
drwxr-xr-x   2 root root 4096 Sep 15 08:42 srv
dr-xr-xr-x  13 root root    0 Nov 16 22:45 sys
drwxrwxrwt   2 root root 4096 Sep 15 08:42 tmp
drwxr-xr-x  11 root root 4096 Sep 15 08:42 usr
drwxr-xr-x  13 root root 4096 Sep 15 08:42 var


root@a344bd936442:/# cd ejemplo/
root@a344bd936442:/ejemplo# ls
texto
root@a344bd936442:/ejemplo# cat texto
Bienvenido al curso Dockerfile!!!
root@a344bd936442:/ejemplo# exit
exit

ubuntu@ubuntu:~/mydockerfiles$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                      PORTS               NAMES
a344bd936442        ubuntu:17.04        "/bin/bash"         About a minute ago   Exited (0) 26 seconds ago                       ejemplo-volum
```

***Modificando la información en el volumen de localhost y verificando el refresco automáico***
Se ha modificado el mensaje del fichero texto en el volumen de datos/texto de localhost y desde dentro del contenedor verificamos que se ha refrescado la información en el fichero del /ejemplo/texto al instante de guardar el fichero editado en localhost.

```
root@b062af057f80:/ejemplo# cat texto
Bienvenido al curso Docker!!!
Prueba de vólúmen de datos en un contenedor:

Este archivo texto ha sido editado desde ubuntu-localhost y
es reflejado/refrescado automáticamente en el volumen de datos
creado en el contenedor bajo el directorio /ejemplo, archivo texto.
```

Si eliminamos el contenedor, el contenido del fichero datos/texto de localhost no se altera.

#

---
> ***Utilizar contenedores como volúmenes de datos***
---
Podemos iniciar un contenedor indicando que reserve un espacio para montar un volumen de datos. 
Para el siguiente ejemplo, el contenedor partirá de una imagen muy ligera `busybox` y le indicaremos que reserve un espacio para montar un vólumen de datos en su raíz de directorios, sin necesidad de referenciar este volumen a un volumen de nuestra máquina Host-(VM-localhost). Al contenedor le llamaremos  `data-container`.
***`$ docker run --name data-container -v /datos busybox`***
```
ubuntu@ubuntu:~$ docker run --name data-container -v /datos busybox
Unable to find image 'busybox:latest' locally
latest: Pulling from library/busybox
0ffadd58f2a6: Pull complete
Digest: sha256:bbc3a03235220b170ba48a157dd097dd1379299370e1ed99ce976df0355d24f0
Status: Downloaded newer image for busybox:latest
ubuntu@ubuntu:~$
```
Una vez generado el contenedor, no obtenemos ninguna salida en pantalla adicional dado que el contenedor está programado para realizar ninguna tarea, ya que sólo lo queremos para almacenar información.

La imagen `busybox` que hemos utilizado para la generación del contenedor apenas tiene de tamaño 1.13MB. El motivo por el que es tan ligera es debido a que sólo cuenta con la base necesaria para que sea utilizada como volumen de datos.

Ya disponemos de un contenedor para que sea utilizado como volumen de datos.
Necesitamos ahora iniciar otro contenedor, que sería nuestra aplicación que utilizará el otro contenedor como volumen de datos.  (ContainerVolume + Container App)

***`$ docker run --name app1 --volumes-from data-container -it ubuntu:17.04 /bin/bash`***

`volume-from` => indica que utilizaremos otro contenedor como volumen de datos.

Al iniciarlo de forma interactiva `-it`, cuando termine de iniciarlos nos encontraremos dentro del contenedor y así para poder realizar algunas acciones.
```
ubuntu@ubuntu:~$ docker run --name app1 --volumes-from data-container -it ubuntu:17.04 /bin/bash
root@9135fd815a38:/# ls -la
total 76
drwxr-xr-x  35 root root 4096 Nov 17 21:58 .
drwxr-xr-x  35 root root 4096 Nov 17 21:58 ..
-rwxr-xr-x   1 root root    0 Nov 17 21:58 .dockerenv
drwxr-xr-x   2 root root 4096 Sep 15 08:42 bin
drwxr-xr-x   2 root root 4096 Apr 10  2017 boot
drwxr-xr-x   2 root root 4096 Nov 17 21:30 datos
drwxr-xr-x   5 root root  360 Nov 17 21:58 dev
drwxr-xr-x  35 root root 4096 Nov 17 21:58 etc
drwxr-xr-x   2 root root 4096 Apr 10  2017 home
drwxr-xr-x   8 root root 4096 Feb 16  2017 lib
drwxr-xr-x   2 root root 4096 Sep 15 08:42 lib64
drwxr-xr-x   2 root root 4096 Sep 15 08:42 media
drwxr-xr-x   2 root root 4096 Sep 15 08:42 mnt
drwxr-xr-x   2 root root 4096 Sep 15 08:42 opt
dr-xr-xr-x 121 root root    0 Nov 17 21:58 proc
drwx------   2 root root 4096 Sep 15 08:42 root
drwxr-xr-x   5 root root 4096 Nov  4 09:45 run
drwxr-xr-x   2 root root 4096 Nov  4 09:45 sbin
drwxr-xr-x   2 root root 4096 Sep 15 08:42 srv
dr-xr-xr-x  13 root root    0 Nov 17 21:58 sys
drwxrwxrwt   2 root root 4096 Sep 15 08:42 tmp
drwxr-xr-x  11 root root 4096 Sep 15 08:42 usr
drwxr-xr-x  13 root root 4096 Sep 15 08:42 var

root@9135fd815a38:/# cd datos
root@9135fd815a38:/datos# touch file1
root@9135fd815a38:/datos# ls
file1
root@9135fd815a38:/datos#  (Inserte Ctrl + p + q para salir del contenedor sin detenerlo)
ubuntu@ubuntu:~$
```

A continuación, crearemos otro contenedor, también de forma interactiva, con una segunda aplicación, `app2`.
Este nuevo contenedor utilizará también el contenedor `data-volume` como volumen de datos.
Una vez termine de generar el contendor y encontrarnos dentro del mismo, crearemos otro fichero, `file2`.
Comprobaremos que `data-volume` puede compartir inforamción con múltiples contenedores.

***`$ docker run --name app1 --volumes-from data-container -it ubuntu:17.04 /bin/bash`***

```
ubuntu@ubuntu:~$ docker run --name app2 --volumes-from data-container -it ubuntu:17.04 /bin/bash
root@ba175f7c7c4d:/# ls -la
total 76
drwxr-xr-x  35 root root 4096 Nov 17 22:09 .
drwxr-xr-x  35 root root 4096 Nov 17 22:09 ..
-rwxr-xr-x   1 root root    0 Nov 17 22:09 .dockerenv
drwxr-xr-x   2 root root 4096 Sep 15 08:42 bin
drwxr-xr-x   2 root root 4096 Apr 10  2017 boot
drwxr-xr-x   2 root root 4096 Nov 17 21:59 datos
drwxr-xr-x   5 root root  360 Nov 17 22:09 dev
drwxr-xr-x  35 root root 4096 Nov 17 22:09 etc
drwxr-xr-x   2 root root 4096 Apr 10  2017 home
drwxr-xr-x   8 root root 4096 Feb 16  2017 lib
drwxr-xr-x   2 root root 4096 Sep 15 08:42 lib64
drwxr-xr-x   2 root root 4096 Sep 15 08:42 media
drwxr-xr-x   2 root root 4096 Sep 15 08:42 mnt
drwxr-xr-x   2 root root 4096 Sep 15 08:42 opt
dr-xr-xr-x 123 root root    0 Nov 17 22:09 proc
drwx------   2 root root 4096 Sep 15 08:42 root
drwxr-xr-x   5 root root 4096 Nov  4 09:45 run
drwxr-xr-x   2 root root 4096 Nov  4 09:45 sbin
drwxr-xr-x   2 root root 4096 Sep 15 08:42 srv
dr-xr-xr-x  13 root root    0 Nov 17 21:58 sys
drwxrwxrwt   2 root root 4096 Sep 15 08:42 tmp
drwxr-xr-x  11 root root 4096 Sep 15 08:42 usr
drwxr-xr-x  13 root root 4096 Sep 15 08:42 var

root@ba175f7c7c4d:/# cd datos/
root@ba175f7c7c4d:/datos# touch file2
root@ba175f7c7c4d:/datos# ls
file1  file2
root@ba175f7c7c4d:/datos# ubuntu@ubuntu:~$
```
Podemos ver que automáticamente ha aparecido el fichero `file1`, ya que el fichero fue guardado automáticamente en `data-volume` cuando lo creamos en el contenedor de `app1`. De la misma forma sucede con el fichero `file2`.

Vamos a verificar que se encuentran los 3 contenedores creados en funcionamiento:
```
ubuntu@ubuntu:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                         PORTS               NAMES
ba175f7c7c4d        ubuntu:17.04        "/bin/bash"         12 minutes ago      Up 12 minutes                                      app2
9135fd815a38        ubuntu:17.04        "/bin/bash"         23 minutes ago      Up 23 minutes                                      app1
b330ab85033d        busybox             "sh"                About an hour ago   Exited (0) About an hour ago                       data-container
```

Para confirmar todo lo anterior, vamos a acceder a `app1` para verificar que el fichero file2 se encuentra también compartido desde `data-volume`.
Para poder acceder en un contenedor que ya se encuentra en funcionamiento, vamos a utlizar el siguiente comando, unir o adjuntar e indicando el nombre del contenedor al que queremos acceder:
_Recodar al acceder estarémos utilizando la misma aplicación bash con la que iniciamos en app1._

***`$ docker container attach app1`***
```
root@9135fd815a38:/datos# ls
file1  file2
```

#

---
> ***Salvar la información***
---
Nuestros datos están guardados en un sistema de archivos dentro de nuestro contenedor `data-container`.
Para salvar los datos vamos a utilizar la siguiente línea de comandos:
***`$ docker container run -rm --volumes-from data-container -v $(pwd):/backup ubuntu:17.04 tar cvf /backup/backup-data.tar /datos`***

Analizando el comando...
- Inicia un contenedor que tiene como base `ubuntu:17.04`
- Adiciona un volumen, que será el contenedor `data-container`
- Indica el destino donde salvar la información en un archivo comprimido. `tar cvf /backup/data-backup.tar`
- Indica el origen de la fuente de datos. Será el contenido del directorio `/datos` de este contenedor.
- Conectar este contenedor al Host-(localhost-VM) para poder obtener el fichero comprimido que se encuentra dentro de la carpeta `/backup/` en la raíz del contenedor: `-v $(pwd):/backups`
Crea un volumen desde nuestro directorio `$(pwd)`de (localhost-VM) hasta este nuevo contenedor.
- Una vez que este contenedor realice las funciones anteriores y termine, no vamos a necesitar más de el. Borramos el contenedor al terminar `docker run --rm`

```
ubuntu@ubuntu:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                    PORTS               NAMES
ba175f7c7c4d        ubuntu:17.04        "/bin/bash"         About an hour ago   Up About an hour                              app2
9135fd815a38        ubuntu:17.04        "/bin/bash"         About an hour ago   Up About an hour                              app1
b330ab85033d        busybox             "sh"                2 hours ago         Exited (0) 2 hours ago                        data-container

ubuntu@ubuntu:~$ cd mydockerfiles/
ubuntu@ubuntu:~/mydockerfiles$

ubuntu@ubuntu:~/mydockerfiles$ docker container run --rm --volumes-from data-container -v $(pwd):/backup ubuntu:17.04 tar cvf /backup/backup-data.tar /datos
tar: Removing leading `/' from member names
/datos/
/datos/file2
/datos/file1

ubuntu@ubuntu:~/mydockerfiles$ ls
backup-data.tar  datos  Dockerfile
```
Podemos ver que se ha creado en nuestro directorio del Host-VM un nuevo fichero `backup-data.tar`

***Comprobar que los datos se han salvado:***
- Borramos el directorio original del Host `datos/`, y su contenido `-r` _recursivamente_.
- Descomprimimos el archivo `tar xvf backup-data.tar` generado.
- Verificamos que se ha recuperado la carpeta `/datos` y su contenido, gracias al archivo salvado.

```
ubuntu@ubuntu:~/mydockerfiles$ ls
backup-data.tar  datos  Dockerfile

ubuntu@ubuntu:~/mydockerfiles$ sudo rm -r datos/
[sudo] password for ubuntu:
ubuntu@ubuntu:~/mydockerfiles$ ls
backup-data.tar  Dockerfile

ubuntu@ubuntu:~/mydockerfiles$ sudo tar xvf backup-data.tar
datos/
datos/file2
datos/file1

ubuntu@ubuntu:~/mydockerfiles$ ls
backup-data.tar  datos  Dockerfile

ubuntu@ubuntu:~/mydockerfiles$ cd datos/
ubuntu@ubuntu:~/mydockerfiles/datos$ ls
file1  file2
```

#

---
##### _Sección 07_
#### Publicar servicios.


---
##### _Sección 08_
#### Publicar imagenes en Docker Cloud.


---
##### _Sección 09_
#### Publicar imagenes desde Github.


---
## Tercer bloque
##### _Sección 10_
#### Desplegar en producción.


---
##### _Sección 11_
#### Conectando contenedores.


---
##### _Sección 12_
#### Registro privado de imagenes.


---
##### _Sección 13_
#### Conclusiones y resultados.


---
##### _Sección 14_
#### Ejercicios y actividades.



---
[img-dockerhead]: https://jsitech1.gitbooks.io/meet-docker/content/DockerLogo.png "Icono Docker"
[img-docker]: https://www.docker.com/sites/default/files/Package%20software.png
[img-container]: https://www.docker.com/sites/default/files/Container%402x.png

[img-docker_lite]: https://raw.githubusercontent.com/docker-library/docs/c350af05d3fac7b5c3f6327ac82fe4d990d8729c/docker/logo.png
[img-compose]:https://cdn-images-1.medium.com/max/1200/1*ciSVYUq_0LvhY1yeD8RLZQ.png
[img-swarm]:https://blog.alexellis.io/content/images/2017/03/docker_swarm.png
[img-jubernates]:https://cdn-images-1.medium.com/max/280/1*QtnQTnrgQ-N-r5k-nYUZ0g.png
[img-machine]:https://cormachogan.com/wp-content/uploads/2016/06/docker-machine.png
[img-registry]:https://blog.irontec.com/wp-content/uploads/2017/02/registry-274x300.png
[img-docker_vm]: http://www.media.formandome.es/markdownslides/docker/img/docker_vs_vm.jpg
[img-docker+vm]: https://www.docker.com/sites/default/files/containers-vms-together%402x.png


[s1]: <https://github.com/josemanuelCRV/docker-notes#introducción-a-contenedores-y-docker>
[s2]: <https://github.com/josemanuelCRV/docker-notes#instalar-docker>
[s3]: <https://github.com/josemanuelCRV/docker-notes#primeros-pasos-con-docker>
[s4]: <https://github.com/josemanuelCRV/docker-notes#rutinas-diarias-con-imagenes-y-contenedores>
[s5]: <https://github.com/josemanuelCRV/docker-notes#construyendo-imagenes>

[s6]: <https://github.com/josemanuelCRV/docker-notes#volúmenes-en-docker>
[s7]: <https://github.com/josemanuelCRV/docker-notes#publicar-servicios>
[s8]: <https://github.com/josemanuelCRV/docker-notes#publicar-imagenes-en-docker-cloud>
[s9]: <https://github.com/josemanuelCRV/docker-notes#publicar-imagenes-desde-github>

[s10]: <https://github.com/josemanuelCRV/docker-notes#desplegar-en-producción>
[s11]: <https://github.com/josemanuelCRV/docker-notes#conectando-contenedores>
[s12]: <https://github.com/josemanuelCRV/docker-notes#registros-privados-en-docker>
[s13]: <https://github.com/josemanuelCRV/docker-notes#conclusiones-y-resultados>
[s14]: <https://github.com/josemanuelCRV/docker-notes#ejercicios-y-actividades>



[s1s1s1]: <https://github.com/josemanuelCRV/docker-notes#comportamiento-distinto-en-función-del-entorno>
[s1s2s2]: <https://github.com/josemanuelCRV/docker-notes#qué-son-los-contenedores-y-las-imagenes>
[s1s3s3]: <https://github.com/josemanuelCRV/docker-notes#qué-es-docker>
[s1s4s4]: <https://github.com/josemanuelCRV/docker-notes#productos-y-herramientas>
[s1s5s5]: <https://github.com/josemanuelCRV/docker-notes#los-contenedores-no-son-máquinas-virtuales>

[s1s2s1]: <https://github.com/josemanuelCRV/docker-notes#plataformas-disponibles-para-la-instalación-de-docker>
[s1s2s2]: <https://github.com/josemanuelCRV/docker-notes#crear-mv-para-la-instalación-de-ubuntu>
[s1s2s3]: <https://github.com/josemanuelCRV/docker-notes#instalar-docker-en-ubutu>
[s1s2s4]: <https://github.com/josemanuelCRV/docker-notes#nuestro-primer-contenedor>

[s1s3s1]: <https://github.com/josemanuelCRV/docker-notes#extructura-de-comandos>
[s1s3s2]: <https://github.com/josemanuelCRV/docker-notes#imagenes-y-contenedores>
[s1s3s3]: <https://github.com/josemanuelCRV/docker-notes#docker-store>
[s1s3s4]: <https://github.com/josemanuelCRV/docker-notes#imagenes-oficiales-de-docker-en-github>

[s1s4s1]: <https://github.com/josemanuelCRV/docker-notes#iniciar-y-listar-los-contenedores>
[s1s4s2]: <https://github.com/josemanuelCRV/docker-notes#mostrar-los-logs>
[s1s4s3]: <https://github.com/josemanuelCRV/docker-notes#elimiar-imagenes-y-contenedores-locales>
[s1s4s4]: <https://github.com/josemanuelCRV/docker-notes#salvar-y-cargar-imagenes>

[s1s5s1]: <https://github.com/josemanuelCRV/docker-notes#introducción-a-dockerfile>
[s1s5s2]: <https://github.com/josemanuelCRV/docker-notes#construcción-de-la-primera-imagen>
[s1s5s3]: <https://github.com/josemanuelCRV/docker-notes#instrucciones-en-dockerfile>
[s1s5s4]: <https://github.com/josemanuelCRV/docker-notes#buenas-prácticas-en-dockerfile>

![Docker][img-dockerhead]
***

> La siguiente información sobre [_Docker_](https://docs.docker.com/) tiene exclusivamente carácter didáctico personal, como respaldo de mis apuntes, notas y pequeñas prácticas. Sirviendo como fuente de consulta, tanto para mí como para cualquiera a quien pudiera interesar. 


# Introducción a DOCKER
### Secciones del curso:
##### Primer bloque
- [01 - Introducción a contenedores y Docker][s1]
- [02 - Instalar Docker][s2]
- [03 - Primeros pasos con Docker][s3]
- [04 - Rutinas diarias con imágenes y contenedores][s4]

##### Segundo bloque
- [05 - Construyendo imágenes][s5]
- [06 - Volúmenes en Docker][s6]
- [07 - Publicar servicios][s7]
- [08 - Publicar imágenes en Docker Cloud][s8]
- [09 - Publicar imágenes desde Github][s9]

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
- Orquestar y escalar servicios
- Crear registros privados en Docker Registry
---
### Primer bloque
##### _Sección 01_
### Introducción a contenedores y Docker.
- [Comportamiento distinto en función del entorno][s1s1]
- [¿Qué son los contenedores y las imágenes?][s1s2]
- [¿Qué es Docker?][s1s3]
- [Productos y herramientas][s1s4]
- [Los Contenedores no son máquinas virtuales][s1s5]

#

---
>#### Comportamiento distinto en función del entorno
---

En muchas ocasiones, nos encontramos conflictos a la hora de distribuir y ejecutar el software desarrollado. Muchos de estos conflictos son ocasionados por las diferencias entre plataformas (desarrollo/producción), sistemas operativos, librerías y componentes, recursos del sistema e infraestructura, entre otros. 

Docker nos permite eliminar este tipo de conflictos mediante el uso de Imágenes/Contenedores. Esta tecnología nos permite generar una imagen en la que se encapsula y empaqueta la aplicación con todas las dependencias que son necesarias para que sea ***autónoma y autocontenida*** con sus librerías, fuentes, OS, servidor, evitando de ese modo comportamientos distintos entre las máquinas utilizadas para el desarrollo de software respecto a las máquinas destinadas a pruebas, pruebas piloto y despliegue en entornos de producción. 


---
>#### ¿Qué son los contenedores y las imágenes?
---

Un ***contenedor*** es una unidad de software estandarizada, es un paquete ejecutable, ligero y autónomo con todo lo necesario para su ejecución. (App, servidor de la app, bibliotecas y componentes, configuraciones, O.S. con sólo los ficheros necesarios).

Es ***portable***, al conservar todos los elementos de una máquina a otra. 

Funcionan de forma ***aislada***, sin necesitar de otros procesos para su ejecución ni entrar en conflicto con dependencias de otros contenedores desplegados en el mismo servidor, dado que los contenedores ***son estancos***.

 Las ***imágenes*** son el resultado del empaquetado y el ***Contenedor*** es la ejecución de la imagen. 
- De una imagen pueden ejecutarse muchos contenedores.
- Una imagen no tiene estado, sólo es el empaquetado. 
- Un contenedor puede tener distintos estados (Iniciado - Detenido/Pausado - Terminado)

![docker][img-docker]

#

---
>#### ¿Qué es Docker?
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
>#### Productos y herramientas
---
Utilizados para la gestión de los contenedores e imágenes:

| Logo | Herramienta | 
| ------ | ------ | 
|![][img-docker_lite] | ***Docker:***  Motor principal para la gestión de contenedores. Encargado de crear, obtener y publicar imágenes, así como el despliegue, ejecución y parada de los contenedores.
| ![][img-compose]  | ***Docker-Compose:*** Ayuda para gestionar múltiples contenedores y servicios al mismo tiempo a través de sencillas configuraciones. |
| ![][img-swarm] | ***Docker-Swarm:*** Ayuda para gestionar las imágenes y contenedores, no solo en un nodo, sino a través de clusteres. |
| ![][img-jubernates] | **Ver Kubernates:*** El producto de Google sustituye a Docker-Swarm . |
| ![][img-machine] | ***Docker-Machine:*** Ayuda para gestionar las imágenes y contenedores, no solo en un nodo, sino a través de clusteres. |
| ![][img-registry] | ***Docker-Registry:*** Permite Almacenar y gestio |

#

---
>#### Los Contenedores no son máquinas virtuales
---

Vamos a mostrar las diferencias/ventajas entre máquinas virtuales y contenedores a trvés de un paralelísmo donde las máquinas virtuales representan _Casas_ y los Contenedores representan _Pisos_.

 ventajas que ofrece Docker frente a las máquinas virtuales haciendo un paralelísmo entre Casas-Challets Vs Pisos.

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

- La construcción de las imágenes con Docker parten de lo más básico y van adicionando sólo lo necesario.
- La construcción de máquinas virtuales se realiza al inverso, parten de una instalación de todo el sistema operativo y, dependiendo de la aplicación, se van instalando los componentes necesarios.


![][img-docker_vm]


***Combinando máquinas virtuales y contenedores***
Es posible que coexistan MV y Contenedores a la vez. Esta mezcla, bien combinada, puede darnos la receta perfecta para nuestra infraestructura. Veamos un ejemplo:

![][img-docker+vm]

#

---
##### _Sección 02_
### Instalar Docker.
- [Plataformas disponibles para la instalación de Docker][s2s1]
- [Crear MV para la instalación de Ubuntu][s2s2]
- [Instalar Docker en Ubutu][s2s3]
- [Nuestro primer Contenedor][s2s4]

#

---
>#### Plataformas disponibles para la instalación de Docker
---
- El ***sistema principal de Docker*** (motor/engine) se encuentra disponible para instalarlo sobre plataformas con sistemas operativos basados en el ***Kernel de Linux***. 
- Docker también permite instalarlo sobre plataformas ***Windows*** gracias a [Kitmatic](https://kitematic.com/). Es un programa que contiene las herramientas Docker a través de una interfaz gráfica. Al ser necesario un OS basado en Linux, para solucionarlo, éste programa crea una máquina virtual ligera para instalar _Ubuntu Server_ como sistema operativo sobre el que  montará el motor de Docker. 
- De la misma forma, Docker, facilita `Kitematic` para sistemas ***macOS***. 

#

---
>#### Crear MV para la instalación de Ubuntu
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

Desde la interface de VBox, entramos en:
- `Setting->Network->Advance->Reenvio de Puertos` de la máquina creada.
- publicamos el `HostPort` -> ***22*** al  `GuestPort` ->***2222***.


![][img-vbox-net-rules-redirect]



La conexión SSH desde un invitado por el puerto 2222 será encaminado al puerto 22 de la máquina creada. 
- ***Conectamos a la máquina***  por el puerto 2222 desde un cliente SSH,(MobaXterm,Putty..):

***`$ ssh ubuntu@localhost -p 2222`***




#

---
>#### Instalar Docker en Ubutu
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
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2016-05-01 06:53:52 CDT; 1 weeks 3 days ago
     Docs: https://docs.docker.com
 Main PID: 749 (docker)
```

La instalación de Docker ahora le ofrece no sólo el servicio Docker (daemon), sino también la utilidad de línea de comandos docker o el cliente Docker. Exploraremos cómo utilizar el comando docker más adelante en este tutorial.

#

***Paso 2 — Ejecutar el Comando Docker Sin Sudo (Opcional)***

De forma predeterminada, ejecutar el comando docker requiere privilegios de root, es decir, tiene que prefijar el comando con sudo. También puede ser ejecutado por un usuario en el grupo docker, que se crea automáticamente durante la instalación de Docker. 

Si intenta ejecutar el comando docker sin prefijarlo con sudo o sin estar en el grupo docker, obtendrá una salida como esta:
```
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
>#### Nuestro primer contenedor
---
Los contenedores Docker se ejecutan desde imágenes de Docker. De forma predeterminada, extrae estas imágenes de Docker Hub, un registro de Docker administrado por Docker, la compañía detrás del proyecto Docker. 

Cualquier persona puede construir y alojar sus imágenes Docker en Docker Hub, por lo que la mayoría de las aplicaciones y distribuciones Linux que necesitará para ejecutar contenedores Docker tienen imágenes alojadas en Docker Hub.

Para comprobar si puede acceder y descargar imágenes de Docker Hub, escriba:
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
- [Estructura de comandos][s3s1]
- [imágenes y Contenedores][s3s2]
- [Docker Store][s3s3]
- [imágenes oficiales de Docker en GitHub][s3s4]

#

---
>#### Estructura de comandos
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
>#### imágenes y Contenedores
---
Algunas acciones con imágenes y Contenedores: 

| imágenes      | Contenedores  |
| ------------- |:-------------:|
| pull          | run           |
| push          | stop          |
| build         | restart       |
| save          | inspect       |
| load          | stats         |



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
>### Docker Store [(site)](https://store.docker.com/)
---

Plataforma donde obtener información sobre las imágenes que tiene Docker.
Con el buscador web de Docker Store podemos encontrar imágenes oficiales y de la comunidad, aplicar filtros por categorías, ver descripción, información de descarga y utilización sobre las imágenes.

***Desde la terminal de comandos***, también podemos realizar búsquedas de imágenes: 
Puede buscar imágenes disponibles en Docker Hub utilizando el comando docker con el subcomando search. Por ejemplo, para buscar la imagen de Ubuntu, escriba:
```
$ docker search ubuntu
```
El script rastreará Docker Hub y devolverá una lista de todas las imágenes cuyo nombre coincida con la cadena de búsqueda. En este caso, la salida será similar a esto:

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

La salida debería ser similar a esto:
```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              c5f1cf30c96b        7 days ago          120.8 MB
hello-world         latest              94df4f0ce8a4        2 weeks ago         967 B
```

Como veremos más adelante, las imágenes que utilice para ejecutar contenedores pueden modificarse y utilizarse para generar nuevas imágenes, que luego pueden cargarse (pushed es el término técnico) a Docker Hub u otros registros de Docker.



***Descargar una versión específica***

Lo indicaremos a través de las `TAG` de la siguiente forma:

`image:tag`

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
>#### Imágenes oficiales de Docker en GitHub
---

A través de [_GitHub_](https://github.com/docker-library), podremos consultar las versiones de cada imagen oficial, junto a su documentación técnica. 

Por ejemplo, las distintas versiones disponibles de [Ubuntu](https://github.com/docker-library/docs/tree/master/ubuntu).


#

---
##### _Sección 04_
#### Rutinas con imágenes y contenedores.

- [Iniciar y listar contenedores][s4s1]
- [Mostrar los logs][s4s2]
- [Eliminar imágenes y contenedores locales][s4s3]
- [Salvar y cargar imágenes][s4s4]

#

---
>#### Iniciar y listar contenedores
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
>#### Mostrar los logs
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

El flag `--detach` permite que los procesos que se ejecutan en este contenedor no estén anclados a esta terminal, realizándolos en segundo plano. No detiene el contenedor al salir y seguir haciendo otras actividades:

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

- Utilizamos el flag `--follow` para mantener el seguimiento en la terminal de logs que se van generando: 

***`$ docker container logs --follow blissful_boyd`***

#

---
>#### Eliminar imágenes y contenedores locales
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

Listamos las imágenes:

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
>#### Salvar y cargar imágenes
---

***`$ docker image save [OPTIONS] IMAGE [IMAGE...]`***

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

***1º*** - Eliminaremos la imagen de nuestro repositorio local de imágenes para realizar el proceso inverso: 
```
$ docker image rm ubuntu:17.04
```

***Error response from daemon:***

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

***2º*** - Una  vez eliminada la imagen, vamos a ver cómo cargar imágenes desde archivos.

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
#### Construyendo imágenes.

- [Introducción a Dockerfile][s5s1]
- [Construcción de la primera imagen][s5s2]
- [Instrucciones en DockerFile][s5s3]
- [Buenas prácticas en DockerFile][s5s4]

#

---
>#### Introducción a Dockerfile
---
Docker construye las imágenes a partir de las instrucciones definidas en el fichero de texto Dockerfile.
Dockefile define la estructura necesaria para que nuestra aplicación funcione correctamente.
- Dependencias del sistema operativo.
- Programas (servidor, bbdd...).
- Configuraciones del sistema. 
- Dependencias/librerías para la aplicación.
- Código fuente.

Una vez que definido nuestro Dockerfile, podemos lanzar desde la línea de comandos el comando _`build`_, encargado de leer y procesar el fichero Dockerfile para llevar a cabo la construcción de la imagen.

Las imágenes construidas ***se estructuran en capas***. Cada línea del fichero dockerfile representa una capa.

---
>#### Construcción de la primera imagen
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

***Comando asociados a las imágenes de Docker:***

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
>#### Instrucciones en DockerFile
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
>#### Buenas prácticas en DockerFile
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
#### Volúmenes en Docker.

- [Qué son los volúmenes][s6s1]
- [Utilizar volúmenes de datos][s6s2]
- [Utilizar contenedores como volúmenes de datos][s6s3]
- [Salvar la información][s6s4]


---
>#### ¿Qué son los volúmenes?
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
- Al actualizar las imágenes, no se modifica la información en los volúmenes.
- La información contenida en el volumen no se elimina al eliminar los contenedores.

***Formas de uso de los volúmenes***
- Volúmenes de datos.   
- Contenedores como volúmenes de datos.

#

---
>#### Utilizar volúmenes de datos
---
Iniciar un contenedor a partir de la imagen de base de Ubuntu que venimos utilizando.
Al iniciarlos, vamos a montar un volumen en el contenedor con datos/texto del host.
El volumen de datos/ será montado en la raíz del contenedor en el directorio /ejemplo

Vamos a mostrar el contenido del fichero `/ejemplo/texto` una vez que el volumen ha sido montando dentro del contenedor.

Nueva habilidad- Iniciar el contenedor de forma interactiva. Implica que una vez iniciado nos quedaremos dentro de la estructura del contenedor para poder trabajar desde dentro.

***`$ docker run --name ejemplo-volum -v /home/ubuntu/mydockerfiles/datos:/ejemplo -it ubuntu:17.04 /bin/bash`***

`--name ejemplo-volum` => asignamos un nombre al contenedor, en lugar de delegar en Docker.

`-v /home/ubuntu/mydockerfiles/datos:/ejemplo` => Indicamos que monte un volumen con /data en el directorio raíz del contenedor creando la carpeta /ejemplo.

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
>#### Utilizar contenedores como volúmenes de datos
---
Podemos iniciar un contenedor indicando que reserve un espacio para montar un volumen de datos.

Para el siguiente ejemplo, el contenedor partirá de una imagen muy ligera llamada `busybox`. 
Indicaremos que reserve un espacio para montar un vólumen de datos en su raíz de directorios, sin necesidad de referenciar este volumen a un volumen de nuestra máquina Host-(VM-localhost). 
Al contenedor le llamaremos  `data-container`.

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

Podemos ver que automáticamente ha aparecido el fichero `file1`, ya que el fichero fue guardado automáticamente en 
`data-volume` cuando lo creamos en el contenedor de `app1`. De la misma forma sucede con el fichero `file2`.

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
>#### Salvar la información
---
Nuestros datos están guardados en un sistema de archivos dentro de nuestro contenedor `data-container`.
Para salvar los datos vamos a utilizar la siguiente línea de comandos:

***`$ docker container run --rm --volumes-from data-container -v $(pwd):/backup ubuntu:17.04 tar cvf /backup/backup-data.tar /datos`***

Analizando el comando...


- Inicia un contenedor `run` que tiene como base `ubuntu:17.04` y en caso de que ya exista lo borras automáticamente `--rm`
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

- [Obtener IP de la máquina virtual][s7s1]
- [Establece IP estática en la máquina virtual][s7s2]
- [¿Qué es publicar un servicio?][s7s3]
- [Publicar un servicio con Nginx][s7s4]
- [Publicar servicios definiendo el puerto][s7s5]
- [Publicar mi sitio web][s7s6]


#

---
>#### Obtener IP de la máquina virtual
---


Obteniendo un identificador único dentro de nuestra red.

***¿Qué IP tiene nuestra máquina virtual?***
Nuestra VM tiene solamente un adaptador de red NAT, por el que nos permite acceder a la VM y además, disponer del mismo internet que el de la máquina que alberga a la VM, nuestra máquina local-Host.


###### Comenzando...

Primero vamos a ver dónde se encuentran las secciones de configuración de red, tanto de VirtualBox como de la máquina virtual-docker.


***VirtualBox***
- Desde VirtualBox, acceder a las configuraciones globales de Red desde la pestaña:

`Archivos => Preferencias => Red => Redes-solo-anfitrión` 

![][img-conf-vbox-net]





***Máquina virtual - (Ubuntu-Docker)***
- Configuraciones de red para la máquina virutual (ubuntu-server-docker)
- - _Para modificar cualquier propiedad, apagar previamente la máquina virtual-docker si está corriendo_.

Para comunicarnos desde nuestra máquina local con la máquina virtual, vamos a añadir un nuevo adaptador de Red a la máquina virtual con las siguientes características:

Adaptador de red: `Adaptador solo-anfitrión` 
Nombre (default): `VirtualBox Host-Only Ethernet Adapter #3`
Tipo Adaptador (default): Intel Pro/1000 MT Desktop (82540EM)
Modo promiscuo (default): Denegar
Dirección MAC: XXXXXXXXXXX  ===> Refrescar para no entrar en conflicto con la MAC del adaptador #1.
Cable conectado (default): check true

![][img-conf-vm-net]

Una vez añadido el adaptador de red en la máquina virtual, es necesario habilitarlo en la configuración.

######  Habilitar el adaptador en la máquina virtual

Arrancamos de nuevo la máquina virtual y verificamos la configuración actual que está funcionándo en nuestro sistema de red:

`$ ifcongif`

```
ubuntu@ubuntu:~$ ifconfig
docker0   Link encap:Ethernet  direcciónHW 02:42:a4:c4:41:53
          Direc. inet:172.17.0.1  Difus.:0.0.0.0  Másc:255.255.0.0
          ACTIVO DIFUSIÓN MULTICAST  MTU:1500  Métrica:1
          Paquetes RX:0 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:0 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:0
          Bytes RX:0 (0.0 B)  TX bytes:0 (0.0 B)

enp0s3    Link encap:Ethernet  direcciónHW 08:00:27:a6:21:ff
          Direc. inet:10.0.2.15  Difus.:10.0.2.255  Másc:255.255.255.0
          Dirección inet6: fe80::a00:27ff:fea6:21ff/64 Alcance:Enlace
          ACTIVO DIFUSIÓN FUNCIONANDO MULTICAST  MTU:1500  Métrica:1
          Paquetes RX:130 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:102 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1000
          Bytes RX:14974 (14.9 KB)  TX bytes:20802 (20.8 KB)

lo        Link encap:Bucle local
          Direc. inet:127.0.0.1  Másc:255.0.0.0
          Dirección inet6: ::1/128 Alcance:Anfitrión
          ACTIVO BUCLE FUNCIONANDO  MTU:65536  Métrica:1
          Paquetes RX:160 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:160 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1
          Bytes RX:11840 (11.8 KB)  TX bytes:11840 (11.8 KB)
```

Observamos que las redes que están dadas de alta son _[docker0, enp0s3, lo]_:


- Vamos a listar las las redes que existen en total en nuestro sistema:

```
ubuntu@ubuntu:~$ ls /sys/class/net/
docker0  enp0s3  enp0s8  lo
```


Como vemos, aparece la red `enp0s8`, que corresponde al nuevo adaptador de red que acabamos de crear. 

Para adicionar este nuevo adaptador, es necesario modificar el fichero de interfaces de red:

`~$ sudo nano /etc/network/interfaces`

Editando con este fichero, habilitamos el adaptador secundario identificándolo por su nombre `enp0s8`.

***`ubuntu@ubuntu:~$ sudo nano /etc/network/interfaces`***


```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto enp0s3
iface enp0s3 inet dhcp

# Secondary adapter network interface
auto enp0s8
iface enp0s8 inet dhcp
```


Una vez modificado el fichero de configuración, es necesario ***reiniciar el servicio de redes*** de nuestra máquina virtual:

***`ubuntu@ubuntu:~$ sudo systemctl restart networking`***

(En el caso que no funcionase el comando para reiniciar el servicio, bastaría con reiniciar la máquina virtual)

Si volvemos a lanzar el comando `ifconfig`, ahora sí aparece nuestro adaptador-secundario `enp0s8`.

```
enp0s8    Link encap:Ethernet  direcciónHW 08:00:27:62:de:c3
          Direc. inet:192.168.99.100  Difus.:192.168.99.255  Másc:255.255.255.0
          Dirección inet6: fe80::a00:27ff:fe62:dec3/64 Alcance:Enlace
          ACTIVO DIFUSIÓN FUNCIONANDO MULTICAST  MTU:1500  Métrica:1
          Paquetes RX:14 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:10 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1000
          Bytes RX:3211 (3.2 KB)  TX bytes:1332 (1.3 KB)
```

Ahora podemos ver la ***IP*** que nos permitirá acceder desde nuestra máquina local-Host a nuestra máquina virtual.

***`Direc. inet:192.168.99.100`***

Verificamos la conexión enviando un ping desde nuestra máquina local:

```
C:\Users\josem>ping 192.168.99.100

Haciendo ping a 192.168.99.100 con 32 bytes de datos:
Respuesta desde 192.168.99.100: bytes=32 tiempo<1m TTL=64
Respuesta desde 192.168.99.100: bytes=32 tiempo<1m TTL=64
Respuesta desde 192.168.99.100: bytes=32 tiempo<1m TTL=64
Respuesta desde 192.168.99.100: bytes=32 tiempo<1m TTL=64

Estadísticas de ping para 192.168.99.100:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    Mínimo = 0ms, Máximo = 0ms, Media = 0ms
```

#

---
>#### Establece IP estática en la máquina virtual
---

_(opcional)_ Para evitar que nuestra máquina virtual cambie de IP cada vez que arranque, vamos a establecer un IP fija por la que podamos conectarnos siempre.


Vamos a modificar de nuevo el fichero de interfaces de red:

***`ubuntu@ubuntu:~$ sudo nano /etc/network/interfaces`***


```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto enp0s3
iface enp0s3 inet dhcp

# Secondary adapter network interface - static
auto enp0s8
iface enp0s8 inet static
address 192.168.99.14
network 192.168.99.1
netmask 255.255.255.0
```


Reiniciamos la máquina virtual:

***`$ sudo reboot `*** 

Una vez reiniciado, vamos a realizar verificar la conexión hacia la ***IP estática*** enviando un Ping desde nuestra máquina local:

```
C:\Users\josem>ping 192.168.99.14

Haciendo ping a 192.168.99.14 con 32 bytes de datos:
Respuesta desde 192.168.99.14: bytes=32 tiempo<1m TTL=64
Respuesta desde 192.168.99.14: bytes=32 tiempo<1m TTL=64
Respuesta desde 192.168.99.14: bytes=32 tiempo<1m TTL=64
Respuesta desde 192.168.99.14: bytes=32 tiempo<1m TTL=64

Estadísticas de ping para 192.168.99.14:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    Mínimo = 0ms, Máximo = 0ms, Media = 0ms
``` 



#

---
>#### ¿Qué es publicar un servicio?
---

Para poder hacer accesibles nuestro contenedores desde el exterior, debemos facilitar la comunicación entre Host-Contenedor.

Docker facilita esta tarea estableciendo un ***puente de comunicación*** entre el contenedor y la máquina que lo inició (Host).

Este puerto de comunicación se establece utilizando los puertos de ambos lados,  `Host --> xxxx:xx <-- Contenedor`

Las comunicaciones del exterior accederían a la máquina Host por el puerto 8080.

La máquina Host, que fue la que inció el contenedor, sabe que las peticiones que le lleguen por el puerto 8080 debe redireccionarlas al puerto 80 de nuestro contenedor.

- El puerto 8080, puerto con el que trabaja la máquina Host, se define al inciarse el contenedor.
- El puerto 80, puerto con el que trabaja el contenedor, se define durante la creación de la imagen, en el Dockerfile.


De esta forma, todas las personas podrán acceder a la máquina que ha iniciado el contenedor y a través de este puente acceder al servicio del contenedor.

#

---
>#### Publicar un servicio con Nginx
---

Vamos a crear un contendor que contenga un servidor ***Nginx*** y exponer su página de inicio.


***Comenzamos descargando el servidor _Nginx_***:

***`$ docker pull nginx:1.11-alpine`***

```
ubuntu@ubuntu:~$ docker pull nginx:1.11-alpine
1.11-alpine: Pulling from library/nginx
709515475419: Pull complete
4b21d71b440a: Pull complete
c92260fe6357: Pull complete
ed383a1b82df: Pull complete
Digest: sha256:5aadb68304a38a8e2719605e4e180413f390cd6647602bee9bdedd59753c3590
Status: Downloaded newer image for nginx:1.11-alpine
```


***Ver los puertos definidos en la imagen de Nginx***

Como recordarémos, los puertos de los contenedores son definidos durante la creación de la imagen. 
Vamos a conocer qué puertos se definieron durante la creación de la imagen de Nginx descargada.

***`$ docker image inspect nginx:1.11-alpine | more`***

De toda la información que aparece en el archivo JSON, vamos a fijarnos en esta parte: 

```
"ExposedPorts": {
                "443/tcp": {},
                "80/tcp": {}
            },
```

Como vemos, en la imagen de Nginx, los puertos ***443*** y ***80*** son los utilizados para publicar los servicios.



***Arrancar el contenedor publicando los puertos***

***`$ docker container run --rm -d --publish-all nginx:1.11-alpine`***

`-d --publish-all` => Docker utiliza ese parámetro al inciar los contenedores para publicar todos los puertos expuesto que tiene este contenedor.
Identifica los puertos que expone nuestro contenedor y los enlaza con nuestra máquina utilizando un puerto de forma aleatoria.

```
ubuntu@ubuntu:~$ docker container run --rm -d --publish-all nginx:1.11-alpine
897f94107f38330a3f3c49a7ab7e465008b415655109e311ed93977ab548293a
ubuntu@ubuntu:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                    PORTS                                           NAMES
897f94107f38        nginx:1.11-alpine   "nginx -g 'daemon ..."   11 seconds ago      Up 10 seconds             0.0.0.0:32769->80/tcp, 0.0.0.0:32768->443/tcp   wonderful_heisenberg
```


Para acceder desde el exterior al servicio del contenedor, por ejemplo desde nuestra máquina local a la máquina virtual, debemos conectar por : IP de VM + 32769, puerto expuesto por Docker para el contenedor de Nginx.

Desde el navegador web de nuestra máquina local accedemos a la página de inicio de _Nginx_:

***`http://192.168.99.14:32769/`*** 


***Verlos logs del servicio***

***`$ docker container logs -f wonderful_heisenberg`***

```
ubuntu@ubuntu:~$ docker container logs -f wonderful_heisenberg

192.168.99.1 - - [19/Nov/2017:00:36:04 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36" "-"

192.168.99.1 - - [19/Nov/2017:00:36:16 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36" "-"


```

#

---
>#### Publicar servicios definiendo el puerto
---

En la sección anerior, hemos dejado que Docker asigne aleatoriamente un puerto para comunicar con la máquina virtual.
En ocasiones, necesitamos que se utilice un puerto específico para que se comunique con otras aplicaciones.

Vamos a indicar a Docker que utilice un puerto específico de nuestra máquina virtual para publicar nuestra aplicación.

***`$ docker container run --rm -d -p 8080:80 nginx:1.11-alpine`***

```
ubuntu@ubuntu:~$ docker container run --rm -d -p 8080:80 nginx:1.11-alpine
2bf158d012c5a96c8725ac5c74e3f57259cd2461f754860dabe9147eee322f13
ubuntu@ubuntu:~$ docker container ls
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                           NAMES
2bf158d012c5        nginx:1.11-alpine   "nginx -g 'daemon ..."   4 seconds ago       Up 4 seconds        443/tcp, 0.0.0.0:8080->80/tcp   infallible_lumiere
```

Hemos asignado un puerto específico a la máquina virtual `8080` y las peticiones que lleguen por ese puerto serán redireccionadas al puerto `80` del contenedor para comunicarnos con el servicio.

***`http://192.168.99.14:8080/`***

***Si queremos detener el servicio...***

```
ubuntu@ubuntu:~$ docker container stop infallible_lumiere
infallible_lumiere

ubuntu@ubuntu:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                    PORTS               NAMES
ba175f7c7c4d        ubuntu:17.04        "/bin/bash"         28 hours ago        Exited (0) 5 hours ago                        app2
9135fd815a38        ubuntu:17.04        "/bin/bash"         28 hours ago        Exited (0) 5 hours ago                        app1
b330ab85033d        busybox             "sh"                29 hours ago        Exited (0) 29 hours ago                       data-container
b062af057f80        ubuntu:17.04        "/bin/bash"         2 days ago          Exited (0) 2 days ago                         ejemplo-volum
```

#

---
>#### Publicar mi sitio web
---

***Crear una imagen.***

Vamos a crear una imagen con las siguientes capas:

***Capas:***
- aplicación web
- nginx:1.11-alpine

***`$ docker image build -t miweb .`***


***Descargar el código fuente de la aplicación web***

Creamos un directorio donde guardar repositorios y guardamos los fuentes de la capa de la aplicación web, [clonando el repositorio][website].


```
ubuntu@ubuntu:~$ mkdir repos
ubuntu@ubuntu:~$ ls
mydockerfiles  repos  ubuntu-17.04
ubuntu@ubuntu:~$ cd repos/

ubuntu@ubuntu:~/repos$ git clone https://github.com/mmorejon/cursodocker-website.git
Clonar en «cursodocker-website»...
remote: Counting objects: 18, done.
remote: Total 18 (delta 0), reused 0 (delta 0), pack-reused 18
Unpacking objects: 100% (18/18), done.
Comprobando la conectividad… hecho.
```


Verificamos el contenido descargado y contruimos la imagen a partir del Dockerfile del proyecto descargado.

***`$ docker image build -t miweb .` ***

```
ubuntu@ubuntu:~/repos$ ls
cursodocker-website
ubuntu@ubuntu:~/repos$ cd cursodocker-website/
ubuntu@ubuntu:~/repos/cursodocker-website$ ls
Dockerfile  README.md  static-html

ubuntu@ubuntu:~/repos/cursodocker-website$ docker image build -t miweb .
Sending build context to Docker daemon    618kB
Step 1/3 : FROM nginx:1.11-alpine
 ---> bedece1f06cc
Step 2/3 : LABEL Descripción "Mi servicio web" Autor "Jose Manuel" Versión "v1.0.0"
 ---> Running in 95b2f2811f87
 ---> f5d91bb92542
Removing intermediate container 95b2f2811f87
Step 3/3 : COPY static-html /usr/share/nginx/html
 ---> 98a41d17613f
Removing intermediate container bd6f09995770
Successfully built 98a41d17613f
Successfully tagged miweb:latest
```


Verificamos todas las imágenes:

```
ubuntu@ubuntu:~/repos/cursodocker-website$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
miweb               latest              98a41d17613f        About a minute ago   54.3MB
ejemplo             latest              cff6c019fb4f        2 days ago           94.7MB
imag-welcome        latest              7b155699c350        4 days ago           94.7MB
ubuntu              17.04               5e9fde03a0de        2 weeks ago          94.7MB
hello-world         latest              725dcfab7d63        2 weeks ago          1.84kB
busybox             latest              6ad733544a63        2 weeks ago          1.13MB
nginx               1.11-alpine         bedece1f06cc        7 months ago         54.3MB
```


***Ininiciar el contenedor.***
```
ubuntu@ubuntu:~/repos/cursodocker-website$ docker container run --name contenedor-miweb -d -p 8080:80 miweb
21e4f793257522250888946455f2e336347ab08866c9570e5028e729a745b24c

ubuntu@ubuntu:~/repos/cursodocker-website$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                    PORTS                           NAMES
21e4f7932575        miweb               "nginx -g 'daemon ..."   9 seconds ago       Up 8 seconds              443/tcp, 0.0.0.0:8080->80/tcp   contenedor-miweb
```


#


---
##### _Sección 08_
#### Publicar imágenes en Docker Cloud.

- [Estructura del proyecto pensando en Doceker][s8s1]
- [Registrar repositorio en Docker Cloud][s8s2]
- [Publicar imagen en Docker Cloud][s8s3]
- [Fichero dockerignore][s8s4]
 

---
>#### Estructura del proyecto pensando en Doceker
---
Consejos de estructurar y organizar nuestro proyecto.

Toda tecnología incluida en nuestro proyectos va a disponer de un conjunto de ficheros y va a implicar el cómo organizamos estos proyectos.

Lo conveniente es organizar el proyecto por la funcionalidad que cumple cada parte. 

```
proyecto
|
|-controllers/
|  |-auth
|  |-product
|
|-middlewares/
|  |-auth
|
|-models/
|  |-product
|  |-user
|
|-node_modules/
|  |.../
|
|-routes/
|  |-index.js
|
|-services/
|  |-index
|
|-static/ 
|  |-css/
|  |-fonts/
|  |-images/
|  |-js/
|
|-app.js
|-config
|-index
|-package
|
|-README.md
|-Dockerfile

```


---
>#### Registrar repositorio en Docker Cloud
---
Creamos un repositorio en [Docker Cloud][dockercloud] para almacenar nuestras imágenes del proyecto

Una vez que subidas las imágenes al repositorio en Docker Cloud, podremos acceder y descargarlas desde [Docker Store][DockerStore].

![][img-flujo-docker-cloud]

---
>#### Publicar imagen en Docker Cloud
---
- Primero hemos creado un repositorio en Docker Cloud.
- A continuación subiremos nuestra imagen al repositorio. `($ docker push josemanuelcrv/miweb:tagname)`
- Seguidamente la descargaremos desde Docker Store. `($ docker pull josemanuelcrv/miweb)`

Vamos a renombrar el nombre de nuestra imagen `miweb`, dado que al crear el repositorio observamos que nos asigna nuestro identificador, en este caso `josemanuelcrv`/miweb.

Docker Cloud requiere que para la estructura de nombre de imágenes indiquemos el nombre específico de nuestro repositorio `josemanuelcrv/miweb`.

```
ubuntu@ubuntu:~$ docker image tag --help

Usage: docker image tag SOURCE_IMAGE[:Nombre-actual] TARGET_IMAGE[:nuevo-nombre]

```

***`$ docker image tag miweb josemanuelcrv/miweb`***

Una vez lanzado el comando verificamos la lista de imágenes:

```
ubuntu@ubuntu:~$ docker image tag miweb josemanuelcrv/miweb
ubuntu@ubuntu:~$ docker image ls
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
josemanuelcrv/miweb   latest              98a41d17613f        2 days ago          54.3MB
miweb                 latest              98a41d17613f        2 days ago          54.3MB
```

Observamos que existen dos imágenes con el mismo identificador, pero esto no significa que estén duplicadas y ocupando espacio en disco. Docker tiene dos etiquetas apuntando al mismo objeto. Sólo tiene una única imagen.

Acceder a Docker Cloud desde la máquina virtual:

```
ubuntu@ubuntu:~$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: josemanuelcrv
Password: *tupasword*
Login Succeeded
ubuntu@ubuntu:~$
```

***Subir la imagen al repositorio***

```
ubuntu@ubuntu:~$ docker image push josemanuelcrv/miweb
The push refers to a repository [docker.io/josemanuelcrv/miweb]
04719ad7bf83: Pushed
e6983b701b8b: Mounted from library/nginx
90e9f0ac3473: Mounted from library/nginx
9f654519d2ae: Mounted from library/nginx
9f8566ee5135: Mounted from library/nginx
latest: digest: sha256:79d3e4b1cc1954f7527283fd5042891312b67305ee2de68497b681614f5f2084 size: 1363

ubuntu@ubuntu:~$
```

_Pasos que realiza Docker al subir las imágenes:_

1º Lista las capas que tiene esta imagen y las va subiendo de una en una.

Nuestra imagen fue creada partiendo de:

1ª Capa: base de la imagen de Nginx

Adicionalmente:

2ª Capa: adición de nuestra propias etiquetas.

3ª Capa: Los fichero html que copiamos a la carpeta de Nginx publica sus sitios.

La mayoría de la base de nuestra imagen ya está en docker cloud, solo suben las capas adicionadas.

---
>#### Fichero dockerignore
---

El cometido del fichero  `.dockerignore` es la exclusión de contenido prescindible de nuestro proyecto. (exactamente igual que .gitignore para Git)

Infraestructura, despliegue, integración, todos estos elementos están incorporados dentro de nuestro proyecto. Gran parte de estos son prescindibles para el funcionamiento de nuestra aplicación.

```
proyecto
|
|-.git
|
|-ansible
|
|-static/ 
|  |-index.html
|  |-logo.jpeg
|
|-README.md
|-Jenkinsfile
|-Dockerfile
```


Con el archivo `.dockerignore`  definimos el contenido que no queremos que sea contemplado por el _contexto de construcción_ que realiza Docker al inciar la creación de una imagen, quedando excluidos de la misma.

.dockerignore:
- Patrones de exclusión estructurados en líneas
```
# comment
    */temp*
    */temp*
    temp?

    *.md
    !README.md
```




# 

---
##### _Sección 09_
#### Publicar imágenes desde Github.

- [Filosofía de trabajo con GitHub][s9s1]
- [Crear imágenes desde Github][s9s2]
- [Actualización de nuestras imágenes][s9s3]



---
>#### Filosofía de trabajo con GitHub
---

Ventajas:

- Elimina la responsabilidad al desarrollador de cada aplicación a tener que construir él mismo la imagen.
- Flujo de despliegue más rápido. Solo es necesario subir los fuentes a GitHub y asociarlo con Docker Cloud.
- Tareas más ligeras al sólo subir ficheros a GitHub, en lugar de imágenes a Docker Cloud.
- Delega el trabajo de procesado de las capas de dockerfile a Docker Cloud para construir las imágenes.

![][img-flujo-docker-git]


---
>#### Crear imágenes desde Github
---

Trabajo ejecutado de forma conjunta y colaborativa entre las dos plataformas, GitHub + Docker Cloud.
Configurar nuestro repositorio de Docker Cloud para que se contruyan las imágenes de forma automática.


- 1º Habilitar un proveedor de fuentes [GitHub | Bitbucket]

![][img-sourceprovider]



- 2º Crear repositorio en Docker Cloud asociado al proveedor de fuentes GitHub

![][img-create-repo-docker-cloud-associated]


- En la sección de Build Settings, asociar como proveedor de fuentes nuestro repositorio en GitHub.

![][img-config-autobuild]


- En Builds Rules, indicar la rama, el Tag y la localización del archivo `dockerfile` en el que se basará para la construcción. 
En esta ocasión, le estamos indicando que se encuentra en la raíz del proyecto y se llama Dockerfile.

(Sólo crear el proyecto, no crear y construir)

![][img-autobuild-git-branch]


- Una vez creado, accedemos a la sección de construcciones _Builds_ para lanzar nosotros mismos la construcción _Automated Builds_

![][img-trigger-config]



[imágenes]
- config - activar conector github en Docker Cloud
- - elegir repo/rama 
- - Contrucciones recientes
- - Trigguer build - Automated builds
- - (788ed315) corresponde al commit
- - ver detalle, pasos construcción de docker cloud igual q en local.


---
>#### Actualización de nuestras imágenes
---

Vamos a modificar algún archivo del proyecto y volver a subirlo a GitHub. 

```
ubuntu@ubuntu:~/repos/docker-proyect/docker-proyect$ nano Dockerfile

ubuntu@ubuntu:~/repos/docker-proyect/docker-proyect$ git status
En la rama master
Su rama está actualizada con «origin/master».
Cambios no preparados para el commit:
  (use «git add <archivo>...» para actualizar lo que se confirmará)
  (use «git checkout -- <archivo>...» para descartar cambios en el directorio de trabajo)

        modificado:    Dockerfile

no hay cambios agregados al commit (use «git add» o «git commit -a»)

ubuntu@ubuntu:~/repos/docker-proyect/docker-proyect$ git add .

ubuntu@ubuntu:~/repos/docker-proyect/docker-proyect$ git commit -m "change(Dockerfile): modified author name for image metadata"

[master 64f0b83] change(Dockerfile): modified author name for image metadata
 1 file changed, 1 insertion(+), 1 deletion(-)
ubuntu@ubuntu:~/repos/docker-proyect/docker-proyect$ git push origin master
Username for 'https://github.com': josemanuelCRV
Password for 'https://josemanuelCRV@github.com':
Counting objects: 3, done.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 399 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/josemanuelCRV/docker-proyect.git
   f1265b7..64f0b83  master -> master

ubuntu@ubuntu:~/repos/docker-proyect/docker-proyect$
```

Automáticamente, Docker Cloud detectará el cambio en el repositorio y disparará el _trigger_ para volver a construir la imagen.

***Construcción de forma automática en Docker Cloud.***

Observamos en la inforamción de la construcción que el número entre paréntesis corresponde al _Id_ de commit realizado.

![][img-building-2]


Verificar en Docker Cloud la nueva construcción y desde dónde se realizó.
![][img-building-3]





---
## Tercer bloque
##### _Sección 10_
#### Desplegar en producción.


- [Preparar entorno de producción][s10s1]
- [Publicar nuestro servicio en producción][s10s2]
- [Versionar nuestras imágenes][s10s3]


---
>#### Preparar entorno de producción
---

Crearemos nuestra máquina de producción en la plataforma https://clouding.io/.  
Nos ofrece crear un servidor privado _VPS_ de prueba donde instalar nuestros servicios.

(Crear cuenta; Solicita _VISA_; 5€ de prueba; facturación por horas runnig server; debe borrar servidor para stop)

Otras plataformas:

https://ginernet.com/es/

En la máquina de producción instalaremos unicamente lo fundamental, debe ser lo más ligera posible.

- Para nuestras necesidades, Instalaremos una base de Ubuntu y luego Docker.

![][img-create-vps-2]

![][img-create-vps-3]

- Agregar llave _SSH_

![][img-ssh_key-vps]



- Accedemos por _SSH_ al servidor virtual desde nuestra máquina local, no desde la máquina virtual VM VirtualBox.

Podemos utilizar el subsistema _Bash_ que trae Windows 10, o un cliente SSH MobaXterm.

Indicamos el nombre por defecto de usuario de la instalación de Ubuntu del servidor seguido de la _IP_ pública asignada a nuestro _VPS_

***`$ ssh root@46.183.119.159`***

Solicita el password: (Panel de configuración del _VPS_ en clouding)
Mostrar clave: 65xvJYCnjGvo9vMp

```
[josem.Arrakis] ➤ ssh root@46.183.119.159
root@46.183.119.159's password:

              =======
           =============
          ====       ====
        ====           ===   =====
        ===             =============
    == ===               ====     ====
 =========               ===        ===
====   ====             ===         ===
===     ===             ===         ===
===     ====          ======        ===
====  =========     ===== ====    ====
  =======   ===========    =========

Welcome to Ubuntu 17.04 (GNU/Linux 4.10.0-19-generic x86_64)


¡Felicidades, ya tienes tu Servidor creado!
RECUERDA, si acabas de crear tu Servidor Cloud, el sistema puede estar todavía instalando algunas actualizaciones del Sistema Operativo, por lo que comandos como apt, dpkg, yum o rpm pueden no funcionar con normalidad hasta pasados unos minutos.

¡Esperamos que disfrutes de tu Servidor Cloud!

----------------------------------------------

Congratulations, your Server has just been created!
REMEMBER, if you have just created your Cloud Server, some updates of the Operative System might be deployed automatically, that is why commands like apt, dpkg, yum or rpm may not work normally until after some minutes.

We hope that you enjoy your Cloud Server!



 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

Ubuntu 12.04 LTS end-of-life is April 25, 2017 -- Upgrade your Precise systems!
 $ sudo do-release-upgrade -m server

151 packages can be updated.
83 updates are security updates.


/usr/bin/xauth:  file /root/.Xauthority does not exist
root@dckrprod:~#


```


***Verificamos la versión de Ubuntu instalada en el servidor virtual `dckrprod`***

`$ lsb_release -a`


***Actualizamos la versión de Ubuntu instalada***
```
root@dckrprod:~# sudo do-release-upgrade -d
root@dckrprod:~# sudo do-release-upgrade -m server
```

#

***Instalamos Docker en el servidor***

Replicar los pasos de instalación vistos en la sección de [Instalar Docker en Ubutu][s2s3]



---
>#### Publicar nuestro servicio en producción
---


***Creamos un contenedor en el servidor remoto***
```
root@dckrprod:~# docker container run -d -p 80:80 josemanuelcrv/docker-proyect

Unable to find image 'josemanuelcrv/docker-proyect:latest' locally
latest: Pulling from josemanuelcrv/docker-proyect
709515475419: Pull complete
4b21d71b440a: Pull complete
c92260fe6357: Pull complete
ed383a1b82df: Pull complete
ab7ef3d7916c: Pull complete
Digest: sha256:c08702725c115c7c34a23151a53e108220702979bd993dd9c853951167b5a4cf
Status: Downloaded newer image for josemanuelcrv/docker-proyect:latest
0fc11699c5b8723c5676391b3451c13956db30360fcf0d08ca98d0a89cab8c30

root@dckrprod:~# docker container ls
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                         NAMES
0fc11699c5b8        josemanuelcrv/docker-proyect   "nginx -g 'daemon ..."   11 seconds ago      Up 10 seconds       0.0.0.0:80->80/tcp, 443/tcp   relaxed_lalande

root@dckrprod:~#

```


***Verificar el servicio desplegado en el servidor desde el navegador web***

Acceder por la _IP_ pública asignada por clouding.io:  `http://46.183.119.159/` 


***Detener el contenedor actual y levantar otro contenedor a partir de una imagen específica***

En lugar de utilizar por defecto el _Tag_ _latest_, indicamos una tag específico:

```
root@dckrprod:~# docker container ls
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                         NAMES
0fc11699c5b8        josemanuelcrv/docker-proyect   "nginx -g 'daemon ..."   17 minutes ago      Up 17 minutes       0.0.0.0:80->80/tcp, 443/tcp   relaxed_lalande

root@dckrprod:~# docker container stop relaxed_lalande
relaxed_lalande

root@dckrprod:~# docker container ls -la
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS                      PORTS               NAMES
0fc11699c5b8        josemanuelcrv/docker-proyect   "nginx -g 'daemon ..."   18 minutes ago      Exited (0) 17 seconds ago                       relaxed_lalande


root@dckrprod:~# docker run -d -p 80:80 josemanuelcrv/docker-proyect:v1.0.0
Unable to find image 'josemanuelcrv/docker-proyect:v1.0.0' locally
v1.0.0: Pulling from josemanuelcrv/docker-proyect
709515475419: Already exists
4b21d71b440a: Already exists
c92260fe6357: Already exists
ed383a1b82df: Already exists
3743b093404c: Pull complete
Digest: sha256:326327904962948b559c8d41a64ed12d2b9cf3e0eec9940f701bcd8cb7e59393
Status: Downloaded newer image for josemanuelcrv/docker-proyect:v1.0.0
6fd66beb1d6bb12add47b92f86a18f03045f7f2f527ce37d71510370a9341924

root@dckrprod:~# docker image ls
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
josemanuelcrv/docker-proyect   v1.0.0              56ca7e297990        About an hour ago   54.3MB
josemanuelcrv/docker-proyect   latest              315ad462b25b        6 hours ago         54.3MB
root@dckrprod:~#

```



---
>#### Versionar nuestras imágenes
---

Como indicamos anteriormente, por cada última construcción de imagen que realiza Docker, por defecto, asigna el _tag_ _`latest`_. 

Normalmente vamos a necesitar trabajar con etiquetas específicas, como puede ser un nombre/sufjo, un determinado patrón, una versión asignada en el repositorio de GitHub, entre otras.


Vamos a definir una nueva regla en la sección _Builds de Docker Cloud_.

- Añadimos una nueva regla.
- - Indicamos en ***`Source Type`*** que utilice _Tag_ en lugar de _Branch_.
- - Especificamos una _regex_ para identificar nuestra etiqueta.
- - ***Source***: `/^v([0-9.]+)$/` (v y 3 dígitos separados por puntos). Docker iniciará una nueva construcción cuando encuentre este patrón, por ejemplo: `v1.2.3`
- - ***Docker Tag***: `{\1}` Etiqueta que va a asignar Docker a la nueva imagen. el resultado será el número correspondiente a la versión en GitHub. `1.0.2`

![][img-tag]


- Añadimos la etiqueta a nuestros fuentes en GitHub.

```
C:\Users\josem\WorkSpaces\Docker\docker-course\docker-proyect>git tag v1.0.0

C:\Users\josem\WorkSpaces\Docker\docker-course\docker-proyect>git tag
v1.0.0

C:\Users\josem\WorkSpaces\Docker\docker-course\docker-proyect>git push origin --tag
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/josemanuelCRV/docker-proyect.git
 * [new tag]         v1.0.0 -> v1.0.0

```

- Observamos que se ha creado la etiqueta en GitHub y ha comenzado la autoconstrucción en _Docker Cloud_.

![][img-tag-autobuild]


- Accedemos a nuestro servidor remoto de producción `dckrprod` y descargamos la nueva imagen especificando el `nombre_imagen:version`.

```
root@dckrprod:~# docker pull josemanuelcrv/docker-proyect:1.0.0
1.0.0: Pulling from josemanuelcrv/docker-proyect
709515475419: Already exists
4b21d71b440a: Already exists
c92260fe6357: Already exists
ed383a1b82df: Already exists
1ec6930219e4: Pull complete
Digest: sha256:0511446a29fbd11b09d44fe52c6db776c6d4caea607fe40f2baf68debbd90467
Status: Downloaded newer image for josemanuelcrv/docker-proyect:1.0.0

root@dckrprod:~# docker image ls
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
josemanuelcrv/docker-proyect   1.0.0               d916a7eeff87        15 minutes ago      54.3MB
josemanuelcrv/docker-proyect   latest              315ad462b25b        47 hours ago        54.3MB
root@dckrprod:~#
```


- Arrancamos en un contenedor nuestra nueva imagen descargada.

```
root@dckrprod:~# docker run -d -p 80:80 josemanuelcrv/docker-proyect:1.0.0
53bae3c9aa4cfe7d5c61763d359e9f118961d67bdb37f16ba611c43bc091780a

root@dckrprod:~# docker container ps
CONTAINER ID        IMAGE                                COMMAND                  CREATED             STATUS              PORTS                         NAMES
53bae3c9aa4c        josemanuelcrv/docker-proyect:1.0.0   "nginx -g 'daemon ..."   16 seconds ago      Up 15 seconds       0.0.0.0:80->80/tcp, 443/tcp   quizzical_boyd
```


---
##### _Sección 11_
#### Conectando contenedores.


- [Conectar contenedores manualmente][s11s1]
- [¿Qué es Docker Compose?][s11s2]
- [Instalando Docker Compose][s11s3]
- [Creando fichero Compose][s11s4]
- [Escalar servicios][s11s5]



---
>#### Conectar contenedores manualmente
---
Vamos a conectar múltiples contenedores para que se intercambien información y juntos puedan ofrecer servicios que brinden un mejor resultado.

Escenario 

![][img multi-cont-link]



Dispondremos de dos contenedores. Ambos contenedores contendrán una imagen básica de MariaDB. Un contendor hará de sistema de bbdd y el otro contenedor será el cliente consumidor de información conectandose a la bbdd. 

Docker facilita el recurso `Link` que permite crear un puente de cominicación de manera segura. 


***Creando el Contenedor con el sistema de BBDD***

- Descargar en nuestra VM-local la imagen de MariaDB

```
ubuntu@ubuntu:~$ docker image pull mariadb
Using default tag: latest
latest: Pulling from library/mariadb
85b1f47fba49: Pull complete
5671503d4f93: Pull complete
62466fedcc9d: Pull complete
b4ef8399f3aa: Pull complete
e34b2cf62e1d: Pull complete
7291500bf826: Pull complete
a77c97e1ff71: Pull complete
5024f663c035: Pull complete
dc69980fbc04: Pull complete
e57f4562fa50: Pull complete
49c749b145af: Pull complete
Digest: sha256:338258203d1466202d2332e6f6860a3dd24d3bf3578c1e6999c847c975f7e4ca
Status: Downloaded newer image for mariadb:latest
```

+ info: https://mariadb.com/kb/es/mariadb-spanish/


- Arrancar un contenedor con la imagen de mariadb descargada para que realice las funciones de servidor de bbdd.

***`$ docker container run --name db-servidor -e MYSQL_ROOT_PASSWORD=mi-clave -d mariadb`***

`-e` => Permite adicionar al inicio del contenedor una nueva variable de entorno. En este caso le asignamos el password de nuestra bbdd.

```
ubuntu@ubuntu:~$ docker container run --name db-servidor -e MYSQL_ROOT_PASSWORD=mi-clave -d mariadb
d3e07793d5e851085237f3f546862252abf0d4523b31a06686d6fff4bed04c5c

ubuntu@ubuntu:~$ docker container ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
d3e07793d5e8        mariadb             "docker-entrypoint..."   25 seconds ago      Up 24 seconds       3306/tcp            db-servidor
```

Observamos que ha asignado el puerto `3306/tcp` al contenedor, que es el predeterminado para sistemas MYSQL.  Este puerto no lo hemos publicado, por lo tanto no es visible para la VM-local, solo puede ser utilizado éste contenedor `db-servidor`.  

Vamos a inspeccionar el contenido del contenedor generado para verificar qué _IP_ le ha asignado:

***`$ docker container inspect db-servidor | grep IP`***

```
ubuntu@ubuntu:~$ docker container inspect db-servidor | grep IP
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
                    "IPAMConfig": null,
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
ubuntu@ubuntu:~$

```

Como podemos ver, `"IPAddress": "172.17.0.2",` este es el identificador de red que le dio Docker a este contendor.



***Creando el contenedor del cliente.***

Una vez conocidos la información necesaria del contenedor con sistema de BBDD, vamos a contruir el contenedor del cliete.

Crea un contenedor a partir de la imagen `mariadb` de forma interactiva y posicionandome en una terminal dentro del contenedor `-it /bin/bash` y realiza un enlace `--link` de este contenedor que estamos iniciando con el contenedor `db-servidor` y asignandole un nombre `:mysql` para referirnos e identificarlo dentro de este contenedor.
(dentro de este nuevo contenedor, para referirnos al contenedor `db-servidor` será conocido como `:mysql`)

***`$ docker container run --rm --link db-servidor:mysql -it mariadb /bin/bash`***

```
ubuntu@ubuntu:~$ docker container run --rm --link db-servidor:mysql -it mariadb /bin/bash
root@33ecfbf9ef24:/#
```

Creado el contenedor y estando en una terminal TTY dentro del contenedor, vamos a verificar qué variables de entorno tiene.

```
root@33ecfbf9ef24:/# env
MARIADB_MAJOR=10.2
HOSTNAME=33ecfbf9ef24
MYSQL_ENV_MYSQL_ROOT_PASSWORD=mi-clave
TERM=xterm
MYSQL_ENV_MARIADB_VERSION=10.2.10+maria~jessie
MYSQL_ENV_GOSU_VERSION=1.10
MYSQL_PORT_3306_TCP_PORT=3306
MYSQL_ENV_MARIADB_MAJOR=10.2
MYSQL_ENV_GPG_KEYS=199369E5404BD5FC7D2FE43BCBCB082A1BB943DB     430BDF5C56E7C94E848EE60C1C4CBDCDCD2EFD2A        4D1BB29D63D98E422B2113B19334A25F8507EFA5
MYSQL_PORT_3306_TCP=tcp://172.17.0.2:3306
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
GPG_KEYS=199369E5404BD5FC7D2FE43BCBCB082A1BB943DB       430BDF5C56E7C94E848EE60C1C4CBDCDCD2EFD2A        4D1BB29D63D98E422B2113B19334A25F8507EFA5
PWD=/
HOME=/root
SHLVL=1
MYSQL_PORT_3306_TCP_PROTO=tcp
MYSQL_NAME=/confident_fermi/mysql
MYSQL_PORT_3306_TCP_ADDR=172.17.0.2
GOSU_VERSION=1.10
MARIADB_VERSION=10.2.10+maria~jessie
MYSQL_PORT=tcp://172.17.0.2:3306
_=/usr/bin/env
root@33ecfbf9ef24:/#
```

Para obtener una búsqueda más acotada y ordenada sobre lo que nos intesa conocer, vamos a filtra por el nombre del contenedor al que le habíamos asociado `mysql`:
```
root@33ecfbf9ef24:/# env | grep MYSQL
MYSQL_ENV_MYSQL_ROOT_PASSWORD=mi-clave
MYSQL_ENV_MARIADB_VERSION=10.2.10+maria~jessie
MYSQL_ENV_GOSU_VERSION=1.10
MYSQL_PORT_3306_TCP_PORT=3306
MYSQL_ENV_MARIADB_MAJOR=10.2
MYSQL_ENV_GPG_KEYS=199369E5404BD5FC7D2FE43BCBCB082A1BB943DB     430BDF5C56E7C94E848EE60C1C4CBDCDCD2EFD2A        4D1BB29D63D98E422B2113B19334A25F8507EFA5
MYSQL_PORT_3306_TCP=tcp://172.17.0.2:3306
MYSQL_PORT_3306_TCP_PROTO=tcp
MYSQL_NAME=/confident_fermi/mysql
MYSQL_PORT_3306_TCP_ADDR=172.17.0.2
MYSQL_PORT=tcp://172.17.0.2:3306
root@33ecfbf9ef24:/#
```

Como vemos, nos devuelve toda la informacion relacionada con el contenedor que contiene el sistema de BBDD al que le hemos asociado en el momento de la construcción `--link` y asignado un nombre identificativo `mysql` reconocido por este contenedor-cliente. Tiene la misma _IP_: 172.17.0.2, puerto:3306, password, etc...

Vamos a verificar el acceso desde este contenedor-cliente al contenedor asociado utlizando la siguiente línea de SQL común de conexión a una bbdd y utilizando solo variables de entorno:

***`$ mysql -h"$MYSQL_PORT_3306_TCP_ADDR"  -P"$MYSQL_PORT_3306_TCP_PORT"  -uroot  -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"`***

`-h`=> host específico,  `MYSQL_PORT_3306_TCP_ADDR=172.17.0.2`
`-P`=> puerto por el que trabaja, `MYSQL_PORT_3306_TCP_PORT=3306` 
`-uroot`=> usuario root, que es el usuario principal.
`-p`=> password, `MYSQL_ENV_MYSQL_ROOT_PASSWORD=mi-clave` (con 'p' minúscula a diferencia de '-P' del puerto).

```
root@33ecfbf9ef24:/# mysql -h"$MYSQL_PORT_3306_TCP_ADDR"  -P"$MYSQL_PORT_3306_TCP_PORT"  -uroot  -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 9
Server version: 10.2.10-MariaDB-10.2.10+maria~jessie mariadb.org binary distribution

Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> exit
Bye
root@33ecfbf9ef24:/# exit
exit
ubuntu@ubuntu:~$
```

Conexión realizada correctamente. Pocedemos a salir de la línea de comandos de MYSQL y del propio contenedor.


¿Cómo gestionar múltiples contenedores de forma rápida?

---
>#### ¿Qué es Docker Compose?
---

- Docker Compose nos permite definir y ejecutar múltiples conenedores e imágenes de Dcoker al mismo tiempo.
- Facilita la confifguración de múltiples servicios.
- Facilita el despliegue de las aplicaciones.
- Una única línea para iniciar todos los servicios.

Algunas diferencias sobre lo que necesitábamos hacer para realizar lo anterior, respecto a realizarlo con Docker Compose.

Para generar dos contenedores:

Antes...

***`$ docker container run --name db-servidor -e MYSQL_ROOT_PASSWORD=mi-clave -d mariadb`*** - Sistema de BBDD.

***`$ docker container run --rm --link db-servidor:mysql -it mariadb /bin/bash`*** - Contenedor-cliente.


Después...

***`$ docker compose up -d`*** - Única línea en la que procesa un archivo dockercompose donde van definidas todas las tareas que debe realizar.

Ejemplo de `dockercompose`:

``` 
version: '3'
services:       
  web:            ----------> PRIMER servicio
    build: .      ----------> debe construir a partir del directorio raíz
    ports:        ----------> publicar los puertos externo:interno, 
    - "5000:5000" ----------> en ambos 5000, tanto para el contenedor(int) como para la máquina que lo inicie(ext)
    volumes:    
    - .:/code     ----------> con el siguiente volúmen
    - logvolume01:/var/log
    links:        ----------> el contenedor que se inicie debe estar enlazado  
    - redis       ----------> con el servicio aquí definido
  redis:          ----------> SEGUNDO servicio
    image: redis  ----------> únicamente que utilice la imagen oficial de redis 
volumes:
  logvolume01: {}
```




---
>#### Instalando Docker Compose
---

- Desde nuestra VM-local, nos establecemos como _super-user_ para poder instalar mejor este paquete.

```
ubuntu@ubuntu:~$ sudo -i
[sudo] password for ubuntu:
root@ubuntu:~#
```


- Descargamos e instalamos la herramienta Compose: https://docs.docker.com/compose/install/

```
root@ubuntu:~# curl -L https://github.com/docker/compose/releases/download/1.17.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   617    0   617    0     0    724      0 --:--:-- --:--:-- --:--:--   725
100 8649k  100 8649k    0     0  1401k      0  0:00:06  0:00:06 --:--:-- 2053k
root@ubuntu:~#

```

- Y antes de salir del _super-usuario_, asignamos permisos de ejecución al programa instalado.

```
root@ubuntu:~# chmod +x /usr/local/bin/docker-compose
root@ubuntu:~# exit
logout
ubuntu@ubuntu:~$
```


- Verificamos la versión instalada:

```
ubuntu@ubuntu:~$ docker-compose --version
docker-compose version 1.17.1, build 6d101fb
ubuntu@ubuntu:~$
```

- Consultamos la ayuda de esta herramienta:

```
ubuntu@ubuntu:~$ docker-compose --help | more
Define and run multi-container applications with Docker.

Usage:
  docker-compose [-f <arg>...] [options] [COMMAND] [ARGS...]
  docker-compose -h|--help

Options:
  -f, --file FILE             Specify an alternate compose file (default: docker-compose.yml)
  -p, --project-name NAME     Specify an alternate project name (default: directory name)
  --verbose                   Show more output
  --no-ansi                   Do not print ANSI control characters
  -v, --version               Print version and exit
  -H, --host HOST             Daemon socket to connect to

  --tls                       Use TLS; implied by --tlsverify
  --tlscacert CA_PATH         Trust certs signed only by this CA
  --tlscert CLIENT_CERT_PATH  Path to TLS certificate file
  --tlskey TLS_KEY_PATH       Path to TLS key file
  --tlsverify                 Use TLS and verify the remote
  --skip-hostname-check       Don't check the daemon's hostname against the name specified
                              in the client certificate (for example if your docker host
                              is an IP address)
  --project-directory PATH    Specify an alternate working directory
                              (default: the path of the Compose file)

Commands:
  build              Build or rebuild services
  bundle             Generate a Docker bundle from the Compose file
  config             Validate and view the Compose file
  create             Create services
  down               Stop and remove containers, networks, images, and volumes
  events             Receive real time events from containers
  exec               Execute a command in a running container
  help               Get help on a command
  images             List images
  kill               Kill containers
  logs               View output from containers
  pause              Pause services
  port               Print the public port for a port binding
  ps                 List containers
  pull               Pull service images
  push               Push service images
  restart            Restart services
  rm                 Remove stopped containers
  run                Run a one-off command
  scale              Set number of containers for a service
  start              Start services
  stop               Stop services
  top                Display the running processes
  unpause            Unpause services
  up                 Create and start containers
  version            Show the Docker-Compose version information
ubuntu@ubuntu:~$

``` 




---
>#### Creando fichero Compose
---

Para conocer cómo es el funcionamiento de Compose, vamos a reproducir la siguiente infraestructura de sistemas a través de este escenario:

Un contenedor con una Web, y otro contenedor con un balanceador de carga para gestionar las peticiones que recibe el contenedor que queremos publicar.

El balanceador de carga es el único que estará conectado con nuestra VM-local, es decir, dispondrá de un puerto externo:interno (80:80). Quedando el el externo publicado hacia el host por donde recibe las peticiones y el interno para comunicarse con el contenedor del balanceador.

A su vez, el contenedor del balanceador estará conectado por `--link` con el contenedor del sitio web. De esta forma, podremos estar dando servicio sin necesidad de publicar y exponer nuestra web.


![][img-balanceador]


- Vamos a crear el archivo `docker-compose.yml`. 

```
ubuntu@ubuntu:~$ mkdir proxy
ubuntu@ubuntu:~$ cd proxy/
ubuntu@ubuntu:~/proxy$ nano docker-compose.yml
ubuntu@ubuntu:~/proxy$ cat docker-compose.yml

version: '3' -----------------------------------> Indica versión de Docker Compose, Actualmente la 3. Diferencias por tipo de etiquetas que se pueden usar.
services:
  web:  ----------------------------------------> Servicio web.
    image: dockercloud/hello-world -------------> Imagen que va a utlizar la web.
  lb:   ----------------------------------------> Servicio que balancea la carga.
    image: dockercloud/haproxy -----------------> Imagen del sistema de balanceo.
    links:
       - web
     volumes: ----------------------------------------> Indica que el cotenedor del servicio que balancea la carga va a estar trabajando con el fichero docker.shock
       - /var/run/docker.sock:/var/run/docker.sock ---> Y además debe copiar el mismo arbol de carpetas y archivo en la raiz del contenedor, :/var/run/docker.sock
     ports:
       - 80:80 ----------------------------------------> Establece mismo puerto externo:interno, 80 de nuestra VM : con el 80 de nuestro contenedor. 
```

`docker.shock` => este fichero, ubicado en nuestra VM-local, es el encargado de registrar los eventos y cambios que lleva a acabo Docker. 


- Iniciar nuestros servicios con la herramienta Compose.

***`$ docker-compose up -d`***

```
ubuntu@ubuntu:~/proxy$ docker-compose up -d
Creating network "proxy_default" with the default driver -------> Crea red interna para poner en funcionamiento los contenedores en esta red.
Pulling web (dockercloud/hello-world:latest)...
latest: Pulling from dockercloud/hello-world
486a8e636d62: Pull complete
03374a673b41: Pull complete
101d2c41032c: Pull complete
1252e1f36d2b: Pull complete
8385bb1a4377: Pull complete
f29c06131731: Pull complete
Digest: sha256:c6739be46772256abdd1aad960ea8cf6c6a5f841c12e8d9a65cd5ef23bab45fc
Status: Downloaded newer image for dockercloud/hello-world:latest  --------------------> descarga las imágenes
Pulling lb (dockercloud/haproxy:latest)...
latest: Pulling from dockercloud/haproxy
2aecc7e1714b: Pull complete
b2c043fb3918: Pull complete
f8cc77d1dea5: Pull complete
Digest: sha256:ad5c5d4802dee54d8ab5d3d51105d3facfa978eadc4dcced4c95658139efee5f
Status: Downloaded newer image for dockercloud/haproxy:latest  --------------------------> descarga las imágenes
Creating proxy_web_1 ...
Creating proxy_web_1 ... done  --------------------------> Inicia cada uno de los contenedores
Creating proxy_lb_1 ...
Creating proxy_lb_1 ... done  ---------------------------> Inicia cada uno de los contenedores

ubuntu@ubuntu:~/proxy$
```


- Listar los procesos con docker-compose al igual que listar contenedores:

```
ubuntu@ubuntu:~/proxy$ docker-compose ps
   Name                  Command               State                   Ports
--------------------------------------------------------------------------------------------
proxy_lb_1    /sbin/tini -- dockercloud- ...   Up      1936/tcp, 443/tcp, 0.0.0.0:80->80/tcp
proxy_web_1   /bin/sh -c /run.sh               Up      80/tcp
```

El cambio es de presentación:

```
ubuntu@ubuntu:~/proxy$ docker container ls
CONTAINER ID        IMAGE                     COMMAND                  CREATED             STATUS              PORTS                                   NAMES
774a1ae29e26        dockercloud/haproxy       "/sbin/tini -- doc..."   11 minutes ago      Up 11 minutes       443/tcp, 0.0.0.0:80->80/tcp, 1936/tcp   proxy_lb_1
0e65bb643e2e        dockercloud/hello-world   "/bin/sh -c /run.sh"     11 minutes ago      Up 11 minutes       80/tcp                                  proxy_web_1
```

- Accedemos por el navegador a la IP de la VM-local

```
http://192.168.99.14/
```

Observamos en el mensaje de la página que el contenedor iniciado para ofrecer esta web corresponde con el contenedor creado: My hostname is 0e65bb643e2e




---
>#### Escalar servicios
---

El aumento de instancias de nuestros servicios nos permite poder garantizar la disponibilidad frente a un aumeto de accesos superior al soportado.

![][imag-proxy_escalable]


Consultar la ayuda sobre ***`docker-compose scale --help`***

```
ubuntu@ubuntu:~$ docker-compose scale --help
Set number of containers to run for a service.

Numbers are specified in the form `service=num` as arguments.
For example:

    $ docker-compose scale web=2 worker=3

This command is deprecated. Use the up command with the `--scale` flag
instead.

Usage: scale [options] [SERVICE=NUM...]

Options:
  -t, --timeout TIMEOUT      Specify a shutdown timeout in seconds.
                             (default: 10)
```

_Nota: La ayuda muestra informa que el comando está deprecado. Siendo aún compatible, nos invita a utilizar la nueva sintaxis._ 

***`$ docker-compose up --scale web=4 -d`***

Iniciamos el procesado del fichero docker-compose.yml y le indicamos que escale el servio `web` 4 veces.

```
ubuntu@ubuntu:~/proxy$ docker-compose up --scale web=4 -d
Creating proxy_web_1 ...
Creating proxy_web_2 ...
Creating proxy_web_3 ...
Creating proxy_web_4 ...
Creating proxy_web_1 ... done
Creating proxy_web_2 ... done
Creating proxy_web_3 ... done
Creating proxy_web_4 ... done
Recreating proxy_lb_1 ...
Recreating proxy_lb_1 ... done
ubuntu@ubuntu:~/proxy$
```

Verificamos los contenedores levantados...

```
ubuntu@ubuntu:~/proxy$ docker-compose ps
   Name                  Command               State                   Ports
--------------------------------------------------------------------------------------------
proxy_lb_1    /sbin/tini -- dockercloud- ...   Up      1936/tcp, 443/tcp, 0.0.0.0:80->80/tcp
proxy_web_1   /bin/sh -c /run.sh               Up      80/tcp
proxy_web_2   /bin/sh -c /run.sh               Up      80/tcp
proxy_web_3   /bin/sh -c /run.sh               Up      80/tcp
proxy_web_4   /bin/sh -c /run.sh               Up      80/tcp
ubuntu@ubuntu:~/proxy$
```


![][img-scalable-4]


***Desescalada de los servicios...***

Asumamos que ha pasado la punta de carga en nuestros servicio y ya no es necesario tener las 4 instancias levantadas.

***`$ docker-compose up --scale web=1 -d`***

```
ubuntu@ubuntu:~/proxy$ docker-compose up --scale web=1 -d
Stopping and removing proxy_web_2 ... done
Stopping and removing proxy_web_3 ... done
Stopping and removing proxy_web_4 ... done
Starting proxy_web_1 ... done
proxy_lb_1 is up-to-date

ubuntu@ubuntu:~/proxy$ docker-compose ps
   Name                  Command               State                   Ports
--------------------------------------------------------------------------------------------
proxy_lb_1    /sbin/tini -- dockercloud- ...   Up      1936/tcp, 443/tcp, 0.0.0.0:80->80/tcp
proxy_web_1   /bin/sh -c /run.sh               Up      80/tcp
```




***Adicional:***

Si inciamos el comando sin el flag `-d`  (deatach) para ejecutarlo en el proceso principal en lugar de en segundo plano (daemon background), podemos ver las tareas que  realiza:

- Inicia los contenedores
- Asocia (--link) el balanceador con los nuevos contenedores creados del servicio web.
- Muestra configuracíones del balanceador sobre:  logs, máximas conexiones, eventos, seguridad, planificación de procesos, entre otras. 

```
ubuntu@ubuntu:~/proxy$ docker-compose up --scale web=4
Starting proxy_web_1 ...
Starting proxy_web_1 ... done
Creating proxy_web_2 ...
Creating proxy_web_3 ...
Creating proxy_web_4 ...
Creating proxy_web_2 ... done
Creating proxy_web_3 ... done
Creating proxy_web_4 ... done
Starting proxy_lb_1 ...
Starting proxy_lb_1 ... done
Attaching to proxy_web_1, proxy_web_3, proxy_web_2, proxy_web_4, proxy_lb_1
lb_1   | INFO:haproxy:dockercloud/haproxy 1.6.7 is running outside Docker Cloud
lb_1   | INFO:haproxy:Haproxy is running by docker-compose, loading HAProxy definition through docker api
lb_1   | INFO:haproxy:dockercloud/haproxy PID: 5
lb_1   | INFO:haproxy:=> Add task: Initial start - Compose Mode
lb_1   | INFO:haproxy:=> Executing task: Initial start - Compose Mode
lb_1   | INFO:haproxy:==========BEGIN==========
lb_1   | INFO:haproxy:Linked service: proxy_web
lb_1   | INFO:haproxy:Linked container: proxy_web_1, proxy_web_2, proxy_web_3, proxy_web_4
lb_1   | INFO:haproxy:HAProxy configuration:
lb_1   | global
lb_1   |   log 127.0.0.1 local0
lb_1   |   log 127.0.0.1 local1 notice
lb_1   |   log-send-hostname
lb_1   |   maxconn 4096
lb_1   |   pidfile /var/run/haproxy.pid
lb_1   |   user haproxy
lb_1   |   group haproxy
lb_1   |   daemon
lb_1   |   stats socket /var/run/haproxy.stats level admin
lb_1   |   ssl-default-bind-options no-sslv3
lb_1   |   ssl-default-bind-ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES128-SHA256:AES128-SHA:AES256-GCM-SHA384:AES256-SHA256:AES256-SHA:DHE-DSS-AES128-SHA:DES-CBC3-SHA
lb_1   | defaults
lb_1   |   balance roundrobin
lb_1   |   log global
lb_1   |   mode http
lb_1   |   option redispatch
lb_1   |   option httplog
lb_1   |   option dontlognull
lb_1   |   option forwardfor
lb_1   |   timeout connect 5000
lb_1   |   timeout client 50000
lb_1   |   timeout server 50000
lb_1   | listen stats
lb_1   |   bind :1936
lb_1   |   mode http
lb_1   |   stats enable
lb_1   |   timeout connect 10s
lb_1   |   timeout client 1m
lb_1   |   timeout server 1m
lb_1   |   stats hide-version
lb_1   |   stats realm Haproxy\ Statistics
lb_1   |   stats uri /
lb_1   |   stats auth stats:stats
lb_1   | frontend default_port_80
lb_1   |   bind :80
lb_1   |   reqadd X-Forwarded-Proto:\ http
lb_1   |   maxconn 4096
lb_1   |   default_backend default_service
lb_1   | backend default_service
lb_1   |   server proxy_web_1 proxy_web_1:80 check inter 2000 rise 2 fall 3
lb_1   |   server proxy_web_2 proxy_web_2:80 check inter 2000 rise 2 fall 3
lb_1   |   server proxy_web_3 proxy_web_3:80 check inter 2000 rise 2 fall 3
lb_1   |   server proxy_web_4 proxy_web_4:80 check inter 2000 rise 2 fall 3
lb_1   | INFO:haproxy:Launching HAProxy
lb_1   | INFO:haproxy:HAProxy has been launched(PID: 8)
lb_1   | INFO:haproxy:===========END===========

```


---
##### _Sección 12_
#### Registro privado de imágenes.

- [¿Qué es Docker Registry?][s12s1]
- [Instalar Docker Registry][s12s2]
- [Configurar el cliente con Docker Registry][s12s3]
- [Publicar imagen en Docker Registry][s12s4]
- [Agregar interfaz a Docker Registry][s12s5]
- [Escalar servicios][s12s6]


---
>#### ¿Qué es Docker Registry?
---
Docker Registry es una aplicación altamente escalable que funciona del lado del servidor que nos permite almacenar y distribuir las imágenes de Docker.

Beneficios:

- Total control sobre dónde están almacenadas las imágenes.
- Total control sobre la configuración de despliegue de las imágenes.
- Integración de las imágenes al flujo de desarrollo local.
- Almacenamiento propio sin dependencia total de Docker Cloud.
- Almacenamiento privado de todas nuestras imágenes. Docker Cloud sólo permite una imagen privada de forma gratuita.

###### Flujo de trabajo con Docker Cloud/Store
![][img-pre-registry]

###### Flujo de trabajo con Registry
![][img-pos-registry]


---
>#### Instalar Docker Registry
---

Nuestro registro privado lo vamos a instalar en nuestra máquina privada creada en clouding.io.

2º servidor => dckrprod: 46.183.116.126  pss:uoEf9MqMSPzfjhEI

- Instalamos Docker Compose en nuestro servidor de producción remoto.
- Creamos un directorio `registry` donde almacenar los ficheros de configuración de este registro privado.
- Creamos un fichero con docker-compose donde le vamos a describir la forma en la que debe configurar e iniciar nuestro registro privado.  

```
root@dckrprod:~# cd registry/
root@dckrprod:~/registry# nano docker-compose.yml
```

```
version: '3'

services:
 registry:  ---------------------> Único servicio.
  restart: always  --------------> En caso de caída se reinicie siempre.
  image: registry:2  ------------> imagen y versión de registry.
  ports:
   - 5000:5000  -----------------> Único puerto publicado, mismo puerto ext:int.
  volumes:
   - ./data:/var/lib/registry  --> Volúmen añadido a este inicio de conenedor, donde se va a crear una carpeta /data dentro del directorio donde estamos del servidor remoto, y va a estar enlazada dentro del contenedor con la estructura de carpetas /var/lib/registry. La carpeta del contenedor es donde se guardarán las imágenes. Esto nos permite tener los datos del volúmen respaldados y en caso de necesitar borrar el contenedor, podremos volver a inciar un nuevo contenedor utilizando la misma información.
```

- Iniciar el servicio de Registry con docker-compose.

***`$ docker-compose up -d`***


```
root@dckrprod:~/registry# docker-compose up -d
Creating network "registry_default" with the default driver
Pulling registry (registry:2)...
2: Pulling from library/registry
49388a8c9c86: Pulling fs layer
e4d43608dd22: Pulling fs layer
49388a8c9c86: Downloading [>                                                  ]  32.77kB/2.385MB Waiting
49388a8c9c86: Downloading [==========>                                        ]  523.2kB/2.385MB Downloading [=======================>                           ]  2.49388a8c9c86: Downloading [==================================================>]  2.49388a8c9c86: Extracting [>                                                  ]  32.49388a8c9c86: Extracting [===================>                               ]  95049388a8c9c86: Extracting [==================================================>]  2.349388a8c9c86: Extracting [==================================================>]  2.349388a8c9c86: Pull complete
e4d43608dd22: Extracting [>                                                  ]  32.e4d43608dd22: Extracting [=================>                                 ]  720e4d43608dd22: Extracting [=========================================>         ]  1.6e4d43608dd22: Extracting [===========================================>       ]  1.7e4d43608dd22: Pull complete
3a41740f900c: Pull complete
e16ef4b76684: Pull complete
65f212f7c778: Pull complete
Digest: sha256:d837de65fd9bdb81d74055f1dc9cc9154ad5d8d5328f42f57f273000c402c76d
Status: Downloaded newer image for registry:2
Creating registry_registry_1 ...
Creating registry_registry_1 ... done
root@dckrprod:~/registry#
```



- Verificamos que nuestro Registry está correctamente iniciado.

```
root@dckrprod:~/registry# docker-compose ps
       Name                      Command               State           Ports
-------------------------------------------------------------------------------------
registry_registry_1   /entrypoint.sh /etc/docker ...   Up      0.0.0.0:5000->5000/tcp
```


---
>#### Configurar el cliente con Docker Registry
---

Configurar nuestra máquina virtual para conectarlo al registro privado.


- Desde nuestra VM-local, vamos antes de nada a obtener información sobre Docker de nuestra máquina:

***`$ docker info`***

Vamos a fijarnos en la última sección donde define los registros inseguros con los que Docker va a trabajar:
```
Insecure Registries:
 127.0.0.0/8
```


```
ubuntu@ubuntu:~$ docker info
Containers: 8
 Running: 2
 Paused: 0
 Stopped: 6
Images: 13
Server Version: 17.05.0-ce
Storage Driver: aufs
 Root Dir: /var/lib/docker/aufs
 Backing Filesystem: extfs
 Dirs: 49
 Dirperm1 Supported: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host macvlan null overlay
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: 9048e5e50717ea4497b757314bad98ea3763c145
runc version: 9c2d8d184e5da67c95d601382adf14862e4f2228
init version: 949e6fa
Security Options:
 apparmor
 seccomp
  Profile: default
Kernel Version: 4.4.0-98-generic
Operating System: Ubuntu 16.04.3 LTS
OSType: linux
Architecture: x86_64
CPUs: 1
Total Memory: 1.953GiB
Name: ubuntu
ID: JWJU:EU4K:TQOZ:BENY:33UO:73SV:4WSY:KP6L:4XE4:MJMH:EOGG:EMMY
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Username: josemanuelcrv
Registry: https://index.docker.io/v1/
Experimental: false
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false

WARNING: No swap limit support
ubuntu@ubuntu:~$
```



Para conectar nuestro cliente con el registro privado en nuestro servidor de producción remoto es necesario que aparezca nuestro registro en esta configuración:

- Editar el archivo para añadir la configuración necesaria:

***`$ sudo nano /etc/docker/daemon.json`*** 

```
ubuntu@ubuntu:~$ sudo nano /etc/docker/daemon.json
[sudo] password for ubuntu:
ubuntu@ubuntu:~$ cat /etc/docker/daemon.json

ubuntu@ubuntu:~$ sudo cat /etc/docker/daemon.json

{
"insecure-registries": ["46.183.116.126:5000"]
}
ubuntu@ubuntu:~$

``` 


- Reiniciar el servicio de Docker para que actualice los cambios.

***`sudo service docker restart`*** 

Una vez reiniciado el servicio, podemos comprobar que ahora en la sección de _registros inseguros_ aparece la _IP_:_puerto_ del contenedor de nuestro servidor remoto `dckrprod` que contiene nuestro sistema Registry privado.

```
Insecure Registries:
 46.183.116.126:5000
 127.0.0.0/8
Live Restore Enabled: false

WARNING: No swap limit support
ubuntu@ubuntu:~$
```



---
>#### Publicar imagen en Docker Registry
---

- Debemos modificar el nombre de la imagen
- - En ***Docker Cloud*** nos obligaba a estar registrado en la plataforma y a mantener esta estructura de nombre para las imágenes: `identificador\nombre-imagen`
- - En nuesro ***Registry*** debemos utilizar la siguiente estructura de nombres de imágenes: `ip:puerto/nombre-imagen`  donde se encuentre instalado nuestro registro de imágenes.


- Antes de subir desde nuestra VM-local una imagen a nuestro repositorio privado en el servidor remoto, vamos a cambiarle el nombre de acuerado a la especificación anterior:

Para el ejemplo, utilizaremos la imagen más ligera para que la subida sea lo más rapida posible. `busybox  1.13MB`

```
ubuntu@ubuntu:~$ docker image tag busybox 46.183.116.126:5000/busybox
ubuntu@ubuntu:~$ docker image ls
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
josemanuelcrv/miweb           latest              98a41d17613f        11 days ago         54.3MB
miweb                         latest              98a41d17613f        11 days ago         54.3MB
ejemplo                       latest              cff6c019fb4f        2 weeks ago         94.7MB
mariadb                       latest              abcee1d29aac        2 weeks ago         396MB
imag-welcome                  latest              7b155699c350        2 weeks ago         94.7MB
ubuntu                        17.04               5e9fde03a0de        3 weeks ago         94.7MB
hello-world                   latest              725dcfab7d63        3 weeks ago         1.84kB
46.183.116.126:5000/busybox   latest              6ad733544a63        3 weeks ago         1.13MB
busybox                       latest              6ad733544a63        3 weeks ago         1.13MB
dockercloud/haproxy           latest              d9f469c10c27        5 months ago        42.5MB
dockercloud/hello-world       latest              0b898a637c19        5 months ago        30.8MB
nginx                         1.11-alpine         bedece1f06cc        7 months ago        54.3MB
ubuntu@ubuntu:~$
```


- Subir la imagen al repositorio privado:

***`sudo docker image push 46.183.116.126:5000/busybox`***




---
>#### Agregar interfaz a Docker Registry
---

https://hub.docker.com/r/konradkleine/docker-registry-frontend/


```
root@dckrprod:~/registry# nano docker-compose.yml
root@dckrprod:~/registry# cat  docker-compose.yml
version: '3'

services:
 registry:
  restart: always
  image: registry:2
  ports:
   - 5000:5000
  volumes:
   - ./data:/var/lib/registry
 web-registry:
  restart: always
  image: konradkleine/docker-registry-frontend:v2
  ports:
   - 8080:80
  environment:
   - ENV_DOCKER_REGISTRY_HOST=46.183.116.126
   - ENV_DOCKER_REGISTRY_PORT=5000
root@dckrprod:~/registry#


```


```
root@dckrprod:~/registry# docker-compose up -d
Pulling web-registry (konradkleine/docker-registry-frontend:v2)...
v2: Pulling from konradkleine/docker-registry-frontend
85b1f47fba49: Pull complete
e3c64813de17: Pull complete
6e61107884ac: Pull complete
411f14e0e0fd: Pull complete
987d1071cd71: Pull complete
95913db6ef30: Pull complete
1eb7ee3fbde2: Pull complete
9b6f26b1b1a1: Pull complete
daa6941a3108: Pull complete
86cc842193a6: Pull complete
024ab6890532: Pull complete
af9b7d0cb338: Pull complete
02f33fb0dcad: Pull complete
e8275670ee05: Pull complete
1c1a56903b01: Pull complete
afc4e94602b9: Pull complete
df1a95efa681: Pull complete
d8bcb7be9e08: Pull complete
d9c69b7bcc4f: Pull complete
2a14b209069e: Pull complete
e7c2bcdf63d5: Pull complete
efc16e6bbbea: Pull complete
552460069ca8: Pull complete
e6b075740da3: Pull complete
9976bc800046: Pull complete
Digest: sha256:181aad54ee64312a57f8ccba5247c67358de18886d5e2f383b8c4b80a7a5edf6
Status: Downloaded newer image for konradkleine/docker-registry-frontend:v2
registry_registry_1 is up-to-date
Creating registry_web-registry_1 ...
Creating registry_web-registry_1 ... done
root@dckrprod:~/registry#

```



```
root@dckrprod:~/registry# docker-compose ps
         Name                        Command               State               Ports
------------------------------------------------------------------------------------------------
registry_registry_1       /entrypoint.sh /etc/docker ...   Up      0.0.0.0:5000->5000/tcp
registry_web-registry_1   /bin/sh -c $START_SCRIPT         Up      443/tcp, 0.0.0.0:8080->80/tcp
root@dckrprod:~/registry#

```



#### INSTALACIÓN LOCAL DE REGISTRY:

- Instalación de Registry en local:

Creamos un archivo `docker-compose.yml` en un nuevo directorio `registry` de nuestra VM-local.

Definimos que el HOST va a ser nuestra máquina local

```
ubuntu@ubuntu:~/registry$ sudo nano docker-compose.yml

ubuntu@ubuntu:~/registry$ cat docker-compose.yml

version: '3'

services:
 registry:
  restart: always
  image: registry:2
  ports:
   - 5000:5000
  volumes:
   - ./data:/var/lib/registry
 web-registry:
  restart: always
  image: konradkleine/docker-registry-frontend:v2
  ports:
   - 8080:80
  environment:
   - ENV_DOCKER_REGISTRY_HOST=192.168.99.14
   - ENV_DOCKER_REGISTRY_PORT=5000
```



- Ejecutar docker-compose para generar los dos contenedores, el registry y el frontal web:

***`docker-compose up -d`***

Etiquetar la imagen con la estructura de nombres de acuerdo al host donde vamos a subirla, en este caso, este Registry está en un contenedor de nuestra VM-local, por lo que indicamos la _IP_ de nuestra VM-local.

***`docker image tag busybox 192.168.99.14:5000/busybox`***



Subir la imagen al repositorio de Registry de nuestra VM-local:

***`sudo docker image push 192.168.99.14:5000/busybox`***

WEB:

http://192.168.99.14:8080/home


- Añadir la dirección y puerto de nuestro Registro Inseguro Local `192.168.99.14:5000`: 

```




ubuntu@ubuntu:~/registry$ sudo nano /etc/docker/daemon.json
ubuntu@ubuntu:~/registry$ sudo cat /etc/docker/daemon.json

{
"insecure-registries": ["46.183.116.126:5000", "192.168.99.14:5000"]
}
```



- Reinciar el servicio:

***`ubuntu@ubuntu:~/registry$ sudo service docker restart`***

- Verificar la adición de nuestro registro inseguro local:

```
ubuntu@ubuntu:~/registry$ docker info

Insecure Registries:
 192.168.99.14:5000
 46.183.116.126:5000
 127.0.0.0/8
Live Restore Enabled: false
```






---
##### _Sección 13_
#### Conclusiones y resultados.

![][img-final-review]

Mapa de algunas herramientas utilizadas en tecnológías Cloud. 

![CloudNativeLandscape][CloudNativeLandscape]


---
##### _Sección 14_
#### Ejercicios y actividades.

```
Tarea: Crear un fichero compose para publicar un servicio de wordpress local
120 minutos para finalizar   4 soluciones del estudiante
Deseamos poner en funcionamiento un sitio de wordpress en nuestra máquina local para realizarle algunas pruebas a su última versión. Necesitamos poder consultar la base de datos con facilidad y acceder a la web. De igual forma necesitamos poder modificar el código fuente durante el proceso.
```


Define un docker-compose que permita levantar Wordpress.

Se compondrá de dos servicios, uno con la imagen de wordpress oficial y otro con una bbdd (mysql), necearia almacenar la información necesaria por Wordpress.  

- Creamos el fichero docker-compose.yml dentro del nuevo directorio destinado al proyecto.
- Definimos en el servicio _MYSQL_ el nombre de la bbdd `dbwordpress`, las credenciales de acceso para `admin` y para `user`. 
- Definimos en el servicio _Worpress_ las credenciales de acceso del propio Wordpress a la bbdd. 
- Creamos un directotio en la raiz desde donde se está ejecutando el comando llamado `db_data` que estará asociado con el volumen dentro del contenedor en `/var/lib/mysql` para que se pesistan los cambios efectuados por Wordpress en la bbdd. 

```
ubuntu@ubuntu:~/myproyects$ cd wordpress-docker/
ubuntu@ubuntu:~/myproyects/wordpress-docker$ sudo nano docker-compose.yml
[sudo] password for ubuntu:


ubuntu@ubuntu:~/myproyects/wordpress-docker$ sudo cat docker-compose.yml
version: '3'

services:
 db:
  image: mysql:5.7
  volumes:
   - db_data:/var/lib/mysql
  restart: always
  environment:
   MYSQL_ROOT_PASSWORD: admin
   MYSQL_DATABASE: wordpress
   MYSQL_USER: wordpress
   MYSQL_PASSWORD: wordpress

 wordpress:
  depends_on:
   - db
  image: wordpress:latest
  ports:
   - 8000:80
  restart: always
  environment:
   WORDPRESS_DB_HOST: db:3306
   WORDPRESS_DB_USER: wordpress
   WORDPRESS_DB_PASSWORD: wordpress
volumes:
 db_data:
ubuntu@ubuntu:~/myproyects/wordpress-docker$
```

- Procesamos el fichero con docker-compose

```
ubuntu@ubuntu:~/myproyects/wordpress-docker$ docker-compose up -d
Creating volume "wordpressdocker_db_data" with default driver
Creating wordpressdocker_db_1 ...
Creating wordpressdocker_db_1 ... done
Creating wordpressdocker_wordpress_1 ...
Creating wordpressdocker_wordpress_1 ... done
```

- Verificamos que los contenedores o los procesos de docker-compose están corriendo.

```
ubuntu@ubuntu:~/myproyects/wordpress-docker$ docker container ls
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
971e650f726d        wordpress:latest    "docker-entrypoint..."   6 minutes ago       Up 6 minutes        0.0.0.0:8000->80/tcp   wordpressdocker_wordpress_1
d47d14b6f82d        mysql:5.7           "docker-entrypoint..."   6 minutes ago       Up 6 minutes        3306/tcp               wordpressdocker_db_1

ubuntu@ubuntu:~/myproyects/wordpress-docker$ docker-compose ps
           Name                          Command               State          Ports
-------------------------------------------------------------------------------------------
wordpressdocker_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
wordpressdocker_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:8000->80/tcp
```

Accedemos desde el navegador a la _IP_ de nuestra VM-local y el puerto por donde se publica la web `http://192.168.99.14:8000/` 

Observamos el correcto acceso a la página de bienvenida de Wordpress, donde tras la elección de idioma nos ofrece comenzar a configurar un nuevo site-wordpress.

![][img-wordpress-site-config-1]

![][img-wordpress-site-config-2]


Nombre del sitio: hellomoon
password: ssnha^#8)fXi#(sme&

![][img-wordpress-site-config-3]

![][img-web-wordpress]


- Ahora vamos a acceder al contenedor de la bbdd:

***`docker exec -it wordpressdocker_db_1 mysql -uroot -p`***

El Password es el que establecimos cuando creamos el contenedor, definida en la variable: `MYSQL_ROOT_PASSWORD: admin`

```
ubuntu@ubuntu:~/myproyects/wordpress-docker$ docker exec -it wordpressdocker_db_1 mysql -uroot -p
Enter password:admin
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65
Server version: 5.7.20 MySQL Community Server (GPL)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```


- Vamos a verificar por consola qué Bases de Datos tiene este contedor:

```
mysql> show databases;

+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| wordpress          |
+--------------------+
5 rows in set (0.00 sec)

mysql>

```

- Accedemos a la bbdd de wordpress y mostramos las tablas que contiene:

```
mysql> SHOW TABLES;
+-----------------------+
| Tables_in_wordpress   |
+-----------------------+
| wp_commentmeta        |
| wp_comments           |
| wp_links              |
| wp_options            |
| wp_postmeta           |
| wp_posts              |
| wp_term_relationships |
| wp_term_taxonomy      |
| wp_termmeta           |
| wp_terms              |
| wp_usermeta           |
| wp_users              |
+-----------------------+
12 rows in set (0.00 sec)

mysql>

```

- Mostramos el contenido de alguna de las tablas, por ejemplo `wp_users`:

```
mysql> SELECT * FROM wp_users;
+----+---------------+------------------------------------+---------------+--------------------------+----------+---------------------+---------------------+-------------+---------------+
| ID | user_login    | user_pass                          | user_nicename | user_email               | user_url | user_registered     | user_activation_key | user_status | display_name  |
+----+---------------+------------------------------------+---------------+--------------------------+----------+---------------------+---------------------+-------------+---------------+
|  1 | josemanuelcrv | $P$B0CI5rVchhIkpt5DI/qhW55D4YfP0i. | josemanuelcrv | josemanuel.crv@gmail.com |          | 2017-12-05 14:53:43 |                     |           0 | josemanuelcrv |
+----+---------------+------------------------------------+---------------+--------------------------+----------+---------------------+---------------------+-------------+---------------+
1 row in set (0.00 sec)

mysql>exit
Bye
ubuntu@ubuntu:~/myproyects/wordpress-docker$
```


- Ahora vamos a añadir un nuevo servicio para poder administrar la bbdd de forma visual, a través del conocido programa phpMyAdmin.

- - Configuramos este nuevo servicio definiendo los siguiente valores:
- - Imagen base: `phpmyadmin/phpmyadmin`  es la oficial. 
- - Nombre del contenedor: `phpmyadmin`
- - Varibles de entorno:  definidas con las credenciales de conexión con la bbdd definida en el primer servicio `db` .
- - Política de recuperación: Se auto-reiniciará en caso caída del contenedor.
- - Puerto: Servicio publicado por el puerto `8181`,  evitando colisión con otro servicio existente `hello-world` publicado por el `8080`.
- - Volumen: Directorio /sessions solo en la raiz del contenedor.

```
ubuntu@ubuntu:~/myproyects/wordpress-docker$ sudo nano docker-compose.yml

ubuntu@ubuntu:~/myproyects/wordpress-docker$ sudo cat docker-compose.yml
version: '3'

services:
 db:
  image: mysql:5.7
  container_name: mysql_db
  volumes:
   - db_data:/var/lib/mysql
  restart: always
  environment:
   MYSQL_ROOT_PASSWORD: admin
   MYSQL_DATABASE: wordpress
   MYSQL_USER: wordpress
   MYSQL_PASSWORD: wordpress

 wordpress:
  depends_on:
   - db
  image: wordpress:latest
  container_name: wordpress_cms
  ports:
   - 8000:80
  restart: always
  environment:
   WORDPRESS_DB_HOST: db:3306
   WORDPRESS_DB_USER: wordpress
   WORDPRESS_DB_PASSWORD: wordpress

 phpmyadmin:
  image: phpmyadmin/phpmyadmin
  container_name: phpmyadmin
  environment:
   MYSQL_USERNAME: wordpress
   MYSQL_ROOT_PASSWORD: admin
  restart: always
  ports:
   - 8181:80
  volumes:
   - /sessions

volumes:
 db_data:


ubuntu@ubuntu:~/myproyects/wordpress-docker$
```

![][img-phpmyadmin]

- Procesamos el fichero docker-compose.yml. 

Comenzará a descargar la imagen de phpMyAdmin que aún no disponíamos y, al finalizar la descarga, comenzará a crear los contenedores e iniciar los servicios:

```
ubuntu@ubuntu:~/myproyects/wordpress-docker$ docker-compose up -d
ubuntu@ubuntu:~/myproyects/wordpress-docker$ docker-compose up -d
Pulling phpmyadmin (phpmyadmin/phpmyadmin:latest)...
latest: Pulling from phpmyadmin/phpmyadmin
b56ae66c2937: Pull complete
93cb6536f16d: Pull complete
789a0a6da2b4: Pull complete
a44ddb6a2610: Pull complete
ab68eb8c1c8d: Pull complete
69a585d74b76: Pull complete
6bc4bbea6af0: Pull complete
Digest: sha256:5e3b68a7ecddc5d182f7e49251934cdf988680b533dcaf7fd389d8797f4be383
Status: Downloaded newer image for phpmyadmin/phpmyadmin:latest
Creating mysql_db ...
Creating phpmyadmin ...
Creating mysql_db ... done
Creating phpmyadmin ... done
Creating wordpress_cms ...
Creating wordpress_cms ... done


ubuntu@ubuntu:~/myproyects/wordpress-docker$ docker-compose ps
    Name                   Command               State          Ports
-----------------------------------------------------------------------------
mysql_db        docker-entrypoint.sh mysqld      Up      3306/tcp
phpmyadmin      /run.sh phpmyadmin               Up      0.0.0.0:8181->80/tcp
wordpress_cms   docker-entrypoint.sh apach ...   Up      0.0.0.0:8000->80/tcp

ubuntu@ubuntu:~/myproyects/wordpress-docker$
```

![][img-phpmyadmin-web]


---
##### _Sección 15_
#### Fuetes.


Compose Curl: 
https://docs.docker.com/compose/install/#install-compose

https://github.com/docker/compose/releases

https://hub.docker.com/r/docker/compose/

busybox:

https://docs.docker.com/samples/library/busybox/#run-busybox-shell

docker-registry: 

https://docs.docker.com/registry/deploying/#customize-the-published-port

docker-registry-insecure: 

https://docs.docker.com/registry/insecure/#deploy-a-plain-http-registry

docker-registry-frontend: 

https://hub.docker.com/r/konradkleine/docker-registry-frontend/


kitematic wordpress: 

http://192.168.99.100:8000/ (Entrar con kitematic o docker-terminal )

Repo docker-hub: 

https://hub.docker.com/u/josemanuelcrv/

Repo local-privado-registry: 

http://192.168.99.14:8080/home (front buscador para registri:5000)

Mapa de tecnologías cloud: 

https://raw.githubusercontent.com/cncf/landscape/master/landscape/CloudNativeLandscape_latest.jpg

How to Deploy WordPress with Docker Compose: 

https://www.upcloud.com/support/deploy-wordpress-with-docker-compose/

MySQL Docker Containers: Understanding the basics: 

https://severalnines.com/blog/mysql-docker-containers-understanding-basics

mysql/mysql-docker: 

https://github.com/mysql/mysql-docker

Getting Information About Databases and Tables: 

https://dev.mysql.com/doc/refman/5.5/en/getting-information.html

MySQL command to show list of databases on server: 

https://www.cyberciti.biz/faq/mysql-command-to-show-list-of-databases-on-server/

Docker cookbook. Subir una imagen a nuestro Docker Registry privado: 

https://loquemeinteresadelared.wordpress.com/2016/08/10/docker-cookbook-subir-una-imagen-a-nuestro-docker-registry-privado/

Docker Swarm con Docker Machine, Scripts:

http://mmorejon.github.io/blog/docker-swarm-con-docker-machine-scripts/

How To Install Wordpress and PhpMyAdmin with Docker Compose on Ubuntu 14.04:

https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-and-phpmyadmin-with-docker-compose-on-ubuntu-14-04

Docker Hub - phpmyadmin/phpmyadmin:

https://hub.docker.com/r/phpmyadmin/phpmyadmin/

GitHub - phpmyadmin/docker

https://github.com/phpmyadmin/docker




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
[img-conf-vbox-net]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/conf-vbox-net.PNG 
[img-conf-vm-net]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/conf-vm-net.PNG
[img-vbox-net-rules-redirect]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/conf-vbox-net-rules-redirect.PNG
[img-flujo-docker-cloud]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/docker_cloud.PNG
[img-flujo-docker-git]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/docker_github.PNG
[img-sourceprovider]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/enable-github-source-provider.PNG
[img-git-permiss-cloud]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/github-dockercloud-access-permission.PNG
[img-create-repo-docker-cloud-associated]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/create-repo-docker-cloud-associated.PNG
[img-config-autobuild]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/conf-autobuild.PNG
[img-autobuild-git-branch]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/associate-repo-github.PNG
[img-trigger-config]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/trigger-config.PNG

[img-building-2]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/building-2.PNG
[img-building-3]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/building-3.PNG
[img-create-vps-2]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/create-vps-2.PNG
[img-create-vps-3]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/create-vps-3.PNG
[img-ssh_key-vps]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/ssh_key-vps.PNG
[img-tag]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/tags_rules.PNG
[img-tag-autobuild]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/tag-autobuild.PNG
[img multi-cont-link]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/link.PNG
[img-balanceador]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/proxy_link.PNG
[imag-proxy_escalable]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/proxy_escalable.PNG
[img-scalable-4]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/escalable-4.PNG
[img-pre-registry]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/pre-registry-flow.PNG
[img-pos-registry]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/pos-registry-flow.PNG
[wordpress-site-config-1]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/wordpress_site-config_1.PNG
[wordpress-site-config-2]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/wordpress_site-config_2.PNG
[wordpress-site-config-3]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/wordpress_site-config_hellomoon.PNG
[img-web-wordpress]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/web_hellomoon_1.PNG
[img-phpmyadmin-login]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/phpmyadmin_login.PNG
[img-phpmyadmin-web]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/phpmyadmin_wordpress_db.PNG 
[img-final-review]: https://github.com/josemanuelCRV/docker-notes/blob/master/doc_img/final_course_review.PNG




[dockercloud]: https://cloud.docker.com/
[DockerStore]: https://store.docker.com/
[CloudNativeLandscape]:https://raw.githubusercontent.com/cncf/landscape/master/landscape/CloudNativeLandscape_latest.jpg

[website]: https://github.com/mmorejon/cursodocker-website.git


[s1]: <https://github.com/josemanuelCRV/docker-notes#introducción-a-contenedores-y-docker>
[s1s1]: <https://github.com/josemanuelCRV/docker-notes#comportamiento-distinto-en-función-del-entorno>
[s1s2]: <https://github.com/josemanuelCRV/docker-notes#qué-son-los-contenedores-y-las-imágenes>
[s1s3]: <https://github.com/josemanuelCRV/docker-notes#qué-es-docker>
[s1s4]: <https://github.com/josemanuelCRV/docker-notes#productos-y-herramientas>
[s1s5]: <https://github.com/josemanuelCRV/docker-notes#los-contenedores-no-son-máquinas-virtuales>

[s2]: <https://github.com/josemanuelCRV/docker-notes#instalar-docker>
[s2s1]: <https://github.com/josemanuelCRV/docker-notes#plataformas-disponibles-para-la-instalación-de-docker>
[s2s2]: <https://github.com/josemanuelCRV/docker-notes#crear-mv-para-la-instalación-de-ubuntu>
[s2s3]: <https://github.com/josemanuelCRV/docker-notes#instalar-docker-en-ubutu>
[s2s4]: <https://github.com/josemanuelCRV/docker-notes#nuestro-primer-contenedor>

[s3]: <https://github.com/josemanuelCRV/docker-notes#primeros-pasos-con-docker>
[s3s1]: <https://github.com/josemanuelCRV/docker-notes#estructura-de-comandos>
[s3s2]: <https://github.com/josemanuelCRV/docker-notes#imágenes-y-contenedores>
[s3s3]: <https://github.com/josemanuelCRV/docker-notes#docker-store>
[s3s4]: <https://github.com/josemanuelCRV/docker-notes#imágenes-oficiales-de-docker-en-github>

[s4]: <https://github.com/josemanuelCRV/docker-notes#rutinas-con-imágenes-y-contenedores>
[s4s1]: <https://github.com/josemanuelCRV/docker-notes#iniciar-y-listar-los-contenedores>
[s4s2]: <https://github.com/josemanuelCRV/docker-notes#mostrar-los-logs>
[s4s3]: <https://github.com/josemanuelCRV/docker-notes#eliminar-imágenes-y-contenedores-locales>
[s4s4]: <https://github.com/josemanuelCRV/docker-notes#salvar-y-cargar-imágenes>

[s5]: <https://github.com/josemanuelCRV/docker-notes#construyendo-imágenes>
[s5s1]: <https://github.com/josemanuelCRV/docker-notes#introducción-a-dockerfile>
[s5s2]: <https://github.com/josemanuelCRV/docker-notes#construcción-de-la-primera-imagen>
[s5s3]: <https://github.com/josemanuelCRV/docker-notes#instrucciones-en-dockerfile>
[s5s4]: <https://github.com/josemanuelCRV/docker-notes#buenas-prácticas-en-dockerfile>

[s6]: <https://github.com/josemanuelCRV/docker-notes#volúmenes-en-docker>
[s6s1]: <https://github.com/josemanuelCRV/docker-notes#qué-son-los-volúmenes>
[s6s2]: <https://github.com/josemanuelCRV/docker-notes#utilizar-volúmenes-de-datos>
[s6s3]: <https://github.com/josemanuelCRV/docker-notes#utilizar-contenedores-como-volúmenes-de-datos>
[s6s4]: <https://github.com/josemanuelCRV/docker-notes#salvar-la-información>

[s7]: <https://github.com/josemanuelCRV/docker-notes#publicar-servicios>
[s7s1]: <https://github.com/josemanuelCRV/docker-notes#obtener-ip-de-la-máquina-virtual>
[s7s2]: <https://github.com/josemanuelCRV/docker-notes#establece-ip-estática-en-la-máquina-virtual>
[s7s3]: <https://github.com/josemanuelCRV/docker-notes#qué-es-publicar-un-servicio>
[s7s4]: <https://github.com/josemanuelCRV/docker-notes#publicar-un-servicio-con-nginx>
[s7s5]: <https://github.com/josemanuelCRV/docker-notes#publicar-servicios-definiendo-el-puerto>
[s7s6]: <https://github.com/josemanuelCRV/docker-notes#publicar-mi-sitio-web>

[s8]: <https://github.com/josemanuelCRV/docker-notes#publicar-imágenes-en-docker-cloud>
[s8s1]: <https://github.com/josemanuelCRV/docker-notes#estructura-del-proyecto-pensando-en-doceker>
[s8s2]: <https://github.com/josemanuelCRV/docker-notes#registrar-repositorio-en-docker-cloud>
[s8s3]: <https://github.com/josemanuelCRV/docker-notes#publicar-imagen-en-docker-cloud>
[s8s4]: <https://github.com/josemanuelCRV/docker-notes#fichero-dockerignore>

[s9]: <https://github.com/josemanuelCRV/docker-notes#publicar-imágenes-desde-github>
[s9s1]: <https://github.com/josemanuelCRV/docker-notes#estructura-del-proyecto-pensando-en-doceker>
[s9s2]: <https://github.com/josemanuelCRV/docker-notes#registrar-repositorio-en-docker-cloud>
[s9s3]: <https://github.com/josemanuelCRV/docker-notes#publicar-imagen-en-docker-cloud>

[s10]: <https://github.com/josemanuelCRV/docker-notes#desplegar-en-producción>
[s10s1]: <https://github.com/josemanuelCRV/docker-notes#preparar-entorno-de-producción>
[s10s2]: <https://github.com/josemanuelCRV/docker-notes#publicar-nuestro-servicio-en-producción>
[s10s3]: <https://github.com/josemanuelCRV/docker-notes#versionar-nuestras-imágenes>

[s11]: <https://github.com/josemanuelCRV/docker-notes#conectando-contenedores>
[s11s1]: <https://github.com/josemanuelCRV/docker-notes#conectar-contenedores-manualmente>
[s11s2]: <https://github.com/josemanuelCRV/docker-notes#qué-es-docker-compose>
[s11s3]: <https://github.com/josemanuelCRV/docker-notes#instalando-docker-compose>
[s11s4]: <https://github.com/josemanuelCRV/docker-notes#creando-fichero-compose>
[s11s5]: <https://github.com/josemanuelCRV/docker-notes#escalar-servicios>

[s12]: <https://github.com/josemanuelCRV/docker-notes#registros-privados-en-docker>
[s12s1]: <https://github.com/josemanuelCRV/docker-notes#qué-es-docker-registry>
[s12s2]: <https://github.com/josemanuelCRV/docker-notes#instalar-docker-registry>
[s12s3]: <https://github.com/josemanuelCRV/docker-notes#configurar-el-cliente-con-docker-registry>
[s12s4]: <https://github.com/josemanuelCRV/docker-notes#publicar-imagen-en-docker-registry>
[s12s5]: <https://github.com/josemanuelCRV/docker-notes#agregar-interfaz-a-docker-registry>
[s12s6]: <https://github.com/josemanuelCRV/docker-notes#escalar-servicios>

[s13]: <https://github.com/josemanuelCRV/docker-notes#conclusiones-y-resultados>
[s14]: <https://github.com/josemanuelCRV/docker-notes#ejercicios-y-actividades>






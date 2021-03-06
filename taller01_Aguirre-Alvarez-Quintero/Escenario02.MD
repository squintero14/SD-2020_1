# Taller 01

### Car Lewis Álvarez Cossio - A00310516
### Andrés Felipe Aguirre Aguilar - A00329792
### Juan Sebastián Quintero Yoshioka - A00310448

## Infraestructura como código
## Objetivos:
- Comprender las motivaciones de la automatización de infraestructura.
- Realizar de forma autónoma el aprovisionamiento automático de infraestructura.
- Diagnosticar y ejecutar de forma autónoma las acciones necesarias para lograr infraestructuras estables.

## Escenario 02 (sesión en clase)

Con el fin de probar una aplicación web, se requieren montar dos servidores con CentOS 8.1: en al primero se ejecutará el servidor web NGINX y en el segundo un servidor de PostgreSQL

## Pre Requisitos

- VirtualBox
- Vagrant
- Ansible

## Actividades

1. Con acompañamiento del profesor elabore la creación y provisionamiento de la máquina virtual para la base de datos.

Con el acompañamiento del profesor e investigando, se creó y aprovisionó la máquina virtual para la base de datos. Para ello, es necesario crear los siguientes archivos:

![Archivos necesasios](/taller01_Aguirre-Alvarez-Quintero/imagenes/ArchivosNecesarios.png)

- Dentro del archivo playbooks/server.yml se realizará el aprovisionamiento de la máquina virtual.
- En el archivo ansible.cfg iría lo siguiente: 

<code> [defaults] </code> <br>
<code> hostfile = hosts </code> <br>
<code> host_key_checking = False

- En el archivo hosts se especifica una lista o grupo de listas de los hosts en los cuales Ansible realizará el aprovisionamiento.

Posteriormente se realiza la configuración en el Vagrantfile con los siguientes parámetros:

Se configuran parámetros tales como: La imagen del sistema operativo que queremos montar, la dirección IP del servidor y, además, se realiza la configuración de los archivos de ansible que debe de leer para aprovisionar la máquina.

![Vagrantfile](/taller01_Aguirre-Alvarez-Quintero/imagenes/Vagrant.png)

A continuación, se congigura el archivo de HostDatabase, donde se especifíca la dirección ip del servidor de la base de datos.

![Host Database](/taller01_Aguirre-Alvarez-Quintero/imagenes/HostDatabase.png)

Seguido a esto, realizamos la configuración del playbook, server.yml, donde especificamos cómo queremos provisionar nuestro servidor. En ella encontramos los comandos requeridos para: dar nombre a nuestro servidor, convertir el usuario de administración como root, y además instalar y ejecutar postgreSQL.

![Ansible Database](/taller01_Aguirre-Alvarez-Quintero/imagenes/AnsibleDatabase.png)

Luego de tener la configuración antes mencionada, podemos ejecutar el comando "vagrant up" para que se inicie el proceso de creación de la máquina virtual y el aprovisionamiento del servidor por medio de ansible.

![Vagrant Up](/taller01_Aguirre-Alvarez-Quintero/imagenes/VagrantUP.png)

2. Realice la conexión via SSH a la máquina virtual (con acompañamiento del profesor).

Despues de que Vagrannt cree nuestra máquina virtual, nos podemos conectar a ella mediante SSH, usando el comando "vagrant ssh @nameServer".

![SSH Database](/taller01_Aguirre-Alvarez-Quintero/imagenes/SSHDatabase.png)

Después del aprovisionamiento por medio de ansible, verificamos el funcionamiento de PostgreSQL de la siguiente manera:

![Funcionamiento PostgreSQL](/taller01_Aguirre-Alvarez-Quintero/imagenes/PostgresFuncionando.png)

3. Destruya y reconstruya la máquina virtual de la BD (con acompañamiento del profesor).

Para destruir una máquina virtual creada con vagrant usamos el comando "vagrant destroy @nombreServer"

![Destrucción ServerDB](/taller01_Aguirre-Alvarez-Quintero/imagenes/VagrantDestroy.png)

4. A partir del conocimiento anterior cree y provisione la máquina virtual para el servidor web, recuerde que el servidor web sea acessible desde la máquina local.

Para realizar el montaje del servidor web, no necesitamos repetir todos los pasos anteriores, solo debemos cambiar la configuración del playbook serveryml de ansible y especificar que ahora se requiere instalar y ejecutar el servidor web Nginx.

Los cambios realizados fueron los siguientes:

![Configuración Ansible Web Server](/taller01_Aguirre-Alvarez-Quintero/imagenes/AnsibleWebServer.png)

Además, también debemos configurar la dirección IP del servidor. En este caso, usamos la misma que se usó en el servidor de base de datos.

![Conf ip web server](/taller01_Aguirre-Alvarez-Quintero/imagenes/HostWebServer.png)

Finalmente, volvemos a correr el comando "vagrant up" para que se cargue el nuevo serviodr y nos conectamos mediante SSH.

![SSH Web Server](/taller01_Aguirre-Alvarez-Quintero/imagenes/SSHandHttpdRunning.png)

#### Dificultades

1. Durante la elaboracion del ***Escenario 2*** se encontró como dificultad la elaboración correcta del archivo *Vagrantfile*, dado que se debe tener cuidado al momento de la escritura de la maquina virtual que se desea descargar, por ejemplo, para una maquina de *Centos* se puede usar la sentencia **centos/7**, para una maquina ubuntu se puede escribir **bento/ubuntu-18.04**, se debe prestar atencion en que la caja se defina de esta manera para poder ser descargada.
2. Se tuvo dificultades en el momento de utilizar un proveedor para estas maquinas ya que, se intento utilizar **vmware** como proveedor pero se encontro con la situacion de que se deben descargar algunas utilidades de *vagrant* para *vmware* y estas deben ser activadas a traves de una licencia mediante un metodo de pago, por lo tanto se declino el uso de vmware como proveedor.
3. Finalmente, se analizo que en el momento de destruir las maquinas con el comando *vagrant destroy NombreDelaMaquina* se debe utilizar el mismo archivo Vagrantfile que se uso para crearlas, dado que este archivo se utiliza para gestionar todo lo que tiene declarado en él.

#### ¿Por qué esta forma de crear ambiente de pruebas puede ser apropiado (o inapropiado) para desplegar réplicas de este ambiente?

Esta forma de crear ambientes puede ser apropiado en el sentido de que es cómodo, facil y relativamente sencillo descargar maquinas virutales, replicarlas y correrlas. Además, que nos ahorra tiempo, puesto que la configuración y aprovisionamiento se realizó en menos de 5 minutos, comparado con el Escenario anterior que nos tomó cerca de 1 hora. Es claro que hay configuraciones dentro del Vagrantfile que suelen ser algo complicadas, por ejemplo, la configuracion ssh, pero sigue siendo más práctico usar vagrant para estas actividades que buscar descargar una archivo ISO con la imagen de un sistema operativo y pasar por el proceso de instalacion de esté. Tambien se debe aclarar que puede ser un trabajo tedioso tener que entrar a cada maquina por medio de ssh para descargar las aplicaciones que se deseen, sin embargo, como metodo de descarga y despliegue de maquinas virtuales, termina siendo mucho mas eficiente y apropiado realizar este tipo de procesos mediante plataformas como Ansible.

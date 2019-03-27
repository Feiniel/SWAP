# Práctica 1 SWAP: Preparación de las herramientas
    Autores: David Joaquín Gonzalez-Venegas Guerra-Librero y Marina Hurtado Rosales
    Correos: davidvenegasfb@correo.ugr.es; marinahurtado@correo.ugr.es
En esta práctica el objetivo es configurar las máquinas virtuales (al menos dos) para
trabajar en prácticas posteriores, asegurando la conectividad entre dichas máquinas.
Específicamente, hay que llevar a cabo las siguientes tareas:
1. Acceder por ssh de una máquina a otra
2. Acceder mediante la herramienta curl desde una máquina a la otra

------------------------------------------------------------------------------------
## Instalación
Para crear las dos máquinas virtuales que se piden en la práctica hemos utilizado el software de virtualización VirtualBox. Primero hemos creado una nueva instancia de máquina virtual, cargando en la unidad óptica virtual la imagen *ubuntuServer-16.04.iso* dada por el profesor en clase. Para la instalación hemos seguido los pasos dados en el guión, dejando todos los valores por defecto. En un momento de la instalación nos pregunta los programas que queremos instalar, en este caso indicamos que se instalen *LAMP server* y *OPENSSH server*, tal y como se ve en la imagen:

![captura1](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c1.png)

Tras esta instalación comprobamos la versión del servidor Apache instalado mediante el comando:

> $ apache2 -v

![captura2](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c2.PNG)

Asimismo, comprobamos que está en ejecución con el siguiente comando:

> $ ps aux | grep apache

![captura3](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c3.PNG)

Una vez hecho esto solamente falta instalar *curl* para que la instalación esté completa y podamos clonar esta máquina.

![captura4](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c4.PNG)

Una vez hecho esto, clonamos esta máquina.

## Conexión por SSH
Para conectar las dos máquinas por SSH primero es necesario crear una red interna entre ambas. Para ello primero añadimos la red en cada una de las máquinas desde el menú de VirtualBox:

![captura5](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c5.PNG)

Una vez está añadida, hay que configurar esta red en ambas máquinas. Para ello se modifica el archivo */etc/network/interfaces* y se añade la información correspondiente a la red interna en ambas máquinas:

![captura6](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c6.PNG)

![captura7](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c7.PNG)

Al ejecutar *ifconfig* todavía no aparece la red interna, y eso es porque es necesario ejecutar el siguiente comando:

> $ systemctl restart networking.service

Aquí se observa la salida del comando *ifconfig* en ambas máquinas una vez se detecta la red interna:

![captura8](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c8.PNG)

![captura9](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c9.PNG)

Una vez hecho esto, comprobamos mediante un ping que ambas máquinas se ven:

![captura10](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c10.PNG)

![captura11](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c11.PNG)

Ahora probamos a conectarnos por SSH desde la máquina 1 a la 2, creamos un archivo en esa máquina, cerramos la conexión SSH y luego comprobamos desde la máquina 2 que se ha creado el archivo con éxito:

![captura12](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c12.PNG)

![captura13](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c13.PNG)

Y viceversa:

![captura14](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c14.PNG)

![captura15](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c15.PNG)


## Conexión usando *curl*
Hemos creado un archivo html en ambas máquinas, llamado *hola.html* en la carpeta */var/www/html*, y utilizando *curl* hemos accedido a este desde la otra máquina. 
Primero desde la máquina 2 a la 1:

![captura16](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c16.PNG)

![captura17](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c17.PNG)

Y luego desde la máquina 1 a la 2:

![captura18](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c18.PNG)

![captura19](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c19.PNG)

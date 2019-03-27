# Práctica 1 SWAP: Preparación de las herramientas
    Autores: David Joaquín González-Venegas Guerra-Librero y Marina Hurtado Rosales
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
```sh
$ apache2 -v
```

![captura2](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c2.PNG)

Asimismo, comprobamos que está en ejecución con el siguiente comando:
``` sh
$ ps aux | grep apache
```

![captura3](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c3.PNG)

Una vez hecho esto solamente falta instalar *curl* para que la instalación esté completa y podamos clonar esta máquina.

![captura4](https://github.com/Feiniel/SWAP/blob/master/practica1/imagenes/c4.PNG)

Una vez hecho esto, clonamos esta máquina.

## Conexión por SSH

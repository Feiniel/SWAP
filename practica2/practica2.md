# Práctica 2: Clonar la información de un sitio web
    Autores: David Joaquín González-Venegas Guerra-Librero y Marina Hurtado Rosales
    Correos: davidvenegasfb@correo.ugr.es; marinahurtado@correo.ugr.es
Los objetivos de esta segunda práctica son:
- Aprender a copiar archivos mediante ssh.
- Clonar contenido entre máquinas.
- Configurar el ssh para acceder a máquinas remotas sin contraseña.
- Establecer tareas en cron.
--------------------------------------------------------------------------------------------------------------------

## Crear un tar con ficheros locales en un equipo remoto

Creamos un archivo tar directamente en un equipo de destino (porque por ejemplo no tengamos espacio en el equipo local).

Usamos el siguiente comando: 
    
> tar czf - directorio | ssh equipodestino 'cat > ~/tar.tgz'


Mandando así al ssh la salida de la creacion del tar

* Podemos ver aquí como lo hemos ejecutamos un ls en una máquina y no hay nada

![img](https://github.com/davidvenegasfb/SWAP/blob/master/1.png)

* Aquí vemos como ejecutamos el comando en otra máquina conectada previamente por ssh

![img](https://github.com/davidvenegasfb/SWAP/blob/master/2.png)

* Y aquí vemos como la máquina primera ya si tiene el arvhivo

![img](https://github.com/davidvenegasfb/SWAP/blob/master/3.png)

Sin embargo esto no sirve para cantidades grandes de información.

## Instalar la herramienta rsync

Hemos instalado rsync mediante

> sudo apt-get install rsync

Y trabajaremos como usuario no root

### Probar el funcionamiento de rsync

Vamos a clonar la carpeta del servidor web principal mediante el comando

> rsync -avz -e ssh ipmaquina1:/var/www/ /var/www/

* Para ello en primer lugar modificaremos una de las carpetas:

![img](https://github.com/davidvenegasfb/SWAP/blob/master/4.png)

![img](https://github.com/davidvenegasfb/SWAP/blob/master/5.png)

* Y pasamos a usar el comando:

![img](https://github.com/davidvenegasfb/SWAP/blob/master/6.png)

* No nos pide la contraseña ya que ya había configurado ssh para que no nos pidiese contraseña

## Acceso sin contraseña para ssh
Es muy útil a la hora de ejecutar scripts sin que sea necesario que se teclée la contraseña.
Por tanto vamos a pasar a obtener acceso sin contraseña a ssh.
* En primer lugar mediante ssh-keygen generamos la clave
* Por tanto ejecutamos:

> ssh-keygen -b 4096 -t rsa

![img](https://github.com/davidvenegasfb/SWAP/blob/master/8.png)

Pasamos a copiar la clave al equipo remoto, añadiendola al fichero

> ~/.ssh/authorized_keys

Necesitamos tener permisos 600:

![img](https://github.com/davidvenegasfb/SWAP/blob/master/9.png)

Para hacer la copia usamos el comando:

> ssh-copy-id maquina1

![img](https://github.com/davidvenegasfb/SWAP/blob/master/10.png)

## Programar tareas con crontab
Vamos a establecer una tarea en cron que se ejecute cada hora para mantener
actualizado el contenido del directorio /var/www entre las dos máquinas

* Para ello hemos de modificar el archivo /etc/crontab

![img](https://github.com/davidvenegasfb/SWAP/blob/master/7.png)

Donde modificamos una sentencia para que realize el comando que usamos al principio de la práctica.

Y hasta aquí esta práctica

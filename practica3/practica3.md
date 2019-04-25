# Práctica 3: Balanceo de carga
    Autores: David Joaquín González-Venegas Guerra-Librero y Marina Hurtado Rosales
    Correos: davidvenegasfb@correo.ugr.es; marinahurtado@correo.ugr.es
En esta tercera práctica se configurará una red entre varias máquinas de forma que tengamos un balanceador que reparta la carga entre varios servidores finales.
El problema a solucionar es la sobrecarga de los servidores. Se puede balancear
cualquier protocolo, pero dado que esta asignatura se centra en las tecnologías web, balancearemos los servidores HTTP que tenemos configurados.
 De esta forma conseguiremos una infraestructura redundante y de alta disponibilidad.
 El objetivo es obtener la siguiente red de máquinas:
 
<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/graficoGranjaWweb.PNG">
</p>

De esta manera en esta práctica se realizarán las siguientes tareas:
- Configurar una máquina e instalar **nginx** como balanceador de carga.
- Configurar una máquina e instalar **haproxy** como balanceador de carga.
- Someter a la granja web a una alta carga, generada con la herramienta **Apache Benchmark**, teniendo primero nginx y después haproxy.


--------------------------------------------------------------------------------------------------------------------
## Instalación y configuración de nginx como balanceador de carga
Partimos de una máquina virtual con Ubuntu server 16.04 instalado. Lo primero que hacemos es actualizar la máquina:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/C1.PNG">
</p>

Una vez hecho esto, procedemos a instalar nginx con el siguiente comando:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/C2.PNG">
</p>

Ya que está instalado, iniciamos el servicio de nginx con el siguiente comando:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/C3.PNG">
</p>

Con esto finalizaría la instalación, por lo que podemos proceder a su configuración como balanceador de carga. Para ello tenemos que modificar el archivo */etc/nginx/conf.d/default.conf*, así que eliminamos el contenido que tuviese antes y lo cambiamos por el siguiente:

```
upstream apaches {
	server 192.168.1.100;
	server 192.168.1.101;
}
server{
	listen 80;
	server_name balanceador;
	
	access_log /var/log/nginx/balanceador.access.log;
	error_log /var/log/nginx/balanceador.error.log;
	root /var/www/;
	
	location /
	{
		proxy_pass http://apaches;
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_http_version 1.1;
		proxy_set_header Connection "";
	}
}
```

En esta configuración se utiliza el algoritmo **round-robin**, de manera que ambos servidores finales tienen la misma importancia. La configuración para que el balanceador funcione con ponderación sería la siguiente:

```
upstream apaches {
	server 192.168.1.100 weight=2;
	server 192.168.1.101 weight=1;
}
server{
	listen 80;
	server_name balanceador;
	
	access_log /var/log/nginx/balanceador.access.log;
	error_log /var/log/nginx/balanceador.error.log;
	root /var/www/;
	
	location /
	{
		proxy_pass http://apaches;
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_http_version 1.1;
		proxy_set_header Connection "";
	}
}
```

En esta configuración por **ponderación** hemos establecido que por cada tres peticiones que lleguen al balanceador, la máquina con IP 192.168.1.100 atienda 2 de ellas, mientras que la otra solamente una. Esto se hace así porque en el enunciado se ha indicado que la primera máquina es el doble de potente que la segunda.
Una vez configurado todo es necesario deshabilitar nginx como servidor. Para ello se modifica el archivo */etc/nginx/nginx.conf*, comentando la línea que dice 
```
include /etc/nginx/sites-enabled/*;
```

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/C4.PNG">
</p>

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/C5.PNG">
</p>

Una vez hecho esto reiniciamos el servicio de **nginx**. 
Para comprobar que funciona el balanceo de carga y que ejecuta correctamente ambos algoritmos vamos a hacer una serie de peticiones desde una cuarta máquina virtual.
Primero probamos con el algoritmo **round-robin**, el cual vemos que funciona perfectamente, ya que las 4 peticiones que le hemos hecho, se han ido alternando entre una máquina y otra.

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c6.PNG">
</p>

Ahora probamos el algoritmo por **ponderación**. En la imagen se puede apreciar que funciona, ya que de las 4 peticiones que le hemos hecho no han sido alternadas, sino que en las 3 primeras iteraciones se han ejecutado dos peticiones en la máquina 1 y una en la máquina 2, tal y como queríamos.

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c7.PNG">
</p>

## Instalación y configuración de haproxy como balanceador de carga
Hemos instalado haproxy en la misma máquina que nginx, por lo que lo primero que hay que hacer antes de instalarlo es detener la ejecución de nginx con el siguiente comando:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c8.PNG">
</p>

Una vez hecho esto, procedemos a la instalación de haproxy:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c9.PNG">
</p>

Una vez  instalado debemos modificar el archivo */etc/haproxy/haproxy.cfg* ya que la configuración que trae por defecto no nos sirve. Borramos todo lo que contenía el archivo y los sustituimos por lo siguiente:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c10.PNG">
</p>

Con esto quedaría configurado el balanceador con un algoritmo de **round-robin**. 
Una vez está todo instalado y configurado, lanzamos el servicio **haproxy** para poder probar que funciona correctamente (igual que hemos hecho con nginx). Para lanzar el servicio hemos ejecutado el siguiente comando:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c12.PNG">
</p>

Tras realizar la misma prueba que con nginx observamos que el algoritmo funciona correctamente y va alternando entre una máquina y otra.

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c13.PNG">
</p>


## Sometimiento de la granja web a una alta carga con Apache Benchmark
Para someter a una alta carga el servidor balanceado vamos a utilizar Apache Benchmark, el cual instalaremos en la máquina 4 (la máquina que hace las peticiones). Ejecutamos el comando:
```
$ ab -n 10000 -c 10 http://192.168.1.102/index.html
```
Obteniendo los siguientes resultados para el balanceador **nginx**

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c14.PNG">
</p>

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c15.PNG">
</p>

Y estos para **haproxy**

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c16.PNG">
</p>

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c17.PNG">
</p>

## Resumen comparativo
En la siguiente tabla se muestra el tiempo que ha tardado cada uno de los balanceadores en resolver las 10000 peticiones:
    
   | Balanceador | Tiempo (s) | 
   | :------: |:---------:|
   | nginx | 5.233 |
   | haproxy | 3.739 |

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
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c1.PNG">
</p>

Una vez hecho esto, procedemos a instalar nginx con el siguiente comando:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c2.PNG">
</p>

Ya que está instalado, iniciamos el servicio de nginx con el siguiente comando:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/c3.PNG">
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

En esta configuración hemos establecido que por cada tres peticiones que lleguen al balanceador, la máquina con IP 192.168.1.100 atienda 2 de ellas, mientras que la otra solamente una. Esto se hace así porque en el enunciado se ha indicado que la primera máquina es el doble de potente que la segunda.
Una vez configurado todo es necesario deshabilitar nginx como servidor. Para ello se modifica el archivo */etc/nginx/nginx.conf*, comentando la línea que dice 
```
include /etc/nginx/sites-enabled/*;
```

Una vez hecho esto reiniciamos el servicio de **nginx**. 
Para comprobar que funciona el balanceo de carga y que ejecuta correctamente ambos algoritmos vamos a hacer 3 peticiones desde una cuarta máquina virtual.

## Instalación y configuración de haproxy como balanceador de carga

## Sometimiento de la granja web a una alta carga con Apache Benchmark

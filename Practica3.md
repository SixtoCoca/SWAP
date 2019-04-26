# Practica 3. Balanceo de carga

En esta práctica hay 3 objetivos:

1. configurar una máquina e instalar el nginx como balanceador de carga

2. configurar una máquina e instalar el haproxy como balanceador de carga

3. someter a la granja web a una alta carga, generada con la herramienta Apache
Benchmark, teniendo primero nginx y después haproxy.

---

## Servidor web nginx.

Una vez instalada una nueva máquina virtual sin tener instalado apache.Instalamos nginx sobre esta máquina, con los siguientes comandos instalmos y ejecutamos el nginx:

	sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove
	sudo apt-get install nginx
	sudo systemctl start nginx

Ahora tenemos que configurar el fichero /etc/nginx/conf.d/default.conf:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/capturaconfiguracionnginx.png)

Tambien tenemos que eliminar la línea que configura ngnix como servidor web en el archivo /etc/nginx/nginx.conf

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/nginxconfcomentado.png)

Añadiendo esta configuración al fichero al reiniciar el servicio ya funcionaría correctamente el baleanceador con nginx.

Lo comprobamos con esta configuracion(Round-robin):

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/resultadobalanceadongixroundrobin.png)

Cambiamos la configuracion de el fichero /etc/nginx/conf.d/default.conf para que sea por ponderación:.

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/nginxweight.png)

Lo comprobamos con esta configuracion(Ponderacion):

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/resultadonginxponderacion.png)


## Servidor web haproxy.

Una vez instalada una nueva máquina virtual sin tener instalado apache.Instalamos haproxy sobre esta máquina, con los siguientes comandos instalmos:

	sudo apt-get install haproxy

Ahora tenemos que configurar el fichero /etc/haproxy/haproxy.cfg:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/resultadonginxponderacion.png)


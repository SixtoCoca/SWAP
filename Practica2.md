# Practica 1. Clonar la información de un sitio web

Hay que llevar a cabo las siguientes tareas:

1. probar el funcionamiento de la copia de archivos por ssh

2. clonado de una carpeta entre las dos máquinas

3. configuración de ssh para acceder sin que solicite contraseña

4. establecer una tarea en cron que se ejecute cada hora para mantener
actualizado el contenido del directorio /var/www entre las dos máquinas

---

Para clonar una carpeta utilizamos la siguiente instrucción
	
	rsync -avz -e ssh 192.168.1.20:/var/www/ /var/www/

con esta orden clonamos la carpeta /var/www/

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/copiaP2.png)

Para configurar el ssh sin necesitar contraseña primero genero la clave pública

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/generarkeygenP2.png)

Luego en la otra maquina copio el id usando 

	ssh-copy-id ipdemaquinaprincipal

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/copiaidP2.png)

Ya se puede acceder sin que pida la contraseña

Para establecer una tarea cron hay que modificar el archivo /etc/crontab poniendo la siguiente orden que hace que se clone la carpeta /var/www/ cada minuto

	*	*	* * *	sixto	rsync -avz -e ssh 192.168.1.20:/var/www/ /var/www/

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/crontabP2.png)


# Practica 1. Clonar la información de un sitio web

Hay que llevar a cabo las siguientes tareas:

1. probar el funcionamiento de la copia de archivos por ssh

2. clonado de una carpeta entre las dos máquinas

3. configuración de ssh para acceder sin que solicite contraseña

4. establecer una tarea en cron que se ejecute cada hora para mantener
actualizado el contenido del directorio /var/www entre las dos máquinas

---

Para clonar una carpeta utilizamos la siguiente instruccion
	
	rsync -avz -e ssh 192.168.1.20:/var/www/ /var/www/

con esta orden clonamos la carpeta /var/www/

![img]()

Para configurar el ssh sin necesitar contraseña primero genero la clave publica

![img]()

Luego en la otra maquina copio el id usando 

	ssh-copy-id ipdemaquinaprincipal

![img]()

Ya se puede acceder sin que pida la contraseña

Para establecer una tarea cron hay que modificar el archivo /etc/crontab poniendo la siguiente orden que hace que se clone la carpeta /var/www/ cada minuto

	*	*	* * *	sixto	rsync -avz -e ssh 192.168.1.20:/var/www/ /var/www/

![img]()


# Practica 4. Asegurar la granja web

En esta práctica hay 2 objetivos:

1. Instalar un certificado SSL para configurar el acceso HTTPS a los servidores

2. Configurar las reglas del cortafuegos para proteger la granja web.

---

Ejecutamos en una maquina los siguientes comandos para tener el certificado.
	
	a2enmod ssl
	service apache2 restart
	mkdir /etc/apache2/ssl
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt

	
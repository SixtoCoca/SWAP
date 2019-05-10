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

Editamos el archivo default-ssl añadiendo lo siguiente:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/default-ssl.png)

Reiniciamos apache y hacemos peticiones HTTPS.

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/curlHTTPS.png)

Copiamos la clave generada en las demas maquinas principales y en el baleanceador, no se tienen que generar otras se tienen que copiar de esta.En el baleanceador ngix en el archivo /etc/n/ginx/conf.d/default.conf añadimos lo siguiente.

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/default.conf.png)

Para configurar el cortafuegos vamos a crear un script usando iptables el script es el siguiente:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/scriptiptables.png)

Para que este script se ejecute cada vez que se arranca la maquina(y por tanto tengamos el cortafuegos siempre activo) añadimos lo siguiente en el fichero /etc/rc.local

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/rc.local.png)

Con esto ya podemos ver que nos funciona el cortafuegos en la maquina instalada.

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/iptablesm1.png)

# Practica 5. Replicación de bases de datos MySQL
En esta práctica hay 4 objetivos:

1. Crear una BD con al menos una tabla y algunos datos.

2. Realizar la copia de seguridad de la BD completa usando mysqldump en la máquina principal y copiar el archivo de copia de seguridad a la máquina secundaria.

3. Restaurar dicha copia de seguridad en la segunda máquina (clonado manual de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica.

4. Realizar la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.

---

Creamos la base de datos con algunos datos siguiendo el guion:
	
	mysql> create database contactos;
	mysql> use contactos;
	mysql> show tables;
	mysql> create table datos(nombre varchar(100),tlf int);
	mysql> insert into datos(nombre,tlf) values ("pepe",95834987);

Quedando la base de datos asi:

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

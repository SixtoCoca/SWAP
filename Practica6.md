# Practica 6. Servidor de disco NFS
En esta práctica hay 4 objetivos:

1. Configurar una máquina como servidor de disco NFS y exportar una carpeta a los clientes.
2. Montar en las máquinas cliente la carpeta exportada por el servidor.
3. Comprobar que todas las máquinas pueden acceder a los archivos almacenados en la carpeta compartida.
4. Hacer permanente la configuración en los clientes para que monten automáticamente la carpeta compartida al arrancar el sistema.

---

## Configurar el servidor NFS

Primero en la máquina servidora instalamos las herramientas:

	sudo apt-get install nfs-kernel-server nfs-common rcpbin

Creamos la carpeta /dat/compartida 

!img[https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/cambioesclavo.png]
Añadimos las IP en el archivo /etc/exports y reiniciamos en el servicio

!img[https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/archivoetcexports.png]
## Configurar los clientes

En lso clientes instalamos las herramientas:

	sudo apt-get install nfs-common rpcbind

Creamos la carpeta carpetacliente

!img[https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/crearcarpetaclienteP6.png]

Enlazamas la carpeta carpetacliente con la compartida por el servidor

!img[https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/vincularcarpetaclienteP6.png]

Para hacer la configuracion permanente añadimos la siguiente línea al fichero /etc/fstab:

	10.10.10.13:/dat/compartida /home/usuario/carpetacliente/auto,noatime,nolock,bg,nfsvers=3,intr,tcp,actimeo=1800

!img[https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/etcfstabP6.png]

Ejemplo en el que vemos las 2 maquinas clientes creamos un archivo en 1 y luego vemos como se replica en la otra(al llegar a la otra ha tenido que pasar por el servidor).

!img[https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/ejemploP6.png]
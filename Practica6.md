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

Añadimos las IP en el archivo /etc/exports y reiniciamos en el servicio
## Configurar los clientes

En lso clientes instalamos las herramientas:

	sudo apt-get install nfs-common rpcbind
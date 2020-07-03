# Tabla de Contenidos


# Conectandose al servidor

Para todos los comandos posteriores tienes que estar dentro del servidor para poder ejecutarlos

````bash
ssh -i "<archivo>.pem" ubuntu@ip_servidor
````

## Actualizando paquetes del servidor

````bash
sudo apt update -y; sudo apt upgrade -y
````

> Nota: el comando anterior te mostrara dos ventanas en color rosa a las cuales solo le tienes que dar
> enter 

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  > Esta es la primera ventana que se mostrara
  
  ![update_conf_1](aassets/img/update_conf_1.png)
  
  
  > Esta es la segunda ventana que se mostrara
  
  ![update_conf_2](aassets/img/update_conf_2.png)

</details>

## Instalando paquetes para el servicio FTP

Los siguientes paquetes son necesarios para habilitar el servicio de FTP en el servidor

````bash
sudo apt install apache2 -y; sudo apt install vsftpd -y
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![install_ftp_packages](aassets/img/install_ftp_packages.png)
  
</details>

## Editando el archivo de configuracion de FTP

1 - Vamos a editar el archivo de configuracion `vsftpd.conf` ubicado en `/etc` con el siguiente comando:

````bash
sudo vim /etc/vsftpd.conf
````

2 - Al final del archivo insertamos las siguientes lineas

````text
pasv_enable=YES
pasv_min_port=1024
pasv_max_port=1048
pasv_address=<IP_SERVIDOR>
````

> Nota: tienes que remplazar la palabra "<IP_SERVIDOR>" por la ip del servidor


<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![end_lines](aassets/img/end_lines.png)
  
</details>

3 - Reiniciamos el servicio de FTP

````bash
sudo service vsftpd restart
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![restart_ftp_service](aassets/img/restart_ftp_service.png)
  
</details>


## Agregando un usuario al servicio FTP

````bash
sudo adduser ftpuser
````

> Nota: se te pedira ingresar un password para el usuario, despues de eso solo presiona enter para seleccionar los valores
> default 


<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![add_user](aassets/img/add_user.png)
  
</details>

## Restringiendo el directorio de FTP

Por cuestiones de seguridad debemos restringir el acceso a solo la carpeta que queremos compartir con los siguientes pasos:

1 - Abrirmos el archivo de configuracion `vsftpd` del FTP

````bash
sudo vim /etc/vsftpd.conf
````

2 - Desconmentamos la linea `chroot_local_user=YES` y salvamos el archivo

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![chroot_local_user](aassets/img/chroot_local_user.png)
  
</details>


3 - Reiniciamos el servicio de FTP

````bash
sudo service vsftpd restart
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![restart_ftp_service](aassets/img/restart_ftp_service.png)
  
</details>


## Permitir que Filezilla suba archivos al servidor

Inserta los siguientes comandos en la terminal

````bash
echo 'allow_writeable_chroot=YES' | sudo tee -a /etc/vsftpd.conf
sudo sed -i 's|#write_enable=YES|write_enable=YES|g' /etc/vsftpd.conf
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![allow_filezilla](aassets/img/allow_filezilla.png)
  
</details>

## Paso adicional (cambiando el directorio por default del usuario ftpuser)

Por default el directorio en el cual se subiran los archivos es `/home/ftpuser` lo cual no es conveniente,
si se requiere cambiar el directorio actual insertar los siguientes comados en la terminal:

````bash
sudo mkdir -p /var/www/html/ftpuser
sudo chown -R ftpuser:ftpuser /var/www/html/ftpuser
sudo usermod -d "/var/www/html/ftpuser" ftpuser
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![change_dir_ftp_user](aassets/img/change_dir_ftp_user.png)
  
</details>


Posteriormente reiniciar el servicio FTP

````bash
sudo service vsftpd restart
````

<details>
  <summary>Click aqui para ver la salida del comando anterior</summary>
  
  ![restart_ftp_service](aassets/img/restart_ftp_service.png)
  
</details>
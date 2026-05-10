
## *Servidor FTP con VSFTPD

Empezamos por instalar el servicio ftp

```server
sudo apt install vsftpd
```

Después para arrancarlo usaremos:

```server
sudo systemctl status vsftpd
```

![[vsftpd-activo.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/ftp/Imagenes-ftp/vsftpd-activo.png)

En caso de fallo y que no nos salga activo 
```server
sudo systemctl start vsftpd
```


Una vez hecho esto tendremos que activar los permisos para poder subir archivos.

```server
sudo nano /etc/vsftpd.conf
```

Ahora es muy simple, buscamos la línea `write_enable=YES` `chroot_local_user=YES`, `chroot_list_enable=YES` y `chroot_list_file=/etc/vsftpd.chroot_list` y las descomentamos (quitando #).

![[write_yes.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/ftp/Imagenes-ftp/write_yes.png)
![[chroot_local.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/ftp/Imagenes-ftp/chroot_local.png)
* `chroot_local_user` : con esto indicamos que solo puedan acceder usuarios dentro del dominio
* `chroot_list_enable` : habilita la lista de usuarios que pueden acceder a ftp
* `chroot_list_file`: Indicamos donde y como se llama la lista de usuarios permitidos.

Una vez cambiado y guardado es muy importante reiniciar el servicio ftp para que se vean los cambios 

```server
sudo systemclt restart vsftpd
```

Ya lo único que hay que hacer es meter a los usuarios en el archivo que hemos indicado en `chroot_list_file`.

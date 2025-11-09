
## *Servidor FTP con VSFTPD🛠️*

Empezamos por instalar el servicio ftp

```server
sudo apt install vsftpd
```

Después para arrancarlo usaremos:

```server
systemctl status vsftpd
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

Ahora es muy simple, buscamos la línea `write_enable=YES` y la descomentamos (quitando #).

![[etc-vsftpd.conf.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/ftp/Imagenes-ftp/etc-vsftpd.conf.png)
Una vez cambiado y guardado es muy importante reiniciar el servicio ftp para que se vean los cambios 

```server
sudo systemclt restart vsftpd
```
Para más fiabilidad y es personsal, yo prefiero usar los comandos:
Parar el servicio
```server
sudo systemclt stop vsftpd
```
Y volver a encenderlo
```server
sudo systemclt start vsftpd
```


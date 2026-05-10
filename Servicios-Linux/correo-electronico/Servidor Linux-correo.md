Antes de esto es necesario tener bien configurado el DNS:

![[dns-correo.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/correo-electronico/Imagenes-correo/dns-correo.png)

Paquetes a instalar:

```shell
sudo apt install postfix dovecot-core dovecot-imapd dovecot-pop3d dovecot-lmtpd
```

Y aquí empieza la fiesta.

En postfix: `/etc/postfix/main.cf`
![[postfix.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/correo-electronico/Imagenes-correo/postfix.png)

Después configuramos Dovecot: en `/etc/dovecot/conf.d`

*10-mail.conf*:
![[10-mail.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/correo-electronico/Imagenes-correo/10-mail.png)

*10-auth.conf*:

![[10-auth1.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/correo-electronico/Imagenes-correo/10-auth1.png)
![[10-auth2.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/correo-electronico/Imagenes-correo/10-auth2.png)

*10-ssl.conf*
![[10-ssl.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/correo-electronico/Imagenes-correo/10-ssl.png)



En Thunderbird:

![[thunderbird1.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/correo-electronico/Imagenes-correo/thunderbird1.png)



![[thunderbird2.png]](https://github.com/Henner13/Conf_Server/blob/main/Servicios-Linux/correo-electronico/Imagenes-correo/thunderbird2.png)

`Nota: En caso de que no se hayan creado los usuario será necesario crearlos.`


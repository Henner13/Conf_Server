Para comenzar con este servicio lo primero sería instalarlo.

Para la instalación usaremos el siguiente comando:

```shell
sudo apt install bind9
```
`Nota: En las imagenes no uso sudo porque estoy como usuario root`

![[dns2.png]]
Una vez instalado se creará un nuevo directorio llamado `bind`.
Para llegar a ella usaremos
```shell
cd /etc/bind
```
Y comprobaremos todos los archivos que tenemos. 
```shell
ls -l
```

![[dns3.png]]Primero entraremos en archivo con nuestro editor de texto `named.conf.options`

![[dns4.png]]
Este archivo lo usaremos para añadir servidores DNS externos.

Por ejemplo para añadir el DNS de google.
![[dns5.png]]

El ejemplo anterior se usará para trabajar con redes externas.

Para trabajar con redes internas empezaremos con `named.conf.default-zones`

![[dns6.png]]
Aquí no vamos a tocar nada de la configuración pero es importante saber como se estructura ya que más adelante la vamos a utilizar ya que es la base.

Ahora iremos al primer archivo que tendremos que modificar que es `named.conf.local`

![[dns7.png]]
Aquí vamos a generar dominios, dando de alta tantas zonas como quiera.
![[dns8.png]]
primero indicamos la zona en este caso `prueba.com`
Después es importante tabular y seguir la estructura correcta porque si no nos dará fallos.
En la parte de `file` siempre indicaremos la ruta `/etc/bind/db.nombredezona` en este caso sería `/etc/bind/db.pruebacom`

Como veis para facilitar ponemos todo seguido sin punto y siempre empezando por `db.` que nos indica que es una base de datos.

Podremos añadir tantas zonas como dominios queramos.

Una vez configurado, guardamos con `Ctrl+X`

En este punto lo que tenemos que hacer es crear un archivo `db.prueba` para configurar

Un pequeño atajo para ahorrarnos trabajo podemos copiar directamente el archivo local que tiene todo ya por defecto y lo configuramos a base de ese.

```shell
cp /etc/bind/db.local /etc/bind/db.pruebacom
```
También podríamos copiar en su defecto y por seguridad el archivo `db.empty` , al fin y al cabo es la misma estructura.

![[dns10.png]]

Ahora vamos a terminar nuestra configuración, explicando paso a paso que debemos cambiar y por qué.

![[dns11.png]]

![[dns12.png]]
Empezaremos cambiando el nombre de `localhost` añadiendo `ns.` que significa  `nombre de registro` y cambiando `localhost` por el nombre de dominio que hayamos elegido, en este caso `prueba.com`. Podemos observar que termina en punto, es MUY importante que no se elimine o puede dar fallos ya que concatena con el `ns` que hace referencia al nombre de registro dentro de la zona que hemos creado anteriormente.

Seguido, por seguridad cambiaremos la palabra `root` por `admin` o el nombre que queramos y volveremos a poner nuestro nombre de dominio `prueba.com` y otra vez acabado en punto, no lo olvidemos.

Más abajo volvemos a repetir el cambio de `localhost` por `ns.prueba.com`.
La siguiente línea en este caso sería opcional `@` indica el nombre de la zona principal o raíz definida. Eso mismo se hace en la 3ª línea de forma más específica.

Ahora es simple:
3ª Línea --> Indicamos que es el nombre de registro `ns`, `IN` de internet que prácticamente será siempre y `A` que hace referencia a IPv4, si viéramos `AAAA` haríamos referencia a IPv6,  pero aquí como nuestra IP es una IPv4 usaremos `A`. Por último hay que indicar la IP de nuestro DNS por el que ofrecemos el servicio.

4ª Línea --> Indicamos que es un servicio web con `www` y cual es la IP por la que correrá el servicio.

5ª Línea --> Indicamos que es una `web` por internet `IN` y ahora indicamos que vamos a señalar su alias con `CNAME` y ponemos ese alias `www.prueba.com`

Una vez hecho esto ya solo tenemos que guardar el archivo,  comprobar que el estado de nuestro servicio DNS y el funcionamiento en un cliente.

Para comprobar el estado de nuestro servidor a mi me gusta pararlo, reanudarlo y ya comprobar si funciona :
```shell
service bind9 stop
```
```shell
service bind9 start
```
```shell
service bind9 status
```

![[dns13.png]]
Si todo nos sale habilitado como en la imagen de arriba no deberíamos tener problemas con nuestro servicio de DNS interno.


Y en el cliente, en mi caso un Ubuntu 24.10 con el comando 
```shell
nslookup www.prueba.com
```

![[dns14.png]]
También podemos usar para ver los servidores de NS:
```shell
dig www.prueba.com NS
```

![[dns15.png]]

En caso de fallo habría que comprobar con un `ping` para ver si hay conexión entre nuestro cliente y servidor, que muchas veces es el principal problema.
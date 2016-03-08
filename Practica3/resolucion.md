# Practica 3

## 1. Instalación de NginX y HAproxy

Trás crear una nueva máquina virtual llamada **balanceador**, instalamos haproxy con el comando: **apt-get install haproxy**.
A continuación, pasamos a la instalación de nginx. Dicho proceso se muestra en la captura de abajo:

- [Instalando NginX](http://s1380.photobucket.com/user/adnan1989/media/install%20nginx_zpsexho8yyh.png.html)


## 2. Configuración de HAproxy y realización de peticiones desde máquina externa

Una vez instalado, pasamos a configurarlo para que reparta la carga siguiendo el algoritmo robin-round y lo lanzamos
con el comando: **/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg**. Después, nos vamos a otra máquina para hacer 
peticiones al balanceador con curl:

- [Configurando HAproxy para Robin-Round](http://s1380.photobucket.com/user/adnan1989/media/haproxy%20confi%20rr_zpsgpx6i02f.png.html)
- [Haciendo peticiones](http://s1380.photobucket.com/user/adnan1989/media/access%20haproxy%20robin-round_zpsd8xbbj29.png.html)

Ahora pasamos a configurarlo para que reparta la carga según la ponderación que tengan los servidores de la granja y lo reiniciamos.
A continuación, igual que en el proceso anterior, hacemos peticiones con curl desde otra máquina:

- [Configurando HAproxy para ponderación](http://s1380.photobucket.com/user/adnan1989/media/haproxy%20confi_zpsw3m6bm5a.png.html)
- [Haciendo peticiones](http://s1380.photobucket.com/user/adnan1989/media/access%20haproxy%20pond_zpst4dkk2wx.png.html)


## 3. Configuración de NginX y realización de peticiones desde máquina externa

Lo configuramos para que reparta la carga siguiendo el algoritmo robin-round y lo iniciamos con el comando: **service nginx start**. 
Una vez hecho esto, nos vamos a otra máquina para hacer las peticiones:

- [Configurando Nginx para robin-round](http://s1380.photobucket.com/user/adnan1989/media/nginx%20robin-round_zpsr3upnlnx.png.html)
- [Haciendo peticiones](http://s1380.photobucket.com/user/adnan1989/media/access%20nginx%20robin-round_zpsdubwftvk.png.html)

Ahora lo configuramos para que reparta la carga según la ponderación de los servidores de la granja y lo reinicimos con
el comando: **service nginx restart**. A continuación, desde otra máquina hacemos las peticiones:

- [Configurando NginX para ponderación](http://s1380.photobucket.com/user/adnan1989/media/nginx%20ponderacion_zpswkbehcxz.png.html)
- [Haciendo peticiones](http://s1380.photobucket.com/user/adnan1989/media/access%20nginx%20pond_zpsdnijz2va.png.html)

# Práctica 2

## 1. Creación del tar con ficheros locales en una máquina remota

Desde la máquina principal, creamos un tar con el directorio /root/Desktop en la segunda máquina.

- [Creando el tar](s1380.photobucket.com/user/adnan1989/media/tar server1_zpsuz88nzi1.png.html)
- [tar creado](http://s1380.photobucket.com/user/adnan1989/media/tar%20server2_zpswhes10pk.png.html)


## 2. Instalar rsync

Trás instalar la herramienta con el comando: **apt-get install rsync**, clonamos la carpeta web /var/www en
la segunda máquina.

- [Clonando carpeta](http://s1380.photobucket.com/user/adnan1989/media/rsync%20server2_zpsjjwifsxb.png.html)


## 3. Configurar ssh para que no pida contraseña

Desde la segunda máquina generamos las claves públicas y privadas, a coninuación copiamos la pública en la
máquina principal, y comprobámos que se puede acceder sin contarseña.

- [Generando claves](http://s1380.photobucket.com/user/adnan1989/media/ssh-keygen%20server2_zpsjjswn38l.png.html)
- [Copiando clave y accediendo](http://s1380.photobucket.com/user/adnan1989/media/ssh%20sin%20pass%20server2_zpsvfqq5gzk.png.html)


## 4. Programar tareas con cron

Vamos a programar una tarea para que cron actualice cada hora la carpeta web de la segunda máquina con el contenido de la principal.
Para ello vamos a crear un script llamado 'actualiza.sh' para actulizarla con rsync. A continuación editamos el fichero crontab
para añadirle nuestra tarea.

- [Script](http://s1380.photobucket.com/user/adnan1989/media/script%20rsync%20server2_zpszlstv4a3.png.html)
- [Editando crontab](http://s1380.photobucket.com/user/adnan1989/media/crontab%20server2_zpstuzut1hj.png.html)

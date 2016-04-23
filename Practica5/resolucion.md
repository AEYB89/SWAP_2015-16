# Práctica 5

## 1. Creación de la base de datos MySQL

En el server1 iniciamos la consola de **mysql** con el comando `mysql -u root -p`. A continuación creamos una base de datos llamada `contactos`, en dicha BD creamos una tabla llamada `datos` para insertar los datos.

- [Creando la base de datos](http://s1380.photobucket.com/user/adnan1989/media/crear BD_zpsrdywisvu.png.html)


## 2. Replicación de la base de datos MySQL con mysqldump

Primero creamos una BD en el server2 para restarurarla posteriormente con el archivo de la BD que vamos a importar desde el server1. A continuación nos vamos al server1, bloqueamos las tablas desde la consola de **mysql** con el comando `FLUSH TABLES WITH READ LOCK;` y volcamos la BD en un archivo `.sql` con el comando `mysqldump -u root -p contactos > /root/contactosdb.sql`. Una vez hecho esto, desbloqueamos las tablas desde la consola de **mysql** con el comando `UNLOCK TABLES;`. A continuación nos vamos al server2 e importamos el archivo `contactosdb.sql` mediante **ssh** con el comando `scp root@server1.local:/root/contactosdb.sql /root`.Y por último, restauramos la BD con el comando `mysql -u root -p contactos < /root/contactosdb.sql` y comprobámos los datos.

- [Creando la base de datos](http://s1380.photobucket.com/user/adnan1989/media/crear BD server2_zpsauhzdkqj.png.html)
- [Bloqueando tablas y volcando la base de datos](http://s1380.photobucket.com/user/adnan1989/media/dump BD_zpsb6d7tx7n.png.html)
- [Desbloqueando tablas](http://s1380.photobucket.com/user/adnan1989/media/unlock BD_zpsyzcn53tl.png.html)
- [Importando la base de datos y restaurándola](http://s1380.photobucket.com/user/adnan1989/media/restaurar BD server2_zpsh7kb6632.png.html)
- [Comprobando la base de datos restaurada](http://s1380.photobucket.com/user/adnan1989/media/acceso BD server2_zpstcobsg5n.png.html)


## 3. Configuración maestro-esclavo para la replicacíón de la base de datos

Primero editamos los archivos `my.cnf` de ambos servidores, comentando la línea `bind-address 127.0.0.1`, asignándole un `server-id` (1 en caso del maestro y 2 en el del esclavo), un `log-error` y un `log-bin`. A continuación se crea el usuario **esclavo** en el server1 y se reinicia el servicio para más tarde comprobar el estado con el comando `SHOW MASTER STATUS;`, mientras que en el server2 se indica los datos del maestro y se inicializa con el comando `START SLAVE;`. Comprobamos su estado con el comando `SHOW SLAVE STATUS;`, y nos fijamos que el parámetro `Seconds_Behind_Master` no esté a null (en mi caso está a 0 por lo tanto funciona correctamente). Una vez hecho esto, lo único que nos queda es insertar nuevos datos en el maestro y comprobar que se ha modificado la BD en el esclavo, previo desbloqueo de las tablas con el comamando `UNLOCK TABLES:`.

- [Configurando maestro](http://s1380.photobucket.com/user/adnan1989/media/conifg maestro_zpsfgbwu2dd.png.html)
- [Configurando esclavo](http://s1380.photobucket.com/user/adnan1989/media/config esclavo_zpsxv6boigs.png.html)
- [Creando usuario "esclavo"](http://s1380.photobucket.com/user/adnan1989/media/repli config maestro_zpswalwsl7y.png.html)
- [Indicando datos del maestro](http://s1380.photobucket.com/user/adnan1989/media/repli config esclavo_zpsxnuj46ky.png.html)
- [Estado del esclavo](http://s1380.photobucket.com/user/adnan1989/media/estado esclavo_zpscih0hxoa.png.html)
- [Insertando nuevos datos en el maestro](http://s1380.photobucket.com/user/adnan1989/media/modificar BD_zpsj1ovxu9c.png.html)
- [Comprobando la insercción de datos en el esclavo](http://s1380.photobucket.com/user/adnan1989/media/comprobar modificacion BD server2_zpsroygtxgb.png.html)

**Nota:** Aunque no aprezca en las capturas de pantalla de los archivos `my.cnf`, la línea `bind-address` está comentada tal que así: `#bind-address 127.0.0.1`

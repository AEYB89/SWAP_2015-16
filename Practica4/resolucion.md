# Práctica 4

## 1. Midiendo el rendimiento con ab

Trás crear un documento de prueba en los dos servidores llamado `prueba.html` pasamos a hacer peticiones a un servidor,
al balanceador con **nginx** y al balanceador con **haproxy**. Para ello ejecutamos los siguientes comandos:

- `ab -n 10000 -c 100 http://192.168.1.148/prueba.html` para el servidor
- `ab -n 10000 -c 100 http://192.168.1.42/prueba.html`para el balanceador

Con el parámetro **-n** indicamos la carga, y con **-c** la concurrencia.

Hacemos diez pruebas y nos quedamos con los siguientes datos:

|	 |**servidor**|**servidor**|**servidor**|**nginx**|**nginx**|**nginx**|**haproxy**|**haproxy**|**haproxy**|
	 |:----------:|:----------:|:----------:|:-------:|:-------:|:-------:|:---------:|:---------:|:---------:|
	 |T. N. P. P. |S. F.       |S. P. S.    |T.N.P.P. |S. F.    |S. P. S. |T. N. P. P.|S. F.      |S. P. S.   |
|Prueba 1|1,391       |0           |7910,58     |5,291    |0        |1688,83  |2,963	  |0	      |3374,97	  |
|Prueba 2|1,637	      |0	   |6108,21	|5,889    |0	    |1697,97  |2,862	  |0	      |3494,10	  |
|Prueba 3|1,505	      |0	   |6645,88	|5,346	  |0	    |1870,48  |3,450	  |0	      |2801,07	  |
|Prueba 4|1,355	      |0	   |7377,45	|5,425	  |0	    |1843,35  |2,767	  |0	      |3614,62	  |
|Prueba 5|1,429	      |0	   |6996,52	|5,551	  |0	    |1801,62  |2,774	  |0	      |3604,97	  |
|Prueba 6|1,392	      |0	   |7181,82	|5,870	  |0	    |1703,50  |2,729	  |0	      |3664,23	  |
|Prueba 7|1,444	      |0	   |6926,10	|5,929	  |0	    |1660,55  |2,698	  |0	      |3706,64	  |
|Prueba 8|1,521	      |0	   |6574,10	|5,993    |0	    |1668,52  |2,913	  |0	      |3432,47	  |
|Prueba 9|1,325	      |0	   |7547,22	|6,151	  |0	    |1625,76  |2,715	  |0	      |3682,92	  |
|Prueba 10|1,07	      |0	   |9291,91	|5,891	  |0	    |1718,55  |2,692	  |0	      |3715,24 	  |
|	  |	      |		   |		|	  |	    |	      |		  |	      |		  |
|Media	  |1,4075     |0	   |7255,979	|5,7894   |0	    |1727,913 |2,8683	  |0	      |3509,123	  |
|D. T.	  |0,14	      |0	   |837,215	|0,247	  |0	    |77,905   |0,250	  |0	      |261,058	  |

**T.N.P.P.** : Tiempo necesario para la prueba (segundos).
**S.F.** : Solicitudes fallidas.
**S.P.S.** : Solicitudes por segundo.
**D.T.** : Desviación típica.


Apartir de la tabla anterior obtenemos las siguientes gráficas:

- [Media: Tiempo necesario para la prueba](http://s1380.photobucket.com/user/adnan1989/media/ab%20-%20media%20tnpp_zps8b0ro9d0.jpg.html)
- [Desviación típica: Tiempo necesario para la prueba](http://s1380.photobucket.com/user/adnan1989/media/ab - DT tnpp_zpsk64w0w1g.jpg.html)
- [Media: Solicitudes por segundo](http://s1380.photobucket.com/user/adnan1989/media/ab - media pps_zps5oxcy6ht.jpg.html)
- [Desviación típica: Solicitudes por segundo](http://s1380.photobucket.com/user/adnan1989/media/ab - DT pps_zpsbqfg2zyr.jpg.html)



## 2. Midiendo el rendimiento con siege

Para ello, hacemos lo mismo que con **ab**: Probamos un servidor, el balenceador con **nginx** y el balanceador con **haproxy**. Ejecutamos los siguientes comandos:

- `siege -b -t60S -c 20 -v http://192.168.1.148/prueba.html` para el servidor
- `siege -b -t60S -c 20 -v http://192.168.1.42/prueba.html`para el balanceador

Con el parámetro **-b** indicamos que haga una prueba de benchmarking, con **-t** indicamos el tiempo de la prueba, con **-c** indicamos la concurrencia y con **-v** indicamos que nos muestre las pruebas por pantalla.


Hacemos diez pruebas y nos quedamos con los siguientes datos:

|  |**server**|**server**|**server**|**server**|**nginx**|**nginx**|**nginx**|**nginx**|**haproxy**|**haproxy**|**haproxy**|**haproxy**|
   |:--------:|:--------:|:--------:|:--------:|:-------:|:-------:|:-------:|:-------:|:---------:|:---------:|:---------:|:---------:|
   |D.	      |T. E.	 |T. R.	    |S. P. S.  |D.	 |T. E.	   |T. R.    |S. P. S. |D.	   |T. E.      |T. R.	   |S. P. S.   |
|P1|100%      |59,90	 |0,01	    |3512,50   |100%	 |59,77	   |0,01     |1791,82  |100%	   |59,66      |0,01	   |2594,55    |
|P2|100%      |59,10	 |0,01	    |3520,86   |100%	 |59,99	   |0,01     |1717,02  |100%	   |59,13      |0,01	   |2744,75    |
|P3|100%      |59,82	 |0,01	    |3699,78   |100%	 |59,47	   |0,01     |1684,65  |100%	   |59,27      |0,01	   |2730,13    |
|P4|100%      |59,95	 |0	    |4056,80   |100%	 |59,40	   |0,01     |1794,48  |100%	   |59,95      |0,01	   |2751,09    |
|P5|100%      |59	 |0	    |4126,90   |100%	 |59,49	   |0,01     |1765,54  |100%	   |59,97      |0,01	   |2761,11    |
|P6|100%      |59	 |0	    |4098,21   |100%	 |59,91	   |0,01     |1735,44  |100%	   |59,79      |0,01	   |2565,43    |
|P7|100%      |59,27	 |0	    |4111,44   |100%	 |59,60	   |0,01     |1704,21  |100%	   |59,79      |0,01	   |2642,10    |
|P8|100%      |59,40	 |0	    |4078,30   |100%	 |59,62	   |0,01     |1806,42  |100%	   |59,93      |0,01	   |2646,15    |
|P9|100%      |59,32	 |0	    |4107,89   |100%	 |59,65	   |0,01     |1735,26  |100%	   |59,71      |0,01	   |2590,25    |
|P10|100%     |59,35	 |0	    |4129,49   |100%	 |59,69	   |0,01     |1743,34  |100%	   |59,45      |0,01	   |2768,92    |
|   |	      |          |	    | 	       |	 |	   |	     |	       |	   |	       |	   |	       |
|Media|100    |59,411	 |0,003	    |3944,217  |100	 |59,659   |0,01     |1747,818 |100	   |59,665     |0,01	   |2679,448   |
|DT   |0      |0,341	 |0,0045    |245,393   |0	 |0,179	   |0	     |38,772   |0	   |0,276      |0	   |75,701     |

**D.** : Disponibilidad.
**T.E.** : Tiempo de ejecución (segundos).
**T.R.** : Tiempo de respuesta (segundos).
**S.P.S.** : Solicitudes por segundo.
**D.T.** : Desviación típica.


Apartir de la tabla anterior obtenemos las siguientes gráficas:

- [Media: Disponibilidad](http://s1380.photobucket.com/user/adnan1989/media/siege%20-%20media%20dispo_zpsbrnordrd.jpg.html)
- [Media: Tiempo de ejecución](s1380.photobucket.com/user/adnan1989/media/siege - media TE_zpsrjh1wmnu.jpg.html)
- [Desviación típica: Tiempo de ejecución](http://s1380.photobucket.com/user/adnan1989/media/seige%20-%20DT%20TE_zpslpib9xqn.jpg.html)
- [Media: Tiempo de respuesta](http://s1380.photobucket.com/user/adnan1989/media/siege%20-%20media%20TR_zpsfug9asex.jpg.html)
- [Desviación típica: Tiempo de respuesta](http://s1380.photobucket.com/user/adnan1989/media/siege%20-%20DT%20TR_zpsip3y54i9.jpg.html)
- [Media: Solicitudes por segundos](http://s1380.photobucket.com/user/adnan1989/media/siege%20-%20media%20pps_zpsi2kxx35c.jpg.html)
- [Desviación típica: Solicitudes por segundo](http://s1380.photobucket.com/user/adnan1989/media/siege%20-%20DT%20pps_zpssk2jl9f1.jpg.html)

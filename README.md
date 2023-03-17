# Docker-odoo

¿Que ocurre si en el ordenador local el puerto 5432 está ocupado? ¿Como lo puedes solucionar?
***
Lo que podemos hacer es dirigirnos al archivo de configuración de postgresql llamado "postgresql.conf" y modificar ahí el puerto si está ocupado.

Docker Compose es una herramienta para definir y ejecutar aplicaciones de Docker de varios contenedores. En Compose, se usa un archivo YAML para configurar los servicios de la aplicación. Después, con un solo comando, se crean y se inician todos los servicios de la configuración.

## Docker compose ##

![](https://github.com/davidbrodrigues/Docker-odoo/blob/f6e8df1b32e0ea895f23983c31b92c54eaaa4a9a/Capturas/uno.png)

En la consola del ide ponemos el comando docker-compose up -d y se inician los servicios.

# Breve explicacion de los pasos -> 

Para comenzar, especificamos la versión del documento.

```
version: '3'
```

Luego lo separaremos en dos partes, es decir los dos servicios que utilizaremos.
El servicio de odoo y el servicio de postgresql pra la base de datos.
En mi caso los llamo web y db:

```
services:
  web:
    ...
  db:
    ...
```

Para comenzar especifico en ambos casos la versión de la imagen, en mi caso la más reciente.

```
image: odoo:latest
...
image: postgres:latest

```

En el paratado de puertos mapeo los puertos de ambos servicios.

```
Para odoo->
    ports:
      - "8069:8069"
Para sql->
    ports:
      - "5432:5432"
```

El apartado volumes, es para mapear las carpetas de configuración de ambos servicios localmente
para en un futuro poder hacer modificaciones y saber donde se situan.

```
Para odoo->
    volumes:
      - /home/dam2a/Escritorio/odoo/srv/odoo:/var/lib/odoo
      - /home/dam2a/Escritorio/odoo/srv/odoo/config:/etc/odoo
Para sql->
    volumes:
      - /home/dam2a/Escritorio/odoo/sql:/var/lib/postgresql/data
```

Y por último para el apartado de envroment en sql, pondremos los datos de acceso a la misma y su nombre.

```
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
```

***

Una vez iniciados los servicios, ejecutamos Pycharm para manejar la sql. Abrimos el directorio de isntalación donde se mapearon las carpetas y se vería así.
![](https://github.com/davidbrodrigues/Docker-odoo/blob/f6e8df1b32e0ea895f23983c31b92c54eaaa4a9a/Capturas/dos.png)
***

Para conectarnos a la base de datos, procedemos a darle click a un boton situado en la parte sueprior derecha con un icono de una especie de BD.
Una vez abierto le damos a añadir sql y seleccionamos postgresql y se nos abrirá la siguiente ventana:

![](https://github.com/davidbrodrigues/Docker-odoo/blob/f6e8df1b32e0ea895f23983c31b92c54eaaa4a9a/Capturas/tres.png)

Dentro de esta ventana rellenamos todos los datos necesarios para la instalación y le damos a conectar.
***


Una vez conectados podemos abrir las tablas y ver su estructura e información.

![](https://github.com/davidbrodrigues/Docker-odoo/blob/f6e8df1b32e0ea895f23983c31b92c54eaaa4a9a/Capturas/cuatro.png)



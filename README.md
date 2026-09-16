# Manual de instalación de la aplicación web

## Decisiones de proyecto

|Elemento|Decisión|Versión|Justificación|
|--------|-------|--------|-------------|
|Servidor Web|Apache|2|Sencillo de usar, popular|
|Base de datos|MySQL|8|Experiencia previa, popular|
|Lenguaje servidor|Python|3|Muy interesante para ASIR, uso extendido|
|Framework|Flask|3|Sencillo de usar, pensado específicamente para web (formularios, sesiones)|
|Control de versiones|Git|2|Muy extendido|
|Documentación|Markdown|-|Muy utilizado con github|

## ¿Qué hace un servidor web?

Recibe peticiones HTTP y devuelve recursos al navegador

## Proceso de instalación / puesta en marcha

1. Actualizar el sistema
```
sudo apt update
sudo apt upgrade
```
2. Instalar git
```
sudo apt install git
```
3. Instalar VS Code + Plugins:
    - Markdown all in one

4. Instalar Apache2
`sudo apt install apache2`
5. Cambiar permisos carpeta /var/www/html
```
sudo chown -R $user:$user /var/www/html
sudo chmod -R u=rwx,go=rx /var/www/html
```
6. Crear un archivo index html en la carpeta /var/www/incidencias.teis con la página principal de incidencias.
   
7. Hacer visible la página con el nombre incidencias.teis en la configuración de apache.

![apache-configuracion](/home/alumno/Incidencias-AlbertoL/Images/apache-configuracion.png)

8. Desactivar el sitio configurado por defecto en apache
`sudo a2dissite 000-default.conf`

9. Activar el sitio de incidencias.teis 
``
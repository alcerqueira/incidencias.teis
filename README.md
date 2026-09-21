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
```bash
sudo apt update
sudo apt upgrade
```
2. Instalar git
```
sudo apt install git
```
3. Instalar VS Code + Plugins:
    - Markdown all in one
    - Python

4. Instalar Apache2
`sudo apt install apache2`
5. Cambiar permisos carpeta /var/www/html
```bash
sudo chown -R $user:$user /var/www/html
sudo chmod -R u=rwx,go=rx /var/www/html
```
6. Configuración apache

   -  Crear un archivo index html en la carpeta /var/www/incidencias.teis con la página principal de incidencias.
   
   - Hacer visible la página con el nombre incidencias.teis en la configuración de apache.

![apache-configuracion](Images/apache-configuracion.png)

   - Desactivar el sitio configurado por defecto en apache
```bash
sudo a2dissite 000-default.conf
```

   - Activar el sitio de incidencias.teis 
```bash
sudo a2ensite incidencias.teis.conf
```

7. Instalar mysql server

```bash
sudo apt install mysql-server
```

8. Configuración mysql
```sql
-- crear la base de datos incidencias
create database incidencias;

-- crear el usuario incidencias
create user 'incidencias'@'localhost' identified by 'incidencias';

-- darle todos los permisos al usuario incidencias para toda la base de datos incidencias
grant all privileges on incidencias.* to 'incidencias'@'localhost';

-- crear la tabla de los registros de las incidencias
create table registro( id int auto_increment primary key, aula varchar(30), usuario varchar(20), descripcion text, estado varchar(30) );

-- crear registros de prueba
insert into registro (aula, usuario, descripcion, estado) values ('Taller 1', 'alcerqueira', 'PC 24 no arranca', 'ABIERTA'),('Taller 1', 'alcerqueira', 'Proyector no se ve nitido', 'ABIERTA');
```

9. Instalar Python y componentes relacionados.
```bash
sudo apt install python3 python3-pip python3-venv -y
```

10. Crear entorno virtual.
```bash
python3 -m venv venv
source venv/bin/activate
```

11. Instalar Flask y mysql-connector para poder conectar el mysql con python.
```bash
pip install flask
pip install mysql-connector-python
pip list
pip freeze > requirements.txt
```

## Rutina de trabajo con flask (venv)

Al empezar:
```bash
cd /home/alumno/Incidencias-AlbertoL
source venv/bin/activate
python app.py #Lanzar app
```

Al terminar:
```bash
deactivate
```
## Aplicación Python/Flask

1. Aplicación inicial (app.py)
```python
  from flask import Flask

app = Flask(__name__)

@app.route('/')
def inicio():
    return "<h1>Incidencias IES Teis</h1>"
if __name__ == "__main__":
    app.run(debug=True)
```

2. Ejecutar aplicación.

`python3 app.py`

3. Comprobar abriendo http://incidencias.teis:5000

## Migración del formulario a Python/Flask

1. Crear carpeta templates y mover el archivo index.html

2. Modificar app.py:
```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def inicio():
    return render_template("index.html")
if __name__ == "__main__":
    app.run(debug=True)
```

3. Comprobar abriendo http://incidencias.teis:5000

## Recibir los datos del formulario

1. Importar request.

2. Añadir ruta en app.py para recibir los datos del formulario:
```python
@app.route("/incidencia", methods=["POST"])
def crear_incidencia():
    aula = request.form["aula"]
    usuario = request.form["usuario"]
    descripcion = request.form["descripcion"]

    print("Aula:" + aula)
    print("Usuario:" + usuario)
    print("Descripcion:" + descripcion)

    return "Incidencia recibida"
```

## Configuración de git/github

1. Crear repositorio local, añadir archivos y commit
```bash
git init
git add .
git commit -m "comentario"
```

2. Crear cuenta github, crear repositorio en github.

3. Conectar repositorio local con remoto
```bash
git remote add origin url-repositorio
git branch -M main
git push -u origin main
```

4. Clonar repositorio en otro sistema/directorio.

`git clone url-repositorio`

5. Actualizar repositorio subido en github.

`git pull`
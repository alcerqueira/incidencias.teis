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
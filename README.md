# cursoNPM

![alt text](https://static.platzi.com/media/user_upload/JS%20%E2%80%93%2031-dd8defe4-29bf-4bb9-8260-07fb80d965bc-81e296f1-6370-44e0-8e6d-fe1946826aba.jpg)
![alt text](https://static.platzi.com/media/user_upload/npm-9cda5bab-e878-4672-b1a7-101a355f255d.jpg)

## INICIAR UN PROYECTO NPM

Primero abrimos nuestra terminal y nos posicionamos donde guardamos nuestros archivos.
Podemos crear una carpeta para nuestro proyecto con el comando
mkdir project_name nos movemos dentro de la carpeta con cd project_name ya dentro de la carpeta podemos iniciar:

Primeros pasos
git init: Para tener el control de cambios y versiones en nuestro proyecto
npm init: con este comando vamos a crear nuestro archivo de configuración del proyecto, el package.json
Luego nos saldrá lo siguiente
package name: el nombre de nuestro proyecto, generalmente es el nombre de la carpeta
version: version con la que iniciaremos el proyecto, generalmente aparece 1.0.0
description: descripcion breve del proyecto
entry point: punto de acceso a nuestro proyecto
test command: comando para gestionar los test
git repository: repositorio de github u otro servicio
keywords: palabras claves del proyecto
author**: nombre del autor y < correo > **license`: licencia que tendrá el proyecto
```html
<h3>2da opción (para hacer package rápido)</h3>
Escribimos npm init -y y esto generará un package.json vacio para que lo configuremos más adelante.

<h3>3ra opción (configuramos algunos elementos)</h3>
```
Escribimos en nuestra terminal
npm set init.author.email "your@email"
npm set init.author.name "your name"
npm set init.license "license name"
npm init -y
Y se creará un package.json con los datos que seleccionamos.

## Instalación de dependencias

npm install moment --save-dev 
asi instalamos la dependencia moment, save es para guardar en produccion, es improtante saber cuando va para producción o para cuando no
dev indica que solo es necesario en el entorno de desarrollo.
Es importante no mandar dependencias a producción y omitir algunas que deban de estar

npm i date-fns -D
Es lo mismo, instalamos una dependencia y que será para desarrollo

npm i moment -S
Lo guardamos como parte del proyecto

A veces necesitaremos un paquete que corra de manera global

Por ejm moment ser usado dentro del contexto del proyecto pero no en otros si no esta instalado

Usamos nodemon
Generamos un demonio que va a escuchar cmabios y va a dejar mantener un proceso de node

Y aquí no te dejará hacer npm install -g nodemon por permisos 

Evita tener que hacer sudo cuando hagas un
npm i -g

Con estos tips del equipo de NPM 👉
https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally

Como queremos evitar el sudo, haremos: 
npm config set prefix "/usr/local"
sudo chown -R $USER /usr/local

luego instalaremos nodemon
npm install nodemon -g

chequeamos los paquetes instalados con 
npm list -g --depth 0

instalaremos eslint
npm install eslint -O 

la O es de opcional
Pero te pedirá financiamiento
"14 packages are looking for funding"

con npm fund veremos los recursos

### tip
No es recomendable realizar el comando “sudo npm install -g nodemon” al instalar un paquete pues comprometemos la seguridad de nuestro sistema. Para eso podemos realizar estos dos comandos:

npm config set prefix "/usr/local"
sudo chown -R $USER /usr/local

El primer comando le dice a npm que no utilize “/usr/lib/node_modules/” sino que redireccione las instalaciones a la carpeta “/usr/local”. El segundo comando añade al usuario actual como dueño de la carpeta “usr/local” para que así tengas control total sobre los archivos. Con eso hemos solucionado el problema de las instalaciones globales de npm.

Existen otras formas de solucionarlo como por ejemplo ejecutar la instalación como root o añadir el parámetro --no-bin-links al comando npm, pero no son seguros estos métodos.

fuentes:
http://stackoverflow.com/questions/13527889/global-installation-of-grunt-js-fails
http://howtonode.org/introduction-to-npm

## Instalación de dependencias con force

Esta dependencia no va a ser instalada en el proyecto pero si queremos ver el output que genera, osea simular que se instala

npm install react(paqueteNombre) --dry-run

Pero en las dependencias no lo encontramos a react

El force nos permitirá instalar un paquete forzando la instalacion desde el ultimo recurso del servidor de npm

npm install webpack(nombrePaquete) -f

### Tips:
Un error que cometemos al clonar un proyecto de un repositorio remoto, es querer iniciar la aplicación de forma local inmediatamente después de descargar el código. Seguramente, nada funcionará, debido a que no existe la carpeta node_modules que contiene las dependencias requeridas.

Como regla, siempre ejecuten npm install después de clonar el proyecto.


El paquete json-server es fantástico, se pueden hacer peticiones HTTP a un archivo json, yo lo uso con Ngrok y hago peticiones externas.

> Puede una dependencia estar en producciony dev?? 

Ejecuta npm install una vez modifiques el package manualmente para instalar todo

npm install json-server@0.15.0 
te traes el paqute y la version especifica

## Actualizar y eliminar paquetes

npm list mostrara el arbol de jerarquia de los paquetes instalados

Y como actualizar ese paquete a la ultima version??

npm outdate para ver que paquetes puedan estar desactualizados

npm outdate --d vemos todo el output

npm update actualiza los paquetes a esa ultima versión

npm install json-server@latest
instalamos la ultima version de json server

Para desinstalar paquetes, aunque eliminemos el paquete manualmente en package.json, este seguirá en node_modules por lo que no es la mejor práctica

Lo haremos con:
npm uninstall packageName

Por ejm desisntalaremos json server

npm uninstall json-server

Y para desinstalar un paquete sin eliminar del package json

npm uninstall webpack --no-save
por ejemplo con webpack estaría en el node modules pero si en el package json

Con la extension npm de vscode, si un paquete no instalado correctamente te avisará en el package json


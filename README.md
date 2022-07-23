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
author**: nombre del autor y < correo >**license`: licencia que tendrá el proyecto

```html
<h3>2da opción (para hacer package rápido)</h3>
Escribimos npm init -y y esto generará un package.json vacio para que lo
configuremos más adelante.

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
<https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally>

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
<http://stackoverflow.com/questions/13527889/global-installation-of-grunt-js-fails>
<http://howtonode.org/introduction-to-npm>

## Instalación de dependencias con force

Esta dependencia no va a ser instalada en el proyecto pero si queremos ver el output que genera, osea simular que se instala

npm install react(paqueteNombre) --dry-run

Pero en las dependencias no lo encontramos a react

El force nos permitirá instalar un paquete forzando la instalacion desde el ultimo recurso del servidor de npm

npm install webpack(nombrePaquete) -f

### Tips

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

## Package lock y el uso los símbolos ^ y ~

![alt text](https://static.platzi.com/media/user_upload/wheelbarrel-no-tilde-caret-white-bg-w1000-72ca1a72-4c7f-4abe-8482-425c01a72f89.jpg)

package log te ayuda a ver que paquetes se han instalado y que versiones andan ahí

Cambio mayor > Cambios menores (cambian ciertas funcionalidades pero no son tan grandes para ser una version nueva) > Parches (pequeñas modificaciones)

Al eliminar el ^ nos aseguramos que se quede en la version especificada

Además de esos símbolos, también tenemos:

< : Versión menor a la indicada.
<= : Versión menor o igual a la indicada.

> : Versión mayor a la indicada.
> = : Versión mayor o igual a la indicada.
> Los cuales se utilizan así:

```js
"dependencies": {
    "json-server": ">0.15.1",
    "moment": ">=2.26.0",
    "date-fns": "<2.14.0",
     "react": "<=16.12.0"
}
```

^ = Si mantenemos el caret dentro de la configuración de nuestro package estamos garantizando que cuando realicemos una actualización o tengamos un cambio que podamos realizar, vamos a hacer actualización de los cambios menores y de los parches o bug fixes.
Para quedarnos en una sola versión eliminamos el caret.

~ = Establece que vamos a recibir actualizaciones o cambios solamente de los cambios que son parches o bug fixes.

## Ejecutar tareas

Los scripts son comandos que se establecen para poder usarlos desde la consola

A mi me gusta crear tres scripts.

"dev": "webpack-dev-server --mode development",
"build": "webpack --mode production",
"start": "serve ./dist -s -l 8080"
dev: Modo desarrollo.
build: Compila todo y me crea un directorio dist.
start: Toma el directorio dist y lanzo un servidor en modo producción.

Haciendo comandos:
"hola": "node",
"deploy": "npm run format && npm run build"

corremos los cripts con npm run nombreDelScript

### Crear un comando en tu proyecto

Para crear un comando en tu proyecto sigue la siguiente estructura, donde <nombre> es el nombre del comando que debería ser muy descriptivo y <comando> es el comando que utilizarías en la terminal:

{
"scripts": {
"<nombre>": "<comando>"
}
}
Una vez hayas escrito el comando en el archivo package.json, la manera de ejecutarlo será con el comando npm run.

Por ejemplo, creemos tres comandos para iniciar el proyecto (start), crear un archivo para producción (build) y combinarlos (deploy). Que no te preocupe si no entiendes cada comando, solo entiende cómo ejecuta NPM el script.

{
"scripts": {
"start": "webpack-dev-server --open --mode development",
"build": "webpack --mode production",
"deploy": "npm run format && npm run build"
}
}

Y para ejecutarlos, es necesario utilizar el comando pertinente en la terminal:
```
$ npm run start
$ npm run build
$ npm run deploy
Contribución creada con aportes de: Andrés Guano
```
Sales del area con .exit

## Solucion de problemas en proyectos con NPM

Para poder activar la opción de verbose (es decir que nos muestre mayor información de lo que esta haciendo el comando)

```js
npm run [comando] --dd
```

En caso de que nuestros archivos de node_module no estén bien instalados o tengamos una versión anterior lo que podemos hacer es lo siguiente:

npm cache clear --force

Para verificar que verdaderamente se borro podemos usar

npm cache verify

Uno de los errores que podemos tener es tener algún valor corrupto en node_module, o tambien que la instalación no este completa de los paquetes que hemos instalado, para ello podemos eliminar el paquete con el siguiente comando:
rm -rf node_modules  #este comando eliminar la carpeta 
Otra alternativa para eliminar de forma segura una carpeta es instalando el siguiente paquete:
sudo npm install -g rimraf
Ahora podemos ejecutar el siguiente comando para eliminar node_module
rimraf node_modules 

Ahora podemos volver a instalar nuestro paquetes

npm install

Documentación de rimraf:
https://www.npmjs.com/package/rimraf

sudo npm install -g rimraf

## Gestionar la seguridad en proyectos con NPM

npm audit para ver las vulnerabilidades que tenemos en nuestro proyecto

npm audit --json nos genera un json con información un poco mas detallada de lo que esta pasando con estos paquetes que instalamos una ves sepamos cual es la vulnerabilidad podemos proceder a actualizar cualquiera de los paquetes ejem:

npm update eslint-utils --depth 2 esto para instalar todas sus dependencias

npm audit fix es para solucionar las vulnerabilidades que tengamos en nuestro proyecto básicamente, actualiza a la ultima version nuestros paquetes con las dependencias que requieren, después de esto volvemos a correr npm audit para ver que ya no tenemos vulnerabilidades.

también hay una herramienta que garantiza que estemos siempre actualizados con nuestras dependencias del proyecto y es snyk.io

Para **Generar un Archivo de Texto** con la auditoria generada por formato en JSON, ejecutar el comando

npm audit --json  > auditoria.txt

Para paquetes globales npm audit no funciona.
Investigando conseguí la siguiente solución

npm install -g npm-check-updates

Que lo que hace es actualizar las dependencias globales, verificando que estén en su última versión, y manejando las vulnerabilidades

## Crear un paquete para NPM

Ejecutar el comando para saber donde estoy ubicado
```js
pwd
mkdir random-messages
cd random-messages/
git init
npm init
```
Se crea el archivo index.js en la carpeta src
```js
// Se declara el arreglo
const messages = [
    "David",
    "Diana",
    "Ana Maria",
    "Isabela",
    "Antonio",
    "Norma"
]

//Crear función para enviar aleatoriamente  los nombres del arreglo
const randomMsg = () => {
    const message = messages[Math.floor(Math.random()*messages.length)]
    console.log(message)
}

// Exportar como un módulo

module.exports = { randomMsg }
```

Se debe crear una carpeta bin donde se crea ele archivo global.js (Configuración que se necesita

```js
#!/usr/bin/env node
// se va ejecutar dentro de bash

//Variable que llama la funcion que exportamos
let random = require('../src/index.js')

//Ejecuto la funcion
random.randomMsg()
//Modifico el package.json y coloco la configuración de bin que necesito

  "bin": {
    "random-msg": "./bin/global.js"
  },
  "preferGlobal": true
```

#!/usr/bin/env node es una instancia de una línea shebang : la primera línea en un archivo de texto plano ejecutable en plataformas similares a Unix que le dice al sistema a qué intérprete debe pasar ese archivo para su ejecución , a través del comando línea siguiendo la magia #! prefijo (llamado shebang ).

Nota: Windows no admite líneas shebang , por lo que efectivamente se ignoran allí; en Windows es solo la extensión del nombre de archivo de un archivo dado que determina qué ejecutable lo interpretará. Sin embargo, todavía los necesita en el contexto de npm

## Publicar un paquete en NPM

Primero se debe probar de forma local.

pwd
sudo npm link
#Se ejecuta la función
random-msg
Otra forma de instalar el paquete

sudo npm install -g ~/Estudio/GestionDeDependenciasYPaquetesConNPM/random-messages/
Crear cuenta para poder subir el paquete - Npm.js https://www.npmjs.com/
Verificar la cuenta que llega al correo electrónico registrado.

Se loguea a la cuenta creada por consola y se publica el paquete

npm adduser

npm publish
Gracias @facmartoni

Solución al error “403 Forbidden - PUT http://registry.npmjs.org/random-messages - You do not have permission to publish “random-messages”. Are you logged in as the correct user?”

En el archivo package.json cambiar el atributo name a un nombre original, puesto que el profe ya subió su repositorio con el nombre de random-messages, por lo que no podemos tener nosotros un proyecto del mismo nombre en NPM 😉.

Yo coloque random-messages-dbz y funciono.

Eliminar paquetes publicados
1 . Si quieres eliminar el paquete o versión publicada para los paquetes recién creados, siempre que ningún otro paquete en el Registro público de npm dependa de su paquete, puede anular la publicación en cualquier momento dentro de las primeras 72 horas después de la publicación, a menos que usted sea el único propietario del módulo con:

npm unpublish <package_name> --force
y si se quiere anular la publicación de una versión en específico:

npm unpublish <package_name>@<version>
2 . Para paquetes que tienen publicados más de 72 horas, independientemente de cuánto tiempo hace que se publicó un paquete, puede anular la publicación de un paquete que cumpla con lo siguiente:

ningún otro paquete en el Registro Público de npm depende de otro
tuvo menos de 300 descargas durante la última semana
tiene un solo propietario / mantenedor
npm tiene detalles de la política para anular la publicación de paquetes, más detalles aquí: npm Unpublish Policy 😉

## Paquetes privados

Para usar paquetes privados, debes:

Estar usando una versión igual o superior a la 2.7.0 de NPM
Tener una cuenta de usuario u organización de pago
En un paquete privado de NPM, solo pueden participar el propietario y los colaboradores autorizados. De esta manera, puedes seguir construyendo el paquete con una combinación de código privado y dependencias públicas.

Actualizar tus paquetes con buenas prácticas
Tu paquete debe contener toda la información posible para que el usuario puede instalarlo, utilizarlo y hasta colaborar para solucionar posibles bugs. Por ende, es necesario que tengas configurado, por lo menos, un archivo README.md y un repositorio remoto (GitHub, GitLab, etc.).

Una vez tengas estos requisitos, puedes actualizar tu paquete a una nueva versión, luego publicalo nuevamente.

Crear un archivo README.md para tu paquete
Para crear un archivo README.md puedes utilizar esta estructura base y adecuarla a tu proyecto. Puedes mirar el código haciendo clic en el botón “Raw”.

Crear un archivo repositorio remoto para tu paquete
Para crear un repositorio remoto, utiliza el comando pertinente para conectar tu repositorio local de Git con un servicio en la nube, usualmente se utiliza GitHub. Por ejemplo:

$ git remote add origin <https://...>
Si no conoces este comando, te recomiendo seguir con el Curso Profesional de Git y GitHub, en el que aprenderás el software de control de versiones de tu código más importante en tu carrera como desarrollador.

Después, debes actualizar tu archivo de package.json con la información de tu repositorio remoto. Puedes hacerlo manualmente modificando el archivo, o emplear el comando npm init que no cambiará tu configuración, solamente la actualizará con la nueva información que ingreses.

Debería agregar las propiedades "repository", "bugs" y "homepage" con los enlaces pertinentes del repositorio remoto, en el archivo de configuración de la siguiente manera:

//package.json
{
    ... ,
    "repository": {
        "type": "git",
        "url": "http://github/.../random-msg.git"
    },
    "bugs": {
        "url": "http://github/.../random-msg/issues"
    },
    "homepage": {
        "url": "http://github/.../random-msg#readme"
    }
}

Para poder enviar el comando:

npm version patch/minor/major
Deben primero dejar limpio el working directory de git, es decir deben hacer un commit de los cambios que se realizaron o revertir cambios.

Este error puede ocurrir cuando se añade en el package.json el repositorio de git, como se modifica el archivo es necesario hacerle commit antes de enviar el version patch

Paquete de mensajes de personas celebres: https://www.npmjs.com/package/cosmos-messages


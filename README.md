  <h1>Backend con Node.js</h1>
</div>	</div>


<div align="center">
  <img src="./assets/nodejs-logo.svg"
    width="60%"
   alt="nodejs-logo">
</div>

## Tabla de contenido	## Tabla de contenido
- [¿Qué es Node.js y para que sirve?](#qué-es-nodejs-y-para-que-sirve)	
- [Fechas importantes de NodeJS](#fechas-importantes-de-nodejs)
- [Diferencias entre NodeJs y Javascript](#diferencias-entre-nodejs-y-javascript)
- [Instalación de Node.js](#instalación-de-nodejs)
- [Arquitectura orientada a eventos](#arquitectura-orientada-a-eventos)
- [Event Emiter](#event-emiter)
- [Primer Servidor HTTP](#primer-servidor-http)
- [Sreams](#sreams)
- [Readable y Writable Streams](#readable-y-writable-streams)
- [Duplex y Transforms streams](#duplex-y-transforms-streams)
- [Uso de utilidades que tiene NodeJS](#uso-de-utilidades-que-tiene-nodejs)
  - [Utilidades del sistema operativo](#utilidades-del-sistema-operativo)
  - [Utilidades con el sistema de archivos](#utilidades-con-el-sistema-de-archivos)
- [Administrar directorios y archivos](#administrar-directorios-y-archivos)
- [Consola, utilidades y debuggin](#consola-utilidades-y-debuggin)
- [Deprecate](#deprecate)
- [Debuggin en node](#debuggin-en-node)
- [Clusters y procesos hijos](#clusters-y-procesos-hijos)
- [Request y Response Objects](#request-y-response-objects)
  - [Request body](#request-body)
  - [Request params](#request-params)
  - [Request query](#request-query)
  - [Response object](#response-object)
- [Exploremos los métodos más comunes](#exploremos-los-métodos-más-comunes)
  - [Response end()](#response-end)
  - [Response json()](#response-json)
  - [Response send()](#response-send)
- [¿Qué es express y para que sirve?](#qué-es-express-y-para-que-sirve)
  - [Crea tu primer servidor en express](#crea-tu-primer-servidor-en-express)
- [Anatomía de una API Restful](#anatomía-de-una-api-restful)
- [Estructura de una película con Mockaroo](#estructura-de-una-película-con-mockaroo)
- [Implementando un CRUD en express.js](#implementando-un-crud-en-expressjs)
  - [Métodos idempotentes del CRUD](#métodos-idempotentes-del-crud)
- [Implementando una capa de servicios en express](#implementando-una-capa-de-servicios-en-express)
- [Creación de una BD en MongoAtlas](#creación-de-una-bd-en-mongoatlas)
  - [Conexión a MongoAtlas una instancia de MongoDB](#conexión-a-mongoatlas-una-instancia-de-mongodb)
  - [Implementación de las acciones de MongoDB](#implementación-de-las-acciones-de-mongodb)
  - [Conexión de nuestros servicios con MongoDB](#conexión-de-nuestros-servicios-con-mongodb)
- [¿Qué es un middleware?](#qué-es-un-middleware)
- [Manejador de erroes asíncronos y síncronos en Express](#manejador-de-erroes-asíncronos-y-síncronos-en-express)
- [Capa de validación de datos a travéz de un middleware](#capa-de-validación-de-datos-a-travéz-de-un-middleware)
- [¿Qué es Join y Boom?](#qué-es-join-y-boom)
  - [Implementando Boom](#implementando-boom)
  - [Implementando Joi](#implementando-joi)
- [Middlewares populares en Express.js](#middlewares-populares-en-expressjs)
- [Debugging e inspect](#debugging-e-inspect)
  - [Haciendo debugging](#haciendo-debugging)
- [Ejecutando el modo inspect en desarrollo](#ejecutando-el-modo-inspect-en-desarrollo)
- [Tests](#tests)
  - [Creación de test para nuestros endpoints](#creación-de-test-para-nuestros-endpoints)
  - [Creación de Test para nuestros servicios](#creación-de-test-para-nuestros-servicios)
  - [Creación de Test para nuestras utilidades](#creación-de-test-para-nuestras-utilidades)
  - [Agregando un comando coverage](#agregando-un-comando-coverage)
- [Considerenado las mejores prácticas para el despliegue](#considerenado-las-mejores-prácticas-para-el-despliegue)
- [Variables de entorno, CORS y HTTPS](#variables-de-entorno-cors-y-https)
  - [Como usar las variables de entorno para diferentes ambientes](#como-usar-las-variables-de-entorno-para-diferentes-ambientes)
  - [¿Cuando no es posible acceder al servidor remoto?](#cuando-no-es-posible-acceder-al-servidor-remoto)
  - [Variables de entorno de forma nativa](#variables-de-entorno-de-forma-nativa)
  - [Habilitando CORS en producción](#habilitando-cors-en-producción)
  - [Habilitar CORS para todos los request (No recomendado en producción)](#habilitar-cors-para-todos-los-request-no-recomendado-en-producción)
  - [Habilitar CORS para los request específicos de un cliente (Recomendado para producción)](#habilitar-cors-para-los-request-específicos-de-un-cliente-recomendado-para-producción)
- [Cómo funciona y por qué es importante el uso de HTTPS](#cómo-funciona-y-por-qué-es-importante-el-uso-de-https)
  - [Por qué usar HTTPS](#por-qué-usar-https)
  - [Cómo habilitar HTTPS en nuestro servidor](#cómo-habilitar-https-en-nuestro-servidor)
- [Como implementar una capa de manejo de caché en express](#como-implementar-una-capa-de-manejo-de-caché-en-express)
- [¿Cómo contener tu aplicación en Docker?](#cómo-contener-tu-aplicación-en-docker)
- [Despliegue en now](#despliegue-en-now)

## ¿Qué es Node.js y para que sirve?



La definición formal de nodejs es: un entorno de ejecución para javascript construido con el motor v8.

El entorno de ejecucíon: es la capa que corre por el sistema operativo que ejecuta software, básicamente se encarga de como se consume memoria, como acceder a las variables y como corre el garbage collector.

Chrome V8 Es un engine de Javascript por de chromiund-project para chrome y chromium. Además de chrome existen 2 proyectos que son chromium que es la versión open source y luego chrome canary, chrome canary se llamá así por una analogía donde antiguamente los mineros iban a la mina y para detectar si habia gases o algún peligro, ponían a un canario en una pequeña jaula, si había un gas y pasaba algo, el canario lasimosamente moría y es la manera en como se daban cuenta si había algún error, lo mismo pasa con chrome canary, es la manera como detectan errores y si todo sale bien, lo pasan a chrome.

Chrome V8 lo que hace es compilar javascript a código máquina. Recordemos que los lenguajes interpretados se ejecutan muy rápido, pero cuando hay un loop de código muy seguido se demoran, porque cada vez que pasan por esa linea de código tienen que volverla a interpretar a diferencia de los lenguajes compilados que se demoran mucho en cargar, porque tienen que pasar precisamente por ese proceso de compilación, luego se ejecutan muy rápido porque compilan esa linea, por eso cada vez que vuelven a pasar por ese loop, ya esta perfectamente compilado.

Javascript solía ser interpretado y ahora es compilado con una tecnologia llamada Just in time compiler ó compilación en tiempo de ejecución, está tecnología lo que tiene es un monitor que se encarga de revizar cada cuanto se ejecuta nuestro código, si el código se ejecuta mucho pone un estado warm y lo que hace es que ese código lo compila, si ese código compilado se ejecuta muchas veces, lo coloca en un estado HOT y es básicamente es hacerle una optimización a ese compilado, para que cuando se llame, ya llame a la versión optimizada.

Nodejs fue tomar el engine de JS chrome V8 para crear un entorno de ejecución y poder usar javascript del lado del servidor, recordemos que tenemos otros engine de JS como: spiderMonkey, JavascriptCore y Chakra. Pero como recientemente van a renovar la versión de Each van a empezar a implementar el motor V8 como Js engine.

## Fechas importantes de NodeJS

- En 2009 por primera vez Ryan Dahl mostró al mundo nodejs.

- En 2011 por primera vez Linkenlin usa nodejs en producción.

- En 2013 se saca Gust que es una Plataforma de plugin.

- A la vez Paypal saca un framework de nodejs llamado Krakenjs.

- En 2015 sale la competencia de nodejs llamada IOJS, pero afortunadamente se reconcilian y crean lo que hoy es La Nodejs foundation.

- En 2017 Nodejs Se vuelve Messing con un 8.8 millones de instancias funcionando.

## Diferencias entre NodeJs y Javascript

En Javascript tenemos el DOM document object model es la interfaz que nos permite interpretar el documento html en javascript como lo es el objeto window, también tenemos el CSSDOM que es la interfaz que nos permite manipular el css en javascript, por otro lado tenemos el FetchAPI que por el cual podemos hacer request y que nos devuelva una promesa, también tenemos toda la capa de webstorage que consiste en el sessionStorage y el localStorage que eso no existe en nodejs, tenemos el modulo de canvas API que nos permite hacer gráficos en la web en 2D y 3D y apartir de ahi tenemos una seríe de APIS como lo son: el Web Bluetooth AP, AudioAPI y webAutenthicationAPI.

Por otro lado en Nodejs tenemos una serie de modulos:

- Http: permite crear servidores
- Sistema operativo: nos permite comunicarnos entre el sistema operativo y darnos información sobre el.
- Utilidades: que son una serie de utilidades excusivas para nodejs
- Debugger: una manera en la que podemos hacer debuggin con nodejs.
- Streams: nos permiten manejar grandes colecciones de datos-
- Eventos: podemos definir acciones y dispararlas más adelantel.
- Ecmascript Modules: se pueden ejecutar en nodejs mediante un feature flag
- Consola: es muy similar a la del navegador.

## Instalación de Node.js

Para instalar Node.js tienes que dirigirte a nodejs.org y elegir entre la ultima versión o la version LTS.

Por defecto Node.js detecta tu sistema operativo y descarga el archivo indicado para la instalación, si no es tu caso puedes dirigirte al enlace de otras descargas


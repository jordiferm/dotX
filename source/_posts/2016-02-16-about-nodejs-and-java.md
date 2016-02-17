---
layout: post
title: "About NodeJS and Java"
permalink: about-nodejs-and-java
date: 2016-02-16 23:58:36
comments: true
description: "About NodeJS and Java"
keywords: ""
categories:

tags:

---

# Java vs NodeJS

Sin duda uno de los temas de moda en internet en los sitios visitados por desarrolladores, arquitectos de software, etc...

Me veo obligado a hablar sobre ello porqué la mayoria de publicaciones son demasiado tendenciosas. Intentaré ser el máximo objetivo, claro y analítico posible. Mi objetivo es que al leer este artículo tengais más claro qué tecnología es mejor para implementar vuestra solución.

# Las Arquitecturas

El primer tema que se pone sobre la mesa cuando hablamos de las virtudes de NodeJS es su arquitectura. Echemosle un vistazo:

## Arquitectura de NodeJS
Node JS consta de un núcleo implementado en C y C++ que consta del motor intérprete de Javascript V8 de Google, i la implementación de un patron de arquitectura event-driven con topologia de event procesor en un solo thread para gestionar las peticiones.

![NodeJs Structure][nodejs_internal_structure_image]

Toda la entrada y salida es asincrona para asegurar que sea Non-Blocking.

La idea detras de  es que un procesador de eventos escucha los eventos entrantes y los envia usando la libreria Libuv para que los delegue al proceso correspondiente. Libuv optimiza los threads priorizando el bajo consumo de recursos.

![NodeJs event loop][nodejs_event_loop_image]

Gestionando una petición HTTP cada petición genera un evento y se le asigna un proceso ligado a un callback luego es liberado el procesador para poder atender a otras peticiones o eventos. Cuando el proceso  termina se llama al callback relacionado.
El mismo comportamiento se reproduce cuando se realiza una operación de entrada y salida, por ejemplo escribir en un archivo.

### Beneficios

* El primer beneficio de usar esta arquitectura es que se puede optimizar el consumo de recursos para peticiones simultanias. Por eso se suele decir que node es capaz de gestionar mas peticiones concurrentes con los mismos recursos que otros sistemas (Java).
* Debido al que usa Javascript nodeJS es bueno manejando JSON (La representacion estándar de los objetos en Javascript)
* Con entrada y salida asincrona en node podemos procesar un archivo mientras esta siendo procesado, lo que lo hace un buen candidato para aplicaciones con flujos de datos pesados.
* Gracias tambien a Javascript en las aplicaciones web podemos escribir tanto el Front-End com o el Back-End en un mismo lenguaje.


### Limitaciones

* El núcleo de node no abstrae las llamadas a V8 de echo está muy acoplado a él. Esto hace que sea muy difícil mantener el núcleo al dia con los cambios de V8.
* Debido a que su procesador de eventos es "Single Thread" la plataforma tienen un "Single point of failure" lo que hace muy poco tolerante a los fallos. Un pico de peticiones intenso puede saturar al servidor y bloquear todas la peticiones.
* Tambien por su naturaleza "Single Thread" si una excepcion llega al procesador de eventos este romperá todo el servicio. Aunque podemos reiniciarlo la recuperación puede ser muy costosa.

Estas limitaciones se refieren puramente a la arquitectura.

## Arquitectura de Java

¿ Cual es la arquitectura de Java ?

Comparar node con Java por su arquitectura no tiene ningún sentido. Supongo que muchas veces se tiende a ligar Java con JEE y una arquitectura web 3 capas.

Existen muchas implementaciones de la architectura de nodeJS en Java:

* [Play Framework](https://www.playframework.com/)
* [Netty](http://netty.io/)
* https://mina.apache.org/
* https://grizzly.java.net/
* https://mina.apache.org/

Muchas de ellas mas maduras que nodeJS.

![SOA Pattern][soapattern_event_procesor_image]

Pero aún asi con arquitecturas tradicionales es muy simple escribir código asincrono, que responda a una petición.

//TODO: Exemple spring + Async

Por no hablar de las implementaciones para la gestión asíncrona con actores como AKKA.

### Beneficios
Cuales serian pues los beneficios de usar la implementación de una arquitectura como la de node en Java ?

A demás que los que veremos más adelante relativos al lenguage, a las herramientas y a los frameworks podriamos destacar también:

#### No tengo el modelo asincrono impuesto
Debido a que existen modelos hibridos como Play o que es facil implementar un handler asincrono.
Si un proceso por ejemplo hace llamadas a una api que tienen que sincronizarse NodeJS pierde el sentido. No tenemos mas remedio que sincronizar código asincrono cosa que complica nuestra implementación innecesariamente.

#### No estoy ligado a Javascript
Muchos lenguages compilan al ByteCode de Java, Por ejemplo Skala o Clojure, Groovy a demas son compatibles con sus herramientas de perfilado, gestión de dependéncias, etc...




---

# Los lenguajes

* Diversidad

PolyFills (Librerias por funcionalidades del lenguage ej: underscore)

## La calidad

* Control de excepciones.

## Déuda tecnológica

---

# Herramientas

## Monitorización

## Testing

## Project managers

## Control de versiones/dependencias


# Los frameworks

## Librerias
### Seguridad
### Logging
### Monitorización
### Patrones

### Spring

## La documentación

## Continuidad

## La comunidad

https://github.com/nodejs/node/pulse

vs

https://github.com/spring-projects/spring-framework/pulse#new-issues

(Spring) => 0 Issues, 10 branches, 83 releases, 144 contributors, 11593 commits

(Node) => 470 Issues , 126 branches, 335 releases, 847 contributors  13192 Commits





[nodejs_internal_structure_image]: /assets/images/nodevsjava/node_internal_structure.png
[nodejs_event_loop_image]: /assets/images/nodevsjava/nodejs_event_loop.png
[soapattern_event_procesor_image]: /assets/images/nodevsjava/soapattern_event_processor.png
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

Me veo obligado a hablar sobre ello por dos motivos: Primero porqué la mayoría de publicaciones son demasiado tendenciosas y segundo porque durante el último año he tenido la suerte de poder ser arquitecto de un proyecto con nodeJS y de otro con Java.

Intentaré ser el máximo objetivo, claro y analítico posible. Mi objetivo es que al leer este artículo tengáis más claro qué tecnología es mejor para implementar vuestra solución.

Comparar NodeJS con Java no es correcto. Puesto que NodeJS es la implementación de una arquitectura con una serie de tecnologías y lenguajes y Java es en si un lenguaje.

Lo correcto seria estudiar una solución a partir de tecnologías relacionadas con NodeJS o con tecnologías relacionadas con Java.

vamos a ello:


# Solución NodeJS

¿Qué es NodeJS, cuales son sus virtudes, como es su arquitectura ? A continuación vamos a explicarlo:

## Arquitectura

Node JS se compone de un núcleo implementado en C y C++ que consta del motor intérprete de Javascript V8 de Google, i la implementación de un patron de arquitectura event-driven con topología de event procesor en un solo thread para gestionar las peticiones.

![NodeJs Structure][nodejs_internal_structure_image]

Toda la entrada y salida es asincrona para asegurar que sea Non-Blocking, puesto que el procesador de eventos es de un solo thread.

La idea  es que el procesador de eventos escucha los eventos entrantes y los envia (usando la libreria Libuv) al proceso correspondiente. Libuv optimiza los threads priorizando el bajo consumo de recursos.

Gestionando una petición HTTP cada petición genera un evento y se le asigna un proceso ligado a un callback luego es liberado el procesador para poder atender a otras peticiones o eventos. Cuando el proceso  termina se llama al callback relacionado.
El mismo comportamiento se reproduce cuando se realiza una operación de entrada y salida, por ejemplo escribir en un archivo.

### Beneficios

* El primer beneficio de usar esta arquitectura es que se puede optimizar el consumo de recursos para peticiones simultanias. Por eso se suele decir que node es capaz de gestionar mas peticiones concurrentes con los mismos recursos que otros sistemas (p ej: Java Tradicional).
* Con entrada y salida asincrona en node podemos procesar un archivo mientras esta siendo procesado, lo que lo hace un buen candidato para aplicaciones con flujos de datos pesados.

![NodeJs event loop][nodejs_event_loop_image]


## El Lenguaje

NodeJS esta íntimamente ligado a Javascript una de las piezas clave de su núcleo es el intérprete de Javascript Google V8. Este componente se dedica a ejecutar o procesar eventos con tareas escritas en scripts de Javascript.

[JavaScript](https://en.wikipedia.org/wiki/JavaScript) es un lenguaje de programación interpretado, de alto nivel, dinámico, sin tipado fuerte y multi-paradigma.
Es multi-paradigmo porque soporta los estilos de programación Orientada a Objetos, funcional y imperativa.

Inicialmente fue diseñado para ejecutarse en la parte cliente de las tecnologías web. Los navegadores. Pero actualmente es usado también en [la parte servidor](https://en.wikipedia.org/wiki/Comparison_of_server-side_JavaScript_solutions).

### Beneficios

* Debido al que usa Javascript nodeJS es bueno manejando JSON (La representación estándar de los objetos en Javascript) actualmente muy utilizado en para la serialización de objetos con los FrontEnds debido a la popularidad de uso de JavaScript en los clientes como los navegadores.
* Gracias también a Javascript en las aplicaciones web podemos escribir tanto el Front-End com o el Back-End en un mismo lenguaje.
* Al ser un lenguaje interpretado no tenemos que compilar para ejecutar nuestro código. Esto agiliza las pruebas.

![Javascript Logo][javascript_logo_image]

## Frameworks y Herramientas

Una de las características que hace a un Framework interesante es que tenga todos los componentes necesarios para desarrollar nuestra solución.

Existen [infinidad de Frameworks](http://nodeframework.com/) implementados en base a NodeJS. Para diferentes necesidades, por ejemplo:

* [Hapi](http://hapijs.com/)
* [Kraken](http://krakenjs.com/)
* [Sails](http://sailsjs.org/)
* [Express.js](http://expressjs.com/)
* [LoopBack](http://loopback.io/)

De forma genérica en cualquier solución se necesita que un framework tenga soporte para:

* Control de dependencias
* Persistencia
* Generación de vistas
* Connectividad en tiempo real
* Configuración por entornos
* Implementación de patrones de diseño, de integración
* Buena integración con otros sistemas
* Seguridad, Authenticación y Autorización
* Logging
* Cache
* Monitorización
* Procesado masivo de datos
* Gestión de dependencias
* Testing

Otra característica importante que necesita un buen Framework es que sea escalable.


A demás de implementaciones web en Node tambien se desarrollan herramientas para automatizar tareas por ejemplo para generación de código, minificado de front-end, gestión de dependencias, etc...
* [gulp](http://gulpjs.com/)
* [yeoman](https://www.npmjs.com/package/yo)
* [bower](http://bower.io/)
* etc...

Sin duda pero una de las herramientas mas importantes de node es su gestor de paquetes. [npm](https://docs.npmjs.com/how-npm-works/packages), centrado en la definición de paquetes y sus dependencias con un repositorio central y gestión de versiones.

### Beneficios

* Los Frameworks suelen tener la curba de entrada es muy rápida y disfrutan de las ventajas inherentes a JavaScript.
* La mayoria son OpenSource y hospedados en GitHub con gran cantidad de aportaciones y muy activos.
* Multiplataforma, el núcleo de NodeJS esta portado a varias plataformas y por tanto implicitamente sus herramientas
* Los packages de node se distribuyen a partir del código.


![Frameworks][frameworks_image]

## La Comunidad

Con unas cifras indudablemente grandes, a día de hoy, 241,473 paquetes en **npm** con más de 150 millones de descargas diarias y siendo javascript el lenguage más utilizado en GitHub: http://githut.info/ la [comunidad de NodeJS](https://nodejs.org/en/get-involved/) es sin duda de gran importancia y a la que hay que tener en cuenta.

### Beneficios

* Gran cantidad de soluciones y aportaciones.
* Soporte on-line
* Open Source

## Uso adecuado

Todos los beneficios que acabamos de describir hacen a NodeJS adecuado o seductor para soluciones tipo:

* **Chat**: al ser una aplicación ligera con mucho tráfico, mucho manejo de datos y poco proceso/computación. Su arquitectura event driven le va como anillo al dedo.
* **API REST sobre objectDB basada en Json**: Reduciendo así el "impedance-mismatch" y por tanto el mapeo de datos y la carga computacional.
* **Data Streaming** Su anatomia asincrona permite por ejemplo procesar archivos mientras se suben.
* **MicroServices** Su microkernel permite con un mínimo de recursos construir servicios que hagan tareas singulares y se comuniquen con un ecosistema de servicios parecidos.


---

# Limitaciones de la Solucion NodeJS

Una vez vistas las ventajas, vamos a estudiar las limitaciones, Las repasaremos apartado por apartado siguiendo el orden de los apartados anteriores:

## Arquitectura

Inicialmente la arquitectura de nodeJS presenta varios problemas:

* El núcleo de node no abstrae las llamadas a V8 y a demás está muy acoplado a él. Esto hace que sea muy difícil mantener el núcleo al día con los cambios de V8.
* Debido a que su procesador de eventos es "Single Thread" la plataforma tienen un "Single point of failure" lo que hace muy poco tolerante a los fallos. Un pico de peticiones intenso puede saturar al servidor y bloquear todas la peticiones.
* También por su naturaleza "Single Thread" si una excepción llega al procesador de eventos este romperá todo el servicio. Aunque podemos reiniciarlo la recuperación puede ser muy costosa y casi con toda seguridad perderemos todas las respuestas que teníamos pendientes, que por su rendimiento pueden ser muchas.

Los patrones de diseño son muy buenos cuando se usan bien pero todo lo contrario cuando se usan mal.
Uno de los problemas de la arquitectura de NodeJS es que a menudo hay soluciones en las que hay que aplicar varios patrones. El patrón de NodeJS nos es útil en algunos casos pero cuando no lo necesitamos puede ser contraproducente. Por ejemplo la entrada y salida sea asíncrona.

### I/O Asíncrona
Si no me interesa una I/O asíncrona ni un Event driven, ¿Como uso NodeJS? ¿De qué me sirve su kernel?
Hay muchísimos casos donde no me interesa tener I/O asíncrona, por ejemplo cuando me interesa tener los resultados serializados, ya sea llamando a servicios o consultando bases de datos. Casos en los que tengo que esperar a un resultado para hacer un cálculo con él y esperar a la escritura para por ejemplo comprobar que se ha realizado con éxito.
Por supuesto que node y Javascript me propone [muchas soluciones](http://alexeypetrushin.github.io/synchronize/docs/index.html) para hacerlo, pero todas tienden a complicar el código y es un problema más que tengo que tener en cuenta.

En los casos en los que no tengo que sincronizarlos sigo teniendo que lidiar con [llamadas asincronas](http://howtonode.org/promises), vuelvo a pagar coste de desarrollo cuando no tengo tan claro que me aporte nada sobre ninguna necesidad real de mi solución.

Por ejemplo otro caso, si quiero hacer logs ordenados de mis operaciones de entrada y salida.

### Rendimiento
Se pueden encontrar por la red [comparaciones de rendimiento](https://dzone.com/articles/performance-comparison-between), la arquitectura de NodeJS debería favorecer a contestar muchas peticiones por segundo. Lo interesante es que en la mayoría de soluciones no necesitamos tanto rendimiento y NodeJS nos impone un patrón de arquitectura. En muchas de ellas se habla de miles de peticiones por segundo. Tengamos en cuenta que por ejemplo Google.com tiene unos 5 mil millones de peticiones diarias, eso supone unas 50000 por segundo. En muchos casos 100 o 200 peticiones por segundo son más que suficientes.



## El Lenguaje

Dicen que un trozo de código vale más que 1000 palabras.

He seleccionado 2 trozos de código para representar la sensación que se tiene cuando se lee código Java o Javascript:


{% highlight java %}
@Override
	public void handleReturnValue(Object returnValue, MethodParameter returnType,
			ModelAndViewContainer mavContainer, NativeWebRequest webRequest) throws Exception {

		if (returnValue == null) {
			mavContainer.setRequestHandled(true);
			return;
		}

		WebAsyncTask<?> webAsyncTask = (WebAsyncTask<?>) returnValue;
		webAsyncTask.setBeanFactory(this.beanFactory);
		WebAsyncUtils.getAsyncManager(webRequest).startCallableProcessing(webAsyncTask, mavContainer);
	}
{% endhighlight %}
Ejemplo de código Java originario de [Spring](https://github.com/spring-projects/spring-framework/blob/d5ee787e1e6653257720afe31ee3f8819cd4605c/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/AsyncTaskMethodReturnValueHandler.java).


{% highlight javascript %}
async.forEachOfSeries =
    async.eachOfSeries = function (obj, iterator, callback) {
        callback = _once(callback || noop);
        obj = obj || [];
        var nextKey = _keyIterator(obj);
        var key = nextKey();
        function iterate() {
            var sync = true;
            if (key === null) {
                return callback(null);
            }
            iterator(obj[key], key, only_once(function (err) {
                if (err) {
                    callback(err);
                }
                else {
                    key = nextKey();
                    if (key === null) {
                        return callback(null);
                    } else {
                        if (sync) {
                            async.setImmediate(iterate);
                        } else {
                            iterate();
                        }
                    }
                }
            }));
            sync = false;
        }
        iterate();
    };
{% endhighlight %}
Ejemplo de código JavaScript originario de la [libreria async](https://github.com/caolan/async/blob/master/lib/async.js)

Des de luego que se puede escribir buen código independientemente del lenguaje. Pero en la práctica los códigos en general en JavaScript son mucíssimo más crípticos. Por su naturaleza multi-proposito.
En Javascript no hay una sola forma de hacer las cosas, se pueden definir objetos de varias formas distintas, no hay tipado fuerte, las funciones son objetos. Incluso hay varias formas de referenciar un método de un objeto.


### Exception handling

{% highlight javascript %}
try {
  foo.bar();
} catch (e) {
  if (e instanceof EvalError) {
    console.log(e.name + ': ' + e.message);
  } else if (e instanceof RangeError) {
    console.log(e.name + ': ' + e.message);
  }
  // ... etc
}
{% endhighlight %}

Al no tener tipos la gestión de excepciones en JavaScript pierde una de sus grandes vazas. Como especializo el control ?
En su esencia controlar excepciones es delegar el error a otro nivel o a otra capa. Cuando cazo una excepción es porque puedo actuar en consecuencia, aportar algo a ese control. Si no puedo seleccionar que tipos de escepcion
Para seleccionar me veo obligado a hacer comprovación de tipos en tiempo de ejecución.

A demás la practica de usar callbacks especialmente en NodeJs compilca aún mas la gestion de excepciones.

### Errores en tiempo de ejecución
Por su naturaleza tan dinàmica y al tener cosas como el tipado dévil, objetos en base a prototipos y ningún compilador muchos errores en JavaScript se producen en tiempo de ejecución. Las soluciones suelen ser incrementar la cobertura el testing. Las capas de testing suelen ser bastante difíciles de mantener ahora a la postre estoy obligado a cubrir con testing aspectos que con otros lenguages no son necesarios.

> Resumiendo diremos que en JavaScript por su naturaleza tiende a empeorar muchísimo la calidad del código

La déuda tecnológica es una de las grandes cosas a tener en cuenta en cualquier aplicación.

### Mismo lenguaje en back y en Front

No se si decirle ventaja cuando normalmente el codigo que se comparte entre back y Front, si realmente las partes estan bién separadas es muy pequeña.


![Javascript Good Parts image][javascript_good_parts_image]

## Frameworks y Herramientas

Sobre los Frameworks, es verdad que existen bastantes implementaciones, pero la mayoria por no decir todas sufren de:



### Ciclos de desarrollo demasiado rapidos rompiendo compatibilidades
[Por ejemplo meteor](https://github.com/meteor/meteor/graphs/contributors) desde febrero de 2011 a Febrero del 2016 tiene la friolera de:

* 649 Releases
* 374 Ramas
* 266 Contribuidores

Cuando [Spring](https://github.com/spring-projects/spring-framework) con un periodo de tiempo 3 años mas largo y muchíssimas más prestaciones tenga solo:

* 83 Releases (Y yo añadiria la pincelada de Estables)
* 10 Ramas
* 146 Contribuidores

Esto complica mucho mantenerse al dia. Esto provoca que nuestra solución se tenga que afianzar con unas versiones concretas de nuestras dependéncias. NodeJS a la postre permite tener dependencias locales, de forma que las dependencias transitivas (Dependencias de mis dependencias) pueden formar un árbol con diferentes versiones de librerias entre sus nodos.
Esto acaba dejenerando hasta niveles de locura, por ejemplo instalando bower y gulp llego a tener unos 40000 archivos.

### Documentaciones muy pobres
Solo hay que ver los ejemplos de los principales frameworks. Por ejemplo si comparamos la de [Sails](http://sailsjs.org/documentation/concepts/) con [Solo una parte pequeña de Spring](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/) a simple vista vemos que algo no cuadra.
Los ciclos infernales de cambios, ramas y aportaciones tambien condicionan mucho a que la poca documentación que hay no esté actualizada.

 Demasiada Diversidad

### FullStack ?

¿Qué le pido a un Framework ?

Lo primero que busco en un Framework es compatibilidad, cohesión, capacidad para dar una amplica gama de soluciones con una misma base. Los Frameworks de node que se autodenominan FullStack alegando que tienen soluciones integrales se quedan a mitad de medio camino.
No he encontrado frameworks con todas necesidades básicas como:

 * Control de dependencias
 * Persistencia
 * Generación de vistas
 * Connectividad en tiempo real
 * Configuración por entornos
 * Implementación de patrones de diseño, de integración
 * Buena integración con otros sistemas
 * Seguridad, Authenticación y Autorización
 * Logging
 * Cache
 * Monitorización
 * Procesado masivo de datos
 * Gestion de dependencias
 * Testing

Pero es que ni al 50%. Eso no significa que no tenga librerias para cubrirlo todo, significa que estas librerias no forman un Framework y por tanto no se han puesto de acuerdo. Para llegarlas a integrar puede que necesite conocerlas mejor que el desarrollador.

¿ Que me pasará por ejemplo si quiero integrar un servicio SOAP con nodeJS ?

### Despliege
No existe tampoco ningún standar o sistema de empaquetado para nodeJS, los despliegues en el servidor suelen ser con herramientas para ejecutar como un servicio de forma redundante el nucleo de node. Se suele tambien versionar cada proyecto con el código de todas sus dependencias debido a que a veces npm tiene problemas de conectividad, caches, etc...


## La Comunidad

Una comunidad muy grande no tiene porque ser una ventaja. En el caso de node es un caos de aportaciones dificilisimas de controlar debido en parte al descontrol de compatibilidades y al no tener una linia unos estandares, unas pautas, etc...

## Uso adecuado

Hemos hablado de que NodeJS es adecuado en algunos casos, pero cuando no es adecuado:

* En sistemas con Bd Relacionales. Debido a la immadurez de los ORM y de la necesidad de hacer llamadas sincronas.
* Encuanto tengamos uso intensivo de CPU (Bloquearia la responsibidad de node)
* En bd NoSQL donde los objetos no sean JSON.

En los que supuestamente es adecuado hay que perfilar más. Por ejemplo que pasa con un servicio de Streaming que analice en tiempo real los datos ? Usará la CPU no ?

### ¿ Y en los **MicroServices** ?

En un ecosistema de ese tipo, necessito gestores de configuración centralizados, sistemas para autodiscovery de servicios activos, circuit breakers, global locks, sessiones distribuidas, leadership elections, ...
Qué Framework me proporciona esto ? Si uso distintas librerias Node que problemas de integración me supone ? ¿ Y si me integro con otras soluciones de distintas tecnologias ?


> Nodo esto me hace pensar si hay alguna otra solución en el mercado con la que pueda disponer de las ventajas de Node sin sus limitaciones:

---

# Solución Java

![Java Logo][java_logo_image]

Pues estamos de suerte porque existe una solución, está mas consolidada, usada y es a dia de hoy mas conocida.

## Arquitectura

Comparar node con Java por su arquitectura no tiene ningún sentido. Supongo que muchas veces se tiende a ligar Java con JEE y una arquitectura web 3 capas y quizá por esto las comparaciones erroneas.
Existen muchas implementaciones de la architectura de nodeJS en Java:

* [Play Framework](https://www.playframework.com/)
* [Netty](http://netty.io/)
* https://mina.apache.org/
* https://grizzly.java.net/
* http://www.coralblocks.com/index.php/category/coralreactor/

Muchas de ellas mas maduras que nodeJS.
Luego el argumento de que la arquitectura de node es mejor que la de Java se deberia de reformular quizá en que la arquitectura de NodeJS es mejor que la del modelo de aplicaciones web 3 capas o de servlet tradicional.

### Beneficios

Cuales serian pues los beneficios de usar la implementación de una arquitectura como la de node en Java ?

#### No tengo el modelo asincrono impuesto
Debido a que existen modelos hibridos como Play o que es facil implementar un handler asincrono.
Si un proceso por ejemplo hace llamadas a una api que tienen que sincronizarse NodeJS pierde el sentido. No tenemos mas remedio que sincronizar código asincrono cosa que complica nuestra implementación innecesariamente.

#### No estoy ligado a Javascript
Muchos lenguages compilan al ByteCode de Java, Por ejemplo Skala o Clojure, Groovy a demas son compatibles con sus herramientas de perfilado, gestión de dependéncias, etc...

#### Performance
http://www.olympum.com/java/java-aio-vs-nodejs/


## El Lenguaje

Java es un lenguaje de propósito general basado en classes y especialmente diseñado para tener el mínimo de dependencias posibles. Es de tipado fuerte y compilado con la peculiaridad que se compila a un bytecode que lo ejecuta una máquina virtual. Al existir esa máquina virtual para todas la plataformas el código compilado de java puede funcionar en todas las plataformas.

En esencia mucho [más eficiente](https://medium.com/@tschundeee/express-vs-flask-vs-go-acc0879c2122#.9d4qj5p1d) que Javascript en todos los sentidos.

No tiene las limitaciones que hemos hablado anteriormente para el control de escepciones, los errores en tiempo de ejecución, etc... Y a diferencia de JavaScript tiende a obligar a escribir buen código. Por ejemplo puede imponer que se implemente una interfaz.

Pero es que a demás en términos de cantidad de proyectos que usan el lenguage la adopción de java en los últimos años ha sido incluso [superior al de Javascript](https://github.com/blog/2047-language-trends-on-github).


A demás existen alternativas a lenguages que compilan a byteCode de Java como skala o Clojure, Groovy, etc con los que puedo integrarme a nivel binario.

## Frameworks y Herramientas

Existen muchísimas mas herramientas aún si solo hablamos de las estables y maduras en Java que en Node. Voy a enumerar solo las que conozco muy bién

Desde gestores de proyectos como:

* Maven o Gradle con mas capacidades que npm
* librerias de Monitorización como [Metrics](https://dropwizard.github.io/metrics/3.1.0/)
* Para logging [LogBack](http://logback.qos.ch/)
* Para control de versiones en BD: [Liquibase](http://www.liquibase.org/)
* Cache [EHCache](http://www.ehcache.org/)
* Tests [Mockito](http://mockito.org/)
* etc... TODO Completar

Pero si hablamos de Frameworks existe uno que se lleva el premio Gordo.

[Spring  Framework](http://spring.io/projects)

Spring nació en **2002** para simplificar el desarrollo de Java partiendo con un núcleo de IOC o injeccion de dependencias y AOP.


![Spring Overview][spring_overview_image]

Una de las muchas cosas que ha hecho muy bien Spring es integrar un ecosistema de librerias para tener el honor de poderse llamar Full Stack:

* Spring Boot (Configuració, staging, ejecución)
* Spring Framework (Núcleo de Spring)
* Spring XD (Big Data)
* Spring Cloud (Todo lo necesario para MicroServices)
* Spring Data (Persistencia)
* Spring Batch (Procesado de volumenes grandes de datos)
* Spring Integration (Todos los patrones Enterprise Integration)
* Spring Security (Authorizacion y Authenticación)
* Spring HATEOAS (Nivel 3 de RestFUL)
* Spring Social (Integracion con redes sociales)
* Spring AMPQ (Patrones de Message queues)
* Spring Mobile
* Spring Web
* Spring Web Services
* Spring Session
* ...

Otra gran virtud de Spring es que es extremadamente escalable. Todas las capas que deben son abstractas. Por ejemplo la gesión de sessiones, de cache, de Transacciones todo es reimplementable o intercambiando piezas, confirugando el contexto hago cosas como cambiar la persistencia de sessión sin tocar nada más que una definición de Bean.


## La Comunidad

Las herramientas conservan las ventajas de ser comunidades de código abierto, pero suelen priorizar la estabilidad y compatibilidad de los proyectos, los códigos no son tan crípticos ni las aportaciones tan descontroladas y caoticas.

## Uso adecuado

Para todos los usos adecuados en NodeJS encontramos igual o mejores soluciones en Java y también para todos los usos no adecuados en node. De forma que Java me sirve para un mayor catálogo de soluciones. Aprender Java es mejor inversión y me permite sobretodo manter soluciones a largo plazo.

---


# Concretando La solución

Implementación de una solución SOA con un bus de servicios expuesto en una API RestFul con los siguientes servicios:

* De infrastructura
  * Authenticacion OpenID
  * Authorizacion JAVA
* Indexador
* Recomendador
* Calendario
* CMS de documentos orientado a API.


![SOA Pattern][soapattern_general_image]

# Apendice: Experiencias en NodeJS

## Netflix
[Uso Node en netflix](http://www.talentbuddy.co/blog/building-with-node-js-at-netflix/)
Para que sus front-enders pudieran escribir también backend

## Ebay
Reconocen que no comprovaron otras opciones diferentes que el modelo tradicional de servlets en Java.

http://www.talentbuddy.co/blog/

## Mi experiencia con Frameworks de node:
* Sails


## Moraleja:
> A fool with a tool is still a fool :)

----


[nodejs_internal_structure_image]: /assets/images/nodevsjava/node_internal_structure.png
[nodejs_event_loop_image]: /assets/images/nodevsjava/nodejs_event_loop.png
[soapattern_event_procesor_image]: /assets/images/nodevsjava/soapattern_event_processor.png
[javascript_logo_image]: /assets/images/nodevsjava/javascript_logo.png
[frameworks_image]: /assets/images/nodevsjava/frameworks.png
[spring_overview_image]: /assets/images/nodevsjava/spring-overview.png
[java_logo_image]: /assets/images/nodevsjava/Java_Logo.jpg
[javascript_good_parts_image]: /assets/images/nodevsjava/javascript-the-good-parts-the-definitive-guide.jpg
[soapattern_general_image]: /assets/images/nodevsjava/soa.png
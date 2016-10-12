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

![Fight][fight_image]

Comparar NodeJS con Java no es correcto. Puesto que NodeJS es la implementación de una arquitectura con una serie de tecnologías y lenguajes y Java es en si un lenguaje.

Lo correcto seria estudiar una solución a partir de tecnologías relacionadas con NodeJS o con tecnologías relacionadas con Java.

vamos a ello:



# Solución NodeJS

¿Qué es NodeJS, cuales son sus virtudes, como es su arquitectura?

## Arquitectura

Node JS se compone de un núcleo implementado en C y C++ que consta del motor intérprete de Javascript V8 de Google, y la implementación de un patrón de arquitectura event-driven con topología de event procesor en un solo thread para gestionar las peticiones.

![NodeJs Structure][nodejs_internal_structure_image]

Toda la entrada y salida es asíncrona para asegurar que sea Non-Blocking, puesto que el procesador de eventos es de un solo thread.

La idea  es que el procesador de eventos escucha los eventos entrantes y los envia (usando la libreria Libuv) al proceso correspondiente. Libuv optimiza los threads priorizando el bajo consumo de recursos.

Cuando NodeJs gestiona una petición HTTP la petición genera un evento y se le asigna un proceso ligado a un callback. En ese momento el procesador de eventos es liberado para poder atender a otras peticiones o eventos. Cuando el proceso termina se llama al callback relacionado.
El mismo comportamiento se reproduce cuando se realiza una operación de entrada y salida, por ejemplo escribir en un archivo.

### Beneficios

* El primer beneficio de usar esta arquitectura es que se puede optimizar el consumo de recursos para peticiones simultanias. Por eso se suele decir que node es capaz de gestionar mas peticiones concurrentes con los mismos recursos que otros sistemas (p ej: Java Tradicional).
* Con entrada y salida asíncrona en node podemos procesar un archivo mientras esta siendo subido, lo que lo hace un buen candidato para aplicaciones con flujos de datos pesados.

![NodeJs event loop][nodejs_event_loop_image]


## El Lenguaje

NodeJS esta íntimamente ligado a Javascript una de las piezas clave de su núcleo es el intérprete de [Javascript Google V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)). Este componente se dedica a ejecutar o procesar eventos con tareas escritas en scripts de Javascript.

[JavaScript](https://en.wikipedia.org/wiki/JavaScript) es un lenguaje de programación interpretado, de alto nivel, dinámico, sin tipado fuerte y multi-paradigma.
Es multi-paradigma porque soporta los estilos de programación Orientada a Objetos, funcional y imperativa.
Inicialmente fue diseñado para ejecutarse en la parte cliente de las tecnologías web. Los navegadores. Pero actualmente es usado también en [la parte servidor](https://en.wikipedia.org/wiki/Comparison_of_server-side_JavaScript_solutions).

### Beneficios

* Debido al que usa Javascript nodeJS es bueno manejando JSON (La representación estándar de los objetos en Javascript) actualmente muy utilizado en para la serialización de objetos con los FrontEnds debido a la popularidad de uso de JavaScript en los clientes como los navegadores.
* Gracias también a Javascript en las aplicaciones web podemos escribir tanto el Front-End com o el Back-End en un mismo lenguaje.
* Al ser un lenguaje interpretado no tenemos que compilar para ejecutar nuestro código. Esto agiliza las pruebas cuando desarrollamos.

![Javascript Logo][javascript_logo_image]

## Frameworks y Herramientas

Una de las características que hace a un Framework interesante es que tenga **todos los componentes necesarios para desarrollar nuestra solución**.

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

Otra característica importante que necesita un buen Framework es que sea escalable. Escalable significa que permita que la aplicación pueda crecer o cambiar sin modificar mucho el código.


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
* **Data Streaming** Su anatomia asíncrona permite por ejemplo procesar archivos mientras se suben.
* **MicroServices** Su microkernel permite con un mínimo de recursos construir servicios que hagan tareas singulares y se comuniquen con un ecosistema de servicios parecidos.


---

# Limitaciones de la Solucion NodeJS

![Hombre confundido][confused_man_image]

Una vez vistas las ventajas, vamos a estudiar las limitaciones, Las repasaremos apartado por apartado siguiendo el orden de los anteriores:


## Arquitectura

Inicialmente la arquitectura de nodeJS presenta varios problemas:

* **[Acoplamiento a V8](http://jxcore.com/node-needs-an-abstraction-layer-for-javascript-engines/)**: El núcleo de node no abstrae las llamadas a V8 por lo tanto está muy acoplado a él. Esto hace que sea muy difícil mantener el núcleo al día con los cambios de V8, cada vez que V8 evoluciona deja de ser compatible con el núcleo de NodeJS.
* **Single point of failure**: Debido a que su procesador de eventos es "Single Thread" la plataforma tienen un "Single point of failure" lo que hace muy poco tolerante a los fallos. Un pico de peticiones intenso puede sobrecargar la CPU hasta que el gestor de eventos no pueda hacer su trabajo. Esto saturará al servidor y bloqueará todas la peticiones y respuestas pendientes de servir.
* **Excepciones no controladas rompen el event loop**: También por su naturaleza "Single Thread" si una excepción llega al procesador de eventos este romperá todo el servicio. Aunque podemos reiniciarlo la recuperación puede ser muy costosa y casi con toda seguridad perderemos todas las respuestas que teníamos pendientes, que por su rendimiento pueden ser muchas.

Los patrones de diseño son muy buenos cuando se usan bien pero todo lo contrario cuando se usan mal.

La arquitectura de NodeJS resulta útil para algunas soluciones pero cuando no es así necesitamos poder cambiar el modelo. Esto no es posible en NodeJS.
Veamos, por ejemplo, el caso en que no necesitamos que la entrada y salida sea asíncrona.

### I/O Asíncrona
Hay muchísimos casos donde no me interesa tener I/O asíncrona:

Por ejemplo en los casos en que el backend realiza cálculos o necesita llamar a servicios por orden o que la llamada a un servicio desencadena o no otra llamada segun su resultado.
Por supuesto que node y Javascript me propone [muchas soluciones](http://alexeypetrushin.github.io/synchronize/docs/index.html) para hacerlo, pero todas tienden a complicar el código y es un problema más que tengo que tener en cuenta.

En los casos en los que no tengo que sincronizarlos sigo teniendo que lidiar con [llamadas asíncronas](http://howtonode.org/promises), vuelvo a pagar coste de desarrollo cuando no tengo tan claro que me aporte nada sobre ninguna necesidad real de mi solución.

Por ejemplo otro caso, si quiero hacer logs ordenados de mis operaciones de entrada y salida.

### Rendimiento
Se pueden encontrar por la red [comparaciones de rendimiento](https://dzone.com/articles/performance-comparison-between), la arquitectura de NodeJS debería favorecer a contestar muchas peticiones por segundo.

Cuidado con las comparaciones, si habeis revisado el enlaze anterior fijaos en que el código de NodeJS solo se conecta una vez a la base de datos en cambio el código de Java se conecta de nuevo en cada thread. Esto no se tiene en cuenta en la comparación. Hay que contrastar bién la información que encontramos en internet.

Si hablamos de rendimiento tengamos en cuenta, que por ejemplo, que Google.com tiene unos 5 mil millones de peticiones diarias, eso supone unas 50000 por segundo. En muchos casos 100 o 200 peticiones por segundo son más que suficientes. En la mayoria de soluciones no necesitamos una arquitectura de alto rendimiento.



## El Lenguaje

> JavaScript por su naturaleza tiende a empeorar muchísimo la calidad del código.

Dicen que un trozo de código vale más que 1000 palabras.
He seleccionado 2 trozos de código para representar la sensación que se tiene cuando se lee código Java o Javascript:

Ejemplo de código Java originario de [Spring](https://github.com/spring-projects/spring-data-rest/blob/76380eb65087146c8e297bf03a50653c1669fd33/spring-data-rest-webmvc/src/main/java/org/springframework/data/rest/webmvc/BasePathAwareHandlerMapping.java):
```
@Override
protected HandlerMethod lookupHandlerMethod(String lookupPath, HttpServletRequest request) throws Exception {
    List<MediaType> mediaTypes = new ArrayList<MediaType>();
    boolean defaultFound = false;
    for (MediaType mediaType : MediaType.parseMediaTypes(request.getHeader(HttpHeaders.ACCEPT))) {
        MediaType rawtype = mediaType.removeQualityValue();
        if (rawtype.equals(configuration.getDefaultMediaType())) {
            defaultFound = true;
        }
        if (!rawtype.equals(MediaType.ALL)) {
            mediaTypes.add(mediaType);
        }
    }
    if (!defaultFound) {
        mediaTypes.add(configuration.getDefaultMediaType());
    }
    return super.lookupHandlerMethod(lookupPath, new CustomAcceptHeaderHttpServletRequest(request, mediaTypes));
}
```


Ejemplo de código JavaScript originario de la [libreria async](https://github.com/caolan/async/blob/master/lib/async.js)
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

Estos son dos códigos seleccionados al azar que creo que representan muy bien lo que nos solemos encontrar en Java y los que nos solemos encontrar en Javascript.

En el primer ejemplo (Java) encontramos nombres descriptivos, complejidad ciclomática baja, funciones pequeñas que atienden a su responsabilidad. Como resultado, podemos hacernos una idea de lo que hace el código de inmediato.

En el segundo caso (JavaScript), encontramos nombres de variables no descriptivos y ambiguos como: **obj**, **callback**, **sync**, control de errores sin excepciones que aumentan la complejidad ciclomatica, etc... Resultado: códigos mas difíciles de leer.

Si queréis un ejemplo con códigos más similares aquí tenéis una [cesta de la compra en Java](https://github.com/dpaani/springmvc-shoppingcart-sample/blob/master/shoppingcart/src/main/java/com/codetosalvation/shoppingcart/web/controller/ShoppingCartController.java) y [otra similar en JavaScript](https://github.com/krakenjs/kraken-example-with-shoppingcart/blob/master/controllers/cart/index.js)
En este ejemplo se ve como en Java se tiende a escribir más clases cada cual con su responsabilidad =&gt; (Clean Code) y en JavaScript es frecuente encontrar funciones largas con expresiones de distintos niveles de detalle en la misma función =&gt; (Bad Code).

Des de luego que se puede escribir buen código independientemente del lenguaje. Pero en la práctica los códigos que encontramos en los proyectos Open Source en JavaScript son de una calidad de inferior.
Quizá por su naturaleza multi-proposito, o porqué en Javascript no hay una sola forma de hacer las cosas, se pueden definir objetos de varias formas distintas, no hay tipado fuerte, etc... Al final no creo que los programadores que escriben proyectos OpenSource en Javascript sean peores sinó que el lenguaje no les ayuda para escribir código de calidad.

### Exception handling

Al no tener tipos la gestión de excepciones en JavaScript pierde una de sus grandes bazas. ¿Como especializo el control de excepciones?
En su esencia controlar excepciones es delegar el error a otro nivel o a otra capa. Cuando cazo una excepción es porque puedo actuar en consecuencia, aportar algo a ese control. En JavaScript no puedo seleccionar fácilmente que tipos de excepción voy a controlar y para ello me veo obligado a hacer comprobación de tipos en tiempo de ejecución.

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

A demás el control de excepciones en códigos de naturaleza asíncrona, en esencia con muchos callbacks, se complica muchísimo.

### Errores en tiempo de ejecución
Por su naturaleza tan dinámica y al tener cosas como el no tipado fuerte, objetos basándonos en prototipos y ningún compilador muchos errores en JavaScript se producen en tiempo de ejecución. Las soluciones suelen ser incrementar la cobertura el testing. Las capas de testing suelen ser bastante difíciles de mantener ahora a la postre estoy obligado a cubrir con testing aspectos que con otros lenguajes no son necesarios.

La deuda tecnológica es una de las grandes cosas a tener en cuenta en cualquier aplicación.

### Mismo lenguaje en back y en Front

Realmente, si el BackEnd y el FrontEnd están separados como deberían, la cantidad de código que van a compartir es muy poco. Tan solo se me ocurren casos muy concretos como:

* Casos concretos de Validación de entrada de datos que se suelen hacer tanto en front como en back-end.
* Previsualización de un gráfico interactivo en front-end que luego se genera en un PDF del backend.

Aun así si pensamos bien la arquitectura el sobrecoste de estas replicaciones es mínimo.

El perfil de los programadores de Front-End y el de los de BackEnd es muy distinto. Raramente un programador de FrontEnd entenderá las implicaciones derivadas por ejemplo de una consulta a la base de datos, y por el otro lado, rara vez un programador de BackEnd entenderá las consecuencias de hacer, por ejemplo, cambios en un CSS.

Por tanto el poder compartir código en FrontEnd y en BackEnd no supone ninguna ventaja significativa.

![Javascript Good Parts image][javascript_good_parts_image]

## Frameworks y Herramientas

La mayoría de los frameworks desarrollados sobre NodeJS sufren de:


### Ciclos de desarrollo demasiado rápidos rompiendo compatibilidades
[Por ejemplo meteor](https://github.com/meteor/meteor/graphs/contributors) desde febrero de 2011 a Febrero del 2016:

* 649 Releases
* 374 Ramas
* 266 Contribuidores

Cuando [Spring](https://github.com/spring-projects/spring-framework) con un periodo de tiempo 3 años mas largo y muchísimas más prestaciones:

* 83 Releases (Y yo añadiría la pincelada de Estables)
* 10 Ramas
* 146 Contribuidores

En demás proyectos los números son muy parecidos.

Los cambios en los proyectos de NodeJS son muy elevados y normalmente poco rigurosos.
Esto complica mucho mantenerse al día. Supone que nuestra solución se tenga que afianzar con unas versiones concretas de nuestras dependencias.

NodeJS también permite tener [**"Nested Dependencies"**](http://maxogden.com/nested-dependencies.html), de forma que las dependencias transitivas (Dependencias de mis dependencias) pueden formar un árbol con diferentes versiones de librerías entre sus nodos.
Esto por un lado provoca que no se fuercen los cambios, pero por otro y en la práctica duplica considerablemente el número de archivos y de instancias de objetos a memoria, claro.
![Nested deps image][nested_deps_image]

Por ejemplo en uno de mis proyectos con módulos de node habituales y básicos, grunt, karma, jshint tengo en local 39462 archivos de dependencias.

### Documentaciones muy pobres
Comparando por ejemplo la documentación de [Sails](http://sailsjs.org/documentation/concepts/) o [ExpressJS](http://expressjs.com/en/guide/routing.html) con [Solo una parte pequeña de Spring](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/) vemos que al menos por la cantidad ya hay una diferencia podríamos decir de unas 300 linias a 1.

Si nos fijamos en la calidad habrá muchas opiniones pero normalmente los ciclos tan rápidos de cambios, ramas y aportaciones también condicionan que la calidad de la documentación de los frameworks de NodeJS tienda a la baja.

### FullStack ?

¿Qué le pido a un Framework ?

Lo primero que busco en un Framework es compatibilidad, cohesión, capacidad para dar una amplia gama de soluciones con una misma base.
Si comparamos el Framework de NodeJS con mas prestaciones con Spring, tenemos que el Framework de node no llega a darnos ni un 10% de lo que nos da Spring.

A día de hoy No he encontrado frameworks en NodeJS con todas necesidades básicas como:

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

Eso no significa que no tenga librerías para cubrirlo todo, significa que estas librerías no forman un Framework y por tanto no se han puesto de acuerdo. Para llegarlas a integrar puede que necesite conocerlas mejor que el desarrollador.

¿Que me pasará por ejemplo si quiero integrar un servicio SOAP con nodeJS y que intervenga por ejemplo en middleware de Sails?

### Despliege

No existe tampoco ningún estándar o sistema de empaquetado para nodeJS, los despliegues en el servidor suelen ser con herramientas para ejecutar como un servicio de forma redundante el núcleo de node. Se suele también versionar cada proyecto con el código de todas sus dependencias debido a que a veces npm tiene problemas de conectividad, caches, etc...


## La Comunidad

Una comunidad muy grande no tiene porque ser una ventaja.
La calidad de las aportaciones es muy importante, también para facilitar a los integradores el poder incluir estas aportaciones de forma estable y segura.
Indiscutiblemente el punto de entrada a NodeJS es muy rápido, mucho mas que en Java seguramente. Esto es bueno porque aporta programadores pero se convierte en malo cuando estos programadores no son de calidad. Al final que empecemos a hacer programas no significa que seamos buenos programadores.

## Uso adecuado

Hemos hablado de que NodeJS es adecuado en algunos casos, pero cuando no es adecuado:

* En sistemas con Bd Relacionales. Debido a la immadurez de los ORM y de la necesidad de hacer llamadas síncronas.
* Si tuviéramos uso intensivo de CPU (Bloquearía la respuesta de Node)
* En bd NoSQL donde los objetos no sean JSON.

En los que supuestamente es adecuado hay que perfilar más. Por ejemplo que pasa con un servicio de Streaming que analice en tiempo real los datos ? Usará la CPU no ?

### ¿ Y en los **MicroServices** ?

En un ecosistema de ese tipo, necesito gestores de configuración centralizados, sistemas para autodiscovery de servicios activos, circuit breakers, global locks, sesiones distribuidas, leadership elections, ...

¿Qué Framework me proporciona esto? ¿Si uso distintas librerías Node que problemas de integración me supone? ¿Y si me integro con otras soluciones de distintas tecnologias?


> Todo esto me hace pensar si hay alguna otra solución en el mercado con la que pueda disponer de las ventajas de Node sin sus limitaciones:

---

# Solución Java

![Java Logo][java_logo_image]


Solemos identificar Java con sus modelos clásicos a menudo propuestos por Sun Microsystems, como la [especificación de Servlets](http://download.oracle.com/otn-pub/jcp/servlet-3.0-fr-eval-oth-JSpec/servlet-3_0-final-spec.pdf?AuthParam=1456183031_2f62340d91f6ca0dcfb9c7e2004df9ba) lo interesante es que soluciones con la arquitectura de NodeJS ya existen en Java incluso desde antes que node. El problema fue quizá que al asociarse Java con su modelo tradicional, nadie lo tubo en cuenta como solución.

## Arquitectura

Existen muchas implementaciones de la arquitectura de nodeJS en Java:

* [Akka](http://akka.io/)
* [Vert.x](http://vertx.io/)
* [Play Framework](https://www.playframework.com/)
* [Netty](http://netty.io/)
* [Apache Mina](https://mina.apache.org/)
* [Grizzly](https://grizzly.java.net/)
* [CoralReactor](http://www.coralblocks.com/index.php/category/coralreactor/)

Muchas de ellas más maduras que nodeJS.
Luego el argumento de que la arquitectura de node es mejor que la de Java se ha de reformular quizá en que la arquitectura de NodeJS es mejor que la del modelo de aplicaciones web 3 capas o de servlet tradicional con el que se relaciona Java.

Saliendo de implementaciones de terceros y volviendo a Java tradicional, Java soporta [entrada y salida asíncrona](http://en.wikipedia.org/wiki/New_I/O) desde 2002 y Java SE 1.4. En 2009 la especificación de Servlet 3.0 estandarizó el procesado "Non-Blocking" pudiendo usarse si queremos servidores de aplicaciones tradicionales como GlassFish, Tomcat, Jetty o cualquier alternativa comercial.

### Beneficios

¿Cuales serian pues los beneficios de usar la implementación de una arquitectura como la de node en Java?

#### No tengo el event Driven Impuesto.
El modelo de Event Driven

#### No tengo el modelo asíncrono impuesto
Debido a que existen modelos híbridos como Play, [Spring](http://callistaenterprise.se/blogg/teknik/2014/04/22/c10k-developing-non-blocking-rest-services-with-spring-mvc/) o que es fácil implementar un método concreto de forma asíncrona.
Si un proceso por ejemplo hace llamadas a una api que tienen que sincronizarse NodeJS pierde el sentido. No tenemos mas remedio que sincronizar código asíncrono cosa que complica nuestra implementación innecesariamente.

En Java es muy fácil implementar una de nuestras llamadas de forma explicitamente asíncrona.
Ejemplo llamada asíncrona en Java:

{% highlight java %}
@Service
public class GitHubLookupService {

    RestTemplate restTemplate = new RestTemplate();

    @Async
    public Future<User> findUser(String user) throws InterruptedException {
        System.out.println("Looking up " + user);
        User results = restTemplate.getForObject("https://api.github.com/users/" + user, User.class);
        // Artificial delay of 1s for demonstration purposes
        Thread.sleep(1000L);
        return new AsyncResult<User>(results);
    }

}
{% endhighlight %}

En este punto también podemos mencionar que existen implementaciones como [akka](http://akka.io/) que facilitan la programación asíncrona muchísimo más que las de los actuales de NodeJS.

#### No estoy ligado a Javascript

Muchos lenguages compilan al ByteCode de Java, Por ejemplo Skala o Clojure, Groovy a demas son compatibles con sus herramientas de perfilado, gestión de dependéncias, etc...

#### Performance
http://www.olympum.com/java/java-aio-vs-nodejs/

## El Lenguaje

Java es un lenguaje de propósito general basado en clases y especialmente diseñado para tener el mínimo de dependencias posibles. Es de tipado fuerte y compilado con la peculiaridad que se compila a un bytecode que lo ejecuta una máquina virtual. Al existir esa máquina virtual para todas las plataformas el código compilado de java puede funcionar en todas las plataformas.

En esencia mucho más eficiente que Javascript. V8 esta evolucionado en la parte cliente y Java lleva más de 20 años optimizando sus compiladores. Sin incluir NodeJS tenemos una penalización extra con los bindings de Node a V8.
Aquí tenemos algunos ejemplos y pruebas de rendimiento:
* [Benchmark algoritmos](http://benchmarksgame.alioth.debian.org/u32/javascript.html)
* [Comparación peticiones por segundo con distintos Frameworks](https://medium.com/@tschundeee/express-vs-flask-vs-go-acc0879c2122#.9d4qj5p1d)


Java No tiene las limitaciones que hemos hablado anteriormente para el control de excepciones, los errores en tiempo de ejecución, etc... Y a diferencia de JavaScript tiende a obligar a escribir buen código. Por ejemplo puede imponer que se implemente una interfaz.
Java, debido a sus contratos y su tipado fuerte es un lenguaje más Auto Documentado "Self-Documenting". Esta es una característica que cobra mucha importancia en proyectos grandes.
Pero es que a demás en términos de cantidad de proyectos que usan el lenguaje la adopción de java en los últimos años ha sido incluso [superior al de Javascript](https://github.com/blog/2047-language-trends-on-github).

A demás existen alternativas a lenguajes que compilan a byteCode de Java como skala o Clojure, Groovy, etc con los que puedo integrarme a nivel binario.

## Frameworks y Herramientas

En el mundo de los Frameworks y las Herramientas existen una mayor cantidad en Java que en Node. Por ejemplo mirando a los repositorios de paquetes: De los 243k paquetes en [npm](https://www.npmjs.com) pasamos a los 1246k en el [repositorio de maven](http://mvnrepository.com/) 5 veces mas.
Voy a enumerar unas cuantas herramientas y frameworks que conozco personalmente:

* Maven o Gradle con mas capacidades que npm
* librerías de Monitorización como [Metrics](https://dropwizard.github.io/metrics/3.1.0/)
* Para logging [LogBack](http://logback.qos.ch/)
* Para control de versiones en BD: [Liquibase](http://www.liquibase.org/)
* Cache [EHCache](http://www.ehcache.org/), [HazelCast](https://hazelcast.com/)
* Tests [Mockito](http://mockito.org/), [JUnit](http://junit.org/)
* Persistencia [Hibernate](http://hibernate.org/)
* Componentes graficos [Vaadin](https://vaadin.com/home)
* Gestión de repositorios [Nexus](http://www.sonatype.com/nexus/solution-overview)
* Serialización [Jackson](https://github.com/FasterXML/jackson)
* Reporting [Jasper Reports](http://community.jaspersoft.com/project/jasperreports-library)
*


Pero si hablamos de Frameworks existe uno que se lleva el premio Gordo.

[Spring  Framework](http://spring.io/projects)

Spring nació en **2002** para simplificar el desarrollo de Java partiendo con un núcleo de IOC o inyeccion de dependencias y AOP.

![Spring Ecosystem][spring_ecosystem_image]

Una de las muchas cosas que ha hecho muy bien Spring es integrar un [ecosistema de librerías](https://spring.io/projects) para tener el honor de poderse llamar Full Stack:

* **Spring Boot** (Configuració, staging, ejecución)
* **Spring Framework** (Núcleo de Spring, IOC, AOP, Acceso de datos, web apps, messaging y mucho más)
* **Spring XD** (Big Data)
* **Spring Cloud** (Todo lo necesario para MicroServices, Configuration management, service discovery, micro-proxy, circuit breakers, sesiones distribuidas, etc...)
* **Spring Data** (Persistencia, Sql, NoSQL, map-reduce, etc)
* **Spring Batch** (Procesado de volumenes grandes de datos)
* **Spring Integration** (Todos los patrones Enterprise Integration, Adaptadores declarativos)
* **Spring Security** (Authorizacion y Authenticación totalmente extensible)
* **Spring HATEOAS** (Nivel 3 de RestFUL)
* **Spring Social** (Integracion con redes sociales)
* **Spring AMPQ** (Patrones de Message queues)
* **Spring Mobile** (Deteccion de dispositivos, desarollo de webapps para móbiles)
* **Spring Web Services** (Integración con Servicios contract-first SOAP)
* **Spring Session** (Distintas implementaciones de gestión de sessiones de usuario)
* etc...

Otra gran virtud de Spring es que es extremadamente escalable. Todas las capas que deben son abstractas. Por ejemplo la gestión de sesiones, de cache, de Transacciones todo es reimplementable o intercambiando piezas, configurando el contexto hago cosas como cambiar la persistencia de sesión sin tocar nada más que una definición de Bean.

El código de Spring es de altísima calidad y con gran variedad de patrones de diseño muy bién aplicados.

## La Comunidad

Las herramientas conservan las ventajas de ser comunidades de código abierto, pero suelen priorizar la estabilidad y compatibilidad de los proyectos, los códigos no son tan crípticos ni las aportaciones tan descontroladas y caóticas.

## Uso adecuado

Para todos los usos adecuados en NodeJS encontramos igual o mejores soluciones en Java y también para todos los usos no adecuados en node. De forma que Java me sirve para un mayor catálogo de soluciones. Aprender Java es mejor inversión y me permite sobretodo mantener soluciones a largo plazo.

---

# Conclusión

Comparando NodeJS con el modelo tradicional de Java solo tenemos en cuenta un pequeño subconjunto de Java.
Este ha evolucionado mucho desde antes de NodeJS, ja no es ese código monolítico que seguía a la arquitectura J2EE de SUN com EJB2.0. El propio **Spring** surgió para mejorar y simplificar al de SUN. Gracias a esto y a que se ha sabido adaptar a los cambios impuestos por internet ahora disponemos de implementaciones mas modernas y robustas que cualquiera de las demás.

![Conclusion image][conclusion_image]

Existen muchas implementaciones del patrón de NodeJS en Java por lo general mucho más eficientes. A diferencia de NodeJS, Java no nos impone su arquitectura y tenemos muchas mas herramientas para trabajar y garantizar unos niveles de calidad.
Una ventaja que resulta clave en Java es la posibilidad de escribir código de más calidad, más transferible, más robusto, mantenible y donde los errores se detectarán con más claridad.

De NodeJS nos quedamos con el rápido punto de entrada, que resulta muy atractivo para acercar a los programadores de Front-End al Back-End, también es una buena herramienta para soluciones simples, prototipos y pruebas de concepto.
Pero para proyectos de cierta duración, envergadura y robustez no nos interesa un punto de entrada rápido, sino perfiles con amplio conocimiento de los patrones de diseño y arquitecturas y herramientas como Java que les permitan aplicarlos de forma eficiente.

---

# Apendice: Experiencias en NodeJS

## Gad
Mi experiencia en NodeJS con Sails y Restful. La aproximación fue inmediata, pero a la semana de trabajo ya empezamos a leer código de Sails por poca documentación. Luego al subir de complejidad la capa de servicio nos obligó a refactorizarla con poco éxito. Finalmente procesos con llamadas a servicios sincronizadas nos ocuparon mucho mas tiempo del esperado. A la semana de subir a producción teniamos un problema grabe en Sails que se arregló en una nueva versión que al instalarla rompió toda la capa de servicio ya que habían cambiado interfaces de su api.

## Netflix
[Netflix uso NodeJs](http://www.talentbuddy.co/blog/building-with-node-js-at-netflix/)
uno de sus motivos fue para que sus front-enders pudieran escribir también backend

## Ebay
Ebay tubo sus [experiencias en node en 2013](http://www.ebaytechblog.com/2013/05/17/how-we-built-ebays-first-node-js-application/), en ella reconocen que no comprobaron otras opciones diferentes que el modelo tradicional de servlets en Java.

![Ebay testimony][ebay_testimony_image]

----


[fight_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/fight.jpg
[nodejs_internal_structure_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/node_internal_structure.png
[nodejs_event_loop_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/nodejs_event_loop.png
[soapattern_event_procesor_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/soapattern_event_processor.png
[javascript_logo_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/javascript_logo.png
[frameworks_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/frameworks.png
[java_logo_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/Java_Logo.jpg
[javascript_good_parts_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/javascript-the-good-parts-the-definitive-guide.jpg
[soapattern_general_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/soa.png
[nested_deps_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/nested-deps.png
[ebay_testimony_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/ebay_testimony.png
[spring_ecosystem_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/spring-ecosystem.jpg
[conclusion_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/conclusion.jpg
[confused_man_image]: https://raw.githubusercontent.com/jordiferm/dotX/master/source/assets/images/nodevsjava/confused_man.jpg

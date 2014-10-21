Creando aplicaciones en la nube: Uso de PaaS y SaaS
==

<!--@
previous: Intro_concepto_y_soporte_fisico
next: Tecnicas_de_virtualizacion
-->

<div class="objetivos" markdown="1">

##Objetivos 


### Cubre los siguientes objetivos de la asignatura

2. Conocer los conceptos relacionados con el proceso de virtualización
tanto de software como de hardware y ponerlos en práctica. 

4. Justificar la necesidad de procesamiento virtual frente a real en el contexto de una infraestructura TIC de una organización.

### Objetivos específicos

5. Comprender los conceptos necesarios para trabajar con diferentes
   plataformas PaaS

6. Aplicar el concepto de *DevOps* a este tipo específico de plataforma.

7. Aplicar el sistema de control de fuentes `git` para despliegue de aplicaciones en la nube.

</div>

Entornos virtuales de desarrollo
---

Una de las partes esenciales del *DevOps* es primero la gestión de
configuraciones y luego la automatización. El uso de entornos
virtuales cubre las dos necesidades: te permite decidir exactamente
qué versión del lenguaje se va a usar y también automatizar la tarea
de instalación del mismo mediante el uso de una sola orden que
seleccione la versión precisa que se va a usar. 

Y estos entornos virtuales vienen del hedo de que los lenguajes de scripting tales como Perl, Python y Ruby tienen
ciclos de desarrollo muy rápidos que hacen que a veces convivan en
producción diferentes versiones de los mismos, incluso *major*
versions. Eso hace complicado desarrollar e incluso probar los
programas que se desarrollan: si el sistema operativo viene con Perl
5.14, puede que haga falta probar o desarrollar para 5.16 o 5.18 o
incluso probar la versión más avanzada.

Por eso desde hacer cierto tiempo se han venido usando *entornos
virtuales de desarrollo* tales como
[virtualenv para Python](https://virtualenv.pypa.io/en/latest/),
[nodeenv para node.js](https://pypi.python.org/pypi/nodeenv/),
[rbenv para Ruby](https://github.com/sstephenson/rbenv) y
[perlbrew para Perl](http://perlbrew.pl).

Una vez instalados, estos programas permiten instalar fácilmente
nuevas versiones de tu lenguaje de programación (con las librerías
asociadas) y probar un programa en todas ellas. Se usan principalmente
para reflejar localmente los entornos que se usan en producción; por
ejemplo, usar en el entorno de desarrollo local la misma versión y
librerías que nos vamos a encontrar en un PaaS tal como los que
veremos a continuación.

<div class='ejercicios' markdown="1">

Instalar un entorno virtual para tu lenguaje de programación favorito
(uno de los mencionados arriba, obviamente).

</div>

Usando un servicio PaaS
-----

La mayoría de los servicios PaaS están ligados a una pila de
soluciones determinada o a un vendedor determinado. Han surgido
muchos, por ejemplo, en torno a [node.js](http://nodejs.org), un
intérprete de JavaScript asíncrono que permite crear fácilmente
aplicaciones REST.

Algunos servicios PaaS son específicos (sólo alojan una solución
determinada, como [CloudAnt](https://cloudant.com/) que aloja una base
de datos con CouchDB o genéricos, permitiendo una serie de soluciones
en general relativamente limitada; [Heroku](http://www.heroku.com) y
[OpenShift](http://www.openshift.com) están entre estos últimos. 

<div class='ejercicios' markdown="1">

Darse de alta en algún servicio PaaS tal como Heroku, [Nodejitsu](https://www.nodejitsu.com/) u OpenShift.

</div>

Estos servicios proveen un número limitado de máquinas virtuales y
siguen en general un modelo *freemium*: capacidades básicas son
gratuitas y para conseguir mayores prestaciones o un uso más
intensivo, o bien capacidades que no entren en el paquete básico, hay
que pasar al modelo de pago. Estas máquinas virtuales se denominan
[*dynos*](https://devcenter.heroku.com/articles/dynos) en Heroku y
simplemente aplicaciones en OpenShift, aunque los *dynos* son mucho
más flexibles que las aplicaciones de OpenShift.

La interacción con los PaaS se hace en general a través de una
herramienta de línea de órdenes que permite, para empezar, crear
fácilmente a partir de una plantilla una aplicación básica con las
características definidas; en ambos casos habrá que descargar una
aplicación libre para llevar a cabo ciertas tareas como monitorizar el
estatus y hacer tests básicos; una vez creado el fuente de la
aplicación el despliegue en la máquina virtual se hace mediante
`git` tal como hemos contado anteriormente. 

Los lenguajes más habituales en las PaaS son los de scripting, que
permiten crear aplicaciones rápidamente; las bases de datos
disponibles son tanto las clásicas DBMS aunque, con más frecuencia, se
usan las bases de datos NoSQL como MongoDB, Redis o CouchDB.

En cualquier caso, los PaaS suelen tener un panel de control que
permite hacer ciertas cosas como configurar *plugins* o *add-ons*
desde la web fácilmente. Estos suelen seguir el mismo modelo freemium:
diferentes tamaños o instancias son gratuitas o tienen un coste; en
algunos casos cualquier instancia tiene un coste. 


<div class='ejercicios' markdown="1">

Crear una aplicación en OpenShift y dentro de ella instalar
WordPress. 

</div>

<div class='nota' markdown='1'>

Este
[vídeo explica como usar `heroku` para aplicaciones en Ruby](http://www.youtube.com/watch?v=dqAXmratgzE);
en
[este un poco más extenso y hecho por una persona de Heroku](http://www.youtube.com/watch?v=VZgHItD9bAQ)
te explica cómo usarlo. No hay muchos vídeos en español, pero en
[este explica cómo crear una aplicación Django y subirla a Heroku](http://www.youtube.com/watch?v=3k2eg0stnCI)

</div>

Creando aplicaciones en la nube
-----

Algunos SaaS como Google Drive o, más propiamente, Google Apps,
permiten crear también aplicaciones que trabajen con los datos y
objetos que forman parte del mismo. Todos estos sistemas suelen
incluir algún lenguaje de *scripting* y, en general, se suele tratar
de JavaScript.

> Si no sabes JavaScript, es el momento
> [de aprenderlo](https://github.com/JJ/curso-js). Tras más de 15 años
> de existencia, JS se ha convertido en un lenguaje emergente e
> imprescindible para un *full stack programmer*. En particular, es el
> lenguaje que se usa para trabajar con aplicaciones en la nube.

El nivel de control que tiene uno sobre las aplicaciones es bastante
variado. Se puede desde usar Google Drive como un PaaS para alojar
aplicaciones hasta simplemente añadir pequeños *scripts* que lleven a
cabo alguna labor como [cambiar el interfaz de usuario o añadir
funcionalidad a alguna aplicación de Google Drive](https://developers.google.com/apps-script/overview).

Crear un *script* para Google Drive es similar a hacer una macro para
una aplicación. Se hace de la forma siguiente

1. Ir a Herramientas -> Editor de secuencias de comandos. Se abre un
   entorno de desarrollo para *scripts* en el que ya está prerrellena
   la función que la añade al menú y a la que se llama.

2. Se edita la función, se guarda y se publica.
3. Se vuelve a abrir el documento correspondiente. Aparecerá un menú
   nuevo, *Script Center Menu*, que incluirá un enlace con el nombre
   de la aplicación.
4. Cuando se ejecute por primera vez, pedirá que se autorice su uso.


<div class='ejercicios' markdown="1">

Crear un *script* para un documento Google y cambiarle el nombre con
el que aparece en el menú, así como la función a la que llama. 

</div>



A dónde ir desde aquí
-----

En el [siguiente tema](Tecnicas_de_virtualizacion.md) usaremos
diferentes técnicas de virtualización para la creación de contenedores
y jaulas que aislan procesos, usuarios y recursos del resto del sistema. Previamente habrá que [realizar la
práctica correspondiente a esta materia](../practicas/1.PaaS.md). 

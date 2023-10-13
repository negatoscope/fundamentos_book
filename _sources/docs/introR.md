---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: R
  language: R
  name: ir
output: learnr::tutorial
runtime: shiny_prerendered
description: Tutorial
---

(probability)=

# 4 Introducción a R

Esta sección tiene como objetivo que conozcas los fundamentos más básicos del lenguaje de programación R que nos puedan servir para el desarrollo de las clases de nuestra asignatura. No pretendo que te conviertas en un/a programador/a al terminar este curso; busco presentar una herramienta alternativa muy utilizada para el análisis estadístico y su enseñanza, y si esto despertará tu interés, encontrarás más adelante enlaces con recursos educativos formales muy buenos y estaré encantado de ayudarte si así lo deseas.

## 4.1 ¿Qué es R?

R es un lenguaje de programación, que a diferencia de otros, se especializa en sus aplicaciones para el análisis estadístico y gráfico. Es ampliamente utilizado tanto por matemáticos e ingenieros, como científicos de ciencias sociales incluidos los que hacen investigación en Educación. 

En realidad, R por sí mismo consiste en una serie de reglas y comandos pre-establecidos que permiten la creación de pequeños "programas" para resolver alguna cuestión específica. Por ejemplo, es posible crear un "programa" que te permita subir tus propios datos, realice un test estadístico, realice un informe con los resultados y que dibuje una figura que nos permita visualizarlos. A diferencia de otros lenguajes de programación, este procedimiento es relativamente sencillo y no requiere muchos pasos o *líneas de código*.

Otra ventaja que tiene R, es el hecho de ser una herramienta gratuita y abierta a todo el mundo, lo cual significa que cualquier usuario puede crear nuevos "programas" o pequeñas aplicaciones y compartirlas con aquellos que estén interesados. Esto se hace a través de *paquetes* que un usuario puede crear y subir para que otro usuario lo pueda descargar y utilizar.

Para poder utilizar el lenguaje R es necesario utilizar un programa que pueda ejecutarlo. En los ordenadores tenemos la aplicación [RStudio](https://posit.co/download/rstudio-desktop/), que es una interfaz gráfica (término técnico para un programa de ordenador que puedes ver y con el que puedes interactuar) que puedes tener instalada y usar en cualquier momento. Además, existen plataformas online como [Posit Cloud](https://posit.cloud/), que es lo mismo que RStudio pero almacenado en una página web. Esta segunda opción es un poco más limitada, pero para el usuario promedio (como nosotros) suele ser más que suficiente.

Para nuestra clase de Fundamentos de Investigación II lo he puesto un poco más fácil. Debajo encontrarás una caja de texto que llamamos **_terminal_**. La he programado de forma que puedas escribir en lenguaje R directamente sin tener que descargar ninguna aplicación. Para que funcione, selecciona en la parte superior de esta página sobre el símbolo de un cohete la opción que pone "Live Code". Si es la primera vez que lo haces, este proceso puede durar unos 10 minutos, por lo que te pido paciencia. Una vez que esté listo verás la leyenda "Launching from mybinder.org: **_ready_**". Esto significa que podemos empezar a programar. Intenta hacer alguna operación matemática (por ejemplo, copia y pega 2023*2022), dando clic en el botón "run" para que la ejecute. 

```{code-cell} ir
# Escribe líneas de código aquí. Para ejecutar el código, presiona el botón de "Play"
```
Si todo funciona correctamente, en la parte inferior de la caja deberás observar el resultado de la operación (4090506). ¡Felicidades, ahora tienes R en tus apuntes! Como habrás notado, puedes utilizarlo una calculadora, pero lo interesante es que podemos utilizarlo para hacer cálculos más demandantes (como los tests estadístico), y, sobre todo, para crear imágenes y gráficos sobre los datos y los cálculos que hagamos, lo cuál nos permitirá entender mejor los conceptos de la asignatura. 

## 4.2 Conceptos e ideas básicas sobre programación con R

Como he dicho, esta no es una asignatura sobre programación. Sin embargo, creo que es importante que al menos conozcas algúnos de los conceptos y comandos de R más elementales. De cualquier forma, si observar el código que he escrito para estos apuntes, verás que la mayor parte de las líneas de código que hacer algo importante están explicadas tienen un comentario (que inicia con este signo #) que explica brevemente para qué funciona esa línea en concreto. 

### 4.2.1 Funciones

Las funciones son objetos que contienen líneas de código interrelacionadas y con un orden predefinido que se ejecutan cada vez que el usuario "llama" o "pide" a R esa función. Esto se explica mejor con un ejemplo.

Imagina que quieres sumar los números 5, 11, 2, 7 y 8. Ya sabes que R puede funcionar como una calculadora, por lo que lo único que tendrías que hacer es:

`5 + 11 + 2 + 7 + 8`

Sin embargo, tenemos una función específica para sumar `sum()`. Si queremos sumar los mismos números utilizando esta función escribiríamos:

`sum(5,11,2,7,8)`

Si lo ejecutas, comprobarás que el resultado es el mismo. Y así como tenemos una función para sumar, tener funciones para cualquier operación matemática, y en realidad, para casi cualquier cosa que te puedas imaginar: dibujar un mapa que muestre volcanes activos, buscar y contar en un archivo de Excel los datos que contengan un número, etc... 

Utilizar esta función con sólo 5 números te podrá resultar redundante o poco útil; sin embargo, las funciones cumplen mejor con su función cuando las utilizamos en conjunto con los *vectores* y *variables*.

### 4.2.2 Vectores y variables

Un vector es el tipo de objeto más sencillo de R. Un vector es esencialmente un conjunto de elementos (números, nombres, etc.), que agrupados nos permite realizar operaciones de forma más sencilla. Para definir un vector utilizamos la función `c()`. Siguiendo el ejemplo anterior: 

`c(5,11,2,7,8)`

Un vector es más útil cuando le ponemos un nombre, es decir, *cuando lo convertimos en una variable*. Esto es porque es más fácil referirnos al nombre del conjunto (variable), que escribir todos los números cada vez que los necesitemos. Por ejemplo, pongamos el nombre "a" para definir nuestra variable de 4 numeros:

`a <- c(5,11,2,7,8)`

Generalmente, los vectores y las variables los utilizamos en el contexto de una función cuando queremos que sean un elemento más dentro de muchos otros. Imagina que ahora tenemos una nueva variable "b" con 4 nuevos números:

`b <- c(12,4,10,6)`

Si quisieras usar la función `sum()` podrías meter uno a uno los números de los vectores y obtener así la suma. O si no, puedes simplemente incluir "a" y "b" dentro de la función, y así sumar sus elementos:

`sum(a,b)`

Podemos aprovechar y obtener la media de cada variable:

`mean(a)`

Como puedes ver, usar variables puede facilitar nuestro trabajo cuando trabajemos con una función. Esto se hace más evidente cuando los vectores o variables tiene más elementos.

Además de `sum()` y `mean()` existen muchísimas más funciones por defecto ya incluidas en R y que nos ayudan a calcular/crear prácticamente cualquier cosa ([aquí](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjv2vqB9syBAxUkTaQEHe0VBYoQFnoECBQQAQ&url=https%3A%2F%2Fraw.githubusercontent.com%2Frstudio%2Fcheatsheets%2Fmain%2Ftranslations%2Fspanish%2Fbase-r_es.pdf&usg=AOvVaw3vYU2o5apla4SkYUTEEfgn&opi=89978449) puedes consultar algunas de ellas y cómo usarlas). Además, tú puedes crear también tus propias funciones para resolver problemas específicos que puedas tener. 

## 4.3 ¿Cómo resolver los ejercicios en R de la asignatura?

Seguramente habrás notado que estos apuntes de la asignatura vienen acompañados de algunas figuras o imágenes que ayudar a ilustrar los conceptos que han sido presentados. Sin embargo, ¡cada una de esas figuras fue construída utilizando R! Esto significa que si modificamos los parámetros del código que las producen podríamos observar, por ejemplo, cómo cambia una distribución si modificamos la media o la desviación típica.

Para facilitar la accesabilidad, y poder utilizar R sin tener que descargar e instalar programas (con los riesgos que ello conlleva), he adaptado esta página web de tal forma que podamos editar directamente el código R que construye las figuras.

Para activar esta funcionalidad deberás seguir los siguientes pasos:

1. Hacer clic en el "cohete" localizado en la parte superior de la página web y seleccionar la opción *Live Code*. Esto iniciará una serie de procesos remotos (básicamente, conectarse con un ordenador que ejecutará el código). Si lo haces por primera vez (o si ha pasado mucho tiempo desde la última vez) esto puede tardar unos 5-10 minutos. El proceso habrá terminado cuando veas en la parte superior de la página el mensaje: "Launching from mybinder.org: **_ready_**".

2. En cada Figura verás un botón desplegable, que al hacer clic en él, muestra una caja con el código que construye esa figura. Si has seguido el paso 1. verás también 3 botones: *run*, *restart* y *restart & run all*. De estos tres, el que más nos importa es el botón de **_run_** que ejecutará el código presente en la caja.   

3. Puedes ejecutar el código y obtener la imagen original de los apuntes. Sin embargo, y esto lo interesante, puedes modificar alguno de los elementos del código y explorar cómo eso afecta la visualización resultante. Para saber qué elementos puedes cambiar, verás que he puesto un comentario encima o al final de cada línea (seguido por el símbolo #), indicando en pocas palabras lo que hace esa línea. Así, tendrás una guía sobre qué elementos cambiar y pensar sobre cuáles serán los posibles efectos de ellos.

Intenta seguir estos pasos con el siguiente ejemplo:

```{code-cell} ir
:tags: ["hide-input"]
# vamos a crear una variable "datos" que contenga un vector con 10 números que representan la edad de 10 participantes
datos <- c(25, 30, 35, 40, 45, 50, 55, 60, 65, 70)

# con la siguiente función podremos dibujar una gráfica que de dibuje un histograma con los elementos de la variable "datos" y sobre el eje horizontal describimos que estos datos hacen referencia a la "Edad" de los participantes
hist(datos, xlab = "Edad")

# verás que el histograma resultante es uniforme (barras con el mismo número de elementos o altura). Edita la variable "datos" de forma que el histograma adquiera una forma de distribución normal (o de campana de Gauss)
```

```{code-cell} ir
:tags: ["hide-input"]

library(learnr)

question("What number is the letter A in the English alphabet?",
  answer("8"),
  answer("14"),
  answer("1", correct = TRUE),
  answer("23")
)
```

```{code-cell} ipython3
note = "Python syntax highlighting"
print(note)
```
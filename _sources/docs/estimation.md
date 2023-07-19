---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: R
  language: R
  name: ir
---

(estimation)=

# Estimación{#estimation}

Al comienzo del capítulo inicial, vimos la distinción que existe entre la *estadística descriptiva* y la *estadística inferencial*. El papel de la estadística descriptiva es resumir de manera concisa lo que *ya sabemos*. Por otro lado, el propósito de la estadística inferencial es “aprender lo que no sabemos a partir de lo que hacemos”. Ahora que tenemos cierto conocimiento sobre la teoría de la probabilidad, podemos pensar en el problema de la inferencia estadística. ¿Qué tipo de información nos gustaría conocer o aprender? ¿Y cómo lo aprendemos? Estas son las preguntas que se encuentran en el corazón de la estadística inferencial y tradicionalmente se dividen en dos “grandes ideas”: la estimación y la prueba o contraste de hipótesis. El objetivo de este capítulo es presentar la primera de estas grandes ideas, la teoría de la estimación. Pero antes, hablaré sobre la teoría del muestreo, ya que la teoría de la estimación no tiene sentido hasta que no se comprende el muestreo. Como consecuencia, este capítulo se divide en dos partes, las secciones \@ref(srs) a \@ref(samplesandclt) se centran en la teoría del muestreo, y las secciones \@ref(pointestimates) y \@ref(ci) hacen uso de esa teoría del muestreo para discutir cómo piensan los estadísticos sobre la estimación.
 
---

## Muestras, poblaciones y muestreo{#srs}

Antes hemos hablado sobre el proceso de inducción inferencial, donde recalcamos que *todo* aprendizaje (o aquello que queremos llegar a conocer) requiere que hagamos suposiciones. Aceptando que esto es cierto, hemos de aceptar algunas suposiciones generales sobre los datos que hemos adquirido para poder utilizarlos. Aquí es donde entra en juego la **_teoría del muestreo_**. Si la teoría de la probabilidad representa los cimientos sobre los que se construye toda la teoría estadística, la teoría del muestreo es el marco alrededor del cual se puede construir el resto de la casa. La teoría del muestreo juega un papel muy importante en la especificación de los supuestos en los que se basan sus inferencias estadísticas. Y para hablar sobre "hacer inferencias" de la forma en que los estadísticos lo piensan, debemos ser un poco más explícitos acerca de *qué* es lo que estamos extrayendo  (la muestra) y *sobre qué* es de lo que estamos haciendo inferencias (la población).

En casi todas las situaciones de interés, lo que tenemos a nuestra disposición como investigadores es una *muestra* de datos. Podríamos, por ejemplo, haber realizado un experimento con un cierto número de participantes; una empresa de encuestas podría haber telefoneado a algunas personas para hacer preguntas sobre las intenciones de voto, etc. Independientemente de cual sea el caso, el conjunto de datos disponibles que tengamos es finito e incompleto. No podemos conseguir que todas las personas del mundo realicen nuestro experimento; una empresa de encuestas no tiene el tiempo ni el dinero para llamar a todos los votantes del país, etc. Para la estadística descriptiva esta muestra es lo único que importa. Con la estadística inferencial daremos un paso más allá. 

---

### Definición de una población{#pop}

Una muestra es una cosa muy concreta. Puedes abrir un archivo de Excel y ahí podrás encontrar los datos de una muestra. Una **_población_**, por otro lado, es una idea más abstracta. Se refiere al conjunto de todas las personas posibles, o todas las observaciones posibles, sobre las que desea sacar conclusiones y, en general, es *mucho* más grande que la muestra. En un mundo ideal, el investigador comenzaría el estudio con una idea clara de cuál es la población de interés, ya que el proceso de diseñar un estudio y probar una hipótesis sobre los datos que produce depende de la población sobre la que se quiere hacer afirmaciones. Sin embargo, en la práctica esto no sucede siempre: por lo general, el investigador tiene una idea bastante vaga de lo que es la población y diseña el estudio lo mejor que puede sobre esa base.

A veces es fácil indicar cuál es la población de interés. En el ejemplo de la "empresa de encuestas" que vimos en el capítulo anterior, la población consistía en todos los votantes inscritos en un momento del estudio: varios millones de personas. En cambio, la muestra fue un conjunto de 1,000 personas que pertenecen todas a esa población. Sin embargo, en la mayoría de los casos, definir esta muestra/población no es tan fácil. En estudios o experimentos con seres humanos, determinar la población de interés es un poco más complicado. Supongamos que realizo un experimento con 100 estudiantes de pregrado que representan mi muestra. Mi objetivo es, por ejemplo, intentar aprender algo sobre cómo una intervención educativa modifica la dinámica de una clase. Tomando en cuento a la muestra que tenemos, ¿cuál de las siguientes opciones contará como "la población"?:

- ¿Todos los estudiantes de educación de la Universidad de Navarra?      
- ¿Estudiantes de grado en educación en general, de cualquier parte del mundo?      
- ¿Españoles vivos actualmente?      
- ¿Españoles de edades similares a las de mi muestra?
- ¿Hispanoparlantes?
- ¿Cualquier persona viva actualmente?      
- ¿Cualquier ser humano, pasado, presente o futuro?      

Cada una de estas opciones define un grupo real de personas, las cuales podrían ser todas de interés para mí como investigador en educación, y no es tan obvio cuál debería ser la verdadera población de interés. 

---

### Muestras aleatorias simples

```{code-cell} ir
:tags: ["remove-cell"]
knitr::include_graphics(file.path("img/srs1.png"))
```
`Figura 1.1 Muestreo aleatorio simple *sin* reemplazo de una población finita.`

Independientemente de cómo definamos a una población, la clave es que la muestra es un subgrupo de esa población, y nuestro objetivo es utilizar nuestro conocimiento de la muestra para hacer inferencias sobre las propiedades de la población. La relación que exista entre los dos dependerá del *procedimiento* mediante el cual se seleccionó la muestra. Este procedimiento se conoce como **_método de muestreo_** y es importante comprender su importancia.

Pongamos un ejemplo sencillo. Imaginemos que tenemos una bolsa que contiene 10 fichas. Cada ficha tiene una letra única impresa, con la que la podemos distinguir de entre las otras 10 fichas. Las fichas vienen en dos colores, blanco y negro. Este conjunto de fichas es la población de interés y se muestra gráficamente a la izquierda de la Figura \@ref(fig:srs1). Como podrás ver en la imagen, tenemos 4 fichas negras y 6 fichas blancas, pero recuerda que en la vida real esto no lo sabríamos a menos que miráramos en la bolsa. Ahora imagina que realizas el siguiente "experimento": agitas la bolsa, cierras los ojos y sacas 4 fichas sin devolver ninguna de ellas a la bolsa. Primero sale la ficha $a$ (negra), seguida de la ficha $c$ (blanca), luego la $j$ (blanca) y finalmente la ficha $b$ (negra). Una vez extraídas 4 fichas, podrás volver a poner todas las fichas en la bolsa y repetir el experimento, como se muestra en el lado derecho de la Figura \@ref(fig:srs1). Cada vez que repites el experimento obtienes resultados diferentes, pero el procedimiento es idéntico en cada caso. El hecho de que el mismo procedimiento pueda dar lugar a resultados diferentes cada vez, lo define como un proceso *aleatorio*. Y debido a que hemos agitado la bolsa antes de sacar las fichas, parece razonable pensar que todas las fichas tienen las mismas posibilidades de ser seleccionadas. Un procedimiento en el que todos los miembros de la población tienen las mismas posibilidades de ser seleccionados se denomina **_muestra aleatoria simple_**. El hecho de que se *no* se devuelvan las fichas a la bolsa después de salir, significa que no podremos observar la misma ficha dos veces, y en tales casos se dice que ha habido un muestreo **_sin reemplazo_**.

Para comprender la importancia del procedimiento de muestreo, consideremos ahora una forma alternativa en la que podría haberse realizado el experimento. Supongamos que mi sobrino de 3 años coge la bolsa y decide sacar las cuatro fichas negras (le gusta el color negro) sin devolverlas la bolsa. Este esquema de muestreo *sesgado* se muestra en la Figura \@ref(fig:brs). Ahora considera el valor que tiene obtener una muestra con 4 fichas negras y 0 fichas blancas siguiendo el procedimiento de mi sobrino. Vemos pues, como el valor dependerá mucho del método de muestreo. Si sabemos que el método de muestreo está sesgado para seleccionar únicamente fichas negras, entonces una muestra que consta únicamente de fichas negras no dice mucho sobre nuestra población de fichas. Por esta razón, los estadísticos prefieren que un conjunto de datos provenga de una muestra aleatoria simple, ya que facilita *mucho* el análisis de los datos.

```{code-cell} ir
:tags: ["remove-cell"]
knitr::include_graphics(file.path("img/brs.png"))
```
`Figura 1.2 Muestreo sesgado sin reemplazo de una población finita.`

```{code-cell} ir
:tags: ["remove-cell"]
knitr::include_graphics(file.path("img/srs2.png"))
```
`Figura 1.2 Muestreo aleatorio simple *con* reemplazo de una población finita.`

Vale la pena mencionar un tercer procedimiento. Esta vez cerramos los ojos, agitamos la bolsa y sacamos una ficha. Sin embargo, esta vez registramos la observación y luego volvemos a poner la ficha dentro de la bolsa. Nuevamente, cerramos los ojos, agitamos la bolsa y sacamos otra ficha. Repetimos este procedimiento hasta que tengamos 4 fichas. Los conjuntos de datos que hemos generado de esta manera siguen siendo muestras aleatorias simples, pero debido a que volvemos a meter las fichas dentro de la bolsa inmediatamente después de haberlas sacado, se denomina como una muestra **_con reemplazo_**. La diferencia entre este caso y el primero es que es posible observar al mismo elemento de la población varias veces (en este caso la misma ficha), tal como se ilustra en la Figura \@ref(fig:srs2).

Por lo general, la mayoría de los experimentos que veamos en ciencias de la educación tienden a tomar muestras sin reemplazo, ya que la misma persona no puede participar en el experimento dos veces. Sin embargo, una gran parte de la teoría estadística se basa en el supuesto de que los datos surgen de una muestra aleatoria simple *con* reemplazo. En la vida real, esto rara vez importa. Si la población de interés es grande, la diferencia entre el muestreo con y sin reemplazo es demasiado pequeña como para preocuparnos. Sin embargo, la diferencia que existe entre muestras aleatorias simples y muestras sesgadas no es algo no es algo que podemos ignorar tan facilmente.


### La mayoría de las muestras no son muestras aleatorias simples

Si miras la lista anterior de posibles poblaciones, te darás cuenta que es casi imposible obtener una muestra aleatoria simple de la mayoría de esas poblaciones de interés. Cuando hacemos experimentos con estudiantes universitarios, el obtener una verdadera muestra aleatoria de estos estudiantes los podemos considerar como un milagro menor, aunque al final se trate de una población muy específica a partir de la cual generalizar. Mencionaré brevemente algunos de los otros tipos de muestreo que existen y que solemos encontrar con frecuencia:

- *Muestreo estratificado*. Supongamos que tu población está (o puede estar) dividida en varias subpoblaciones o *estratos* diferentes. Quizás sea porque estás realizando un estudio en varios paises diferentes, por ejemplo. En lugar de intentar tomar una muestra aleatoria de toda la población en su conjunto, recolectamos una muestra aleatoria de cada una de las subpoblaciones o estratos. El muestreo estratificado suele ser más fácil de llevar a cabo que el muestreo aleatorio simple, especialmente cuando la población ya está dividida en los distintos estratos. También puede ser más eficiente que el muestreo aleatorio simple, especialmente cuando algunas de las subpoblaciones son raras o poco frecuentes. Por ejemplo, en el estudio de la esquizofrenia, resulta más sencillo dividir la población en dos estratos (con-esquizofrenia y sin-esquizofrenia) y adquirir una muestra de cada grupo. Si seleccionaramos personas al azar, obtendríamos tan pocas personas con esquizofrenia en la muestra que el estudio resultaría inútil. 

- *Muestreo de bola de nieve*. Es una técnica que es especialmente útil cuando se toman muestras de una población "oculta" o de difícil acceso, y es especialmente común en las ciencias sociales. Por ejemplo, supongamos que los investigadores quieren realizar una encuesta de opinión a personas VIH positivo. Es posible que el equipo de investigación solo tenga los datos de contacto de algunas personas VIH positivo, por lo que la encuesta comienza pidiéndoles a esas personas que participen (etapa 1). Al final de la encuesta, se pide a los participantes que proporcionen los datos de contacto de otras personas que podrían querer participar. En la etapa 2, se encuesta a estos nuevos contactos. El proceso continúa hasta que los investigadores obtengan datos suficientes. La gran ventaja del muestreo de bola de nieve es que es capaz de proporcionar datos en situaciones que de otro modo serían imposibles de obtener. Desde el punto de vista estadístico, la principal desventaja es que la muestra es altamente no aleatoria y no aleatoria en formas que son difíciles de abordar. 

- *Muestreo de conveniencia*. En este tipo de muestreo las muestras se eligen de una forma conveniente para el investigador, sin que exista una selección al azar a partir de la población de interés. El muestreo de bola de nieve es un tipo de muestreo de conveniencia, pero hay muchos otros. Un ejemplo son los estudios que se basan en estudiantes de universitarios. Estas muestras generalmente no son aleatorias desde dos puntos de vista: en primer lugar, depender de una muestra de estudiantes universitarios significa automáticamente que estos datos están restringidos a una sola subpoblación. En segundo lugar, los estudiantes suelen elegir los estudios en los que participan, por lo que la muestra es un subconjunto de estudiantes autoseleccionado, no un subconjunto seleccionado al azar. En general, la mayoría de los estudios incluyen muestras de conveniencia de una forma u otra. A veces, puede suponer una limitación en la interpretación de los resultados, pero no siempre.


### ¿Cuánto importa si no se tiene una muestra aleatoria simple?

Hemos visto que en muchos casos no es posible recolectar muestras aleatorias simples. ¿Eso qué impacto tiene? Un ejemplo de ese impacto lo podemos apreciar con la diferencia que existe entre las Figuras \@ref(fig:srs1) y \@ref(fig:brs). Sin embargo, no es tan malo como parece. Algunos tipos de muestras sesgadas no representan ningún problema. Por ejemplo, cuando utilizamos el muestreo estratificado, realmente sabemos *cuál* es el sesgo ya que lo hemos creado deliberadamente, con la intención de *aumentar* la efectividad de su estudio, y existen técnicas estadísticas que podemos utilizar para ajustar estos sesgos que hemos introducido. En estos casos, por lo tanto, no tenemos un problema.

Sin embargo, es importante recordar que el muestreo aleatorio es un medio para un fin, no el fin en sí mismo. Supongamos que recolectamos una muestra de conveniencia y, como tal, podemos asumir que está sesgada. Un sesgo en el método de muestreo solo es un problema si nos hace sacar conclusiones equivocadas. Desde esta perspectiva, podemos afirmar que no necesitamos que la muestra sea aleatoria en *todos* los aspectos: necesitamos que sea aleatoria con respecto al fenómeno de interés que buscamos estudiar. Supongamos que estoy haciendo un estudio sobre la capacidad de atención sostenida en niños de 6 años. En el estudio 1, tengo la capacidad de tomar muestras al azar de todos los niños de 6 años del mundo actualmente vivos, con una pequeña excepción: sólo puedo incluir niños nacidos en lunes. En el estudio 2, puedo tomar una muestra al azar de la población española. Con estos estudios quiero generalizar mis resultados a la población de todos los niños de 6 años. ¿Qué estudio es mejor? La respuesta, obviamente, es el estudio 1. ¿Por qué? Porque no tenemos ninguna razón para pensar que “nacer en lunes” influye en la capacidad de atención sostenida. Por otro lado, puedo pensar en varias razones por las que “ser español” podría ser importante. España es un país rico e industrializado con un sistema educativo muy desarrollado. Las personas que crecieron con este sistema habrán tenido experiencias de vida mucho más similares a las experiencias de vida de las personas que diseñaron las pruebas de capacidad de atención sostenida. Esta experiencia compartida podría traducirse fácilmente en creencias similares sobre cómo se debe "realizar una prueba", entre otras razones. Este tipo de características son importantes y podrían, por ejemplo, llevar a una imagen engañosa de lo que es la capacidad atención sostenida.

Existe un reflexión clave oculta en esta discusión. Al diseñar estudios, es importante pensar en la población de interés y en esforzarse por elegir un método de muestreo que sea apropiado para esa población. En la práctica, muchas veces nos veremos obligados a utilizar una "muestra de conveniencia" (por ejemplo, estudiantes de unos pocos centros), pero deberíamos, al menos, dedicar un tiempo a pensar en los riesgos e implicaciones de esta práctica.

### Parámetros poblacionales y estadísticos muestrales

Hasta ahora hemos estado hablando de poblaciones como lo haría un científico. Para un educador, una población puede ser un grupo de niños. Para un ecologista, una población puede ser un grupo de osos. En la mayoría de los casos, las poblaciones son cosas concretas que realmente existen en el mundo real. Los estadísticos, sin embargo, tienen un interés dual. Por un lado, *están* interesados en los datos del mundo real de la misma forma que los científicos. Por otro lado, también operan en el ámbito de la abstracción pura como lo hacen los matemáticos. En consecuencia, la teoría estadística puede ser un poco abstracta cuando define una población. Para ello, los estadísticos operacionalizan el concepto de "población" en términos de objetos matemáticos los cuales ya conocemos: se llaman distribuciones de probabilidad.

La idea es muy simple. Digamos que estamos hablando (otra vez) de puntajes de coeficiente intelectual (CI). Para un educador, la población de interés es un grupo de humanos reales que tienen puntajes de CI. Un estadístico “simplifica” esto al definir operativamente a la población como la distribución de probabilidad representada en la Figura \@ref(fig:IQdista). Las pruebas de CI están *diseñadas* de tal forma que la media sea 100, que la desviación estándar sea 15 y que la distribución de los puntajes sea normal. Estos valores se denominan **_parámetros poblacionales_** porque son característicos de toda la población. Es decir, decimos que la media de la población $\mu$ es 100, y la desviación estándar de la población $\sigma$ es 15.

```{code-cell} ir
:tags: ["hide-input"]
estImg <- list()
emphCol <- rgb(0,0,1)
emphColLight <- rgb(.5,.5,1)
emphGrey <- grey(.5)

colour <- TRUE

	width <- 4.5
	height <- 4.5
	
	# plot
	x <- 60:140
	y <- dnorm(x,100,15)
	plot(x,y,lwd=3,type="l",col=ifelse(colour,emphCol,"black"),
		xlab="CI", ylab="Densidad de probabilidad",frame.plot=FALSE
	)
```


---

```{code-cell} r
:tags: ["remove-cell"]
```

```{code-cell} ir
:tags: ["hide-input"]
```

---

## Resumen

 
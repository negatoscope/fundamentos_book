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

(hypothesis)=

# 3 Contraste de hipótesis

En la Unidad 2 discutimos sobre las ideas que existen detrás del proceso de estimación, que es una de las "grandes ideas" de la estadística inferencial. Ahora toca poner nuestra atención en la otra gran idea, que es el *contraste de hipótesis*. En su forma más abstracta, el contraste de hipótesis consiste en una idea muy sencilla: un investigador/a tiene una teoría sobre el mundo, y quiere determinar si los datos que tiene apoyan o no su teoría. A pesar de su simplicidad, en el contraste de hipótesis los detalles pueden ser complejos, razón por la que muchos piensan que la teoría sobre el contraste de hipótesis es la parte más frustrante en estadística. Esta tercera Unidad seguirá la siguiente estructura. Primero, comenzaremos con una descripción -iremos un poco al detalle- sobre cómo funciona el contraste de hipótesis, utilizando un ejemplo que emplearemos una y otra vez con el objetivo de entender como se "construye" un test de hipótesis. Enseguida, revisaremos cuáles son algunos de los dogmas, reglas y "herejías" que rodean a la teoría del contraste de hipótesis. 
 
---

## Una colección de hipótesis (en plural)

Para ilustrar algunos de los conceptos sobre el contraste de hipótesis vamos a utilizar como referencia una línea de investigación en psicología que fue muy popular hace algunos años y nuevamente recientemente por todo lo que prometía y que finalmente acabo por ser desmentido (aunque a día de hoy, hay algunos que todavía se dedican a ello). Me refiero al estudio de la percepción extrasensorial (PES), conocido coloquialmente como el "sexto sentido".

Supongamos que la Asociación para las Artes Oscuras nos ha dado financiación para hacer el experimento definitivo que nos permitirá decidir de una vez por todos si la PES es real o no. Para empezar realizaremos el experimento más sencillo de la serie. En este experimento cada participante se sienta en una mesa, donde le es mostrada una tarjeta por parte del experimentador. La tarjeta es negra por un lado y blanca por el otro. El experimentado retira la tarjeta y y se la lleva a una habitación adyacente. En esa habitación hay otra mesa, y sobre ella, el experimentador coloca la tarjeta mostrando alguno de los dos lados complementamente al azar. Entonces, un segundo experimentador entra en la habitación donde está el participante y le pide que diga qué lado de la tarjeta está boca arriba, negro o blanco. El participante sólo tiene una oportunidad. En ningún momento vuelve a tener contacto con el primer experimentador que se llevado la tarjeta momentos antes. Así, los datos que obtenemos son bastante simples. Hemos preguntado a un número $N$ de personas sobre el color de la tarjeta, y algún número $X$ de ellos contestará correctamente. Ahora imaginemos, que esta prueba la hemos hecho a $N = 100$ personas, de las cuales $X = 62$ han contestado correctamente... un número sorprendemente alto (si fuera completamente al azar habríamos de esperar sólo un 50%, es decir 50 respuestas correctas). ¿Consideras este resultado como prueba definitiva de que la PES es real y existe? Es en este tipo de casos cuando los tests de hipótesis son útiles. Sin embargo, para hablar de *tests* de hipótesis, primero hemos de tener claro qué es una hipótesis. 

---

### Hipótesis de investigación vs. hipótesis estadísticas

La primera distinción que tenemos que tener clara es aquella entra las hipótesis de investigación y las hipótesis estadísticas. En nuestro estudio la PES, mi objetivo final es demostrar que el "sexto sentido" *sí existe*. Para ello, tengo un objetivo de investigación claro: descubrir evidencia sobre la existencia de la PES. En otros escenarios, podría ser un poco más neutral, por ejemplo diciendo que mi objetivo es saber el "sexto sentido" existe *o no*. Independientemente de cuál sea mi intención, lo que quiero dejar claro es que una hipótesis de investigación implica hacer una afirmación científica sustantiva y comprobable. En el caso de la Psicología, la hipótesis de investigación serán fundamentalmente sobre constructos psicológicos; en Educación las hipótesis deben de tender a resolver preguntas de cualquiera de sus distintas sub-áreas. Las siguientes son algunos ejemplos de **_hipótesis de investigación_**:

- *El uso de móvil en clase reduce la habilidad de prestar atención en clase.* Esta es una afirmación sobre la relación causal que existe entre dos conceptos (uso de móvil afecta a la atención en clase y no al revés).
- *El uso de móvil está asociado con la nota obtenida al final del curso.* Esta afirmación también implica una relación, aunque este caso la conexión entre ambas ideas es correlacional y no causal.
- *El uso de móvil es una pérdida de tiempo*. Esta hipótesis tiene una implicación diferente a las dos anteriores: no plantea una relación entre las dos ideas, sino que pretende hacer una afirmación ontológica sobre el uso de móvil (es una pérdida de tiempo). Probar esta hipótesis es posible, pero no es tan fácil como en las afirmaciones previas. Por ejemplo, ¿qué es "una pérdida de tiempo"? ¿Cómo la definimos? ¿Cómo la medimos? Si podemos responder a estar preguntas, quizás podamos responder también a la afirmación original. 

Volviendo a la PES, si lo pensamos bien, la hipótesis de investigación que he planteado no es muy concisa. He dicho que pretendo demostrar que la PES *existe*, pero esto no describe qué es la *existencia*. Quizás sea más fácil si restrinjo mi hipótesis de investigación a algo como "quiero demostrar que algunas personas tienen poderes adivinatorios". Faltaría definir qué personas, o qué son y cómo se miden los poderes adivinatorios, pero al menos ya hemos dado un primer paso. 

Sin embargo, es importante mencionar que hay algunas cosas que no cuentan como hipótesis de investigación demostrables:

- *Lisboa es increíble.* Aunque es verdad que la capital portuguesa es una ciudad que todos tenemos que visitar, esa afirmación es muy vaga para funcionar como una hipótesis de investigación. Para empezar, tendríamos que *operacionalizar* o definir mejor sus elementos: ¿Qué es Lisboa? ¿Su gente, sus tradiciones, su superficie, su arquitectura, todo? ¿Qué significa que alguna de estas cosas sea "increíble"? Es muy posible que ante conceptos como estos nos equivoquemos, o que simplemente no podamos *operacionalizarlos*.
- *Existen una tetera tan pequeña que no puede ser vista con telescopios que orbita alrededor del sol.* Este es un ejemplo (absurdo) de una afirmación infalsificable -que no se puede demostrar como falsa-. Como no tenemos herramientas que nos permitan ver esa tetera, no podemos decir que sea falso que exista una tetera girando alrededor del sol. No hay alternativa, por lo tanto, no puede ser un hipótesis de investigación. 
- *Más alumnos responderán que SI al ítem 3 de mi cuestionario, que NO.* Esta afirmación no es una hipótesis de investigación porque hace una referencia directa a los datos obtenidos, y no su significado (en este caso, del ítem 3). Sin embargo, esto se parece más a otro tipo de hipótesis que veremos a continuación.

Como habrás podido comprobar, las hipótesis de investigación pueden ser confusas aunque siempre son afirmaciones *científicas*. Sin embargo, las **_hipótesis estadísticas_** no son lo uno ni lo otro. Las hipótesis estadísticas deben ser matemáticamente precisas y deben corresponderse con afirmaciones específicas sobre las características de aquello que ha de generar los datos (en nuestro caso, casi siempre, "los participantes"). La intención es que las hipótesis estadísticas tengan una relación muy clara con la hipótesis de investigación planteada previamente. Por ejemplo, en mi estudio de la PES, mi hipótesis de investigación es que algunas personas tienen poderes adivinatorios. Lo que tengo que hacer ahora es "traducirla" a una idea o frase que describa cómo se generan estos datos. Pensemos un momento cómo sería esta idea. Yo estoy interesado en saber cuantas personas del total contestan correctamente a mi pregunta, es decir una probabilidad $P(\mbox{"correcto"})$. Vamos a usar la letra griega $\theta$ (theta) para referirnos a esta probabilidad. Con esto, podríamos plantear alguna de las siguientes hipótesis de investigación: 

- Supongo que la PES no existe (y me experimento está bien diseñado), entonces estarán adivinando. Por lo tanto, esperaría que acertaran la mitad de las veces, por lo que mi hipótesis estadística sería que la probabilidad de escoger correctamente es de $\theta = 0.5$.
- Supongo que la PES existe y los participantes pueden ver la tarjeta. Si esto es verdad, los participantes acertarán *más* de la mitad de las veces. Por lo tanto la probabilidad de escoger correctamente es de $\theta > 0.5$.
- Supongo que la PES existe, pero una vez que los participantes han contestado yo le doy la vuelta a la tarjeta otra vez. Si esto fuese así, esperaría que los participantes acertasen menos del 50% de las veces. Por lo tanto, la hipótesis estadística sería $\theta < 0.5$.
- Supongo que la PES existe, pero no tengo idea si los participantes están viendo el color correcto o no. En este caso, la única afirmación que puedo hacer es que la probailidad de escoger correctamente *no* es el 50% (es decir, puede ser más o menos). Esto correspondería con la hipótesis de estadística $\theta \neq 0.5$.

Todas estas afirmaciones son ejemplos de hipótesis estadísticas porque son declaraciones sobre un parámetros de una poblaciones (respuestas de participantes) relacionado con mi experimento (conocer o no el color de la tarjeta).

Lo que espero haber dejado claro es que al intentar construir un test de hipótesis estadísticas tiene que considerar dos tipos de hipótesis. Una hipótesis de investigación (una afirmación sobre algún fenómeno observable) que se corresponda con una hipótesis estadística (una afirmación matemática sobre la población que genera los datos). En nuestro ejemplo estos podrían ser: 

```{code-cell} ir
:tags: ["remove-cell"]
knitr::kable(data.frame(stringsAsFactors=FALSE,
   `Dan's.research.hypothesis` = c("ESP.exists"),
                      `Dan's.statistical.hypothesis` = c("$\\theta \\neq 0.5$")
))
```
|Hipótesis.de.investigación |Hipótesis.estadísticathesis  |
|:--------------------------|:----------------------------|
|PES.existe                 |$\theta \neq 0.5$            |

Un aspecto fundamente que tienes que reconocer es el siguiente: *un test de hipótesis (estadísticas) es un test de una hipótesis estadística, no de una hipótesis de investigación*. Si un estudio está mal diseñado, el vínculo entre la hipótesis de investigación y la hipótesis estadística se habrá roto. Si en nuestro estudio sobre la PES, por ejemplo, el participante pudiese ver el color de la carta a través del reflejo de una ventana, encontraremos evidencia de que $\theta \neq 0.5$ o incluso que $\theta > 0.5$., sin embargo, como es lógico, eso no nos dirá nada sobre si la PES existe o no (ya que están haciendo "trampa").

---

### Hipótesis nula e hipótesis alternativa

De momento, tenemos una hipótesis de investigación sobre algún fenómeno que yo creo que es así, que se corresponde con una hipótesis estadística que describe cómo se generan los datos que dan lugar a ese fenómeno. Hasta aquí el camino es fácil. Es partir de aquí donde el asunte se volve confuso o contraintuitivo para muchos. Y es que lo que debemos de hacer a continuación es crear una nueva hipótesis estadística (la hipótesis "nula" $H_0$) que corresponda con lo *opuesto* a lo que yo creo, usar casi exclusivamente esta nueva hipótesis, y "deshacernos" de la hipótesis que describe aquello en lo que estamos interesados de verdad (a partir de ahora, la hipótesis "alternativa" $H_1$). En nuestro ejemplo de la PES, la hipótesis nula es que $\theta = 0.5$, que se refiere a lo que esperaríamos si la PES *no* existiese. Mi apuesta, está claro, es que la PES exista, y por lo tanto, la *alternativa* a esta hipótesis nula es que $\theta \neq 0.5$. En pocas palabras, lo que estamos haciendo es dividir los valores posibles de $\theta$ en dos grupos: aquellos que espero que no sean verdad (la nula) y aquellos valores con los que estaría feliz de obtener (la alternativa). Si lo hacemos así, tenemos que saber reconocer que el objetivo de un test de hipótesis *no* es demostrar que la hipótesis alternativa (quizás) sea verdad; el objetivo final es demostrar que la hipótesis nula es (probablemente) falsa. Es justo esto lo que a muchos les parece contraintuitivo.   

Una metáfora que nos puede ayudar a entender mejor este problema, es imaginar que el test de hipótesis es como un juicio penal... *el juicio de la hipótesis nula*. En este caso, la hipótesis nula es la defensa, el investigador es el fiscal y el test de hipótesis es el juez. Como en cualquier juicio, existe la presunción de inocencia: la hipótesis nula es considerada *verdadera* a menos que el investigador consiga demuestrar lo contrario. Así, puedes diseñar el experimento de la forma que más convenga, siempre y cuando maximice la probabilidad de obtener datos que *encausen* o demuestren que la hipótesis nula es falsa. También como en cualquier juicio, existen reglas para el test de hipótesis que hace las veces de juez, y estas reglas están diseñadas para proteger a la hipótesis nula (al igual que un juicio se protege al acusado), con el objetivo de que en el caso de que la hipótesis nula sea verdadera, las probilidades de condenarla injustamente (decir que es falsa) sean lo más bajas posible. Esto es clave, ya que ante un investigador que busca a toda costa demostrar que la hipótesis nula es falsa, *alguien* tenía que protegerla.

---

## Dos tipos de errores

Antes entrar en detalles sobre cómo se construye un test estadístico, es útil entender la filosofía que hay detrás de ellos. Idealmente nos gustaría construir que nunca cometa errores. Desafortunadamente el mundo en el que vivimos en impredecible, por lo que en la práctica esto es no es posible. A veces simplemente es mala (o buena) suerte: por ejemplo, si lanzas una moneda 10 veces y las 10 veces sale cara. Esto parece evidencia contundente de que hay algo raro con esa moneda, pero también sabemos que este escenario es posible en 1 de 1024 intentos en los que lanzamos 10 veces una moneda que sabemos que es justa. En otras palabras, en la vida real hemos de aceptar que *siempre* existe la probabilidad de hacer las cosas mal. En consecuencia, el objetivo detrás de los test de hipótesis estadísticas no es *eliminar* los errores, sino *minimizarlos* lo más posible. 

Aquí debemos ser un poco más preciso al decir a qué nos referimos cuando hablamos de errores. En primer lugar, establezcamos lo obvio: la hipótesis nula o es verdadera, o es falsa; nuestro test *rechazará* la hipótesis nula o la *mantendrá*[^1]. Así, como la tabla a continuación nos indica, después de llevar a cabo un test de hipótesis, alguna de las siguientes cuatro cosas puede haber pasado:

[^1]: Me gustaría hacer un apunte respecto al lenguaje que se utiliza al reportar los resultados de test estadísticos. *Rechazar* la hipótesis nula se refiere a cuando los datos parecen indicar que aquello que nosotros creemos (hipótesis alternativa) es verdadera; *mantener* o *no rechazar* la hipótesis nula nos indica que los datos parecen favorer a la hipótesis nula o que los datos no son concluyentes. Es importante que notes que nunca hablamos sobre si se acepta, mantiene o rechaza la hipótesis alternativa, sólo lo hacemos con la hipótesis nula. 

```{code-cell} ir
:tags: ["remove-cell"]
knitr::kable(data.frame(stringsAsFactors=FALSE,
NANA = c("$H_0$ is true", "$H_0$ is false"),
`retain.$H_0$` = c("correct decision", "error (type II)"),
`reject.$H_0$` = c("error (type I)", "correct decision")
), col.names = c("", "retain $H_0$", "reject $H_0$"))
```
|                    |mantener $H_0$     |rechazar $H_0$     |
|:-------------------|:------------------|:------------------|
|$H_0$ es verdadera  |decisión correcta  |error (tipo I)     |
|$H_0$ es falsa      |error (tipo II)    |decisión correcta  |

Podemos ver que existen *dos* tipos de error diferentes. Si rechazamos la hipótesis nula cuando, de hecho, es verdadera, estamos cometiendo un **_error tipo I_**. Por otro lado, si mantenemos la hipótesis nula cuando, de hecho, es falsa, entonces cometemos un **_error tipo II_**.

¿Recuerdas como antes hemos dicho que los tests de hipótesis son como juicios penales? Un juicio penal requiere que demuestres que el acusado es culpable "más allá de toda duda razonable". Las reglas que rigen el proceso están diseñadas (en teoría, al menos) para asegurar que (casi) es imposible condenar equivocadamente a un acusado que es inocente. Los juicios han sido diseñados de forma que protejan los derechos del acusado: ya lo insinuaba el jurista William Blackstone con su famosa fórmula donde dice que "es mejor que diez personas culpable escapen a que un inocente sufra". Esto significa que en un juicio no se tratan de igual manera los dos tipos de errores... castigar al inocente se percibe como algo mucho peor que dejar a un culpable libre. En un test estadístico pasa algo parecido: el objetivo más importante de un test es *controlar* la probabilidad de cometer errores tipo I, manteniéndolo debajo de una probabilidad predeterminada. Esta probabilidad, que se denota como $\alpha$, es usualmente referida como el **_nivel de significación_** de un test. Por lo tanto, se dice que un test de hipótesis tiene un nivel de significación $\alpha$ si la tasa de error tipo I es menor que $\alpha$.

¿Y qué hay de la tasa de error de tipo II? También estamos interesados en tenerla bajo control, denotando esta probabilidad como by $\beta$. Sin embargo, es mucho más probable que nos encontremos este valor bajo el nombre de **_poder_** estadístico o del test, que es la probabilidad con la que rechazamos la hipótesis nula cuando realmente es falsa, calculada como $1-\beta$. Para tener todo esto en orden, actualicemos la tabla anterior con estos valores:

```{code-cell} ir
:tags: ["remove-cell"]
knitr::kable(data.frame(stringsAsFactors=FALSE,
NANA = c("$H_0$ is true", "$H_0$ is false"),
retain = c("$1-\\alpha$ (probability of correct retention)",
                   "$\\beta$ (type II error rate)"),
reject = c("$\\alpha$ (type I error rate)",
                   "$1-\\beta$  (power of the test)")), col.names=c("", "retain $H_0$", "reject $H_0$")
)

```
|                    |mantener $H_0$                                      |rechazar $H_0$                    |
|:-------------------|:---------------------------------------------------|:---------------------------------|
|$H_0$ es verdadera  |$1-\alpha$ (probabilidad de mantener correctamente) |$\alpha$ (tasa de error tipo I)   |
|$H_0$ es falsa      |$\beta$ (tasa de error tipo II)                     |$1-\beta$  (poder del test)       |

Un "buen" test de hipótesis es aquel que tenga un valor bajo de $\beta$, manteniendo un valor fijo (bajo) de $\alpha$. Por convención, los científicos suelen usar tres nivel distintos de $\alpha$: $.05$, $.01$ y $.001$. Nótese la asimetría aquí... los tests se han diseñado para *asegurar* un nivel bajo de $\alpha$, pero no hay valores correspondientes para $\beta$. Es cierto que nos *gustaría* tener una tasa de error tipo II baja también, y debemos intentar diseñar tests estadísticos que cumplan con ellos, sin embargo, este aspecto es secundario en comparación con la difícil tarea de controlar la tasa de error tipo I. Como Blackstone habría dicho si se hubiese dedicado a la estadística, "es mejor mantener 10 hipótesis nulas falsas que rechazar una sola que sea verdadera". Esta es la "filosofía" de los test estadísticos frecuentistas.

---

## Tests estadísticos y distribuciones muestrales

Llegados a este punto necesitamos concretar cómo es que se construye un test de hipótesis. Para ello, volvamos a nuestro ejemplo sobre la PES. Ignoremos, de momento, los resultados que hayamos podido obtener, y pensemos sobre la estructura del experimento. Sin importar cuáles sean las cifras, la *forma* que tendrán nuestros datos es que $X$ de $N$ personas habrán identificado correctamente el color de la tarjeta. Ahora *supongamos* por un momento que la hipótesis nula es verdadera: la PES no existe y por lo tanto la probabilidad de que alguien escoja el color correcto es exactamente $\theta = 0.5$. ¿Cómo *esperamos* que sean los datos? Como es obvio, esperaríamos que la proporción de personas que den la respuesta correcta sea muy cercana al 50%. O, en términos matemáticos, diríamos que $X/N$ es aproximadamente $0.5$. Es claro que no esperaríamos que esta fracción o porcentaje sea *exactamente* del 50%: si evalúamos a $N=100$ personas y obtenemos que $X = 53$ han contestado correctamente, el resultado parece alinearse con nuestra hipótesis nula. Por otro lado, si  $X = 99$ participantes contestan correctamente, podemos decir con cierta autoridad que la hipótesis nula es falsa. Llegaríamos a la misma conclusión si sólo  $X = 3$ contestan correctamente. Si somos un poco más técnicos lo que esto nos dice es: tenemos una cantidad $X$ que obtenemos al mirar nuestros datos; después de mirar el valor de $X$, tomamos una decisión sobre si la hipótesis es verdadera, o si rechazamos la hipótesis nula en favor de la alternativa. Este número que hemos calculado y que nos sirve como guía en nuestra toma de decisiones le llamamos **_estadístico de contraste_**.

Una vez que hemos calculado nuestro estadístico de contraste, el siguiente paso es establecer precisamente qué valores de este estadístico de contraste nos llevarían a rechazar la hipótesis nula y qué valores a mantenerla. Para poder hacerlo, necesitamos determinas cómo es la **_distribución muestral del estadístico de contraste_** suponiendo que la hipótesis nula es verdadera (recuerda que el concepto de distribuciones muestrales lo revisamos en la Unidad 2). ¿Por qué necesitamos saber esto? Porque es la distribución misma la que nos dirá qué valores de $X$ deberíamos esperar de nuestra hipótesis nula. Por ello, podemos utilizar esta distribución como una herramienta para evaluar qué tanto concuerdan nuestros datos con la hipótesis nula.

```{code-cell} ir
:tags: ["hide-input"]

nhstImg <- list()
emphCol <- rgb(0,0,1)
emphColLight <- rgb(.5,.5,1)
emphGrey <- grey(.5)

eps <- TRUE
colour <- TRUE
	width <- 8
	height <- 5.5
	
	# distribution
	x <- 0:100
	y <- dbinom(x,100,.5)
	
	# plot
	plot(x,y,type="h",lwd=3, col=ifelse(colour,emphCol,"black"),
		xlab="Número de respuestas correctas (X)", ylab="Probabilidad",
		main="Distribución muestral de X si la hipótesis nula es verdadera",
		font.main=1, frame.plot=FALSE
	)
```
`Figura 1.1 La distribución muestral de nuestro estadístico de contraste $X$ cuando la hipótesis nula es verdadera. Para nuestro ejemplo con la PES, esta es una distribución binomial. No es de sorprender que si la hipótesis nula dice que la probabilidad de obtener una respuesta correcta es de $\\theta = .5$, la distribución muestral nos diga que el valor más probable sea 50 (de 100) respuestas correctas. Nota cómo la mayor parte de la probabilidad se encuentra entre 40 y 60`

¿Y cómo sabemos cuál es la distribución muestral de un estadístico de contraste? Este es un paso complicado en el caso de muchos tests de hipótesis, sin embargo, en esta asignatura revisaremos únicamente los tests más básicos (y más utilizados) por lo que será relativamente sencillo. Y si seguimos con el ejemplo de la PES, encontraremos uno de los casos más sencillos. Nuestro parámetro poblacional $\theta$ es la probabilidad de contestar correctamente a la pregunta, y nuestro estadístico de contraste $X$ es la *cuenta* del número de personas que lo han hecho correctamente de un total (tamaño de muestra) $N$. Esto es justo lo que describe la distribución binomial que hemos visto anteriormente. Si quisieramos denotar en este caso que la hipótesis nula predice que $X$ sigue una distribución binomial, lo escribiríamos de la siguiente manera:

$$
X \sim \mbox{Binomial}(\theta,N)
$$

Ya que la hipótesis nula establece que $\theta = 0.5$ y nuestro experimento incluye a $N=100$ personas, ya tenemos la distribución muestral que necesitamos (Figura 1.1). El resultado no nos sorprende: la hipótesis nula que dice que $X=50$ y es 50 el valor más probable, además de saber que lo más seguro es que encontremos un valor entre 40 y 60.

---

## Tomando decisiones

Recapitulemos brevemente. Hemos elegido y construído un estadístico de contraste ($X$) que nos permite afirmar con cierta seguridad que si el valor de $X$ es cercano a $N/2$, entonces podemos mantener la hipótesis nula y si no, podemos rechazarla. La cuestión es la siguiente: exactamente ¿qué valores del estadístico de contraste debemos asociar con la hipótesis nula, y cuáles valores con la hipótesis alternativa? En el estudio de la PES, por ejemplo, observamos un valor de $X=62$. ¿Qué decisión debemos tomar? ¿Forma parte de los valores de la hipótesis nula o de la hipótesis alternativa?

## Regiones críticas y valores críticos

Para a estas preguntas, tenemos que presentar el concepto de **_región crítica_** para el estadístico de contraste $X$. La región crítica de un test se corresponde con los valores de $X$ que nos llevarían a rechazar la hipótesis nula (razón por la que la región crítica a veces es llamada como región de rechazo). ¿Y cómo encontramos esa región crítica? Consideremos lo que ya sabemos:

- $X$ debería ser o muy grande o muy pequeña para poder rechazar la hipótesis nula.
- Si la hipótesis nula es verdadera, la distribución muestral de $X$ es Binomial$(0.5, N)$.
- Si $\alpha =.05$, el valor crítico deberá cubrir un 5\% de esta distribución muestral.

Es importante tener bien claro este último punto: la región crítica representa los valores de $X$ que nos van a permitir rechazar la hipótesis nula, y la distrubución muestral en cuestión describe la probabilidad de que obtengamos un valor particular de $X$ asumiendo que la hipótesis nula es de hecho verdadera. Ahora supongamos que escogemos una región crítica que cubra un 20\% de la distribución muestral, y supongamos que la hipótesis nula es verdadera. ¿Cuál sería la probabilidad de rechazar incorrectamente la hipótesis nula? La respuesta, por supuesto, es del 20\%. Así entonces habremos construído un test que tiene un nivel $\alpha$ de $0.2$. Si quisiéramos un $\alpha = .05$, la región crítica sólo podría cubrir un 5\% de la distribución muestral de nuestro estadístico de contraste.

```{code-cell} ir
:tags: ["hide-input"]
# needed for printing
	width <- 8
	height <- 5.5
	
	setUpPlot <- function() {
		
		plot.new()
		plot.window(xlim=c(0,100),ylim=c(0,.08))
		axis(1)
		title(xlab="Número de respuestas correctas (X)")
		
	}
	
	addDistPlot <- function(x,y,z) {
		
		# colour key
		col.key <- c(
			 grey(.9),
			 ifelse(colour,emphCol,"black")
		)
		
		# plot
		lines(x,y,col=col.key[as.numeric(z)+1],type="h",lwd=3)
		
	}
	
	addArrow <- function(x,h, text) {
		
		arrows(x0 = x[1], y0 = h, x1 = x[2], y1 = h, length = .1)
		lines(c(x[1],x[1]),c(h-.002,h+.002),'type'="l")
		
	}
	
	# distribution
	x <- 0:100
	y <- dbinom(x,100,.5)
	
	# plot 1
	setUpPlot()
	z <- x<=40 | x>=60
	addDistPlot(x,y,z)
	h <- .03
	addArrow(c(40,20),h)
	addArrow(c(60,80),h)	
	text(22,h+.013,"región crítica inferior")
	text(22,h+.007,"(2.5% de la distribución)")
	text(75,h+.013,"región crítica superior")
	text(75,h+.007,"(2.5% de la distribución)")
	title(main="Regiones Críticas para un test de dos colas",font.main=1)
```
`Figura 1.12 Región crítica asociada con el test de hipótesis para el estudio de la PES, con nivel de significancia de $\\alpha = .05$. La figura muestra la distribución muestral de $X$ bajo la hipótesis nula: las barras grises corresponden con los valores de $X$ con los que mantendríamos la hipótesis nula. Las barras negras muestran la región crítica: valores de $X$ con los cuales rechazaríamos la hipótesis nula. Ya que la hipótesis alternativa es de dos colas (contemplamos tanto $\\theta <.5$ como $\\theta >.5$), la región crítica cubre ambos extremos de la distribución. Para asegurar un valor de $\\alpha$ de $.05$, necesitamos que las dos regiones contengan a un 2.5% de la distribución muestral.`

The critical region associated with the hypothesis test for the ESP study, for a hypothesis test with a significance level of $\\alpha = .05$. The plot itself shows the sampling distribution of $X$ under the null hypothesis: the grey bars correspond to those values of $X$ for which we would retain the null hypothesis. The black bars show the critical region: those values of $X$ for which we would reject the null. Because the alternative hypothesis is two sided (i.e., allows both $\\theta <.5$ and $\\theta >.5$), the critical region covers both tails of the distribution. To ensure an $\\alpha$ level of $.05$, we need to ensure that each of the two regions encompasses 2.5% of the sampling distribution.

Como podemos ver, estos tres aspectos resuelven nuestro problema: la región crítica consiste de los *valores más extremos*, mejor conocidos como las **_colas_** de la distribución. Esto queda ilustrado en la Figura 1.2. Por lo tanto, si queremos un $\alpha = .05$, entonces nuestras regiones críticas corresponden con $X \leq 40$ y $X \geq 60$. Esto quiere decir que si el número de personas que "aciertan" está entre 41 y 59 entonces mantenemos la hipótesis nula. Si por el contrario, el número está entre 0 y 40 o entre 60 y 100, entonces podemos rechazar la hipótesis nula. Los número 40 y 60 suelen ser llamados como **_valores críticos_**, ya que definen los límites de la región crítica.

Llegados a este punto, hemos completado nuestro test de hipótesis: (1) hemos escogido un nivel $\alpha$ (p.e., $\alpha = .05$), (2) hemos creado un estadístico de contraste (p.e. $X$) que cumple con su rol de comparar $H_0$ con $H_1$, (3) hemos descifrado la distribución muestral de este estadístico de contraste bajo la suposición de que la hipótesis nula es verdadera (en este caso, binomial o a dos colar) y finalmente (4) hemos calculado la región crítica que produce un nivel $\alpha$ adecuado (0-40 y 60-100). Lo único que nos queda por hacer es calcular el valor del estadístico de contraste para los datos que tenemos ($X = 62$) y luego compararlo con los valores críticos y tomar una decisión. En este caso el estadístico de contraste está calculado -$X = 62$-, y como es mayor que el valor crítico de 60, rechazaríamos la hipótesis nula. En otras palabras, y como encontrarás en cualquier estudio científico, este test de hipótesis ha producido un resultado **_estadísticamente significativo_**[^2].

[^2]: Sólo una observación. En esta frase, la palabra **_signficativo_** no es sinónimo de importancia o relevancia (como lo podríamos entender en español), simplemente se refiere a que el resultado a superado un umbral que ha sido indicado con anterioridad. En este caso, el umbral está determino por nuestro $\alpha = .05$.

### La diferencia entre test de una y dos colas

Antes de continuar, me gustaría señalar un aspecto sobre el test de hipótesis que hemos construído. Si recordamos cuáles son las hipótesis estadísticas que hemos utilizado,

$
\begin{array}{cc}
H_0 : & \theta = .5 \\
H_1 : & \theta \neq .5 
\end{array}
$

veremos que la hipótesis alternativa es la posibilidad de que $\theta < .5$ pero *también* la posibilidad de que $\theta > .5$. Esto tiene sentido que nosotros creemos que la PES puede producir un resultado superior al azar (>50\%) *o* inferior al azar (<50\%). En lenguaje estadístico, esto es un ejemplo de **_test de dos colas_**. Se le llama así porque la hipótesis alternativa cubre el área a ambos *lados* de la hipótesis nula, y como consecuencia, la región crítica del test cubre ambas colas de la distribución muestral (2.5\% a cada lado en caso de $\alpha =.05$), como se muestra en la Figura 1.12.

Sin embargo, no es la única posibilidad. Por ejemplo, también podría darse el caso de que yo crea que la PES produce resultados mejores que el azar. En este caso, mi hipótesis alternativa deberá cubrir unicamente la posibilidad de que $\theta > .5$, y en consecuencia la hipótesis nula ahora se convierte en $\theta \leq .5$:

$
\begin{array}{cc}
H_0 : & \theta \leq .5 \\
H_1 : & \theta > .5 
\end{array}
$

Este es el caso de un **_test de una cola_**, y aquí la región crítica cubre sólo un extremo de la distribución muestral. Esto se ilustra en la Figura 1.13.

```{code-cell} ir
:tags: ["hide-input"]
setUpPlot()
	z <- x>=58
	addDistPlot(x,y,z)
	h <- .03
	addArrow(c(58,80),h)	
	text(75,h+.013,"región crítica")
	text(75,h+.007,"(5% de la distribución)")
	title(main="Región crítica para un test de una cola",font.main=1)
```
`Figura 1.13 Región crítica para un test de una cola. En este caso, la hipótesis alternativa es que $\\theta > .05$, por lo que solo podemos rechazar la hipótesis nula con valores altos de $X$. En consecuencia, la región crítica sólo cubre la parte superior de la distribución muestral; específicamente el 5% superior de la distribución. Compara esto con el test de dos colas.`

## El valor $p$ de un test estadístico

Hasta aquí, parece que hemos completado nuestro test de hipótesis; hemos construído un estadístico de contraste, hemos encontrado cúal es su distribución muestral si la hipótesis nula es verdadera y hemos calculado los valores críticos de delimitan las regiones críticas del test. Sin embargo, he omitido el valor más importante de todos: **_el valor $p$_**. 

### La probabilidad de obtener datos extremos

Si recuerdas, cuando construíamos nuestras regiones críticas, vimos que estas correspondían con las *colas* (los valores extremos) de la distribución muestral. Esto no es una coincidencia: una región crítica adecuada es aquella que se corresponde con los valores menos probables del estadístico de contraste, asumiendo que la hipótesis nula es verdadera. Si esta regla es verdadera, entonces podemos definir al valor-$p$ como **_la probabilidad de observar un valor de estadístico de contraste igual o más extremo que el que hemos obtenido_**. Es decir, si los datos que hemos obtenidos son extremadamente poco probables para nuestra hipótesis nula, pues quizás la hipótesis nula sea incorrecta. 

Para saber qué valores de esta probabilidad -valor-$p$- corresponden con qué valor del estadístico de contraste podemos recurrir a las *tablas de probabilidad* para dicho estadístico de contraste (p.e. $t$, $F$, etc.). Estos valores de probabilidad son siempre los mismos para cada estadístico de contraste ya que están extraídos de una distribución muestral que cumple con ciertos supuestos necesarios (por ejemplo, que los datos se distribuyan de forma normal). Por lo tanto, es muy importante usar la tabla que correcta, ya que un valor de estadístico de contraste puede tener distintas probabilidades en diferentes tablas. 

Ahora que sabemos cuál es una definición correcta del valor-$p$, me gustaría dedicar este párrafo para explicar lo que *no* es un valor-$p$, ya que, como seguro habrás pensado, no es una definición intuitiva y tiende a ser malinterpretada con frecuencia. Muchas veces se entiende -repito, *equivocadamente*- que el valor-$p$ es "la probabilidad de que la hipótesis nula sea verdadera". Aunque es una forma más intuitiva de interpretar este valor, es una aproximación errónea por una razón que nos resultará familiar: (1) los tests de contraste de hipótesis son herramientas frecuentistas, y hemos visto que una aproximación frecuentista a la probabilidad *no* permite asignar probabilidades a la hipótesis nula (recuerda que sólo se asignan probabilidades a la larga, después de muchas repeticiones), sino que la hipótesis nula en cuestión es verdadera o no lo es.

## ¿Cómo reportar los resultados de un test de hipótesis?

Estamos al final del proceso de construcción de nuestro test de hipótesis, y lo único que falta es reportar el resultado final. Para fines de la asignatura, esta conclusión deberá contener 3 elementos:

1. Si el resultado del test estadístico es estadísticamente significativo o no. Esto depende de si se rechaza la hipótesis nula (sí es significativo) o de si se mantiene (no es significativo)
2. El valor-$p$ o si el resultado es mayor o menor al valor $\alpha$ que hemos establecido previamente (usualmente, 0.05).

Por ejemplo, podemos decir algo así como "Nuestro test muestra un resultado estadísticamente significativo, con un valor-$p$ de 0.03". Esto significa que nuestro test de hipótesis rechaza la hipótesis nula, ya que la probabilidad que tenemos de encontrar estos datos asumiendo que la hipótesis nula es verdadera es muy baja, de tan sólo el 3%. 

Compara ese ejemplo con este otro: "Nuestro test muestra un resultado que *no* es estadísticamente significativo, con un valor-$p$ de 0.27". Aquí se nos dice que mantenemos la hipótesis nula (o que no la podemos rechazar) ya que la probabilidad de encontrar estos datos asumiendo que esa hipótesis nula es verdadera es muy alta, del 27%. 

## Resumen

Los tests de hipótesis son uno de los elementos omnipresentes en la teoría estadística. La gran mayoría de los estudios reportan sus resultados utilizando algún tipo de test estadístico. En consecuencia, es casi imposible impartir una clase y aprender sobre los fundamentos de investigación sin incluir una explicación de los tests estadísticos. Estos son algunos de los puntos clave revisados en esta Unidad:

* Hipótesis de investigación e hipótesis estadísticas
* Hipótesis nula e hipótesis alternativa
* Estadísticos de contraste y sus distribuciones muestrales
* Tests estadísticos y el proceso de toma de decisiones
* El valor-$p$ y su importancia

En realidad, esta tercera Unidad no termina aquí: ahora pondremos en práctica lo que hemos aprendido sobre los tests de hipótesis y aplicarlo según los datos que tengamos. Esto será lo que determine si debemos utilizar un test de chi-cuadrada, un test-t o un análisis factorial. Aunque existen muchos otros tipos de tests estadísticos, estos son los más elementales y además, los más frecuentemente utilizados en investigación.

---

 
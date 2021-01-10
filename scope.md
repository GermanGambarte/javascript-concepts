Cuando hacemos referencia a una variable JavaScript va a empezar a buscar su definición en el entorno mas cercano y seguira buscando cada vez en entornos mas lejanos hasta que encuentre un entorno donde la variable esté declarada, cada uno de estos entornos recibe el nombre de **scope**

El scope es lo que le da significado a las variables y además determina el conjunto de variables a las que podemos acceder desde una linea de código. 

El scope en el que va a entrar cada variable depende de como y donde la declaremos y eso es algo que tenemos que decidir nosotros cuando escribimos el código de nuestro programa 

Con "como" me refiero a si la declaramos de la forma antigua, es decir usando **var** 
```
var fruta ='manzana';
```
o con la forma moderna usando **let** y **const**
```
let fruta1 = 'manzana';
const fruta2 = 'banana';
```
Y con "donde" me refiero a si la declaramos de manera libre, es decir fuera de toda función o bloque de código
```
<script>
    var fruta = 'manzana'
</script>
```
O si la declaramos adento de una función
```
<script>
    function comer() {
        var fruta = 'manzana'
    }
</script>
```
O a dentro de un bloque de código, como por ejemplo en un **if** pero solo con let o con const
```
<script>
    function comer() {
        if(true) {
            let fruta = 'manzana'
        }
    }
</script>
```
Decimos que JavaScript tiene un **Scope Léxico** ya que el scope de cada variable se determina leyendo el código del programa sin tener que ejecutarlo, por eso a este modelo tambien se lo conoce como **Scope Estático** 

# Scope

MDN define al scope como el contexto actual de ejecución. El contexto en el que los valores y las expresiones son "visibles" o pueden ser referenciados. Poniendolo palabras esto se entender por el ejemplo cuando decimos "me voy a comer una manzana" o "me voy a dar una vuelta a la manzana", la palabra es la misma, pero el contexto es absolutamente diferente, ese contexto es el scope.

Pongamoslo mas gráfico
```
function comer() {
    var fruta = 'manzana';
    console.log('comiendo' + fruta)
}
function lavar() {
    var fruta = 'banana';
    console.log('lavando' + fruta)
}
```
En el contexto de la primer función cuando queramos hacer referencia a la variable fruta, esta va a tener el valor "manzana". Mientras que en el contexto de la segunda función esta va a tener el valor "banana".

Por eso, de acuerdo a cual sea el contexto actual de ejecución el mismo identificador puede significar una cosa u otra

Ahora, la palabra contexto puede crear un poco de confusión. Los terminos **contexto** y **contexto de ejecución** se parecen mucho, pero son dos cosas distintas.

El contexto es el valor que tiene la variable ***this*** en algún momento de la ejecución. Es decir el objeto que está ejecutando una función.

Cuando hablamos de Scope, hablamos del contexto de ejecución o en otras palabras del entorno, de lo que le da significado a las variables.

## Tipos de Scopes
De acuerdo a como escribamos nuestro código podemos decidir si nuestra variable va a vivir en un **scope global** o en un **scope local**.

Las variables globales pueden ser accedidas desde cualquier lugar de nuestro programa. Mientras que las locales sólo se pueden acceder desde una parte de nuestro programa.

Existen dos subtipos de scope local, **Scope de Función** y **Scope de Bloque**

Si declaramos una variable fuera de toda función o bloque de código, esta va a tener un scope global
```
<script>
    var fruta = 'manzana'
</script>
```
Y no importa si lo hacemos con **var**, **let** o **const**. Lo mismo sucede con las funciones, van a poder ser accedidas en cualquier parte del programa
```
<script>
    var fruta = 'manzana'
</script>

function comer() {

}
```
Si dentro de la función creamos otra variable 
```
function comer() {
    var otraFruta = 'banana';
    console.log('Comiendo ' + otraFruta)
}
```
A esa variable solo se va a poder acceder desde esa función. Si intentamos accederla desde fuera vamos a tener un error de referencia en cuanto esa linea se q  uiera ejecutar.
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var otraFruta = 'banana';
    console.log('Comiendo ' + otraFruta)
}

console.log(otraFruta)
// ↪ ReferenceError: otraFruta is not defined
```


Lo mismo sucede con los parametros de las funciones, si bien no estan declarados con **var**, **let** o **const** esos parametros solo se van a poder acceder desde esa función.

Y por mas que estemos en un bloque de un **if**
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var otraFruta = 'banana';
    if (true) {
        var unaFrutaMas = 'pera';
    }
    console.log('Comiendo ' + otraFruta)
}
```
Como la variable está declarada con **var** por el [hoisting] esta se va a poder acceder sin problemas dentro de todo el cuerpo de la función en donde se encuentra su declaración, si quisieramos podriamos accder a ella desde fuera del **if** donde fue declarada
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var otraFruta = 'banana';
    if (true) {
        var unaFrutaMas = 'pera';
    }
    console.log('Comiendo ' + otraFruta)
    console.log('Comiendo ' + unaFrutaMas)
}
```
Algo similar sucede con el scope de bloque, un bloque de código en JavaScript es toda porción de código que está encerrada entre llaves: {}.

Pude ser el bloque de un **if** o un **else**
```
if (condition) {

} else {

}
```
el de un **while**
```
while (condition) {

}
```
O un ciclo **for**
```
for (inciación; condición; incremento) {

}
```
Y el cuerpo de una función tambien es un bloque de código en si, pero si dentro de esa función creamos in **if** donde inicializamos un variable con **let** o **const** no vamos a poder acceder a ella fuera de ese **if**
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var otraFruta = 'banana';
    if (true) {
        let unaFrutaMas = 'pera';
    }
    console.log('Comiendo ' + otraFruta)
    console.log('Comiendo ' + unaFrutaMas)
    // ↪ ReferenceError: unaFrutaMas is not defined
}
``` 
Esto sucede porque las variables con scope de bloque solo son accesibles dentro del bloque en el que se encuentran, no fuera de este.

¿Cual es mejor? ¿El scope global o el scope global?

Si cada función tiene que leer variables globales y de acuerdo a los valores que tengan, las funciones van devolver una cosa u otra, entonces la ejecución de una función dependera del estado en que se encuentre nuestro programa en ese momento. 

Las funciones se vuelven mas impredecibles porque depende de cosas externas, haciendo que nuestro código se vuelva mas deficil de entender y que se mas facil intoducir bugs.

Una buena practica de programación debemos declarar nuestras variables con el scope más reducido posible.

Ademas las variables globales van a estar en memoria durante toa la ejecución del programa, mientras que las que se encuentren en el scope local van estar en memoria durante la ejecución de la función o bloque de código al que pertenece, al no ser que se trate de un **closure**, pero ese es asunto para otro dia.

## ¿Cómo encuentra un variable JavaScript?

En JavaScript es muy común tener una función dentro de otra función
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var otraFruta = 'banana';

    function lavar() { 
        console.log('lavando' + otraFruta)
    }
    lavar()
    console.log('Comiendo ' + otraFruta)
}
```
Por lo tanto decimos que la función **lavar** es **hija** de la función **comer** porque esta declarada directamente dentro de ella y a su vez la función **comer** es **hija** de la función global.

Entender la jerarquia que se generan entre los distintos scopes que existen de acuerdo a como escribamos nuestro código es la clave para etender como funciona este mecanismo.

## Scope Chain
Si este código se estuviera ejecutando
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var otraFruta = 'banana';

    function lavar() { 
        console.log('lavando' + otraFruta)
    }

    lavar()
    console.log('Comiendo ' + otraFruta)
}
```
Y linea a ejecutar fuese la número 8, JavaScript va a empezar a buscar la variable en el scope mas pequeño, es decir donde se encuentra la ejecución en ese momento
```
function lavar() { 
    console.log('lavando' + otraFruta)
}
```
Como esa variable no está declarada en ese scope, va a seguir buscandola en el scope padre de esa funcion
```
function comer() {
    var otraFruta = 'banana';

    function lavar() { 
        console.log('lavando' + otraFruta)
    }

    lavar()
    console.log('Comiendo ' + otraFruta)
}
```
Como encuentra que esa variable existe en ese scope detiene la busqueda y utiliza el valor de esa variable. En este caso veriamos por consola lo siguiente
```
// ↪ Lavando banana
```
Lo cual no tiene mucho sentido, pero asi funciona nuestro programa :P.

Si quisieramos de la misma funcion podemos acceder a la variable **fruta**
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var otraFruta = 'banana';

    function lavar() { 
        console.log('lavando' + fruta)
    }

    lavar()
    console.log('Comiendo ' + otraFruta)
}
```
JavaScrip primero buscara donde en el scope donde se encuenta la linea de código que se acaba de ejecutar
```
function lavar() { 
    console.log('lavando' + fruta)
}
```
Al no encontrarla va a seguir buscando en el scope padre
```
function comer() {
    var otraFruta = 'banana';

    function lavar() { 
        console.log('lavando' + fruta)
    }

    lavar()
    console.log('Comiendo ' + otraFruta)
}
```
La busqueda va a seguir hasta llegar al scope global que es donde se encuentra declarada la variable
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var otraFruta = 'banana';

    function lavar() { 
        console.log('lavando' + fruta)
    }

    lavar()
    console.log('Comiendo ' + otraFruta)
}
```
## Ocultamiento de variables (Varaible Shadowing)
¿Que pasa si tenemos dos variables con el mismo nombre
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var fruta = 'banana';

    function lavar() { 
        console.log('lavando' + fruta)
    }

    lavar()
    console.log('Comiendo ' + fruta)
}
```
En este caso cuando esta linea de código se ejecute JavaScript va a empezar a buscar esa variable en el mismo bloque de código en donde se ejecuto la orden
```
function lavar() { 
        console.log('lavando' + fruta)
}
```
Como no la encuentra, seguira buscando en el scope mas cercano, el de la función comer  
```
function comer() {
    var fruta = 'banana';

    function lavar() { 
        console.log('lavando' + fruta)
    }

    lavar()
    console.log('Comiendo ' + fruta)
}
```
La encontrará y usará su valor. Al tener el mismo nombre, la variable del scope padre va a estar oculta.

El ocultamiento de variables se produce cuando una variable que está en un scope más reducido tiene el mismo nombre que otra que está en un scope superior siguiendo su cadena de scopes.

Desde el scope más pequeño no podemos acceder a la variable global solo por su nombre, pero si la declaramos con var en el scope global, esta se agrega como propiedad del objeto global **window** de los navegadores, por lo que podremos acceder a ella de la siguiente manera
```
<script>
    var fruta = 'manzana'
</script>

function comer() {
    var fruta = 'banana';

    function lavar() { 
        console.log('lavando' + window.fruta)
    }

    lavar()
    console.log('Comiendo ' + fruta)
}
```













# En javascript el tipado es dinamico y debil

Dinamico porque las variables **no tienen un tipo de dato particular** asociado sinó que podemos asignarle y re-asignarle **cualquier valor** a **cualquier variable**.
y debil porque podemos realizar operaciones entre valores de distintos tipos.

Por ejemplo, sumar un number y un string:

```
2 + '3'
```

Lo que va a suceder acá es que el motor de javascript hará lo posible por resolver la operación, lo que lo lo lleva a inferir automaticamente que lo que queremos es concatenar ambos datos como si fueran de tipo string por lo que obtendremos lo siguiente:

```
2 + '3'
// ↪ "23"
```

Esta conversión implícita de tipos que realiza el motor de Javascript para poder concretar una operación se denomina **coerción de tipos** y el efecto que tiene sobre como se ejecutan nuestros programas es muy grande.

## Tipo de una variable

El tipo de una variable se determina cuando se ejecute la línea de código que contiene a esa variable y depende de la operación que se este realizando con ella.

Por ejemplo, si a la suma anterior la convertimos en una resta:

```
2 - '3'
```

Lo que hará el motor de javascript es convertir automaticamente el string a number y obtendriamos el siguiente resultado:

```
2 - '3'
// ↪ -1
```

# Tipos de datos

Por sus caracteristicas particulares en Javascript exiten dos grandes grupos de tipos de datos, los **primitivos** y los **objetos**, entender las caracteristicas y diferencias de cada grupo es algo que sumará mucho a la hora de trabaja profesionalmente con el lenguaje.

## Datos primitivos

Estos son **valores básicos** e **inmutables** que **no poseen métodos ni propiedades**

## ¿Cómo averiguamos el tipo de dato de un valor o una variable?

Así como existen los operadores de suma, resta, división y multiplicación, tambien existe un operador llamado **typeof**.
Si escribimos **typeof** seguido de un espacio y luego un valor o una variable, obendremos un string con el tipo de dato que tiene ese valor o variable

```
const nombre = "Germán"

typeof nombre
// ↪ "string"
```

```
typeof 35
// ↪ "number"
```

Tambien es valido usarlo con parentesis

```
typeof(true)
// ↪ "boolean"
```

## ¿Qué tipos de datos existen en javascript?

Existen 6 tipos de datos primitivos.

-   Number
-   String
-   Boolean
-   Null
-   Undefined
-   symbol (desde ES2015)

En javascript todo valor que no sea de estos tipos en un Objeto. Si, los objetos literales, los arrays, las funciones, las fechas y las expresiones regulares, son objetos.

## Caracteristicas de los tipos de datos
---

### Strings

Los string representan el texto de nuestros programas.
Para delimitar el texto debemos encerrarlo entre comillas dobles o simples:

```
const nombre = 'Germán';
const apellido = "Gambarte";
```

Eso si, no podemos iniciar con comillas dobles y terminar con simples:

```
const nombre = "Germán';
```

Cualquiera de los dos cumplen la misma función, por lo que podemos usar la que nos guste. Es recomendable elegir solo una de ellas, no debemos escribir parte del programa con comillas simples y otras partes con comillas dobles.

Hay otro caracter que se incorporó al lenguaje en el año 2015 que sirve para delimitar strings el **backtick**(comilla invertida), este caracter nos permite interpolar una variable o una expresión dentro de un string:

```
let nombre = 'Germán';
let apellido = 'Gambarte';
let edad = 22;

let saludo = `Hola, me llamo ${nombre} ${saludo} y tengo ${edad} años`;
```

Es recomendable usarlos solo cuando necesites colocar codigo dentro del string para que el resultado forme parte del mismo, de lo contrario utiliza comillas simples o dobles.

### Codificación **UTF-16**

Para representar los strings Javascript utiliza una codificación que se llama **UTF-16**, lo que nos permite representar caracteres de muchos alfabetos, incluso emojis

### Otras caracteristicas

Si queremos saber la cantidad de caracteres que tiene un string podemos acceder a su propiedad **length**.

```
"German".length
// ↪ 6
```

Existe un Sting que no tiene longitud, este es el string vacio y es util para darle un valor inicial a una variable

```
"".length
// ↪ 0
```
Para obtener un String a partir de una variable podemos usar el metodo **toString()**
```
let edad = 22;

edad.toString();
// ↪ "22"
```
O podemos obtener el mismo resultado concatenandole comillas a la variable
```
edad + "";
// ↪ "22" 
```

Para usar el metodo **toString** debemos asegurarnos que la variable no contiene **null** o **undefined** porque obtendremos un error.

----

### Numbers

Sólo existe un tipo de dato para los números en JavaScript: **number**. y sirve para representar tanto numeros enteros, como decimales y negativos

```
typeof 2
// ↪ "number"

typeof -10
// ↪ "number"

typeof 3.14
// ↪ "number"
```
 Existe el **0** y el **-0**, pero si los comparamos tienen el mismo valor

 ```
 0 === -0
 // ↪ true
 ```
A la hora de represntar números decimales JavaScript no es  muy preciso:
```
0.1 + 0.2
// ↪ 0.30000000000000004
```
Pero esto no solo pasa en JavaScript, tambien ocurre en lenguajes como Ruby, Python o Java. Esto tiene que ver por como estan diseñados los numeros dentro del leguaje.
En estos lenguajes para representar un número se utiliza un formato que se llama **IEEE 754**. En este formato cada número ocupa 64bits en la memoria de la computadora es decir 8 bytes,

Cuando trabajamos con decimales en JavaScript Es muy importante que utilicemos la funsión **toFixed()** para limitar la cantidad de numeros despues de la coma que queremos usar.

```
let numero = (0.1 + 0.2).toFixed(2);

numero
// ↪ "0.30"
```
Como vimos esta funsion devuelve un String, si lo queremos es un número lo que podemos hacer es agregar el simbolo **+** antes de la operación para convertir el resultado a tipo numerico.

```
let numero = +(0.1 + 0.2).toFixed(2);

numero
// ↪ 0.30
```

El rango de números que podemos usar con este formato va desde un número despues que 2^53 negativo
```
let numeroMinimo = -(2 ** 53) + 1;

numeroMinimo
// ↪ -9007199254740991
```
Hasta un número antes que 2^53 positivo
```
let numeroMaximo = (2 ** 53) -  1;

numeroMaximo
// ↪ 9007199254740991
```
Aún así podemos seguir representando números de 64bits mas allá de estos límites, pero estos valores van a ser aproximaciones, por lo que si realizamos calculos con estos números, vamos a obtener resultados que no esperamos.

Por ejemplo, si al límite máximo le sumamos uno obtendremos este resultado:
```
numeroMaximo + 1
// ↪ 9007199254740992
```
Sin embargo si le sumamos 2, el resultado va a ser igual al que obtuvimos sumandole 1:
```
numeroMaximo + 2
// ↪ 9007199254740992
```

A estos numero límites tambien se los puede acceder de la siguiente manera
```
numeroMinimo === Number.MIN_SAFE_INTEGER
// ↪ true

numeroMinimo === Number.MAX_SAFE_INTEGER
// ↪ true
```
 Esto marca el rango de números donde es seguro realizar operaciones numéricas

Para verificar que un que un número se encuentra dentro de los limites podemos usar **Number.isSafeInteger()**:
```
Number.isSafeInteger(9007199254740996)
// ↪ false
```

El número más grande y el más pequeño que podemos ver reprensentados en 64 bits los obtenemos de la siguiente manera:
```
Number.MAX_VALUE
// ↪ 1.7976931348623157e+308

Number.MIN_VALUE
// ↪ 5e-324
```
Hay que recordar que **no es seguro operar con ellos** ya que son solo una aproximación de esos valores

Pero hay dos valores que van más alla de los que mencione hasta ahora, el infinito negativo y positivo
```
Infinity
// ↪ Infinity

-Infinity
// ↪ -Infinity
```
Ningún número es más grande que el infinito positivo, ni mas pequeño que el infinito negativo

Para verificar que un número no sea inifito podemos pasar este por la funsión **isFinite()**:
```
isFinite(300)
// ↪ true

isFinite(Infinity)
// ↪ false
```
Infinito es el resultado de dividir cualquier numero mayor a 0 entre 0
```
3 / 0
// ↪ Infinity

3 / -0
// ↪ -Infinity
```

Ahora, si dividimos 0 entre 0, obtenemos el ultimo valor que esciste de tipo Number: **NaN** (Not a Number)
```
0 / 0
// ↪ NaN
```
Aunque su valor indique lo contrario NaN es de tipo number y es el resultado que obtendremos de computos inválidos, por ejemplo:

Dividir un string entre un número
```
"hola" / 3
// ↪ NaN
```
Y NaN se va a propagar por cualquier otro calculo que querramos hacer con él 
```
NaN + 300
// ↪ NaN
```
Este es un valor muy especial en JavaScript devido a que no es igual a nada, ni siquiera a sí mismo
```
NaN === NaN
// ↪ false
```
Pero existe una funsions que nos indica si el parametro que le pasamos es NaN o no
```
isNaN(30)
// ↪ false

isNaN(NaN)
// ↪ true
```
---
### Booleans

Si un valor es de tipo boolean solo puede tener dos valores posibles: **true** o **false**

Podemos asignarle un boolean a una variable para incializarla:
```
let esMayorDeEdad = false;
```
O tambien podemos obtenerlo a partir de una comparación:
```
let edad = 22;

let esMayorDeEdad = edad < 18;

esMayorDeEdad
// ↪ true
```
Y para obtener el valor opuesto de un boolean usamos un signo de exclamación
```
!esMayorDeEdad
// ↪ false
```

Los booleans se suelen utilizar en la condición de un **if** o también dentro de un ciclo **for** o **while**

si queremos saber si dos valores son **true** al mismo tiempo podemos usar el indiacador de **AND**
```
let tieneIdentificación = false;

esMayorDeEdad && tieneIdentificación
// ↪ false
```

Y si queremos saber si al menos uno de ellos es verdadero podemos usar el indicador de **OR** o **doble pipe**
```
esMayorDeEdad && tieneIdentificación
// ↪ true
```

Otra cosa que hay que saber de los boolean es que si bien hay valores que no son de tipo boolean, pueden ser evaluados como tales. Por ejemplo dentro de la condición de un **if**
```
let mensajesSinLeer = 10;

if (mensajesSinLeer) { // es de tipo number pero se infiere como boolean 
    console.log(`Hay ${mensajesSinLeer} mensajes no leidos`)
} else {
    console.log('No tienes mensajes sin leer')
}
```

Dentro de un contexto booleano hay ciertos valores, conocidos como falsy, que se consideran falsos:

- false
- 0
- -0
- 0n
- ""
- null
- undefined
- NaN

Todos los valores diferentes a los mencionados en la lista anterior se consideran verdaderos.

---
Si bien dije que los datos primitivos no tiene propiedades ni metodos, vimos como con la utlización del metodo **toString()** podemos converir números en una cadena de texto.

Esto es posible porque tanto los strings, como los numbers y booleans tienen su equivalente en el mundo de los objetos:
```
let cadenaDeTexto = new String('Hola');

cadenaDeTexto
// ↪ >String {"Hola"}

// -----------------------------------

let numero = new Number('1234');

numero
// ↪ >Number {1234}

// -----------------------------------

let booleano = new Boolean(true);

booleano
// ↪ >Boolean {true}
```
Pero no es recomendado hacerlo de esta manera porque ahora las variables son objetos, no son valores primitivos por lo que si trabajamos con ellos podemos obtener resultados que no esperabamos.

### Aqui la explicación definitiva:

Cada vez que querramos acceder a un atributo o llamar a un método de un valor primitivo, el motor de javascript va a crear temporalmente lo que se denomina como **object wrapper**, esto es un objeto que envuelve a un valor primitivo cuando queremos acceeder a una propiedad o llamar a un método del mismo y es temporal porque el motor lo utiliza sólo por una fracción de segundo y luego lo desecha, lo borra de la memoria

---
### Null y Undefined

Null es un dato aparte que sólo tiene un valor posible: null. Este representa la **ausencia de valor**. Sirve para decir que una variable no contiene nada, está vacía o que todavía no conocemos su valor

Undefined es un dato muy similar a null pero este representa un **tipo de dato desconocido o no definido**. Se declara undefined a las variables que son declaradas pero no las inicializamos
```
let nombre;

nombre
// ↪ undefined
```

Y si una función se termina de ejecutar sin hacer un **return**, veremos que nos retornará undefined o si llamos una una función y no le pasamos un parametro en caso de que lo requiera, esta devolverá undefined
```
function saludar(nombre) {
    console.log(typeof nombre)
}
 
saludar()
// ↪ undefined
``` 

Null y Undefined son diferentes
```
typeof null === typeof undefined
// ↪ false
```


### Entonces ¿Cuál de los dos deberiamos usar?

Tecnicamente se le puede asignar undefined a una variable, pero no es recomndable, si queremos decir que una variaable está vacia deberiamos asignarle el valor null
```
var nombre = null; 
```
Undefined es un valor que deberíamos dejar para que el motor de JavaScript asigne automáticamente, aunque si podemos preguntar si el tipo de una variable es undefined
```
typeof unaVariable === 'undefined'
// ↪ true
```

Esto significaria que no se le dio ningúm valor, no se recibió ese parámetro o que una función se terminó de ejecutar hasta el final sin devolver ningún valor.

### Hay que tener cuidado con estos valores
Si tenemos alguna variable que tiene alguno de estos valores y queremos acceder a una propiedad o método en ella, vamos a tener unos de los error mas comúnes en JavasCript
```
let nombre = null;

nombre.length
// ↪ Uncaught TypeError: Cannot read property 'length' of null
```
Esto se debe a que null y undefined a diferencia de los strings, numbers y booleans no tiene objects wrappers, por eso es que hay que ser cuidadosos en caso de utilizarlos.

### JavaScript tiene un bug...

Si preguntamos por el tipo de dato que es null, sucederá lo siguiente:
```
typeof null
// ↪ "object"
```
Si, nos dice que null es un objeto, pero esto no es mas que un bug que existe desde el cominezo de JavaScript, si bien hubo un intento de solucionarlo y hacer **typeof null** devuelva **null**, esto se terminó descartando debido a que muhcos sitios web dependen de ese bug para funcionar correctamente, de todas manera esto no va a resultar un problema en tu dia a dia, solo queda dejar bien en claro que null es un tipo de dato primitivo.

---

### Symbol
 Este es un dato relativamente nuevo en JavaScript, apareció en 2015 y se usa para crear **valores únicos**, irrepetibles.

 Para crear un symbol, debemos hacerlo llamando a una función:
 ```
 let s1 = Symbol();
 ```
 podemos pasarle una descripción a los symbols
 ```
 let s = Symbol('descripción')
 ``` 
 Pero esto solo es util cuando queremos entender mejor nuestro código o cuando estamos buscando bugs, no tiene otra funcionalidad.

 Si creamos dos symbols con la misma descripción, o sin ella, estos van a ser diferentes.
 ```
let s1 = Symbol('descripción');
let s2 = Symbol('descripción');

s1 === s2;
// ↪ false
 ```
 ```
let s1 = Symbol();
let s2 = Symbol();

s1 === s2;
// ↪ false
 ```

Esto se debe a que un symbol solo es igual a si mismo, al menos que los creemos de otra manera.

Existe un **registro global de símbolos** y para crear un simbolo que se guarde ahí debemos hacerlo de la siguiente manera:
```
let s1 = Symbol.for('descripción');
```
si ya existe un símbolo con esta descripción obtendremos ese simbolo, de lo contrario será creado con el llamado de la función for() y nos lo devolver. De esta manera podremos acceder al mismo símbolo desde dintistos lugares de nuestro programa a partir de su descripción, ademas este registro es com compartido entre nuestra página y los **serviceWorkers** o **iframes** que esta pueda llegar a incluir.

Si tenemos un símbolo en el registro y queremos saber cual es su descripción lo haremos de la siguiente manera
```
let s1 = Symbol.for('descripción');

let desc = Symbol.keyFor(s1);
// ↪ "descripción"
```

link aqui, para mas información sobre los [symbols]

---
### BigInt
Permite utilizar números enteros sin límite. lo usamos de la siguente manera:

tendremos que agregarle una "**n**" al final del número que queremos utilizar
```
let numeroGrande = 9008788930129900599n;

numeroGrande
// ↪ 9008788930129900599n
```
Tambien podemos crealos con la función **BigInt()** pasandole como parametros una cadena de texto o un número
```
let numeroGrande2 = BigInt('9008788930127990599');

numeroGrande2
// ↪ 9008788930129900599n
```

### ¡Atención!
Si bien Javascript es un leguaje debilmente tipado, cuando intentemos hacer una operacion entre un BigInt y un número, el motor de JavaScript lanzará un error.
```
numeroGrande + 100

numeroGrande
// ↪ Uncaught TypeError: Cannot mix BigInt and other types, use explicit conversions
```
Este tipo de operaciones no está permitida, al igual que tampoco podemos realizar operaciones con Math y BigInts, porque internamente intentará convertirlos a números y lanzará un error.
```
Math.sqrt(numeroGrande)
// ↪ Uncaught TypeError: Cannot convert a BigInt value to a number
```
Tambien hay que tener cuidado si intentamos convertirlos a números, debido a que caeremos otra vez en los errores de aproximación
```
Number(numeroGrande)
// ↪ 9008788930127991000
```


Los BigInt son un tipo de dato a parte solo para los números enteros grandes, tan grandes o tan pequeños como querramos, negativos y positivos y si podemos realizar cuentas entre ellos, pero ambos valores tienen que ser BigInt.
```
let resultado = numeroGrande + 1n;

resultado
// ↪ 9008788930129900600n
```

































[symbols] <es.javascript.info/symbol>
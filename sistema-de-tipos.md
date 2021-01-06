# Sistema de tipos
Los sistemas de tipos son las reglas que impone un lenguaje para clasificar qué tipos de valores existen, cómo podemos manipularlos y cuáles son las operaciones válidas para realizar con ellos.

En este post vamos a analizar a analizar cuatro caracteristicas del sistema de tipos de JavaScript comparandolas con la de otros lenguajes.

## Chequeo de tipos

el chequeo de tipos es el proceso de y hacer cumplir las restricciones de tipos que existen en un lenguaje,basicamente es verificar que si dijimos que una variable va a ser un **número entero** no le asignemos un valor de otro tipo, o que si un método esperaba un **string** no le estemos pasando un número.

Este proceso puede ser de dos tipos:
- Chequeo estático de tipos: Es decir que el proceso se lleva a cabo antes de ejecutar el programa.
- Chequeo dinamico de tipos: Es decir que el proceso se lleva a cabo durante la ejecución del programa.

En los lenguajes compilados el compilador toma nuestro código y lo analiza verificando que cumpla con las restricciones de tipos del lenguaje, como solo basta con leer el código del programa y analizarlo, decimos que este chequeo es estático. Si el programa pasa el chequeo de tipos, el compilador podra traducir el programa a aun lenguaje que la computadora pueda leer y ejecutar. En cambio si nuestro código no cumple con las restricciones de tipos impuestas por el lenguaje, no se va a poder crear el programa a ejecutar.

Este chequeo es una buena red contención para los errores de tipo que podamos llegar a cometer, algunos de los lenguajes con tipado estático son: **C#**, **Java**, **Scala**, **Kotlin**, **Go**, etc. En todos ellos el código se compila antes de ser ejecutado.

Ahora bien, cuando el chequeo se realiza durante la ejecución del programa, la cosa es un poco distinta.

En los **lenguajes interpretados** como JavaScript le entregamos nuestro código directamente a otro programa (algún motor de JavaScript) que lo sabe leer y ejecutar y en este caso no se realiza una compilación del código en un lenguaje que entiende la computadora, sinó que el motor de JavaScript va ejecutando cada instruccion de nuestro programa a medida que lo va leyendo, pero antes de ejecutar cada instrucción chequea que esa linea no esté violando las restricciones del tipos del lenguaje, si las cumple la va a ejecutar y va a continuar con la siguiente linea de instruccion de la secuencia lógica del programa. 

El error lo veremos si encuentra alguna línea que viola las restricciones de tipos e intenta ejecutarla, cuando esto sucede la ejecución del programa se detiene en esa linea y no continúa.

Las variables en JavaSript no están asociadas a un tipo de dato de particular, sino que pueden contener un valor de un tipo y luego se le podemos asignar un valor de otro tipo, esto hace que el asunto sea más complicado. Como desarrolladores/as nosotros somos quienes tenemos que estar más atento y evitar todo tipo de violación a las restricciones de tipo del lenguaje, así nuestros programas se ejecutas por completo.

Decimos que el chequeo es dinamico porque no podemos saber de que tipo son nuestras variables, hasta que el programa se ejecute y estas vayan tomando distintos valores, pero JavaScript no es el único lenguaje que tiene un tipado dinamico, **PHP**, **Ruby** y **Python**, tambien tiene este chequeo de tipos

En los útimos años se empezaron a usar bastante estos lenguajes, debido a su flexibilidad y la velocidad con la que se puede escribir código en ellos.

## Exigencia de tipos
¿Qué tan exigente es un leguaje para considerar que estamos comentiendo un error de tipos?

En **Java** podemos decir que una variable va a ser de tipo float (número decimal) y luego asignarle un número entero.
```
package Developer;

public class Main {
    pucblic static void main(){
        float numero = 22;
    }
}
```
Pero si alguien intenta asignarle la suma de un número y un string.
```
package Developer;

public class Main {
    pucblic static void main(){
        float numero = 22;
        numero = numero + "1";
    }
}
```
Va a haber error de tipos.

En **PHP** podemos asignarle a una variable la suma entre un número y un string.
```
<?php
$numero = 29 + '1';

echo $numero;
```
PHP va a intentar leer el número que esta dentro del string y hacer la suma. Si ejecutamos este código, vamos a ver que no tenemos ningún error.
```
<?php
$numero = 29 + '1';

echo $numero;
// ↪ 30
```

En **Pyhton** Si intentamos sumar un número y un string e imprimir el resultado por pantalla, cuando ejecutemos ese programa vamos a ver que obtendremos un error de tipos.
```
numero = 29 + '1'
print(numero)
// ↪ TypeError: unsopported operand type(s) for +: 'int' and 'str'
```

Cuanto mas estricto sea un lenguaje con ests reglas, decimos que es más fuertemente tipado, en cambio cuanto más relajado sea con estas reglas decimos que su tipado es más débil. Y no es cuestion de blanco o negro como el chequeo de tipos, la exigencia de tipos de divide en niveles

Por ejemplo, el tipado en python es más fuerte que el de PHP, pero no tan fuerte como el de Java o C#.

Muchas persona odian JavaScript porque se podria decir que el tipado es relajado, demasiado relajado.

por ejemplo:

Podemos sumar números y strings
```
2 + '3'
// ↪ "23"
```
Si queremos sumar tres booleanos, tambien podemos hacerlo
```
true + true + true
// ↪ 3
```
¿Sumar strings y arrays? no hay problema
```
'Tengo que comprar: ' + ['bananas', ' naranjas'] + ' y limones'
// ↪ "Tengo que comprar: bananas, naranjas y limones"
```

Ojo, en algunos casos obtendremos errores de tipo, por ejemplo si queremos realizar una operación entre un valor de tipo number y uno de tipo BigInt, hay error de tipos
```
2 + BigInt(20)
// ↪ Uncaught TypeError: Cannot mix BigInt and other types, use explicit conversions
```
O si tenemos una variable que contiene algo que no es una función e intentamos involcarla como si realmente lo fuera, ahi tambien hay error de tipos
```
let texto = 'hola';

texto()
// ↪ Uncaught TypeError: texto in not a function
```
O el error de tipos de más común en JavaScript, tratar de acceder a algún atributo sobre un valor que es null o undefined
```
let user;

user.email
Uncaught TypeError: Cannot read property 'email' of undefined
```

Pero en la mayoria de los casos no va a haber error de tipos si queremos hacer operaciones entre valores de distinto tipo
```
[] + {}
// ↪ "[Object Object]"

[1,2,3] + ' Estoy sumando un array y un string'
// ↪ "1,2,3 estoy sumando un array y un string"

2 + true
// ↪ 3

true + true
// ↪ 2

(true + true) * 50
// ↪ 100
```

El tema es que si no estamos seguros de que tipo son las variables que estamos operando, podemos obtener resultados que no esperamos.

¿Por qué? ¿Comó hace Javascript para realizar esas operaciones? Eso tiene que ver con la tercer caracteristica del sistema de tipos en JavaScript.

## Conversión de tipos
Javascript es super relajado, nos permite realizar operaciones entre valores de distinto tipo sin problema, pero para hacerlo va a tomar ciertas decisiones por nosotros.

Por ejemplo para sumar un número y un string, va a hacer de cuenta que el número es un string y va a realizar la concatenación entre ambos
```
40 + '60' // '40' + '60'
// ↪ "4060"
```

Ahora, si queremos restar un número y un string, la conversión que va a hacer es al reves, va a intentar convertir el string a número para poder concretar la operación
```
40 - '60' // 40 - 60
// ↪ -20
```

Esta conversión implicita de tipos que realiza el motor de JavaScript para poder concretar una operación se llama **coerción de tipos** y es algo con lo que hay que tener mucho cuidado, porque como vimos podemos obtener resultados inesperados.

¿Cómo evitamos que suceda?

Tendriamos qeu hacer una conversión explícita de tipos nosotros mismos. Hay tres tipos de conversiones explícitas que se pueden hacer:
- A string
- A number
- A boolean

Para convertir un valos a alguno de esos tipos podemos usar la función de String(), Number() o Boolean()
```
String(123)
// ↪ "123"

Number('3.14')
// ↪ 3.14

Boolean(null)
// ↪ false
```
Es importante que las uses como funciones y no como **constructores** anteponiendo "**new**"
```
new String(123)
// ↪ String {"123"}

new Number('3.14')
// ↪ Number {3.14}

new Boolean(null)
// ↪ Boolean {false}
```
Ya que así estaremos creando objetos y no valores primitivos

Hay otras formas de hacer conversiones explicitas de tipo en JavaScript

Para convertir un valor a string, debemos concatenarle un string vacio
```
2021 + ''
// ↪ "2021"

true + ''
// ↪ "true"

null + ''
// ↪ "null"
```
Si es un valor suelto podemos envolverlo entre parentesis y llamar al método toString()
```
(2021).toString()
"2021"
```
Y si el valor está dentro de la variable  podemos llamar ese método directamente sobre la variable
```
let valor = true

valor.toString()
"true"
```

Podemos obtener un number anteponiendo un signo de más adelante de la variable o el valor a convertir
```
+'1234'
// ↪ 1234

+'3.14'
// ↪ 3.14

+false
// ↪ 0
```

Ya sea por conversión implícitca o explícita, si un valor si intenta convertir a número y esa operación no se puede concretar, obtendremos **NaN** como resultado
```
3 - 'a'
// ↪ NaN

Number('123a')
// ↪ NaN
```

Y para los booleans podemos usar un signo de exclamación para obtener el opuesto al que queremos
```
let texto = 'hola'

!texto
// ↪ false
```
y anteponiendo dos signos de exclamación obtendremos el que corresponde al valor original
```
let texto = 'hola'

!!texto
// ↪ true
```

¿Cómo es más conveniente convertir tipos? ¿Con funciones u operadores?

 La verdad que esl resultado que tenemos es el mismo.

 Con los strings lo más com´pun es guardar el valor en una variable y despues llamar al método toString()
```
let valor = true

valor.toString()
"true"
```
Con los número los métodos que vimos son igual de utilizados
```
Number('3.14')
// ↪ 3.14

+'3.14'
// ↪ 3.14
```
Y con los booleanos lo más común es utilizar el doble sigo de exclamación
```
let user = {nombre: 'German'}

!!user
// ↪ true
```

A continuación veremos la ultima caracteristica que vamos a mencionar y es muy importante, de hecho es una de las por la cual muchas personas odian JavaScript pero es muy importante entender porqué.

## Equivalencia y compatibilidad de tipos

Aqui vamos a hablar sobre como un lenguaje determina que un tipo es **compatible** con otro tipo o **equivalente** a otro tipo

En **Java** por ejemplo podemos crear dos clases que contengan un método que hace lo mismo, en este caso sumar dos números
```
package Developer;

class Calculadora1 {
    public int sumarDosEnteros(int numero1, int numero2) {
        return numero1 + numero2
    }
}

class Calculadora2 {
    public int sumarDosEnteros(int numero1, int numero2) {
        return numero1 + numero2
    }
}
```
Y luego creamos una variable de tipo Calculadora1 yle asignamos una nueva instancia de la calse Calculadora2
```
package Developer;

class Calculadora1 {
    public int sumarDosEnteros(int numero1, int numero2) {
        return numero1 + numero2
    }
}

class Calculadora2 {
    public int sumarDosEnteros(int numero1, int numero2) {
        return numero1 + numero2
    }
}

public class Main {
    public static void main() {
        Calculadora1 calculadora = new Calculadora2()
    }
}
```
Por mas que las estructuras internas de ambas clases sean iguales, vamos a tener un error de tipos.

Esto es lo que se conoce como **tipado nominal**. Dos tipos son compatibles cuando tienen el mismo nombre o cuando uno es un subtipo del otro (por herencia). Con los lenguajes que tiene este tipado se suelen crear programas escribiendo multiples clases y utilizando patrones de diseño de programación orientada a objetos, lo que da lugar a soluciones elegantes y reconocibles en la ingenieria del software.

Lo malo es que si modificamos algun tipo ya sea una clase o una interface agregando un método, probablemente terminemos modificando varias partes del programa para que los tipos sigan siendo compatibles, pero por otro lado esto ayuda a que los errores de tipos en el programa sean muchos menos.

Algunos ejemplos de leguajes con tipado nominal son: Java, C++, C#, Swift y PHP.

Tambien existe otro sistema de tipos que es el **estructural** esto funciona de la siguiente manera, para que dos tipos sean compatibles sólo basta con que compartan la estructura que nos interesa.

Por ejemplo:

En estos lenguajes podriamos definir una función que recibe como parametro un objeto que contiene un atributo de tipo number
```
function esMayorDeEdad(persona: {ed9ad: number}) {
    return persona.edad > 18;
}
```
Si bien la variable que recibe se llama "persona", esta función podria recibir cualquier cosa que contenga el atributo "edad"

Pero si le pasamos a esta función algo que no tiene un atributo edad, tendremos un error de tipos
```
function esMayorDeEdad(persona: {edad: number}) {
    return persona.edad > 18;
}

let usuario = 'German';
esMayorDeEdad(usuario)
// ↪ Argument of type '{ nombre: string; }' is not assignable to parameter of type '{ edad: number; }'.
```

Estos dos tipados que vimos se realizan estaticamente, es decir antes de ejecutar el programa.

¿Y los lenguajes con tipado dinamico cómo determinan que dos tipos son compatibles?

Estos lenguajes utilizan algo que se llama **Duck Typing**, El termino proviene de un viejo dicho "Si parece un pato, nada como un pato y grazna como un pato, entonces probablemente sea un pato". Es decir debido a sus caracteristicas todo indica que es un pato, pero aunque no estemos 100% seguros de que lo sea, podemos tratarlo como tal. Llevado a programacion, no nos importa de qué tipo es un objeto, siempre y cuando tenga los atributos y métodos a los cuales queramos acceder. 

El problema es que como vimos al principio, el chequeo dinamico se realiza mientras se ejecuta el programa, por lo que el error de tipos va a surgir durante la ejecución de este. Lo malo de esto es que no tenemos una red de contención como en otros lenguajes y esto puede ser perjucial a medida que nuestras aplicaciones crecen en tamaño, por eso mucha gente piensa que los lenguajes que usan Duck Typing solo pueden usarse para crear prototipos, pero no un producto de verdad, sin embargo hay miles de proyectos creados con lenguajes que comparten esta caracteristica como por ejemplo JavaScript, Python o Ruby.

Los lenguajes dinámiscos incentivan a mantener una documentación actualizada y escribir muchos tests para asegurarnos de que el código funciona como deberia antes de lanzar una nueva versión de un programa.

## TypeScript

TypeScript es un superset de JavaScript, creado y mantenido por Microsoft. Parte de la misma sintaxis que JavaScript, pero agrega un chequeo de tipos estructural antes de que se ejecute nuestro programa, ya sea que se ejecute en un navegador, un servidos o donde sea. 
El código que vimos cuando hablamos del chequeo estrucural de tipos, es Typescript
```
function esMayorDeEdad(persona: {edad: number}) {
    return persona.edad > 18;
}

let usuario = 'German';
esMayorDeEdad(usuario)
// ↪ Argument of type '{ nombre: string; }' is not assignable to parameter of type '{ edad: number; }'.
```
Nosotros escribimos código en este lenguaje y luego el compilador lo traduce a JavaScript.

TypeScript sigue siendo JavaScript, pero con chequeo de tipos.
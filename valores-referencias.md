# Valores y Refencias

Acá vamos a intentar entender como se almacenan las variables en la memoria de la computadora cuando programamos en JavaScript.

Antes que nada es importante que entadamos la diferencia entre los dos grandes grupos de tipos de datos que existen en este lenguaje.

Hoy en dia existen seis tipos de datos primitivos.
- Strings: para representar texto.
- Numbers: para representar todo tipo de números (decimales, enteros positivos o negativos, infinitos negativos y positivos y NaN).
- Booleans: para representar condiciones verdaderas y falsas (true y false).
- Symbols: para crear valores únicos e irrepetibles.
-BigInts: para representar números enteros tan grandes como querramos.
- Null: Lo utilizamos para decir que una variable, explicitamente, no contiene nada.
- Undefined: indica que una variable tiene un tipo de dato desconocido.

Ahora bien, si tenemos una variable que contiene algún valor primitivo, como por ejemplo:
```
let fruta = 'banana';
```
Estamos creando un pequeño contenedor en la memoria de la computadora y guardando dentro el valor "banana".

Si a continuación le cambiamos el valor a la variable fruta
```
let fruta = 'manzana';
```
Estaremos cambiando el valor que almacena variable y perdiendo el valor anterior.

Acá viene lo interesante, si creamos una segunda variable y le asignamos como valor la variable fruta:
```
let fruta = 'banana';
let fruta2 = fruta;
```

Se va a crear una **copia** del valor de la variable fruta y va a guardarse en un contenedor diferente al valor de la variable fruta. Es importante entender que se crea una **copia** del valor.

Siempre que una variable contenga un valor primitivo y se lo asignamos a otra es lo mismo que estar asignandole de nuevo ese valor
```
let cantidad = 10;
let cantidad2 = cantidad;

// Es igual que hacer lo siguente...

let cantidad = 10;
let cantidad2 = 10;
```

Lo que intento dejar claro es cuando hacemos esto lo que estamos creando es una copia del valor, esto quiere decir que no hay ningun tipo de relación entre las dos variables, por lo que si cambiamos el valor de la primera variable:
```
let fruta = 'banana';
let fruta2 = fruta;

fruta = 'mandarina';

fruta2
// ↪ 'banana'

```
la segunda variable ni se va a enterar por lo que no sufrira ningún cambio. esto deja en claro que las variables en JavaScript son totalmente independientes, no hay nada que las una entre sí.

Pero con los objetos pasa algo distinto, estos son mucho más complejos que los valores primitivos, en ellos podemos guardar multiples valores.

Para crearlos definimos que propiedades va a tener el objeto y le asignamos un valor a cada propiedad
```
let fruta = {
    nombre: 'banana',
    cantidad: 4,
    tieneCascara: true
};
```
Y despues de haberlo creado podemos seguir agregando propiedades y valores y sacarles los que ya no queremos que tenga
```
// Agregar
fruta.color = 'amarillo';

// Eliminar
delete.fruta.tieneCascara;
``` 

De esta manera los objetos no ocupan un espacio fijo en la memoria de la computadora como lo hacen los valores primitivos sino que su tamaño puede ir cambiando, al igual que sucede con los Arrays, debido a que tambien podemos agregarle o quitarle valores luego de haberlos creado.

Tambien podemos asignarle a una variable una función y despues pasarla como parametro de otra función. Las funciones tambien son tratadas como objetos, objetos que pueden ser invocados y como tales tambien podemos agregarle y quitarle porpiedades y valores.

En JavaScript Cuando decimos "**objetos**" nos estamos refiriendo a un objeto literal, un array o una función, basicamente cualquier cosa que no sea un valor primitivo, como el espacio que ocupan puede ir variando, los objetos no se van a almacenar de  la misma manera que los objetos primitivos, sinó que se almecenan en un área de la memoria destinada para ellos llamada **HEAP** (memoria dinámica).

El HEAP este espacio en la memoria es mucho más grande en comparación a donde se almacenan las variables con valores primitivos, pero tambien es mucho mas lento de acceder, voy a intentar explicar porqué...

Cada vez que asginemos un objeto a una variable, JavaScript va a poner ese objeto en algun espacio de memoria libre que encuentre en el HEAP, lo siguiente que va a suceder es que va a recordad en que direccion de memoria lo puso y esa direccion es lo que va a guardar dentro de la variable. Esta "direccion" o mejor dicho posición de la memoria que se usa para acceder a un objeto se llama **referencia**.

Ahora bien, cuando a una variable le asignamos otra que apunta a un objeto
```
let fruta = {
    nombre: 'banana',
    cantidad: 4
};

let fruta2 = fruta
```
Lo que se va a copiar es la refencia al objeto y como dije antes las variables son independientes, si a la variable "fruta2" le asignamos otro **objeto**, la variable "fruta" ni se va a enterar y lo que va a suceder es que solo se va a modificar la referencia añadiendo la que apunta al nuevo **objeto** asignado.

### ¡Atención!

Si tenemos multiples variables apuntando a un mismo objeto y modificamos una **propiedad** de ese objeto utilizando cualquiera de las variables
```
let fruta = {
    nombre: 'banana',
    cantidad: 4
};

let fruta2 = fruta

fruta.cantidad = fruta.cantidad - 1;
```

Ese cambio se va a relizar sobre el objeto al que ambas hacen refencia. Y como ambas apuntan al mismo objeto cuando usemos la otra variable para acceder a una de las propiedades de ese objeto vamos a ver el cambio que acabamos de realizar
```
let fruta = {
    nombre: 'banana',
    cantidad: 4
};

let fruta2 = fruta

fruta.cantidad = fruta.cantidad - 1;

fruta2.cantidad
// ↪ 3
```
---
## ¿Qué sucede con las funciones y las variables?
 Cuando declaramos una función decimos que parametros va a recibir
 ```
 function comer(cantidad) {
     fruta.cantidad = cantidad - 1;
 }
 ```
 Si a continuación declaramos una variable y la pasamos como parametro al invocar la función
  ```
 function comer(cantidad) {
     cantidad = cantidad - 1;
 }

 let cantidad = 4;

 comer(cantidad);
 ```

Se va a aplicar la misma logica que vimos hasta ahora.

Si la variable contiene un valor primitivo, el parametro va a recibir una copia de ese valor y si la variable apunta a un objeto va a recibir como parametro una copia de la referencia hacia ese objeto.

Y una vez más la variable y el parametro de la función son totalmente independientes entre sí, no hay nada que los una. Si dentro de la función modificamos el parametro de la siguiente manera
  ```
 function comer(cantidad) {
     cantidad = cantidad - 1;
 }
 ```
 La variable que estaba fuera de la función nunca se va a enterar de ese cambio y cuando la función se termine de ejecutar, las variables de esa funcipon se van a descartar.

 En cambio si lo que le pasamos a la función es un objeto
   ```
 function comer(fruta) {
     fruta.cantidad = fruta.cantidad - 1;
 }

 let fruta = {
    nombre: 'banana',
    cantidad: 4
};

comer(fruta);
 ```
 Lo que se va a copiar es la referencia que apunta al objeto, ahora tanto la variable como el parametro apuntan a la misma posición en memoria y alli es donde encontraremos al objeto con sus propiedades y valores. Cuando se termine de trabajar con la función se van sacar de la memoria sus variables locales y se va a seguir trabajando con la función que habia hecho la invocación y con sus variables y como teniamos una variable que hacia referencia al mismo objeto, cuando querramos acceder a ese objeto usando esa variable vamos a ver el objeto modificado.
  ```
 function comer(fruta) {
     fruta.cantidad = fruta.cantidad - 1;
 }

 let fruta = {
    nombre: 'banana',
    cantidad: 4
};

comer(fruta);

console.log(fruta)
// ↪ {nombre: 'banana', cantidad: 3}
 ```   
# 💻  Mercury

Esta es una hoja de trabajo para ver lo que hemos hecho durante el taller, basado en los tutoriales y referencia de Marcury de Timo Hoogland.

Para este taller utilizaremos la versión Web de mercury, que se ejecuta en el navegador (Windows/Mac/Linux)👇

Mercury funciona mejor en navegadores como Brave o Google Chrome. No utilices safari o bing si quieres evitar resultados extraños

### [**https://mercury-playground.pages.dev/](https://mercury-playground.pages.dev/**)

(Mercury también tiene otras versiones, puedes encontrar más información sobre la versión original que funciona en Max8 (sólo Windows/Mac) [aquí](https://github.com/tmhglnd/mercury))

Las acciones que puedes hacer en Mercury son: 

`play` o `alt + return` para activar los sonidos 

`silence` o `alt + .` para Silenciar

`empty`  para borrar todo el código

`Example` para reproducir uno de los ejemplos random

`save` para guardar el texto en un archivo .txt

`record`  para guardar los sonidos

Todas las funciones que vamos a ver a continuación (y más) se encuentra en: [https://tmhglnd.github.io/mercury/reference.html](https://tmhglnd.github.io/mercury/reference.html)  y en los tutoriales incluidos en mercury

# ⚫ `sample`

Para reproducir sonidos los podemos llamar un nuevo `sample`

Escribe el siguiente código:

```jsx
new sample harp_up
```

Ahora presiona `alt + return` (or presiona `play`). Mercury evaluará o ejecutará ahora tu código.

Ahora hemos creado un nuevo sample `new sample` que tiene el nombre `harp_up` Y lo escuchamos en`loop`. Una característica interesante de Mercury es que todos los instrumentos se ejecutan repetidamente. `looping` 🔁.

Ahora presiona `alt + .` (o clica en `silence`) para silenciar los sonidos 

# Funciones

## ⚫`time()`

[https://tmhglnd.github.io/mercury/02-instrument.html#time](https://tmhglnd.github.io/mercury/02-instrument.html#time) 

Con `time` establecemos el intervalo de tiempo con el que se reproduce un sonido, por defecto está en 1/1 (una vez por compás), podemos modificar esa duración:

```jsx
new sample harp_up time(1/4)
```

También podemos añadir un segundo parámetro de offset `time(1/4 1/2)`, o utilizar los triggers de otro instrumento con `time(free "/kick")` 

## Mas samples

Puedes añadir mas samples con diferentes tiempos:

```jsx
new sample harp_up time(1/3)
new sample kick_house time(1/3)
new sample snare_808 time(1/2)
```

## ⚫ `tempo`

Para cambiar los BPM utilizamos `set tempo` y los BPM que queremos utilizar

```jsx
set tempo 100

new sample harp_up time(1/3)
new sample scrape time(1/3)
new sample tongue time(1/2)
```

## ⚫`list`

con `list` generamos listas de diferentes tipos, necesitamos nombrarla

```jsx
list listaSamples [list someSamples [kalimba_a kalimba_e kalimba_g]
```

`list`, followed by the name of the ring. The name can be any characters you like except for numerical values. 

Todos los valores entre `[` y `]` (corchetes) forman parte de la lista. Cada valor separado por un espacio se considera un nuevo valor. En este ejemplo la lista tiene 3 valores.

Ahora podemos sustituir el nombre de la muestra por el nombre de la lista, de esta forma cada vez que se dispara la muestra reproduce la siguiente muestra de la lista.

```jsx
set tempo 100

list listaSamples [kalimba_a kalimba_e kalimba_g]

new sample listaSamples time(1/3)
new sample scrape time(1/3)
new sample tongue time(1/2)
```

## ⚫`play(1)`

Con play podemos decidir cuando se ejecutan los samples con `1` se ejecutan y con `0` no…

Si creamos una lista de ceros y unos generamos un ritmo:

```jsx
list rtm [1 0 0 1 0 1 1 0]
new sample hat_click time(1/12) play(rtm)
```

También podemos utilizar números decimales para definir la probabilidad con la que esos sonidos se ejecutan, por ejemplo `play(0.5)` se ejecuta con una probabilidad del 50%

## ⚫ `speed(1)`

Modifica la velocidad de reproducción, la velocidad normal es `1`

## ⚫ `offset(0.5)`

modifica el punto en el que se comienza a reproducir el sample `0` es el punto inicial y `1` es el final del sonido

```jsx
new sample amen speed(0.5) offset(0.5) 
```

## ⚫ `shape(10 100)`

Genera una envolvente dinámica que modifica la duración del sonido en milisegundos `shape(500 100)` .  También puede definirse con divisiones de tempo: `shape(1/4 1/32)`  

```jsx
new synth saw shape(1/4 1/32) time(1) shape(1/4 1/32) 
```

 `shape(-1)` reproduce durante toto el tiempo 

### Otros sonidos:

Existen varias opciones para cargar  sonidos: 

1. podemos utilizar el menu de `sounds` para cargar los sonidos incluidos en Mercury
2. Cargando los sonidos en el menu en `add sounds` Esta opción permite subir los sonidos desde el ordenador aunque tiene que hacerse cada vez que se abre Mercury
3. Utilizando Freesound 

```jsx
set samples [ 'so1' 'https://cdn.freesound.org/previews/28/28141_214099-lq.mp3' ]

new sample so1
```

1. Subiendo los sonidos a github

```jsx
set samples [ crow 'https://raw.githubusercontent.com/linalab/livecoding-workshop-esmuc/main/sounds/crow_000_crow.wav' ]

new sample crow time(1/4)
```

1. Con un archivo .json  que se añade con  `add sounds`  

```json
{
 	"snare_short" : "https://cdn.freesound.org/previews/671/671221_3797507-lq.mp3",
 	"psykick" : "https://cdn.freesound.org/previews/145/145778_2101444-lq.mp3",
 	"hat_short" : "https://cdn.freesound.org/previews/222/222058_1676145-lq.mp3"
}
```

---

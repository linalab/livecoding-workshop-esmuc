# Hydra

Hoja de trabajo basada en el workshop de Citlali Hernandez AKA Turbulente. 

Versión WEB: https://hydra.ojack.xyz/
 Documentación:
Github: https://github.com/ojack/hydra#Getting-Started
Hydra Book: https://hydra-book.glitch.me/#/
Tutoriales y ejemplos: https://github.com/ojack/hydra/blob/main/examples/README.md

Aquí un listado de funciones de Hydra.
Todas ellas están aquí: https://ojack.xyz/hydra-functions/

`solid().out()`

//////////////// / / / SOURCES O TEXTURAS/ / / //////////////////

//NOISE
//Sintaxis: noise( scale: 10, offset: 0.1 )
//Ejemplo:
`noise(10, 0.1).out(o0)`

//VORONOI:
//Sintaxis:voronoi( scale: 5, speed: 0.3, blending: 0.3 )
//Ejemplo:
`voronoi(5,0.3,0.3).out(o0)`

//OSC
//Sintaxis: osc( frequency: 60, sync: 0.1, offset )
//Ejemplo:
`osc(10, 0.1, 1).out(o0)`

//SHAPE
//Sintaxis: shape( sides: 3, radius: 0.3, smoothing: 0.01 )
//Ejemplo:
`shape(3,0.5,0.001).out(o0)`

//GRADIENT
//Sintaxis: gradient( speed )
`gradient([1,2,4]).out(o0)`

//SOLID
//Sintaxis:solid( r, g, b, a: 1 )
`solid([1,0,0],[0,1,0],[0,0,1],1).out(o0)`

//////////////// / / / GEOMETRÍA / / / //////////////////

//ROTATE
//Sintaxis:rotate( angle: 10, speed )
//Ejemplo:
`osc(50).rotate(1, 0.5).out()`

//SCALE
//Sintaxis:scale( amount: 1.5, xMult: 1, yMult: 1, offsetX: 0.5, offsetY: 0.5 )
// La proporción de todo lo que sucede en Hydra está directamente relacionado con la resolución de la pantalla.
//Ejemplo:
`shape(3).out()` // Un triángulo

`shape(3).scale(0.5, 1,3).out()` //un triángulo alargado en Y

`shape(3).scale(0.5, 3,1).out()` //el mismo triángulo achatado en X

//PIXELATE
//Sintaxis:pixelate( pixelX: 20, pixelY: 20 )
//Ejemplo:
`osc(20, 0.2, 1).rotate(1, 0.5).pixelate(5,5).out()`

//REPEAT
//Sintaxis:repeat( repeatX: 3, repeatY: 3, offsetX, offsetY )
//Ejemplo:
`osc(10).rotate(1, 0.1).repeat(3,3).out()`

//KALEID
//Sintaxis:kaleid( nSides: 4 )
//Ejemplo:
`osc(20, 0.2, 1).rotate(1, 0.5).pixelate(5).kaleid().out()`

//SCROLLX
//Sintaxis:scrollX( scrollX: 0.5, speed )
//Ejemplo:
`shape(3).scale(1, 0.8).scrollX(1, 0.1).out()`

//SCROLLY
//Sintaxis:scrollY( scrollY: 0.5, speed )
//Ejemplo:
`shape(3).scrollY(1, 0.1).out()`

//////////////// / / / COLOR / / / //////////////////

//POSTERIZE
//Sintaxis:posterize( bins: 3, gamma: 0.6 )
//Ejemplo:
`osc(10, 0.1, 1).scrollX(1, 0.05).posterize( [1, 5, 15, 30]).out()`

//INVERT
//Sintaxis:invert( amount: 1 )
//Ejemplo:
`shape(3).invert().out()`

//CONTRAST
//Sintaxis:contrast( amount: 1.6 )
//Ejemplo:
`osc(20).contrast( ({time}) => Math.sin(time) * 5 ).out(o0)`

//BRIGHTNESS
//Sintaxis:brightness( amount: 0.4 )
//Ejemplo:
`osc(20,0,2)
  .brightness( ({time}) => Math.sin(time) )
  .out(o0)`

//LUMA
//Sintaxis:luma( threshold: 0.5, tolerance: 0.1 )
//Ejemplo:
`osc(10,0,1).luma(0.5,({time}) => Math.sin(time)).out(o0)`

//THRESH
//Sintaxis:thresh( threshold: 0.5, tolerance: 0.04 )
//Ejemplo:
`noise(3,0.1).thresh(0.5,0.04).out(o0)`

//COLOR
//Sintaxis:color( r: 1, g: 1, b: 1, a: 1 )
//Ejemplo:
`osc().color(1,0,3).out(o0)`

//SATURATE
//Sintaxis:saturate( amount: 2 )
//Ejemplo:
`osc(10,0,1).saturate( ({time}) => Math.sin(time) * 10 ).out(o0)`

//HUE
//Sintaxis:hue( hue: 0.4 )
//Ejemplo:
`osc(30,0.1,1).hue(({time}) => Math.sin(time)).out(o0)`

//COLORAMA
//Sintaxis:colorama( amount: 0.005 )
//Ejemplo:
// 20Hz oscillator source
// color sequence of Red, Green, Blue, White, Black
// colorama sequence of 0.005, 0.5, 1.0 at 1/8 speed
// output to buffer o0
`osc(20)
  .color([1,0,0,1,0],[0,1,0,1,0],[0,0,1,1,0])
  .colorama([0.005,0.33,0.66,1.0].fast(0.125))
  .out(o0)`

//////////////// / / / MODULATE / / / //////////////////
//MODULATE
//Sintaxis:modulate( color, amount: 0.1 ) // COLOR SE REFIERE A UNA TEXTURA O SOURCE
`shape(50).modulate(osc(20)).out()`

//Existen combinaciones de la función modulate:
  // modulate
  // modulateRepeat
  // modulateRepeatX , modulateRepeatY
  // modulateHue
  // modulateScale
  // modulateKaleid
  // modulatePixelate
  // modulateRotate
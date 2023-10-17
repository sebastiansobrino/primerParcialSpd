# Primera parte

## Integrantes

* Sebastian L. Sobrino

## Proyecto: Contador de dos digitos.

[![Trabajo-parte-1.png](https://i.postimg.cc/Pqc3Sm8Z/Trabajo-parte-1.png)](https://postimg.cc/R37LFJdV)

## Descripción
El proyecto consiste en un contador digital interactivo que muestra valores de 0 a 99 en dos displays de 7 segmentos. Esto es útil en aplicaciones donde se requiere llevar un conteo visual, como un marcador, un temporizador o un contador de productos. El contador utiliza 3 botones: Uno para sumar, otro para restar y el ultimo funciona para reiniciar a 0 el contador.

## Función principal
La función "loop" controla un contador de 0 a 99 utilizando dos displays de 7 segmentos y tres botones. Lee el estado de los botones de suma, resta y reset, ajustando el contador en consecuencia. La técnica de multiplexación se utiliza para mostrar los dígitos en los displays alternativamente. La función prenderLuces gestiona la visualización de las unidades y decenas del contador en los displays. Las funciones auxiliares configuran los segmentos de los displays, controlan qué display se enciende y gestionan el estado de los LEDs.

```
void loop() {      

  reset = digitalRead(RESET);
  sumar = digitalRead(SUMA);
  restar = digitalRead(DISMINUYE);
  
  if(sumar == 0)
  {
  	contador++;
   
      if(contador > 99)
    {
      contador = 0;
    }
  }
  
  if(restar == 0)
  {
    contador--;
    if(contador < 0)
    {
      contador = 99;
    }
  }
  
  if(reset == 0)
  {
     contador = 0;
  } 
  
  prenderLuces(contador);
}
```

## Link al proyecto

https://www.tinkercad.com/things/9I9aw647I0a-trabajoparte1/editel?sharecode=m3-GeQ2a5ULr5s4BRVGlyH1TbC9pf_xpekv5YyVTMmk

# Segunda parte

## Modificación con Interruptor Deslizante y Números Primos

[![Trabajo-parte-dos.png](https://i.postimg.cc/cHQqLHnt/Trabajo-parte-dos.png)](https://postimg.cc/XG712nxn)

## Descripción
Para esta segunda parte se Sustituye uno de los botones por un interruptor deslizante (switch) de dos posiciones.
Dependiendo de la posición del interruptor, el display debe mostrar o bien el contador (como en la Parte 1) o los números primos en el rango de 0 a 99. 

##Función principal
En la funcion principal, leemos el estado de los botones asi como del interruptor que nos avisa si el contador sera de numeros enteros o primos y el sensor de fuerza.
Si el sensor posee un valor mayor a 90, el contador permite sumar o restar numeros (Ya sea primos o enteros dependiendo del valor del interruptor.
En caso de que el sensor de fuerza sea menor a 90, el contador queda estancado en 0 hasta que se ejerza una fuerza mayor.
```
void loop() {      

  interruptor = digitalRead(INTERRUPTOR);
  sumar = digitalRead(SUMA);
  sensor = analogRead(SENSOR);
  restar = digitalRead(DISMINUYE);
  
  
  if (sensor > 90)
  {
    if(interruptor == 1)
    {
      if(sumar == 0)
      {
        contador++;

        if(contador > 99)
        {
          contador = 0;
        }
      }

      if(restar == 0)
      {
        contador--;
        if(contador < 0)
        {
          contador = 99;
        }
      }


      prenderLuces(contador);
    }

    else
    {
      if (verificarNumeroPrimo(contadorPrimo))
      {

        if(sumar == 0)
        {
          numeroAuxiliar = 1;
          contadorPrimo++;

          if(contadorPrimo > 97)
          {
            contadorPrimo = 2;
          }
        }
        else if(restar == 0)
        {
          numeroAuxiliar = 0;
          contadorPrimo--;

          if(contadorPrimo < 2)
          {
            contadorPrimo = 97;
          }
        }
      }
      else 
      {
        contadorPrimo = obtenerNumerosPrimos(contadorPrimo,numeroAuxiliar);
      }

      prenderLuces(contadorPrimo);
    }
  }
  else
  {
    contador = 0;
    prenderLuces(contador);
  }
}
```

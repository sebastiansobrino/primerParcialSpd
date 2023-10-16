# Documentacion

## Integrantes

* Sebastian L. Sobrino

## Proyecto: Contador de dos digitos.

[![Trabajo-parte-1.png](https://i.postimg.cc/Pqc3Sm8Z/Trabajo-parte-1.png)](https://postimg.cc/R37LFJdV)

## Descripción
El proyecto consiste en un contador digital interactivo que muestra valores de 0 a 99 en dos displays de 7 segmentos. Esto es útil en aplicaciones donde se requiere llevar un conteo visual, como un marcador, un temporizador o un contador de productos. El contador utiliza 3 botones: Uno para sumar, otro para restar y el ultimo funciona para reiniciar a 0 el contador.

## Función principal
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

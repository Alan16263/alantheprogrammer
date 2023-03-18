
# Rotary Encoder (KY-040)
![Image text](https://th.bing.com/th/id/R.f71b7bf0dba9210bfb8fa93290bb5d8e?rik=S2AUmiOrekcKKQ&pid=ImgRaw&r=0)

## Que es ?
El Módulo KY-040 es un codificador incremental con dos salidas levemente desfasadas, gracias a esto, veremos que se puede saber en que dirección estamos girando el eje.

Pines del codificador rotatorio KY-040
Un encoder rotativo tiene un número fijo de posiciones por revolución. El KY-40 tiene treinta, estas posiciones son marcadas por clicks conforme se va girando el encoder. Además, posee un pulsador interno.

En los codificadores incrementales (o de cuadratura) como este dispositivo, para saber en qué posición se encuentra, es necesario recurrir al software.

Su funcionamiento es más sencillo de lo que parece: el módulo genera señales digitales sobre los pines A y B. Señales que estarán en nivel alto y que conforme vayamos girando el eje,y en función de hacia qué lado lo giremos, una de esas señales cambiará de estado antes que la otra. Arduino es capaz de detectar estas señales.

## Ejemplo en codigo
*En este código se muestra el sentido de giro horario / antihorario y si se presionó el switch.*

```python
from machine import Pin
from time import sleep

SW = Pin(15, Pin.IN, Pin.PULL_UP)
DT = Pin(14, Pin.IN)      # encoder sin módulo Pin(14, Pin.IN, Pin.PULL_UP)
CLK  = Pin(13, Pin.IN)    # encoder sin módulo Pin(13, Pin.IN, Pin.PULL_UP)

valor_anterior = True
switch_presionado = False

while True:
     if valor_anterior != CLK.value():
         if CLK.value() == False:
             if DT.value() == False:
                 print("horario")
                 sleep(0.2)
             else:
                 print("antihorario")
                 sleep(0.2)
         valor_anterior = CLK.value()   

     if SW.value() == False and not switch_presionado:
         print("SW presionado") 
         switch_presionado = True
     if SW.value() == True and switch_presionado:
         switch_presionado = False
 ```

![Ejemplo del programa](https://github.com/Alan16263/alantheprogrammer/blob/main/Captura%20de%20pantalla%202023-03-15%20140739.gif)

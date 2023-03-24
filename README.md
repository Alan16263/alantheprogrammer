
# Rotary Encoder (KY-040)
![Image text](https://uelectronics.com/wp-content/uploads/2017/06/AR0056-KY-040-V10-500x500.jpg)

## Que es ?
El Módulo KY-040 es un codificador incremental con dos salidas levemente desfasadas, gracias a esto, veremos que se puede saber en que dirección estamos girando el eje.

Pines del codificador rotatorio KY-040
Un encoder rotativo tiene un número fijo de posiciones por revolución. El KY-40 tiene treinta, estas posiciones son marcadas por clicks conforme se va girando el encoder. Además, posee un pulsador interno.

En los codificadores incrementales (o de cuadratura) como este dispositivo, para saber en qué posición se encuentra, es necesario recurrir al software.

Su funcionamiento es más sencillo de lo que parece: el módulo genera señales digitales sobre los pines A y B. Señales que estarán en nivel alto y que conforme vayamos girando el eje,y en función de hacia qué lado lo giremos, una de esas señales cambiará de estado antes que la otra. Arduino es capaz de detectar estas señales.

## ¿Para que sirve el KY-040?
Este Encoder rotatorio es ampliamente utilizado en el control de motores paso a paso, servomotores, control de potenciómetros digitales, controles de máquinas industriales tales como los husillos de tornos y fresadoras CNC, brazos robóticos, controles de instrumentos electrónicos (diales) y hasta es posible verlos todavía en los viejos ratones de computadoras o en algunos TrackBall.

## Características:

- Tipo: Encoder rotatorio incremental
- Voltaje de alimentación: 5v
- Corriente: 10 mA
- Ciclos por revolución 30
- Pulsos por revolución: 20
- Dimensiones: 20 x 30 x 30 mm
- Peso: 10g

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

![Ejemplo del programa](https://github.com/Alan16263/alantheprogrammer/blob/main/Captura%20de%20pantalla%202023-03-17%20193745.jpg?raw=true)

https://wokwi.com/projects/360036869682546689

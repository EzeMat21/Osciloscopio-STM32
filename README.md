TP1 ESPECIAL OSCILOSCOPIO

Los datos son adquiridos a través del ADC a una tasa máxima alcanzada de conversión de 58,8kHz.
Los datos adquiridos son enviados por el puerto UART y visualizados en el programa SerialPlot.
(https://hackaday.io/project/5334-serialplot-realtime-plotting-software

Utilizando un buffer ping pong, se muestran por pantalla los valores de
tensión obtenidos del ADC. El ADC escribe sobre el buffer PING mientras
el puerto UART transmite el contenido del PONG, y luego se intercambian
es decir, el ADC comienza a escribir sobre el buffer PONG y el puerto
UART lo hace sobre el buffer PING. El UART transmite los datos cada vez que se llena, configurandolo a una tasa de 950.000 bits/s.

La maquina de estados tiene 14 estados. Podemos navegar por un menú a través de una pantalla TFT
donde podemos configurar la resolución de los datos, el tipo y umbral del trigger así como también la cantidad de muestras una vez disparado el trigger.
Luego del inicio se pasa al estado guardando_en_ping. Aquí el ADC
va llenando el buffer ping. Cuando este se llena, se activa el evento de
buffer lleno pasando a su vez al estado guardando_en_pong. En esta
transición el puntero de escritura del buffer se cambia, apuntando ahora
al buffer pong y se transmite por UART el contenido del buffer ping.
Ahora el ADC esta llenando el buffer pong, cuando este se llene
nuevamente se activa el evento de buffer lleno y transicionando
nuevamente al estado guardando_en_ping. En esta transición, el puntero
escritura vuelve a apuntar al buffer ping y se envia por el puerto uart
el contenido del buffer pong.

<img src="assets/WhatsApp Image 2024-12-18 at 22.35.58.jpeg" width="300"/> <img src="assets/WhatsApp Image 2024-12-18 at 18.23.42.jpeg" width="150"/>

Bibliografía o links consultados: Mastering STM32: Cap 12:
Analog-To-Digital Conversion STM32F103x8 Reference Manual Interrupciones
por timer:
https://deepbluembedded.com/stm32-timer-interrupt-hal-example-timer-mode-lab/


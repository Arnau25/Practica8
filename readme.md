# Practica 8 Buses de comunicación
### Codigo
````
#include <Arduino.h>

void setup() {
Serial.begin(9600);
Serial2.begin(9600);
  Serial.write("Inicializando...");
}

void loop() {

  if(Serial.available()){
    Serial2.write(Serial.read());
    delay(10);
    if(Serial2.available()){
      Serial.write(Serial2.read());
    }
  }
}

````
Para empezar en el void setup() observamos que hemos creado dos objetos de la clase Serial, los cuales tendran un valor de 9600 de baut rate.

Por lo que hace al void loop() observamos que mediante la función avaliable() miraremos si hay algo disponible para leer desde el serial port del UART0. A partir de ese momento escribimos cualquier cosa y esta se guardará en el buffer. Lo qu ehemos escrito que se a guardado en el buffer lo escribirá el UART2 mediante la función write(). Ya que tenemos cortocircuitados los puertos de recepción y transmisión, lo que transmitamos con write() se recibirá al mismo UART2 con avaliable(). Finalmente con la función read() leeremos lo que hay en el buffer del UART2 y lo escribiremos por el puerto serie del UART0.
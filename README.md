# Workshop 7
Séptimo workshop de la materia de automatización y control de procesos

- [Workshop 7](#workshop-7)
  - [Sensor](#sensor)
  - [Sistema embebido](#sistema-embebido)
    - [Hardware](#hardware)
    - [Software](#software)
  - [Conectividad](#conectividad)
    - [Conectividad física](#conectividad-física)
    - [Protocolo de comuniación](#protocolo-de-comuniación)
  - [Montaje](#montaje)
    - [Simulación](#simulación)
    - [Implementación física](#implementación-física)

## Sensor
Se utilizó el sensor de temperatura LM35 con una salida lineal de voltaje respecto a la temperatura en centigrados. Este sensor posee las siguientes caracteristicas: 
- Calibrado directamente en Celsius (Centigrados).
- Factor lineal de 10 mV/°C
- Exactitud de 0.5°C a 25°C
- Rango de operación de −55°C a 150°C
- Adecuado para aplicaciones remotas
- De bajo costo
- Opera en un rango 4 V a 30 V
- Consumo de corriente menor a 60μA
- Bajo auto calentamiento: 0.08°C en aire quieto
- No lienalidad tipica de ±¼°C

Referencia: [BME280 Datasheet](https://itbrainpower.net/downloadables/BST-BME280-DS002-1509607.pdf) 
## Sistema embebido
Se utiliza dos placas Arduino UNO con las siguientes especificaciones.
### Hardware
- Microcontrolador ATmega328P.
- Tiene 14 pines de entrada o salida análogicas, de los que se pueden usar 6 como salidas PWM (Pulse Width Modulation).
- Tiene 6 entradas análogas.
- Un resonador ceramico de 16 MHz.
- Un puerto para conexión USB
- Un conector para toma de corriente.
- Un botón de reinicio.
- Provee pines con compatibilidad con los protocolos UART, I2C y SPI.
- Tiene una velocidad de relog de 16MHz
- Tiene memorias SRAM, FLASH y EEPROM de 2KB, 32KB, 1KB respectivamente.
- Tiene unas dimensiones de 53.4 mm por 68.6 mm. 

Referencia: [UNO R3](https://docs.arduino.cc/hardware/uno-rev3)  
### Software
- El sistema se montó utilizando el lenguaje de programación C++.
- Se utiliza el firmware embebido en Arduino.
## Conectividad
### Conectividad física
### Protocolo de comuniación
## Montaje
### Simulación
Para la simulación se usó el software Tinkercad, con el cual se procedió a realizar el siguiente montaje:
![conexión circuito](Conexion.png)
En donde se puede evidenciar la siguiente implementacion
![simulacion](Simulacion.gif)
Se utiliza el siguiente código para el Arduino funcionando como controlador:
```c++
#include <Wire.h>
const int ledPIN = 13;

void setup()
{
 //by default A5 is the Serial Clock (SCL) 
//and the serial data(SDA) is A4
  pinMode(ledPIN , OUTPUT);
  Wire.begin();        // join i2c bus (address optional for master)
  Serial.begin(9600);  // start serial for output
}

void loop()
{
  Wire.requestFrom(2, 6);    // request 6 bytes from slave device #2
  String txtTemp="";
  while(Wire.available())    // slave may send less than requested
  {
    char tmpChar = Wire.read(); // receive a byte as character
    txtTemp+=tmpChar;
  }
  float tempCelsius=txtTemp.toFloat();
   Serial.println(txtTemp);
  Serial.println(tempCelsius);
  if(tempCelsius>30){
  digitalWrite(ledPIN , HIGH);  
  }
  else {
    digitalWrite(ledPIN , LOW); 
  }
  delay(500);
}
```
y el siguiente código para el Arduino que funciona como replica: 
```c++
#include <Wire.h>
int sensorPin=0;
float tempCenti=0.0;

void setup()
{
 //by default A5 is the Serial Clock (SCL) 
//and the serial data(SDA) is A4
  Serial.begin(9600);
  Wire.begin(2);                // join i2c bus with address #2
  Wire.onRequest(requestEvent); // register event
}

void loop()
{
  int reading=analogRead(sensorPin);
  float voltagemV=reading*(5000/1024.0);
  tempCenti=(voltagemV-500)/10;
  delay(100);
}

// function that executes whenever data is requested by master
// this function is registered as an event, see setup()
void requestEvent()
{
  String txtTempC= String(tempCenti,2);
  if(tempCenti<10){
  txtTempC="00"+txtTempC;
  }else if(tempCenti<100){
    txtTempC="0"+txtTempC;
  }
  Serial.println(txtTempC);
  /*String testLED="031.00";
  Wire.write(testLED.c_str());*/
   Wire.write(txtTempC.c_str());
  // respond with message of 6 bytes as expected by master
}
```
### Implementación física

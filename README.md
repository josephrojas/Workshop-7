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
- 
## Conectividad
### Conectividad física
### Protocolo de comuniación
## Montaje
### Simulación
Para la simulación se usó el software TInkercad, con el cual se procedió a realizar el siguietne montaje:
![conexión circuito](Conexion.png)
En donde se puede evidenciar la siguiente implementacion
![simulacion](Simulacion.gif)
### Implementación física

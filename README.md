# Documentacion_Parcial2_SPD
![ArduinoTinkercad](https://github.com/YieldingAsh/Documentacion_Parcial_SPD/assets/99512390/bab40be3-f0c3-4d94-9956-880f75f535fe)
# Integrantes
- Matias Nicolas Castrellon
# Visualizacion de proyecto en Tinkercad 
![image](https://github.com/YieldingAsh/SPD2_Practico/assets/99512390/4f36db6e-df14-4303-bed6-570cae1db6f9)
#Requisitos del Proyecto:
Objetivo:
El objetivo de este proyecto es diseñar un sistema de incendio utilizando Arduino que pueda
detectar cambios de temperatura y activar un servo motor en caso de detectar un incendio.
Además, se mostrará la temperatura actual y la estación del año en un display LCD.

Componentes necesarios:

Arduino UNO

Sensor de temperatura

Control remoto IR (Infrarrojo)

Display LCD (16x2 caracteres)

Servo motor

Cables y resistencias según sea necesario

Protoboard para realizar las conexiones

Dos leds.

Funcionalidad requerida:

Conexiones:
Conecta el sensor de temperatura al pin analógico A0 de Arduino.
Conecta el control remoto IR al pin digital 11 de Arduino.
Conecta el display LCD utilizando los pines correspondientes de Arduino.
Conecta el servo motor a uno de los pines PWM de Arduino (por ejemplo, pin 9).

Control remoto:
Configura el control remoto IR para recibir señales.
Define los comandos necesarios para activar y desactivar el sistema de incendio.
Utiliza un algoritmo para determinar la estación del año (por ejemplo, rangos de temperatura
para cada estación).
Detección de temperatura:
Configura el sensor de temperatura y realiza la lectura de la temperatura ambiente.
Muestra la temperatura actual en el display LCD.

Sistema de Procesamiento de Datos

Sistema de alarma:
Define un umbral de temperatura a partir del cual se considera que hay un incendio (por
ejemplo, temperatura superior a 60 grados Celsius).
Cuando se detecta un incendio (temperatura por encima del umbral), se activa el servo
motor para simular una respuesta del sistema de incendio.

Mensajes en el display LCD:
Muestra la temperatura actual y la estación del año en el display LCD.
Cuando se detecta un incendio, muestra un mensaje de alarma en el display LCD.

Punto libre:
Se deberá agregar dos leds y darle una funcionalidad de su elección, acorde al
proyecto previamente detallado.

Recuerda proporcionar un diagrama de conexiones y el código necesario para implementar
cada una de las funcionalidades requeridas. Esto ayudará a comprender y construir el
sistema de incendio con Arduino.

Aclaraciones para la aprobación de la parte práctica:
• Debe haber buen uso de las funciones.
• El código debe ser prolijo y legible.

1- debe poder explicar cada punto

2- debe poder modificar la funcionalidad agregando lo que sea necesario

3- Documentación:

• Deberán presentar un diagrama esquemático del circuito y explicar el
funcionamiento aplicado de cada componente.

• Presentar el código fuente del proyecto de Arduino listo para ser
implementado.

• Deberán explicar el funcionamiento integral utilizando documentación
MarkDown.

# Funcion principal

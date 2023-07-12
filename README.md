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
-La funcion loop es la funcion principal la cual toma el valor del sensor de temperatura luego lo imprime en el display, despues borrra lo que esta en el display y llama a la funcion est la cual imprime en el display en que estacion estamos o si hay un incendio
````
void loop()
{
  valor = analogRead(TMP);
  voltaje = ((valor * 5.00) / 1024.00);
  temperatura = ((voltaje - 0.5) * 100); 
  delay(100);
  lcd.print("Temperatura:");
  lcd.print(temperatura);
  delay(2000);
  est();
  comInc(temperatura, R);
  delay(2000);
  lcd.clear();
}
````
-Funcion que comprueba si hay un incendio teniendo en cuenta la diferencia de temperatura de la estacion elejida
````
void comInc(float T, int A)
{
  switch (A)
  {
    case 0:
    	if( T > 60)
        {
          incendio(true);
        }
    	break;
    case 1:
    	if( T > 15)
        {
          incendio(true);
        }
    	break;
    case 2:
    	if( T > 28)
        {
          incendio(true);
        }
    	break;
    case 3:
    	if( T > 25)
        {
          incendio(true);
        }
   		break;
    case 4:
    	if( T > 24)
        {
          incendio(true);
        }
    	break;
  }
}
````
-Esta funcion se activa cuando se detectaron mas de 60 grados lo indica que hya un incendio, la funcion hace un loop la cual imprime en el display que la Alarma de Incendio esta Activada y llamara la funcion parpadeo para que encienda el led rojo y se apague, cada vez que se repira un servo motor va activarse y se movera un 1 grado de su angulo de 0 hasta 180, se repetira 180 veces luego volvera a resetearse el servomotor a un angulo de 0 y volvera a repetirse siendo 180 y asi hasta que con el contro remoto infrarojo se pulse el boton de apagado para desactivar la alarma.
````
void incendio(bool e)
{
  while (e)
  {
    for(int pos = 0; pos<=180; pos++)
    {
      lcd.print("Alarma Incendio");
      lcd.setCursor(0,1);
      lcd.print("Activada");
      s1.write(pos);
      parpadear();
      if (IrReceiver.decode()) {        
        Serial.println(IrReceiver.decodedIRData.decodedRawData, HEX); 
        if (IrReceiver.decodedIRData.decodedRawData == Boton){
          e = false;
          break;
        }
        IrReceiver.resume();
      }
      lcd.clear();
      delay(20);
    }
  }
  s1.write(0);
}
````
-Esta funcion solo enciende el led rojo y lo apaga para simular un parpadeo
````
void parpadear()
{
  digitalWrite(ledRojo, HIGH);
  delay(500);
  digitalWrite(ledRojo, LOW);
  delay(500);
}
````
-Esta es la funcion la cual se fija en que estacion del año se encuentra y lo imprime en el display y si se encuentra por encima de los 60 grados la temperatura llamara la funcion incendio para activar la alarma de incendio, ademas de que si es invierno se encendera un led azul en cambio si es cualquier otra estacion se apagara el led azul
````
void est()
{
  if (IrReceiver.decode()) { 
      switch(IrReceiver.decodedIRData.decodedRawData)
      {
       case Boton1:
          lcd.clear();
          lcd.print("Estacion:");
          lcd.setCursor(0,1);
          lcd.print("Invierno");
          digitalWrite(ledRojo, HIGH);
          delay(2000);
          R = 1;
          break;

       case Boton2:
          lcd.clear();
          lcd.print("Estacion: Otono");
          digitalWrite(ledRojo, LOW);
  		  delay(2000);
          R = 2;
          break;

       case Boton3:
          lcd.clear();
          lcd.print("Estacion:");
          lcd.setCursor(0,1);
          lcd.print("Primavera");
          digitalWrite(ledRojo, LOW);
          delay(2000);
          R = 3;
          break;

       case Boton4:
          lcd.clear();
          lcd.print("Estacion: Verano");
          digitalWrite(ledRojo, LOW);
          delay(2000);
          R = 4;
          break;

       case Boton0:
          lcd.clear();
          lcd.print("Estacion:");
          lcd.setCursor(0,1);
          lcd.print("Ninguna");
          digitalWrite(ledRojo, LOW);
          delay(2000);
          R = 0;
          break;
      }
    Serial.println(IrReceiver.decodedIRData.decodedRawData, HEX); 
    IrReceiver.resume();
  }
}
````
-Esta funcion es el contructor
````
void setup()
{
  IrReceiver.begin(IR, DISABLE_LED_FEEDBACK);
  Serial.begin(9600);
  pinMode(ledAzul, OUTPUT);
  pinMode(ledRojo, OUTPUT);
  s1.attach(9);
  lcd.begin(16,2);
  s1.write(0);
}
````
-Aca se pueden ver las librerias usadas y las variable declaradas.
````
#include <IRremote.h>

#include <Servo.h>

#include <LiquidCrystal.h>

#define Boton 0xFF00BF00
#define Boton0 0xF30CBF00
#define Boton1 0xEF10BF00
#define Boton2 0xEE11BF00
#define Boton3 0xED12BF00
#define Boton4 0xEB14BF00




int rs = 2;
int e = 3;
int d4 = 4;
int d5 = 5;
int d6 = 6;
int d7 = 7;
int TMP = 0;
int ledAzul = 8;
int ledRojo = 10;
int IR = 11;
int R = 0;
Servo s1;

//pri mas 17 menor 25
//vera mas 21 menor 24
//oto mas 13 menor 28
//invierno mas 8 menor 12

float temperatura = 0;
float valor = 0;
float voltaje = 0;

LiquidCrystal lcd(rs, e, d4, d5, d6, d7);
````
# Link del projecto
https://www.tinkercad.com/things/7GzFudXk5pL
# Link del codigo fuente
https://onlinegdb.com/Jm8BNFpeC

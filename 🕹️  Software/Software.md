# CODIGO ARDUINO

#include <Servo.h>

const int pinSensor = A0;  // Pin del sensor de presión conectado al NanoArduino
const int servo1Pin = 8;    // Pin del primer servomotor
const int servo2Pin = 9;    // Pin del segundo servomotor

Servo servo1;               // Crear objeto para el primer servomotor
Servo servo2;               // Crear objeto para el segundo servomotor

void setup() {
  Serial.begin(9600);      // Iniciar la comunicación serial
  servo1.attach(servo1Pin); // Conectar el primer servomotor al pin D8
  servo2.attach(servo2Pin); // Conectar el segundo servomotor al pin D9
}

void loop() {
  int valorSensor = analogRead(pinSensor);  // Leer el valor del sensor
  float voltaje = valorSensor * (5.0 / 1023.0);  // Convertir a voltaje

  Serial.print("Valor del sensor de presión: ");
  Serial.print(valorSensor);
  Serial.print(" - Voltaje: ");
  Serial.println(voltaje, 3);  // Mostrar el voltaje con 3 decimales

  // Comprobar si el voltaje supera 1.630V
  if (voltaje > 1.710) {
    Serial.println("Voltaje superado, activando servos.");  // Mensaje de depuración
    servo1.write(90);  // Girar el primer servomotor a 90 grados
    servo2.write(90);  // Girar el segundo servomotor a 90 grados
    delay(1000);       // Mantener en esa posición por 1 segundo

    // Regresar a la posición original
    servo1.write(0);   // Regresar el primer servomotor a 0 grados
    servo2.write(0);   // Regresar el segundo servomotor a 0 grados
    Serial.println("Servos regresando a la posición original."); // Mensaje de retorno
    delay(1000);       // Mantener en esa posición por 1 segundo
  }

  delay(1000);  // Esperar 1 segundo antes de la siguiente lectura

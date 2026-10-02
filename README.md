[codigo.txt](https://github.com/user-attachments/files/32971788/codigo.txt)# invernadero-inteligente-

Este proyecto integra un sistema automatizado de control ambiental programado en Arduino que monitorea en tiempo real la temperatura y la humedad mediante sensores analógicos en los pines A0 y A1, desplegando los datos en un monitor serial y en una pantalla LCD 16x2. A través de su lógica de control, el código reacciona a los valores medidos girando un servomotor a 90° en el pin 7 para abrir una compuerta al superar los 30 °C, encendiendo un motor extractor en el pin 8 junto a una alarma en el pin 13 si la temperatura excede los 40 °C, y activando la bomba de riego en el pin 12 cuando la humedad supera el 30 %, todo respaldado por una pausa de 500 ms que garantiza la estabilidad de las lecturas.

<img width="667" height="707" alt="image" src="https://github.com/user-attachments/assets/0de99457-378b-4fb6-bdf7-6730ec5876ac" />

<img width="715" height="432" alt="image" src="https://github.com/user-attachments/assets/5c691b0e-bf86-482c-af00-6f8ff0188979" />

[Uploadin#include <Adafruit_LiquidCrystal.h>
#include <Servo.h>

int TEMPERATURA = 0;
int HUMEDAD = 0;

Adafruit_LiquidCrystal lcd_1(0);
Servo servo_7;

void setup()
{
  lcd_1.begin(16, 2);
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
  Serial.begin(9600);
  
  servo_7.attach(7, 500, 2500);
  pinMode(8, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);

  lcd_1.setBacklight(1);
}

void loop()
{
  // Cálculo de temperatura y humedad
  TEMPERATURA = (-40 + 0.488155 * (analogRead(A0) - 20));
  HUMEDAD = map(analogRead(A1), 0, 1023, 0, 117);

  // Mostrar Temperatura en LCD y Monitor Serial
  lcd_1.setCursor(0, 0);
  lcd_1.print("T=     "); // Espacios para limpiar residuos anteriores
  lcd_1.setCursor(2, 0);
  lcd_1.print(TEMPERATURA);
  Serial.print("Temperatura: ");
  Serial.println(TEMPERATURA);

  // Mostrar Humedad en LCD y Monitor Serial
  lcd_1.setCursor(0, 1);
  lcd_1.print("H=     "); // Espacios para limpiar residuos anteriores
  lcd_1.setCursor(2, 1);
  lcd_1.print(HUMEDAD);
  Serial.print("Humedad: ");
  Serial.println(HUMEDAD);

  // Valores predeterminados (apagado / posición inicial)
  servo_7.write(0);
  digitalWrite(8, LOW);

  // Control del Servo según la temperatura
  if (TEMPERATURA > 30 && TEMPERATURA <= 40) {
    servo_7.write(90);
  } 
  
  // Control de Alarma y Servo para temperaturas más altas
  if (TEMPERATURA > 40 && TEMPERATURA <= 50) {
    servo_7.write(90);
    digitalWrite(8, HIGH); // Encender pin 8
    tone(13, 1661, 1000);  // Tono de alarma
  }

  // Control de Humedad (Pin 12)
  if (HUMEDAD > 30) {
    digitalWrite(12, HIGH);
  } else {
    digitalWrite(12, LOW);
  }

  delay(500); // Pausa para que se alcance a leer bien en la simulación
}g codigo.txt…]()

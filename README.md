# Reporte-3 Práctica ESP32 con DHT11 y Lcd
Programación de un ESP32 con un sensor de temperatura DHT11 y un LCD 16x2(I2C)
## Introducción
## Descripción
Utilizaremos l plataforma WOKWI para simular la adquisición de datos de temperatura y humedad del ambiente mediante un sensor DTH11 y la prorgramación del mismo en un microcontrolador ESP32, los datos se mostrarán en una pantalla LCD

## Material Necesario
Para realizar esta practica necesitas lo siguiente

Plataforma WOKWI
Tarjeta ESP 32
Sensor de temperatura y húmedad modelo DHT11
Pantalla LCD 16x2(I2C)

## Instrucciones
### PREVIO
1. Abrir la plataforma WOKWI.

### Preparación
3. Ir a la pestaña de sketch.ino y borrar el codigo e programación predeterminado
4. Abrir la terminal de programación y colocar la siguente programación:
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");

  delay(1000);
}
```




4. Ir a la pestaña "Library manager" haer clic sobre el icon "+", buscar la libreria "DHT sensor library for ESPx" y agregarla
![](https://github.com/Dave-Mejia/Reporte-2/blob/main/Libreria%20DHT.png?raw=true)

5. Ir al esquema de simulacón, dar clic al icono "+ (add new part)", buscar el sensor DTH11 y agregar
6. Ir al esquema de simulacón, dar clic al icono "+ (add new part)", buscar la pantalla LCD 16x2(I2C)
   
7. Colocar el sensor y la pantalla sobre el esquema de simulación y conectar como indica la figura de abajo
![](https://github.com/Dave-Mejia/Reporte-3-David-Mejia/blob/main/Conexion%20Tarjeta%20ESP32,%20Sensor%20DHT22%20y%20pantalla%20LCD.png?raw=true)

8. Agregar al codigo los siguietes codigos al programa para añadir mensajes adicionales como "bienvenido" "al modulo 5"
     lcd.clear();
     lcd.setCursor(2, 1);
     lcd.print("Bienvendos");
     delay(1000);

```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.clear();
  lcd.setCursor(2, 1);
  lcd.print("Bienvendos");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 1);
  lcd.print("Modulo 5");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 1);
  lcd.print("David Mejia");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  delay(1000);


  delay(1000);
}
```

### Operación
9. Iniciar simulador dando clic en el icono "play"
10. Visualizar los datos en el monitor serial.
11. Colocar la temperatura y humedad dando doble click al sensor DHT11

## Resultados
Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.
![](https://github.com/Dave-Mejia/Reporte-3-David-Mejia/blob/main/Resultado%20ESP32%20sensor%20DTH22%20y%20pantalla%20LCD.png?raw=true)
![](https://github.com/Dave-Mejia/Reporte-3-David-Mejia/blob/main/Resultado%20ESP32%20sensor%20DTH22%20y%20pantalla%20LCD%202.png?raw=true)
![](https://github.com/Dave-Mejia/Reporte-3-David-Mejia/blob/main/Resultado%20ESP32%20sensor%20DTH22%20y%20pantalla%20LCD%203.png?raw=true)

## Créditos
Ralizado por el Ingeniero David Mejía

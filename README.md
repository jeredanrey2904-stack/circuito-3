# circuito-3
iluminacion automatica 

Descripción

Este proyecto implementa un sistema de iluminación automática utilizando un Arduino Uno y un sensor LDR (fotoresistencia). El sistema realiza cinco lecturas consecutivas de la intensidad de luz, calcula el promedio y enciende un LED diferente según el nivel de iluminación detectado.

Además, muestra en el Monitor Serie el valor promedio de la luz y el estado actual del sistema.

Componentes

Arduino Uno R3 Protoboard Sensor LDR (Fotoresistencia) Resistencia de 10 kΩ (para el divisor de voltaje del LDR) 3 LEDs (verde, amarillo y rojo) 3 resistencias de 220 Ω Cables jumper Funcionamiento

El sensor LDR mide la intensidad de luz del ambiente. El Arduino realiza cinco lecturas consecutivas. 
Se calcula el promedio de las lecturas. Dependiendo del valor promedio: Menor de 300: se enciende el 
LED rojo (ambiente oscuro). Entre 300 y 599: se enciende el 
LED amarillo (iluminación media). 
Mayor o igual a 600: se enciende el LED verde (ambiente iluminado).
El Monitor Serie muestra el valor promedio y el estado del sistema.

Archivo INO 
int lecturas[5];
int suma = 0;
int promedio = 0;

// Pines de los LEDs
const int ledVerde = 8;
const int ledAmarillo = 9;
const int ledRojo = 10;
const int ldr = A0;

// SETUP: se ejecuta UNA SOLA VEZ al inicio
void setup() {
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarillo, OUTPUT);
  pinMode(ledRojo, OUTPUT);
  Serial.begin(9600);
  Serial.println("Sistema de iluminacion iniciado...");
}

// LOOP: se ejecuta en BUCLE infinito
void loop() {

  // BUCLE FOR para llenar el ARRAY con 5 lecturas
  suma = 0;
  for (int i = 0; i < 5; i++) {
    lecturas[i] = analogRead(ldr);
    suma = suma + lecturas[i];
    delay(100);
  }

  // Calcular promedio
  promedio = suma / 5;
  Serial.print("Luz promedio: ");
  Serial.println(promedio);

  // CONDICIONAL IF...ELSE para controlar los LEDs
  if (promedio < 300) {
    // Oscuridad total
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarillo, LOW);
    digitalWrite(ledRojo, HIGH);
    Serial.println("Estado: OSCURO - LED Rojo ON");
  }
  else if (promedio >= 300 && promedio < 600) {
    // Luz media
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarillo, HIGH);
    digitalWrite(ledRojo, LOW);
    Serial.println("Estado: MEDIO - LED Amarillo ON");
  }
  else {
    // Mucha luz
    digitalWrite(ledVerde, HIGH);
    digitalWrite(ledAmarillo, LOW);
    digitalWrite(ledRojo, LOW);
    Serial.println("Estado: ILUMINADO - LED Verde ON");
  }

  delay(500);
}
<img width="1437" height="661" alt="image" src="https://github.com/user-attachments/assets/83c6fe18-e69c-4c9d-8804-a216d2806e02" />

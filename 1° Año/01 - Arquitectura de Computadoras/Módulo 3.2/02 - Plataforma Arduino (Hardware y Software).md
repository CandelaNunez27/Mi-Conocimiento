Arduino es una plataforma de electrónica de código abierto (Open Hardware y Open Software) muy popular para prototipado rápido.

## 1. Hardware: Placa Arduino UNO
* **Microcontrolador:** ATmega328.
* **Pines Digitales (0 al 13):** Pueden leer o emitir estados binarios (HIGH=5V, LOW=0V). Algunos tienen el símbolo `~`, lo que indica que soportan **PWM (Modulación por Ancho de Pulso)** para simular salidas analógicas (como variar el brillo de un LED).
* **Pines Analógicos (A0 al A5):** Tienen un Conversor Analógico a Digital (ADC). Transforman un voltaje (0 a 5V) en un número entero (0 a 1023).
* **Pines de Alimentación:** 5V, 3.3V, GND (Tierra), y Vin.

## 2. Estructura del Código (Lenguaje C/C++)
Todo programa de Arduino (llamado *Sketch*) tiene obligatoriamente dos funciones principales:

```cpp
// 1. Zona de declaración de variables globales
int led = 13; 

// 2. Función SETUP: Se ejecuta UNA SOLA VEZ al encender.
// Se usa para configurar pines o iniciar comunicaciones.
void setup() {
  pinMode(led, OUTPUT); // Configura el pin 13 como salida
  Serial.begin(9600);   // Inicia la comunicación con la PC
}

// 3. Función LOOP: Se ejecuta CÍCLICAMENTE hasta el infinito.
// Es el núcleo del programa.
void loop() {
  digitalWrite(led, HIGH); // Enciende el LED
  delay(1000);             // Espera 1000 milisegundos (1 segundo)
  digitalWrite(led, LOW);  // Apaga el LED
  delay(1000);             // Espera 1 segundo
}
```


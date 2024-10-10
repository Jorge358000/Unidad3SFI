# Unidad3SFI

### ¿Cómo se ve un protocolo binario?
- El protocolo binario se basa en el intercambio de datos en formas de bits, estos mensajes se van enviando en una estructura conformada por header, payload y footer (cabeza, cuerpo y cola)
  un ejemplo podrías ser  ([Header: Información de control][Payload: Datos reales][Footer: Verificación de datos]).
### Header
La cabeza es la primera parte del protocolo, y está contiene la longitud, tipo y otros datos; su función es identificar las caracterisitcas del mensaje para darle una correcta
interpretación
### Payload
El cuerpo transmite correctamente el mensaje, una vez se identifica que tipo de mensaje este es enviado a los sensores, comandos o a dónde se le solicite.
### Footer
Este principalmente detecta problemas o errores que se puedan encontrar en el mensaje codificado.

```C++
void setup() {
    Serial.begin(115200);
}

void loop() {
// 45 60 55 d5// https://www.h-schmidt.net/FloatConverter/IEEE754.htmlstatic float num = 3589.3645;
static uint8_t arr[4] = {0};

if(Serial.available()){
if(Serial.read() == 's'){
            memcpy(arr,(uint8_t *)&num,4);
            Serial.write(arr,4);
        }
    }
}
```
Esté código trabaja en little-endian, debido a que manda desde el byte más pequeño hasta el más grande, ya para hacerlo con Big-Edian sería con un array, así

```C++
void setup() {
    Serial.begin(115200);
}

void loop() {
// 45 60 55 d5// https://www.h-schmidt.net/FloatConverter/IEEE754.htmlstatic float num = 3589.3645;
static uint8_t arr[4] = {0};
static float num = 3589.3645;

if(Serial.available()){
if(Serial.read() == 's'){
            memcpy(arr,(uint8_t *)&num,4);
            for(int8_t i = 3; i>=0; i--){
              Serial.write(arr[i]);
            }
            
        }
    }
}
```

### Punto 5
```C++
void setup() {
    Serial.begin(115200);
}

void loop() {
    // Números en punto flotante
    float num1 = 3589.3645;
    float num2 = -1234.5678;
    
    // Arreglos para almacenar los bytes
    uint8_t arr1[4] = {0};
    uint8_t arr2[4] = {0};

    // Copiar los números a los arreglos en formato little-endian
    memcpy(arr1, (uint8_t *)&num1, 4);
    memcpy(arr2, (uint8_t *)&num2, 4);

    // Enviar en formato little-endian
    Serial.println("Little-endian:");
    for (int i = 0; i < 4; i++) {
        Serial.print(arr1[i]);  // Imprime en formato decimal
        Serial.print(" ");
    }
    Serial.println();
    for (int i = 0; i < 4; i++) {
        Serial.print(arr2[i]);  // Imprime en formato decimal
        Serial.print(" ");
    }
    Serial.println();

    // Enviar en formato big-endian
    Serial.println("Big-endian:");
    for (int i = 3; i >= 0; i--) {
        Serial.print(arr1[i]);  // Imprime en formato decimal
        Serial.print(" ");
    }
    Serial.println();
    for (int i = 3; i >= 0; i--) {
        Serial.print(arr2[i]);  // Imprime en formato decimal
        Serial.print(" ");
    }
    Serial.println();

    // Esperar un segundo antes de volver a enviar
    delay(1000);
}
```


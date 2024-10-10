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



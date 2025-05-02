# Microbi-python

## Contador microbit 9-0
'''python
from microbit import *

count = 9
display.show(count)

while True:
    if button_a.is_pressed() and button_b.is_pressed():
        count = 0
        display.scroll(count)
    elif button_b.is_pressed():
        count -= 1
        display.scroll(count)
    elif button_a.is_pressed():
        display.scroll(count)
    sleep(100) '''


– Contador 0 a 9 , agitando el microbit
from microbit import *

contador = 0

while True:
    if accelerometer.was_gesture("shake"):
        contador += 1
        display.clear()  # Limpia la pantalla antes de mostrar el número
        display.show(str(contador))  # Muestra el número actualizado
        sleep(1000)  # Espera 1 segundo para mostrar el número
— RADIO 
EMISOR
from microbit import *
import radio

# Configuración de radio
radio.on()
radio.config(channel=7)  # Canal de comunicación
mensaje = "¡Hola, receptor!"

# Envía el mensaje una vez
radio.send(mensaje)
display.show("SND")  # Muestra "SND" como indicador de envío

# Espera una confirmación durante 2 segundos
respuesta = radio.receive()

if respuesta == "OK":
    display.show("OK")  # Si recibe confirmación, muestra "OK"
    sleep(1000)  # Muestra la confirmación por un segundo
else:
    display.show("ERR")  # Si no recibe confirmación, muestra "ERR"

–RECEPTOR
from microbit import *
import radio

# Configuración de radio
radio.on()
radio.config(channel=7)

while True:
    # Espera recibir un mensaje
    mensaje_recibido = radio.receive()
    
    if mensaje_recibido:
        # Muestra primero la confirmación "OK"
        radio.send("OK")
        display.show("OK")  # Muestra "OK" como confirmación
        sleep(1000)  # Muestra la confirmación por un segundo
        
        # Luego muestra el mensaje recibido
        display.clear()
        display.scroll(mensaje_recibido)  # Despliega el mensaje recibido
        break  # Termina el proceso después de mostrar el mensaje
    else:
        display.clear()
        sleep(100)

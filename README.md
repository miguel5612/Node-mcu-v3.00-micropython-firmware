# Nodemcu v3.00 micropython-firmware

Este repositorio es la compilacion de los pre-requisitos que necesitas para flashar una nodemcu con micropython.

## Instalacion


1. Tu necesitas que tener instalado [ Python 2.7 o Python 3.4 ] los cuales los encuentras para descargar en: (https://www.python.org/downloads/).

2. instalar pip para python (https://pip.pypa.io/en/stable/installing/).

3. Necesitas descargar previamente la ultima version de esptool, que puedes encontrar en el folder --> esptool o en el repositorio --> (http://pypi.python.org/pypi/esptool) 
   Este repositorio lo puedes clonar con git:
	```
	   git clone https://github.com/miguel5612/Node-mcu-v3.00-micropython-firmware	
	``` 
	O puedes  clonar unicamente el esptool.
	```
	   git clone https://github.com/espressif/esptool	
	``` 
	
4. Dentro del folder esptool por cualquiera de los dos metodos anteriores puedes instalar ahora esptool con el siguiente comando:
	```
		pip install esptool
	```
5. Debes descargar el firmware oficial de micropython que se encuentra dentro de la carpeta esptool(esp8266-20170108-v1.8.7), bin(esp8266-20170108-v1.8.7) o en el repositorio: (http://micropython.org/download#esp8266).

6. Vas a cargar el firmware a la tarjeta:

	Los comandos son los siguientes, el primero sera borrar el firmware que contiene la board de fabrica.
	```
		esptool.py --port COM8 write_flash -fm dio -fs 4MB -ff 40m 0x00000 esp8266-20170108-v1.8.7.bin
	```
	Donde COM8 es el puerto donde se encuentra la tarjeta, lo puedes ver en --> panel de control - Dispositivos e impresoras.
	(sino te aparece debes instalar el driver CH340).

	Accion seguida procedemos a cargar el firmware con el siguiente comando:

	```
		esptool.py --port COM8 erase_flash
	```

	En donde el puerto sigue siendo el mismo que el anterior y esp8266-20170101-v1.8.7.bin es el nombre del archivo binario que has descargado de la pagina de micropython o de mi repositorio.

7. Descarga putty y conectate al puerto COM8 o al puerto en el que tengas la tarjeta (https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

8. Cuando te conectes deberias activar webrepl para subir tus scripts personalizados a la tarjeta, esto se realiza de la siguiente manera (en putty escribes los siguientes comandos):
	
	```
		import network
		sta_if = network.WLAN(network.STA_IF)
		ap_if = network.WLAN(network.AP_IF)
		sta_if.active(True)
		sta_if.connect('<your ESSID>', '<your password>')

	```
	ESSID --> Es el nombre de tu WiFi.
	your password --> La contraseña de tu wifi.

	Con el siguiente comando consultas la ip que obtuvó el modulo.

	```
		sta_if.ifconfig()
	```

9. Conociendo de antemano la ip puedes realizar ahora la configuracion de webrepl.
	
	Ahora para activar debes escribir en putty el siguiente comando: 

	```
		import webrepl_setup
	```

	Luego te va a preguntar si lo deseas habilitar, confirmas escribiendo E en mayuscula y presionando enter.
	Ademas estableceras una contraseña que es importante para el paso siguiente (Establecer una que sea facil de recordar)


10. Ahora abres la pagina oficial de webrepl (http://micropython.org/webrepl/?)

	Recuerda que debes conectarte por http, https aun no funciona.
	En donde dice --> ws://192.168.4.1:8266/
	Colocas la ip de tu modulo y el puerto 8266.
	Presionas conect y te solicita la contraseña.

11. Si ya tienes un programa que has probado previamente puedes cargarlo con la opcion Send a file.
	
	El archivo main.py se ejecuta de manera automatica al arranque, si deseas que tu programa este en ejecucion todo el tiempo
	simplemente lo llamas main.py y lo cargas a la tarjeta.

12. Si deseas mas informacion estaremos compartiendo tutoriales en un mes por el canal:

	https://www.youtube.com/channel/UChulzd52h5A4RdtJOXI8o8w?view_as=subscriber



## Agradecimientos

	Agradecimientos a esptool (https://github.com/espressif/esptool).
	Agradecimientos a micropython(http://docs.micropython.org/en/v1.9.3/esp8266/esp8266/tutorial/network_basics.html).

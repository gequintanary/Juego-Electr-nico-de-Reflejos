# Diagrama de bloques

En esta carpeta se presenta el diagramas de bloques que describe la arquitectura funcional del sistema y la interacción entre sus módulos.

<p align="center">
  <img width="565" height="796" alt="Diagrama de Bloques" src="https://github.com/user-attachments/assets/10ea5bc7-768e-4689-b376-a7c444626e4e" />
</p>


1. Fuente de alimentación (5 V DC)

Proporciona la energía necesaria para el funcionamiento de todo el circuito. Esta etapa suministra un voltaje continuo y estable a todos los componentes del sistema durante la operación del juego.

2. Pulsador de inicio

Es el primer elemento de interacción con el usuario. Al presionarlo, genera la señal que activa el temporizador NE555 e inicia una nueva ronda del juego.

3. Temporizador NE555 (Modo monoestable)

Actúa como el controlador del tiempo de respuesta. Cuando recibe la señal del pulsador de inicio, genera un único pulso cuya duración está determinada por la red RC del circuito. Este pulso define el intervalo en el que el jugador puede responder correctamente.

4. LED de estímulo

Indica visualmente al jugador que el tiempo de respuesta ha comenzado. Mientras este LED permanece encendido, el usuario debe presionar el segundo pulsador para registrar una respuesta válida.

5. Pulsador del usuario

Corresponde al botón que utiliza el jugador para responder. Al ser presionado, envía una señal al circuito, la cual será evaluada para determinar si la respuesta ocurrió dentro del tiempo establecido.

6. Etapa de validación

Esta etapa verifica si el segundo pulsador fue accionado mientras la salida del NE555 permanecía activa. Si la respuesta ocurre dentro del intervalo permitido, la señal continúa hacia la siguiente etapa; de lo contrario, se bloquea y el sistema no registra un acierto.

7. Transistor BJT NPN

El transistor 2N2222 funciona como un interruptor electrónico. Cuando recibe una señal válida desde la etapa de validación, se activa y permite el paso de corriente hacia los dispositivos de salida.

8. Actuadores de Salida
Una vez que el transistor se activa, se energizan los elementos que indican el resultado del juego:
  - LED indicador: Se enciende para confirmar que el jugador respondió correctamente dentro del tiempo establecido.
  - Zumbador piezoeléctrico: Emite una señal sonora que confirma el acierto y proporciona una retroalimentación inmediata al usuario.

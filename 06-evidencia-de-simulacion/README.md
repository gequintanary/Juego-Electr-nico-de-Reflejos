# Evidencia de simulación

En esta carpeta se reúnen capturas, archivos y resultados de simulación que verifican el comportamiento esperado.

**Figura 4. Formas de onda de temporización en el osciloscopio virtual**
<img width="633" height="365" alt="image" src="https://github.com/user-attachments/assets/7a677c2e-b2b3-41fb-b2df-9d7509235a15" />

Fig 4. Análisis gráfico de las señales del circuito en Proteus VSM.. La gráfica muestra el comportamiento de las señales principales del circuito durante la simulación. El trazo amarillo (Canal A) representa la señal de activación que inicia el temporizador mediante un pulso de bajada. El trazo azul (Canal B) muestra cómo el capacitor C1 se carga progresivamente hasta alcanzar el nivel necesario para activar el cambio de estado. Finalmente, el trazo rojo (Canal C) corresponde a la señal de salida del NE555, donde se observa el pulso en nivel alto generado durante el tiempo configurado.

--- 

**Figura 5. Circuito en estado de reposo o espera (Estado 1)**
<img width="915" height="563" alt="image" src="https://github.com/user-attachments/assets/7a7d72b0-e9f6-4263-8723-804fa05c07d3" />
Fig 5. Condición inicial del juego electrónico, estado normal. Ningún pulsador ha sido accionado, el temporizador NE555 se encuentra inactivo y todos los indicadores visuales y sonoros permanecen apagados.

--- 

**Figura 6. Activación de la ventana de desafío (Estado 2)**
<img width="933" height="560" alt="image" src="https://github.com/user-attachments/assets/ff46c683-78de-4406-a8bb-b59feb0910c3" />
Fig 6. Al accionar el pulsador de inicio, el circuito NE555 genera un pulso en estado alto que enciende el LED verde de estímulo (LED1V), indicando la ventana de tiempo exacta en la que el usuario debe reaccionar (El LED dura solo unos segundos encendido pero para demostrar el funcionamiento se dejó el botón presionado).

--- 

**Figura 7. Respuesta correcta y a tiempo del jugador (Estado 3)**
<img width="931" height="573" alt="image" src="https://github.com/user-attachments/assets/c88da5a8-50ab-4f38-b970-184611c0a22c" />
Fig 7. Estado del circuito cuando el usuario responde a tiempo. Al presionar el segundo pulsador mientras el LED1V permanece encendido, el transistor Q1 entra en saturación, permitiendo el paso de corriente que activa simultáneamente el LED2V y el zumbador. Esto indica que el usuario presionó el botón dentro del tiempo establecido del circuito, registrando una respuesta correcta.

--- 

**Figura 8. Respuesta anticipada o tardía (Estado 4)**
<img width="939" height="572" alt="image" src="https://github.com/user-attachments/assets/ee071725-4b94-42bb-815a-30e7e865ca43" />
Fig 8. Estado del circuito cuando el usuario responde fuera del tiempo permitido. Si el segundo pulsador se presiona antes o después de la ventana de tiempo generada por el NE555, el LED1V ya no se encuentra activo, por lo que el transistor Q1 no se activa. Como resultado, el LED2V y el zumbador permanecen apagados, indicando que la respuesta del jugador fue incorrecta o demasiado tardía.

--- 

**Figura 9. Medición exacta del tiempo de retardo con Counter Timer**
<img width="868" height="668" alt="image" src="https://github.com/user-attachments/assets/a1ed44b5-92a8-4942-ae26-bd8176181af2" />
Fig 9. Verificación del tiempo de salida del NE555. El medidor digital de Proteus muestra una duración de 0.516 segundos para el pulso en estado alto, valor que coincide con el tiempo calculado en el diseño analítico y confirma el correcto funcionamiento de la etapa de temporización.

--- 

**Figura 10. Comprobación del voltaje de alimentación (VCC)** 
<img width="727" height="569" alt="image" src="https://github.com/user-attachments/assets/d61c47d5-a870-4ca3-b96c-bf759f6f209c" />
Fig 10. Medición del voltaje de alimentación del circuito en el entorno de simulación. El voltímetro de corriente continua (DC) registra un valor de 5.00 V, confirmando que la fuente proporciona un suministro estable y adecuado para el correcto funcionamiento del sistema.

--- 

**Figura 11. Medición del voltaje de salida (VOH) y corriente del LED** 
<img width="863" height="677" alt="image" src="https://github.com/user-attachments/assets/1e34ef50-259f-487f-9dbf-48009d2ed93d" />
Fig 11. Medición del voltaje y la corriente en el circuito mediante un voltímetro y un amperímetro de corriente continua (DC). Las mediciones muestran un voltaje de 4.88 V en la salida (Pin 3) del NE555 y una corriente de 12.0 mA en la rama del LED verde, valores que confirman el correcto funcionamiento de la etapa de salida y la polarización del circuito.

--- 

**Figura 12. Medición de saturación del transistor y caída de voltaje en el diodo**
<img width="862" height="515" alt="image" src="https://github.com/user-attachments/assets/660bbc37-4253-4d65-b0e2-858ce297c602" />
Fig 12. Medición del voltaje en el transistor 2N2222 y en el diodo 1N4148 durante una respuesta correcta del juego. Se registra un voltaje Colector-Emisor (VCE) de 0.36 V, indicando que el transistor se encuentra en saturación, y una caída de tensión de 0.70 V en el diodo 1N4148, valor esperado para su funcionamiento en polarización directa.




**VIDEO**

https://github.com/user-attachments/assets/e7d81720-b110-4fce-86c7-c1d413f1fb88

Secuencia de funcionamiento del circuito
1. Estado de reposo (0:00 – 0:06)

Al energizar el circuito con una fuente de 5.00V, el temporizador NE555 permanece en estado de reposo, por lo que su salida (Pin 3) se mantiene en nivel bajo (0V).

En estas condiciones, la corriente circula a través del LED rojo (LED1R), manteniéndolo encendido e indicando que el sistema está listo para iniciar una nueva ronda. Mientras el temporizador permanece inactivo, el segundo pulsador no tiene alimentación, por lo que al presionarlo no ocurre ninguna acción.

---

2. Inicio del juego (0:06 – 0:07)

Cuando el usuario presiona el botón de inicio, se genera un pulso de disparo en el Pin 2 (Trigger) del NE555.

Como respuesta, la salida del temporizador (Pin 3) cambia inmediatamente a un nivel alto, registrando aproximadamente 4.88 V. Este cambio provoca que el LED rojo se apague y que el LED verde (LED1V) se encienda, indicando que ha comenzado la ventana de tiempo para responder.

Al mismo tiempo, el capacitor C1 inicia su proceso de carga a través de la resistencia R2, con un intervalo de aproximadamente 0.517 segundos, durante el cual el jugador puede registrar una respuesta válida.

---

3. Respuesta correcta del jugador (0:08 – 0:09)

Mientras el LED1V permanece encendido, el jugador presiona el segundo pulsador dentro del tiempo establecido.

El voltaje presente en el Pin 3 del NE555 atraviesa el pulsador, el diodo D3 y la resistencia R4, llegando a la base del transistor Q1 (2N2222).

Al recibir esta corriente, el transistor entra en saturación, permitiendo el paso de corriente hacia la carga. Este comportamiento se observa con la caída de voltaje entre colector y emisor de aproximadamente 0.36 V, indicando que esta funcionando como interruptor.

Como resultado, se enciende el LED verde de acierto (LED2V) y se activa el zumbador piezoeléctrico, indicando que el jugador respondió correctamente dentro del tiempo permitido.


---


4. Finalización del ciclo (0:09 en adelante)

Una vez que el capacitor C1 alcanza aproximadamente 2/3 del voltaje de alimentación, el NE555 finaliza automáticamente el pulso de salida.

El Pin 3 vuelve a 0 V, apagando el LED verde y dejando sin alimentación el segundo pulsador. En consecuencia, el transistor Q1 deja de conducir corriente, por lo que el LED2V y el zumbador se desactivan.

Finalmente, el LED rojo (LED1R) vuelve a encenderse, indicando que el circuito ha regresado a su estado inicial y se encuentra listo para comenzar una nueva ronda.



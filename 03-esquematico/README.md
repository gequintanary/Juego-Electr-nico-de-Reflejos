# Esquemático

En esta carpeta se incluye el esquemático eléctrico completo del circuito, con NE555, diodos, transistores y componentes discretos.

<img width="1150" height="682" alt="Diagrama esquemático" src="https://github.com/user-attachments/assets/e5892326-8624-434a-bb68-df0ff5d529d6" />

<img width="715" height="428" alt="image" src="https://github.com/user-attachments/assets/7f79a6db-019b-4a1b-9400-ce9aed691e24" />


### 1. Etapa de alimentación y disparo (Entrada)

Todo el circuito se alimenta con una fuente de **5 V de corriente continua (VCC)** y su respectiva conexión a **tierra (GND)**.

El **botón de inicio** está conectado al **Pin 2 (Trigger)** del circuito integrado **NE555** a través del diodo **D2 (1N4148)**. En condiciones normales (iniciales), la resistencia **R1 (10 kΩ)** mantiene este pin en un nivel alto (5 V). Cuando el usuario presiona el botón, el voltaje del Pin 2 cae a **0 V**, generando la señal que activa el temporizador e inicia el juego.

---

### 2. Etapa de temporización (NE555)

El **NE555** está configurado en modo **monoestable**, por lo que genera un único pulso de salida cada vez que recibe un disparo en su entrada.

El tiempo durante el cual el juego permanece activo depende de la resistencia **R2 (47 kΩ)** y del capacitor **C1 (10 µF)**. Al activarse el circuito, el capacitor comienza a cargarse y, cuando alcanza aproximadamente **2/3 del voltaje de alimentación**, el NE555 finaliza el pulso y vuelve a su estado inicial.

Además, el capacitor **C2 (100 nF)** conectado al Pin 5 filtra pequeñas variaciones de voltaje, proporcionando un funcionamiento más estable del temporizador.

---

### 3. Etapa de indicadores visuales

El **Pin 3** del **NE555** controla el funcionamiento de los dos LED principales, indicando el estado del juego.

* **LED1R (Rojo):** Permanece encendido cuando el juego está en reposo o cuando terminó el tiempo disponible para responder. Al iniciar el juego, el Pin 3 cambia de estado y el LED rojo se apaga.

* **LED1V (Verde):** Se enciende mientras el temporizador está activo, indicando que el jugador puede presionar el segundo botón para registrar una respuesta válida.

De esta manera, ambos LED informan visualmente cuándo es posible responder y cuándo el tiempo ha finalizado.

---

### 4. Etapa de validación de la respuesta

El **segundo pulsador** recibe alimentación desde la salida del **NE555**. Esto significa que solo tendrá voltaje disponible mientras el **LED verde** permanezca encendido.

Si el usuario presiona el botón dentro de ese intervalo, la señal pasa a través del diodo **D3 (1N4148)** y de la resistencia **R4 (1 kΩ)** hasta la base del transistor **Q1**, activándolo.

La resistencia **R5 (10 kΩ)** mantiene la base del transistor en **0 V** cuando el botón no está presionado, evitando activaciones accidentales provocadas por cambios en la señal.

---

### 5. Etapa de salida

El transistor **Q1 (2N2222)** funciona como un interruptor abierto. Cuando recibe la señal proveniente del segundo botón, permite el paso de corriente hacia los dispositivos de salida.

Al activarse el transistor se pasa la carga simultáneamente a:

* **LED2V (Verde):** Indica que el jugador respondió correctamente dentro del tiempo establecido.
* **Zumbador (LS1):** Emite un sonido que confirma el acierto.

Si el jugador presiona el segundo botón cuando el tiempo ya terminó o antes de que inicie la secuencia, el transistor permanece apagado y ni el **LED2V** ni el **zumbador** se activan, indicando que la respuesta fue incorrecta.

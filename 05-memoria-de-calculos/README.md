# Memoria de cálculos

En esta carpeta se almacenan los cálculos de diseño y validación de etapas electrónicas (tiempos, umbrales, corrientes y potencias).


# 7. Memoria de cálculos y diseño analítico

---

## 7.1 Fuente de alimentación

El circuito se alimenta mediante una fuente regulada de 5V de corriente continua ($V_{CC} = 5\text{V}$), suficiente para el correcto funcionamiento del NE555, los LED, el transistor y el zumbador.

### Cálculo del consumo máximo teórico
Para estimar el consumo máximo del circuito, se considera la corriente del NE555 en reposo, la corriente de los LED encendidos y la corriente que circula por el transistor cuando activa la carga. Con ello se obtiene una corriente total aproximada de:

$$I_{\text{total}} = I_{\text{555}} + I_{LED1R} + I_{LED1V} + I_{C}$$

$$I_{\text{total}} = 3\text{mA} + 13\text{mA} + 13\text{mA} + 22.27\text{mA} = 51.27\text{mA}$$

### Potencia total disipada ($P_{\text{total}}$)
La potencia máxima consumida por el circuito es:

$$P_{\text{total}} = V_{CC} \cdot I_{\text{total}} = 5\text{V} \cdot 0.05127\text{A} = 0.256\text{W}$$

El circuito tiene un consumo máximo aproximado de 51.27 mA y una potencia de 0.256 W, valores que indican un bajo consumo de energía. Esto quiere decir que puede alimentarse perfectamente de una fuente de 5V.

---

## 7.2 Cálculo de la etapa de temporización (Constantes RC del NE555)

El circuito integrado NE555 trabaja en configuración monoestable, por lo que al recibir un pulso de disparo en la terminal TR (Pin 2) genera un único pulso de salida en el Pin 3. La duración de este pulso depende del tiempo que tarda el capacitor C1 en cargarse a través de la resistencia R2.

La ecuación general de carga de un capacitor es:

$$v_c(t) = V_{CC} \left(1 - e^{-\frac{t}{R_2 C_1}}\right)$$

El NE555 cambia nuevamente de estado cuando el capacitor alcanza 2/3 del voltaje de alimentación ($V_{TH} = \frac{2}{3}V_{CC}$). Igualando este valor y despejando el tiempo, se obtiene:

$$\frac{2}{3}V_{CC} = V_{CC} \left(1 - e^{-\frac{t}{R_2 C_1}}\right)$$

$$\frac{2}{3} = 1 - e^{-\frac{t}{R_2 C_1}} \implies e^{-\frac{t}{R_2 C_1}} = \frac{1}{3}$$

$$\ln\left(\frac{1}{3}\right) = -\frac{t}{R_2 C_1} \implies -\ln(3) = -\frac{t}{R_2 C_1}$$

$$T = \ln(3) \cdot R_2 \cdot C_1 \approx 1.0986 \cdot R_2 \cdot C_1$$

Sustituyendo los valores del diseño ($R_2 = 47\text{k}\Omega$ y $C_1 = 10\mu\text{F}$):

$$T = 1.1 \cdot (47 \times 10^3\Omega) \cdot (10 \times 10^{-6}\text{F})$$

$$T = 1.1 \cdot 0.47\text{s} = 0.517\text{ segundos}\ (\approx 517\text{ms})$$

El tiempo de temporización obtenido es de aproximadamente 517 ms, intervalo durante el cual el usuario debe presionar el segundo botón para registrar una respuesta correcta. Una vez transcurrido este tiempo, el NE555 vuelve automáticamente a su estado inicial y finaliza el tiempo de respuesta.

---

## 7.3 Polarización y conmutación del transistor BJT

El transistor 2N2222 (Q1) funciona como un interruptor electrónico encargado de activar el LED de acierto y el zumbador cuando recibe la señal de salida del NE555.

Para que el transistor funcione correctamente como un interruptor, debe operar en la región de saturación, donde el voltaje entre el colector y el emisor es muy pequeño ($V_{CE} \approx 0.2\text{V}$). En estas condiciones, la corriente circula con facilidad hacia el LED y el zumbador, permitiendo el encendido simultáneo de ambos.

Este comportamiento garantiza que la salida del circuito responda correctamente cuando el usuario presiona el botón dentro del tiempo establecido por el temporizador.

---

## 7.4 Dimensionamiento de resistencias

Se calcularon las resistencias necesarias para proteger los componentes y asegurar un funcionamiento estable del circuito.

### Resistencias limitadoras para los LEDs (R3, R5, R6)
Para evitar que los LED reciban una corriente excessive, se calcularon las resistencias limitadoras considerando una diferencia de voltaje de 2.1 V y una corriente de operación de 13 mA:

$$R = \frac{V_{\text{fuente}} - V_f}{I_D} = \frac{5\text{V} - 2.1\text{V}}{13\text{mA}} = \frac{2.9\text{V}}{0.013\text{A}} \approx 223\Omega \approx 220\Omega$$

*(Como 223Ω no corresponde a un valor comercial, se seleccionó la resistencia más cercana de 220Ω)*.

Estas resistencias limitan la corriente que circula por los LED para evitar daños por sobrecorriente y mantener una intensidad de luz adecuada.

### Resistencia de Pull-Up (R1)
La resistencia R1 mantiene el pin de disparo (TR) del NE555 en nivel alto (5V) cuando el botón no está presionado. Esto evita disparos accidentales provocados por cambios en la señal.

$$R_1 = 10\text{k}\Omega$$

Al presionar el botón 1, la corriente que fluye a tierra es:

$$I_{\text{pull-up}} = \frac{V_{CC}}{R_1} = \frac{5\text{V}}{10\text{k}\Omega} = 0.5\text{mA}$$

La corriente de 0.5 mA es suficiente para mantener estable el nivel lógico del pin de disparo sin aumentar de forma significativa el consumo de energía. De esta manera, el NE555 permanece en reposo hasta que el usuario presione el botón.

### Resistencia de Pull-Down de base con botón 2 (R5)
La resistencia R5 mantiene la base del transistor Q1 en nivel bajo (0V) cuando el segundo botón no está presionado, evitando encendidos accidentales:

$$R_5 = 10\text{k}\Omega$$

---

## 7.5 Cálculo de corrientes del transistor

### Corriente de carga/colector ($I_C$)
Se calcula la corriente que circula por el colector considerando el consumo del sounder y del LED de salida:

$$I_{LED2V} = \frac{V_{CC} - V_{LED2V} - V_{CE}}{R_7} = \frac{5\text{V} - 2.1\text{V} - 0.2\text{V}}{220\Omega} = 12.27\text{mA}$$

$$I_C = I_{\text{sounder}} + I_{D4} = 10\text{mA} + 12.27\text{mA} = 22.27\text{mA}$$

### Corriente mínima de encendido total ($I_{B(\text{min})}$)
Se determina la corriente mínima de base necesaria para garantizar que el transistor entre en saturación y actúe como un interruptor cerrado, permitiendo que la corriente fluya desde el colector hacia el emisor:

$$I_{B(\text{min})} = \frac{I_C}{\beta} = \frac{22.27\text{mA}}{10} = 2.227\text{mA}$$

### Resistencia de la base (R4)
Se verifica que la resistencia de base R4 suministra una corriente suficiente para mantener el transistor completamente activado.

El circuito recibe una señal de encendido desde el temporizador 555:
* $V_{OH} = 4.2\text{V}$: Es el voltaje que sale del 555 cuando está en estado "Alto" (High).
* $V_{F(D3)} = 0.7\text{V}$: Antes de llegar al transistor, la corriente pasa por un diodo ($D_3$). Los diodos consumen un poco de energía para funcionar (0.7V).

Después de pasar por el diodo, quedan 3.5V antes de entrar a la resistencia de la base:

$$V_{\text{in}} = V_{OH} - V_{F(D3)} = 4.2\text{V} - 0.7\text{V} = 3.5\text{V}$$

A los 3.5V que teníamos, se le restan otros 0.7V que consume internamente el propio transistor para encenderse (el voltaje Base-Emisor o $V_{BE}$):

$$I_B = \frac{V_{\text{in}} - V_{BE}}{R_4} = \frac{3.5\text{V} - 0.7\text{V}}{1000\Omega} = 2.80\text{mA}$$

Para que el transistor funcione correctamente como un interruptor, debe entrar en saturación. Para ello, el diseño requiere una corriente mínima de base de $I_{B(\text{min})} = 2.227\text{mA}$.

Al comparar este valor con la corriente suministrada por el circuito, se obtiene:

$$I_B\ (2.80\text{mA}) > I_{B(\text{min})}\ (2.227\text{mA})$$

Como la corriente de base disponible es mayor que la mínima requerida, se garantiza que el transistor entra en saturación. En estas condiciones, el voltaje entre el colector y el emisor disminuye hasta un valor muy bajo ($V_{CE} \approx 0.12\text{V} - 0.2\text{V}$), lo que indica que el transistor se comporta como un interruptor cerrado. De esta manera, la corriente puede circular correctamente hacia el LED y zumbador, asegurando que el circuito funcione con una pérdida de energía mínima.

---

## 7.6 Dimensionamiento de los LEDs (diodos)

Para garantizar un funcionamiento seguro de los LEDs, se diseñó el circuito para que cada uno opere con una corriente aproximada de 13 mA, valor suficiente para obtener una buena intensidad sin comprometer su vida útil.

### Resistencia limitadora para LED1R, LED1V y LED2V (R3, R6, R7):

$$R = \frac{V_{\text{fuente}} - V_f}{I_D} = \frac{5\text{V} - 2.1\text{V}}{13\text{mA}} = \frac{2.9\text{V}}{0.013\text{A}} \approx 223\Omega \approx 220\Omega$$

*(Como 223Ω no corresponde a un valor comercial, se seleccionó la resistencia más cercana)*.

Al utilizar una resistencia de 220Ω, la corriente que circula por cada LED se mantiene muy cercana a los 13 mA, permitiendo que todos enciendan con una intensidad adecuada y evitando que una corriente excessive pueda dañarlos.

### Caída de voltaje en diodos lógicos 1N4148 (D2, D3):

$$V_F \approx 0.7\text{V}$$

Este valor de 0.7 V corresponde al comportamiento normal de un diodo de silicio en polarización directa y se considera en los cálculos de polarización del circuito.

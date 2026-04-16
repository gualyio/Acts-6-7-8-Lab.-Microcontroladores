# Emulador de Mouse y Teclado Bluetooth (HID) con ESP32 (Equipo 10 Laboratorio Microcontroladores)

Este proyecto consiste en la creación de un dispositivo periférico inalámbrico utilizando un **ESP32**. El sistema emula un protocolo HID (Human Interface Device), permitiendo controlar una computadora o celular (pasar diapositivas, controlar música o mover el cursor) mediante hardware externo.

---

Representación Gráfica

# Act. 6: Diagrama Pictórico
Este diagrama muestra la conexión física real de los componentes.
![Diagrama Pictórico]<img width="1536" height="1024" alt="pictorico" src="https://github.com/user-attachments/assets/938bea89-4038-4ba1-a224-4f2fec836ced" />
*Descripción: Conexión de los pulsadores y el joystick a los pines GPIO del ESP32 en una protoboard, el cual funciona como el plano de montaje físico que traduce la teoría a la realidad de la protoboard. En este apartado se documenta la disposición espacial de los componentes, mostrando cómo el ESP32 interactúa físicamente con el joystick y los pulsadores de colores a través de conexiones directas y puentes de voltaje. Es una pieza fundamental para la replicabilidad del hardware, ya que permite identificar a simple vista la organización de los cables de datos, las líneas de alimentación de $3.3V$ y los puntos de retorno a tierra común.* 

# Act. 7: Diagrama de Bloques
Visualización de alto nivel del funcionamiento del sistema.
![Diagrama de Bloques](./imagenes/bloques.jpg)
*Descripción: Flujo desde la entrada de datos (Sensores/Botones) -> Procesamiento (ESP32) -> Salida (Bluetooth HID), el diagrama representa la arquitectura lógica y el flujo de información del sistema sin entrar en detalles de cableado. Este resumen gráfico describe la secuencia operativa donde los periféricos de entrada capturan estímulos mecánicos que el microcontrolador procesa mediante sus conversores analógico-digitales para finalmente transmitir paquetes de datos bajo el protocolo Bluetooth HID. Esta etapa es crucial para entender la jerarquía del sistema, dividiendo el proyecto en módulos de adquisición de señales, procesamiento central y comunicación inalámbrica de salida.*

# Act. 8: Diagrama Esquemático
Representación técnica y simbólica del circuito electrónico.
![Diagrama Esquemático](./imagenes/esquemático.jpg)
*Descripción: Circuito detallado indicando resistencias pull-down de $10k\Omega$ y conexiones a tierra, el cual constituye la documentación técnica formal utilizando simbología electrónica universal. En esta actividad se detalla la ingeniería eléctrica del dispositivo, especificando la función crítica de las resistencias de $10k\Omega$ en configuración Pull-down que aseguran la estabilidad de los pines GPIO frente al ruido eléctrico. Este diagrama es la referencia definitiva para el análisis de nodos, validando que todas las señales analógicas del joystick y digitales de los botones cuenten con las referencias de voltaje y tierra necesarias para un funcionamiento preciso y seguro del emulador.*

---

# ¿Cómo funciona internamente?

El proyecto utiliza la pila de protocolos Bluetooth del ESP32 para anunciarse como un dispositivo de entrada estándar. 

**Arquitectura General:**
* **Capa de Hardware:** Pulsadores de colores para funciones digitales y un Joystick para el movimiento de los ejes $X$ e $Y$.
* **Capa de Firmware:** Programado en C++/Arduino, utiliza librerías de emulación HID que traducen los voltajes de los pines en paquetes de datos Bluetooth.
* **Alimentación:** Diseñado para ser portátil mediante una batería LiPo de $3.7V$.

**Tecnologías usadas:**
* **Microcontrolador:** ESP32 (WROOM-32).
* **Entradas:** Joystick analógico y botones táctiles.
* **Protocolo:** Bluetooth Low Energy (BLE) / HID.

---

# Instalación y Uso

# Requisitos
1.  **Hardware:** ESP32, 3 pulsadores, 1 joystick, resistencias de $10k\Omega$, cables.
2.  **Software:** Arduino IDE con el paquete de placas ESP32 instalado.

# Pasos para ponerlo en marcha
1.  Debemos de clonar este repositorio creado por nosotros: `git clone https://github.com/OmarDeLeon1910/Acts-6-7-8-Lab.Microcontroladores.git`
2.  Hay que conectar los componentes según el **Diagrama Esquemático**.
3.  Cargar el código de la carpeta `/codigo` a tu ESP32.
4.  Debemos emparejar el dispositivo vía Bluetooth con el nombre "ESP32 Mouse BT".


# Resumen Técnico
* **Pines Clave:** GPIO 13, 15, 2 (Configurados con resistencias Pull-down).
* **Interfaz:** Bluetooth HID.
* **Componente Principal:** Joystick para navegación de cursor.

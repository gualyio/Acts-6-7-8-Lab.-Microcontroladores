
# Información del Proyecto
# Autores: 
## -[2061110] - Erick Alejandro Francisco Baltazar
## -[2057902] - Omar Santiago De León Salinas
## -[2056820] - Walter Giovani Benavente Tapia
# Nombre del Proyecto: Emulador de Mouse y Teclado Bluetooth (HID) con ESP32 (Equipo 10 Laboratorio Microcontroladores)

Este proyecto consiste en el diseño, desarrollo e implementación de un dispositivo periférico inalámbrico basado en el microcontrolador **ESP32**, capaz de actuar como un dispositivo de interfaz humana (HID por sus siglas en inglés). 
El objetivo principal es emular las funciones de un ratón y un teclado convencional utilizando componentes electrónicos externos, permitiendo que el usuario controle computadoras, tabletas o teléfonos inteligentes mediante el protocolo Bluetooth Low Energy (BLE). Al configurarse como un dispositivo HID, el sistema es reconocido automáticamente por cualquier sistema operativo moderno sin la necesidad de instalar controladores adicionales, lo que garantiza una integración fluida y multiplataforma.
La arquitectura del sistema combina el uso de entradas analógicas y digitales para recrear una experiencia de navegación completa. Un joystick analógico se encarga de traducir los movimientos físicos en coordenadas cartesianas para desplazar el cursor en pantalla, mientras que una serie de pulsadores táctiles se programan para ejecutar acciones específicas como clics, desplazamientos de diapositivas o controles multimedia. Internamente, el firmware procesa los cambios de voltaje en los pines GPIO y los empaqueta en tramas de datos compatibles con los estándares de comunicación HID, ofreciendo una solución técnica versátil que demuestra las capacidades del ESP32 en el ámbito de la conectividad inalámbrica y el control de hardware.

---

# Representación Gráfica

# Act. 6: Diagrama Pictórico
Este diagrama muestra la conexión física real de los componentes.

<img width="1536" height="1024" alt="Diagrama Pictorico" src="https://github.com/user-attachments/assets/2d741794-3795-4a26-8a4d-2a879ee10a10" />

Descripción: Conexión de los pulsadores y el joystick a los pines GPIO del ESP32 en una protoboard, el cual funciona como el plano de montaje físico que traduce la teoría a la realidad de la protoboard. En este apartado se documenta la disposición espacial de los componentes, mostrando cómo el ESP32 interactúa físicamente con el joystick y los pulsadores de colores a través de conexiones directas y puentes de voltaje. Es una pieza fundamental para la replicabilidad del hardware, ya que permite identificar a simple vista la organización de los cables de datos, las líneas de alimentación de $3.3V$ y los puntos de retorno a tierra común. 

# Act. 7: Diagrama de Bloques
Este diagrama es una representación gráfica de lo que se realizó en nuestro proyecto.

<img width="1023" height="355" alt="Diagrama de Bloques" src="https://github.com/user-attachments/assets/5733e63f-9be8-498b-8942-b3c1a4d8b6ed" />

*Descripción: Flujo desde la entrada de datos (Sensores/Botones) -> Procesamiento (ESP32) -> Salida (Bluetooth HID), el diagrama representa la arquitectura lógica y el flujo de información del sistema sin entrar en detalles de cableado. Este resumen gráfico describe la secuencia operativa donde los periféricos de entrada capturan estímulos mecánicos que el microcontrolador procesa mediante sus conversores analógico-digitales para finalmente transmitir paquetes de datos bajo el protocolo Bluetooth HID. Esta etapa es crucial para entender la jerarquía del sistema, dividiendo el proyecto en módulos de adquisición de señales, procesamiento central y comunicación inalámbrica de salida.*

# Act. 8: Diagrama Esquemático
Representación técnica y simbólica del circuito electrónico.

<img width="552" height="306" alt="Diagrama Esquematico" src="https://github.com/user-attachments/assets/1ab6e1da-a60a-4d7f-bc35-cce8c62191df" />

*Descripción: Este es el circuito detallado indicando resistencias pull-down de $10k\Omega$ y conexiones a tierra, el cual constituye la documentación técnica formal utilizando simbología electrónica universal. En esta actividad se detalla la ingeniería eléctrica del dispositivo, especificando la función crítica de las resistencias de $10k\Omega$ en configuración Pull-down que aseguran la estabilidad de los pines GPIO frente al ruido eléctrico. Este diagrama es la referencia definitiva para el análisis de nodos, validando que todas las señales analógicas del joystick y digitales de los botones cuenten con las referencias de voltaje y tierra necesarias para un funcionamiento preciso y seguro del emulador.*

---

## ¿Qué hace el proyecto?

**Contexto:**
Este proyecto surge en el entorno del laboratorio de microcontroladores como una aplicación práctica para explorar las capacidades de conectividad inalámbrica y la emulación de periféricos de hardware modernos.

**Propósito:**
El propósito principal es diseñar y construir un dispositivo periférico inalámbrico autónomo que utilice el microcontr
olador ESP32 para emular un ratón y un teclado estándar (Human Interface Device, HID) a través de Bluetooth.

**¿Qué problemas resuelve?**
El dispositivo ofrece una solución versátil y portátil para controlar sistemas computacionales sin cables y sin depender de drivers propietarios, abordando principalmente:
* **Control Remoto:** Permite al usuario interactuar con una PC, laptop o smartphone (como la HP Pavilion x360 mostrada) a distancia, ideal para presentaciones o navegación multimedia.
* **Integración Multiplataforma:** Soluciona la necesidad de instalar software especial. Al emular el estándar HID universal, es reconocido instantáneamente por Windows, macOS, Linux, Android y iOS.
* **Interfaz Personalizada:** Proporciona un control del cursor mucho más intuitivo que las teclas de flecha y asigna funciones comunes (como "siguiente diapositiva" o clics) a botones físicos claros de colores.

**Alcance:**
El proyecto abarca el diseño físico del hardware sobre protoboard, el desarrollo del firmware en C++ (Arduino IDE) para procesar las señales analógicas y digitales, y la implementación de la pila de Bluetooth Low Energy (BLE) para la comunicación. El resultado es un prototipo funcional que puede realizar movimientos precisos del cursor, clics (izquierdo/derecho) y emular pulsaciones de teclas específicas para controlar diapositivas o reproducir multimedia.

---

## ¿Cómo funciona internamente?

**Descripción Técnica:**
La imagen de arriba muestra la implementación física real del proyecto sobre una laptop. El prototipo consiste en un microcontrolador ESP32 montado en una protoboard estándar, interconectado con un módulo de joystick analógico de 5 pines y una matriz lineal de cuatro pulsadores táctiles de colores. Un cable de datos USB-C (en la parte inferior) provee la alimentación inicial de 5V al ESP32 para su funcionamiento y programación.

**Arquitectura General y Flujo de Datos:**

La arquitectura interna del proyecto se basa en un flujo de control "Adquisición-Procesamiento-Emisión":

1.  **Adquisición (Capa de Hardware):**
    * **Joystick:** Este componente actúa como un dispositivo de entrada analógico de dos ejes. Sus potenciómetros internos generan voltajes variables (entre 0V y 3.3V) según la posición de la palanca. Estas variaciones son leídas por los pines GPIO analógicos (ADC) del ESP32.
    * **Pulsadores (Botones de Colores):** Estos son entradas digitales simples. Cuando el usuario presiona un botón de color (rojo, amarillo, negro), se cierra el circuito y un voltaje sólido (3.3V) viaja a los pines GPIO digitales configurados como entrada.

2.  **Procesamiento (Capa de Firmware):**
    * **Mapeo del Joystick:** El firmware en C++ lee constantemente los valores del ADC y aplica una función de mapeo para convertir los voltajes leídos en un rango de desplazamiento negativo/positivo que representa los píxeles que debe mover el cursor en pantalla. Se implementa una "zona muerta" para evitar movimientos falsos cuando el joystick está en reposo.
    * **Lógica de Botones y Debounce:** El código supervisa los pines digitales y, al detectar un estado alto, asigna y emite el comando HID correspondiente (ej: MOUSE\_LEFT para el clic izquierdo o KEY\_RIGHT\_ARROW para pasar una diapositiva). Se incluye lógica de anti-rebote (debouncing) para asegurar que una sola pulsación física no se interprete como múltiples acciones.

3.  **Emisión (Capa de Comunicación):**
    * **Pila de Protocolos BLE HID:** El ESP32 se anuncia ante la PC (en este caso, la laptop HP Pavilion x360 visible) como un "ESP32 Mouse BT". Utiliza la pila de protocolos de Bluetooth Low Energy para emular la estructura de datos estándar de un "Descriptor de Reporte HID", que es el lenguaje universal que los sistemas operativos entienden para interactuar con ratones y teclados. Los datos procesados se envían de forma inalámbrica en tramas compatibles con BLE HID.
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

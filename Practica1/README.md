# Práctica 1. Primeros pasos con OpenCV

## 1.1. Instalando el entorno de desarrollo

Para esta práctica se ha necesitado utilizar un entorno de desarrollo, el cula fue Anaconda. Para mi caso, utilizo una distribución linux (Arch Linux) y por ello el paquete ha instalar fue miniconda a través de la web oficial.

Luego se creó el entorno y se instaló las libreías necesarias:

```bash
conda create -n VC_P1 python=3.11.5
conda activate VC_P1
conda install numpy matplotlib opencv
```

## Tarea 1

### Primer código: Generación de un tablero de ajedrez con bucles
Este script genera una imagen en escala de grises que simula un tablero de ajedrez. A continuación se detalla el proceso:

1. **Inicialización:** Se definen las dimensiones de la imagen (`800x800` píxeles) y se crea un lienzo en blanco y negro con un solo canal, donde los valores de los píxeles pueden variar de 0 (negro) a 255 (blanco).
2. **Patrón de tablero:** El tablero se estructura en una cuadrícula de 8x8 bloques, donde cada bloque tiene un tamaño de `100x100` píxeles. Usando dos bucles `for`, se recorren las filas y columnas, rellenando alternadamente los bloques con el valor 255 (blanco) para generar el patrón clásico de un tablero de ajedrez.
3. **Visualización:** Se utiliza la biblioteca `matplotlib` para visualizar la imagen en escala de grises.

Este método proporciona una forma directa y controlada de crear patrones en imágenes mediante operaciones pixel a pixel.

### Segundo código: Generación de un tablero de ajedrez usando operaciones matriciales
Este script también genera un tablero de ajedrez en escala de grises, pero utiliza una técnica diferente basada en operaciones matriciales:

1. **Tamaño del bloque:** Se define el tamaño de cada cuadro del tablero (`100x100` píxeles).
2. **Creación del patrón:** Mediante la función `np.kron`, se crea el tablero de ajedrez de forma más compacta y eficiente. La función toma un patrón base (una matriz 2x2 que alterna entre 255 y 0) y lo expande para formar un tablero completo. Esto se logra repitiendo y escalando los bloques según el tamaño especificado.
3. **Visualización:** Similar al primer código, se usa `matplotlib` para mostrar el tablero generado.


## Tarea 2

1. **Inicialización:**
   - Se define el tamaño de la imagen (`800x800` píxeles) y se crea un lienzo negro utilizando `np.zeros`. La imagen tiene tres canales de color (RGB), lo que permite trabajar con colores personalizados.

2. **Dibujar figuras:** 
   - **Rectángulos rojos:** La porción de la imagen entre las filas `0` a `630` y las columnas `220` a `800` se llena con el color rojo (`[255, 0, 0]`).
   - **Rectángulos blancos:** Varias áreas se rellenan con blanco (`[255, 255, 255]`), creando una división visual interesante:
     - La región entre las filas `650` a `800` y las columnas `220` a `700`.
     - Dos pequeñas áreas en la parte inferior derecha (`650` a `720` y `740` a `800`, ambas en las columnas `720` a `800`).
   - **Rectángulo amarillo:** En la parte inferior derecha (`740` a `800`, `720` a `800`), se pinta de amarillo (`[255, 255, 0]`).
   - **Rectángulos adicionales:** Más regiones se llenan de blanco en la parte superior izquierda (`0` a `240`, `0` a `200` y `280` a `630`, `0` a `200`).
   - **Rectángulo azul:** La porción inferior izquierda (`650` a `800`, `0` a `200`) se rellena con azul (`[0, 0, 255]`).

3. **Visualización**

## Tarea 3

Este código genera el tablero de ajedrez de `8x8` utilizando la biblioteca `OpenCV` para dibujar los cuadros.
1. **Inicialización:**
   - Define el tamaño del tablero como `8x8` y el tamaño de cada cuadro como `100x100` píxeles.
   - Crea una imagen en escala de grises (blanco y negro) utilizando `np.zeros`, por lo que inicialmente, toda la imagen es negra.

2. **Dibujo del tablero:**
   - Un bucle `for` recorre las filas y columnas del tablero para dibujar los cuadros alternos.
   - Dentro del bucle, se usa `cv2.rectangle` para dibujar los cuadros blancos en las posiciones donde `(fila + columna) % 2 == 0`, creando el patrón clásico de un tablero de ajedrez.
   - La función `cv2.rectangle` recibe las coordenadas de la esquina superior izquierda y la inferior derecha del cuadro a dibujar, así como el color (255 para blanco) y el grosor (`-1` para rellenar el cuadro).

3. **Visualización**


## Tarea 4

Este código captura video en tiempo real desde la cámara web y realiza una modificación específica sobre uno de los canales de color del fotograma. A continuación, se detallan los pasos del código:

1. **Iniciar la captura de video:** 
   - `vid = cv2.VideoCapture(0)`: Abre la cámara web (índice `0` se refiere a la cámara predeterminada).

2. **Bucle de lectura de fotogramas:** 
   - `while True:` Inicia un bucle infinito para leer cada fotograma capturado por la cámara.
   - `ret, frame = vid.read()`: Captura un fotograma. `ret` es un indicador de éxito, y `frame` es la imagen capturada.

3. **Separación de canales de color:**
   - El fotograma se separa en sus tres canales de color (BGR):
     - `b = frame[:, :, 0]`: Canal azul.
     - `g = frame[:, :, 1]`: Canal verde.
     - `r = frame[:, :, 2]`: Canal rojo.

4. **Modificación del canal rojo:**
   - La modificación realizada en este código es invertir los colores del canal rojo:
     - `r_modified = 255 - r`: Este cálculo invierte la intensidad de cada píxel en el canal rojo. Los píxeles más brillantes (cercanos a 255) se oscurecen y viceversa, creando un efecto visual interesante.

5. **Concatenación de los canales:**
   - Los tres canales se concatenan horizontalmente para mostrar sus variaciones:
     - `collage = np.hstack((r_modified, g, b))`: Apila las imágenes modificadas de los tres canales (`r_modified`, `g`, `b`) una al lado de la otra, creando un collage que muestra la versión invertida del canal rojo junto con los canales verde y azul sin modificaciones.

6. **Mostrar la imagen:**
   - `cv2.imshow`: Muestra el collage redimensionado para que quepa en la pantalla.
   - `cv2.resize(collage, (int(w * 1.5), int(h / 2)), cv2.INTER_NEAREST)`: Cambia el tamaño de la imagen a 1.5 veces su ancho y la mitad de su altura.

7. **Detener el bucle:** 
   - Si se presiona la tecla `ESC` (`cv2.waitKey(20) == 27`), el bucle se rompe, deteniendo la captura de video.

8. **Liberar y cerrar recursos:**
   - `vid.release()`: Libera la cámara web.
   - `cv2.destroyAllWindows()`: Cierra todas las ventanas de OpenCV.


## Tarea 5
### Apartado 5.1
Este código captura video en tiempo real utilizando la cámara web y realiza algunas operaciones para analizar y mostrar información sobre los píxeles más claros y oscuros de cada fotograma.

1. **Captura de video:** 
   - `cv2.VideoCapture(0)` abre la cámara y comienza a capturar el video.
   
2. **Bucle principal:** 
   - Lee cada fotograma de la cámara y convierte la imagen a escala de grises.
   - Encuentra los píxeles más claros y más oscuros en la imagen utilizando `cv2.minMaxLoc`.
   
3. **Dibuja círculos:** 
   - Marca los píxeles más claros con un círculo verde y los más oscuros con un círculo rojo en el fotograma original.

4. **Mostrar valores RGB:** 
   - Si se ha registrado la posición del mouse (`px > -1`), muestra los valores RGB de la posición seleccionada en la imagen.

5. **Mostrar el video:** 
   - Muestra el video en una ventana con los círculos y los valores RGB superpuestos.

6. **Finalizar:** 
   - El bucle se detiene al presionar `ESC`, liberando la cámara y cerrando todas las ventanas abiertas.

### Apartado 5.2

Esta versión del código realiza una tarea más compleja al analizar la imagen capturada en bloques de 8x8 píxeles para encontrar las zonas más claras y oscuras. A continuación, se explica su funcionamiento:

1. **División de la imagen en bloques 8x8:**
   - En lugar de trabajar con píxeles individuales, este código recorre la imagen por bloques de tamaño `8x8`. Esto se hace mediante bucles `for` que avanzan en incrementos de 8 píxeles tanto vertical como horizontalmente.
   - Esto permite un análisis más general de la imagen, centrado en áreas más grandes y evitando la sensibilidad a pequeños cambios de brillo.

2. **Cálculo del brillo promedio de cada bloque:**
   - Para cada bloque de `8x8`, el código utiliza `np.mean()` para calcular el brillo promedio de los píxeles dentro de ese bloque. 
   - A medida que se recorren los bloques, se compara el brillo promedio actual con los valores almacenados (`max_avg` para el más claro y `min_avg` para el más oscuro). 
   - Si se encuentra un bloque con un brillo promedio más alto o más bajo que los almacenados, se actualizan las posiciones de las zonas más claras y oscuras.

3. **Marcado de las zonas más clara y oscura:**
   - Después de identificar las posiciones de las zonas con el brillo promedio más alto y más bajo, se dibujan círculos en los centros de estas zonas utilizando `cv2.circle`.
   - Esto resalta las regiones más claras y oscuras, en lugar de solo puntos específicos.

4. **Uso de variables auxiliares:**
   - Variables como `max_avg` y `min_avg` se utilizan para llevar un registro de los valores máximos y mínimos de brillo promedio encontrados en los bloques, lo que permite identificar las zonas deseadas.
   - Las posiciones de las zonas más clara y oscura (`max_pos` y `min_pos`) se actualizan durante el proceso de recorrido para indicar los centros de las áreas identificadas.


## Tarea 6
Este código transforma los fotogramas en tiempo real en una cuadrícula de imágenes con un efecto "pop art". El efecto se logra aplicando un filtro de contorno y combinándolo con colores vibrantes para crear imágenes estilizadas. La cuadrícula final se muestra en tiempo real, dándole un aspecto visual similar a las obras de arte pop.
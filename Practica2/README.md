# Práctica 2. Funciones básicas de OpenCV

## Marcos Miguel Sánchez Antonio

### 1-TAREA: Realiza la cuenta de píxeles blancos por filas (en lugar de por columnas). Determina el máximo para filas y columnas (uno para cada) y muestra el número de filas con un número de píxeles blancos mayor o igual que 0.95*máximo.

En este apartado se propone un código el cual realiza el análisis de una imagen procesada por el filtro de Canny, con el objetivo de identificar las filas con mayor cantidad de píxeles blancos (píxeles con valor 255) y visualiza los resultados de forma gráfica.

#### Funcionamiento

1. **Cálculo del número de píxeles blancos por fila**:  
   Se utiliza la función `cv2.reduce` para sumar los valores de los píxeles por cada fila en la imagen `canny`. Esto permite obtener el número total de píxeles blancos (valor 255) por fila. La suma se divide entre 255 para obtener el conteo real de píxeles blancos en cada fila.

2. **Cálculo del valor máximo de píxeles blancos por fila**:  
   Se determina el número máximo de píxeles blancos encontrados en una fila de la imagen.

3. **Filas con más del 95% del valor máximo**:  
   Se define un umbral del 95% del valor máximo de píxeles blancos por fila y se identifican las filas que cumplen o superan este umbral.

4. **Visualización de los resultados**:  
   Se genera una gráfica que muestra el porcentaje de píxeles blancos en cada fila. En esta gráfica, se resaltan las filas que tienen al menos el 95% del máximo número de píxeles blancos, utilizando una línea discontinua roja y marcadores verdes en las filas que cumplen con esta condición.

### 2-TAREA: Aplica umbralizado a la imagen resultante de Sobel (convertida a 8 bits), y posteriormente realiza el conteo por filas y columnas similar al realizado en el ejemplo con la salida de Canny de píxeles no nulos. Calcula el valor máximo de la cuenta por filas y columnas, y determina las filas y columnas por encima del 0.95*máximo. Remarca con alguna primitiva gráfica dichas filas y columnas sobre la imagen. ¿Cómo se comparan los resultados obtenidos a partir de Sobel y Canny?

A continuación, voy a comparar los resultados obtenidos en las imágenes, de acuerdo con el enunciado que menciona el análisis y comparación entre Sobel y Canny aplicados en los pasos de umbralizado, y el conteo de píxeles no nulos por filas y columnas.

#### Sobel vs Canny:

1. **Detección de Bordes**:
   - **Canny** es un detector de bordes que aplica un algoritmo más complejo basado en gradientes y umbralización. Este detector puede ser más preciso en la identificación de bordes fuertes en una imagen, eliminando el ruido.
   - **Sobel** es un operador basado en derivadas que resalta los cambios en la intensidad de la imagen en las direcciones X e Y. Genera una salida con menos procesamiento que Canny, lo que podría resultar en la detección de más ruido o bordes más suaves.

2. **Umbralización de Sobel**:
   - Las imágenes resultantes de Sobel, después de la conversión a 8 bits, se han umbralizado. Esto elimina valores bajos de la imagen, dejando solo los bordes más fuertes.
   - Posteriormente, se cuenta el número de píxeles no nulos en las filas y columnas de la imagen Sobel umbralizada, lo que permite visualizar qué áreas contienen la mayor cantidad de bordes detectados.

3. **Conteo de Píxeles No Nulos**:
   - Tanto en Sobel como en Canny, se hace un análisis de los píxeles no nulos por filas y columnas. Para ambos métodos, se observa que hay una fuerte concentración de bordes en áreas clave de la imagen, pero Sobel, al ser más sensible a cambios suaves en intensidad, puede tener más ruido en las zonas de transición.
   - En las gráficas, se resalta con líneas discontinuas rojas las filas y columnas donde el número de píxeles no nulos es mayor al 95% del valor máximo en cada dirección (filas y columnas).

4. **Visualización**:
   - En las gráficas para **Canny**, la curva muestra picos que representan las áreas con mayor concentración de bordes. Estos picos suelen ser más definidos, ya que Canny es más eficiente al eliminar ruido.
   - Para **Sobel**, el comportamiento de la curva puede ser más variado y mostrar más fluctuaciones, lo que refleja su mayor sensibilidad a los gradientes suaves. Esto puede resultar en más filas y columnas destacadas con píxeles no nulos.

#### Conclusiones:
- **Canny** proporciona una mejor discriminación de los bordes principales y elimina el ruido de manera efectiva, mientras que **Sobel** puede capturar más detalles, incluyendo ruido o bordes menos definidos.
- La comparación entre los resultados indica que Canny tiende a resaltar áreas más significativas de bordes, mientras que Sobel responde de manera más uniforme ante pequeños cambios en intensidad. En términos de filas y columnas destacadas, Sobel podría marcar más áreas, pero muchas de estas podrían corresponder a detalles menos relevantes que se consideran ruido.

   

### 3- TAREA: Proponer un demostrador que capture las imágenes de la cámara, y les permita exhibir lo aprendido en estas dos prácticas ante quienes no cursen la asignatura :). Es por ello que además de poder mostrar la imagen original de la webcam, incluya al menos dos usos diferentes de aplicar las funciones de OpenCV trabajadas hasta ahora.

Para el demostrador se ha creado una aplicación en tiempo real utilizando la cámara web para capturar imágenes y aplicar diferentes efectos utilizando OpenCV. Se muestran dos efectos: el filtro Sobel y un efecto de Pop Art. El usuario puede alternar entre estos efectos en tiempo real mientras se visualiza el video de la cámara.

#### Funcionamiento

1. **Captura de video en tiempo real**:  
   El programa utiliza la cámara web (o un archivo de video si se configura) para capturar cuadros en tiempo real.

2. **Filtro Sobel**:
   - Se aplica un filtro Sobel para detectar bordes en las direcciones X y Y.
   - Los bordes detectados en ambas direcciones se combinan y se muestra un collage que incluye los bordes detectados por el filtro en los ejes X, Y, la combinación de ambos, y el cuadro redimensionado original.
   
3. **Efecto Pop Art**:
   - Se aplica el algoritmo de detección de bordes Canny y luego se utilizan diferentes esquemas de color para crear un efecto tipo "Pop Art".
   - Se muestran cuatro versiones del cuadro con diferentes combinaciones de color en un collage 2x2.

4. **Interacción con el usuario**:
   - El programa permite cambiar entre los dos efectos (Sobel y Pop Art) presionando las teclas '1' y '2', respectivamente.
   - Si se presiona la tecla 'q', el programa termina y se cierra la ventana de visualización.

![alt text](assets/tarea3-1.png)

![alt text](assets/tarea3-2.png)

#### Requisitos:
- OpenCV (`cv2`)
- Numpy (`numpy`)

#### Ejecución:
El programa se ejecuta con una cámara web conectada y muestra los efectos en tiempo real en una ventana de video. Para cambiar entre efectos, el usuario debe presionar las teclas '1' o '2', y para salir, la tecla 'q'.


### 4-TAREA: Tras ver los vídeos [My little piece of privacy](https://www.niklasroy.com/project/88/my-little-piece-of-privacy), [Messa di voce](https://youtu.be/GfoqiyB1ndE?feature=shared) y [Virtual air guitar](https://youtu.be/FIAmyoEpV5c?feature=shared) proponer un demostrador reinterpretando la parte de procesamiento de la imagen, tomando como punto de partida alguna de dichas instalaciones.

Este código crea una instalación interactiva inspirada en proyectos como "My little piece of privacy" y "Messa di voce". Utiliza una cámara web para detectar rostros en tiempo real mediante el clasificador Haar Cascade y superpone un sombrero virtual sobre cada rostro detectado.

#### Funcionamiento

1. **Detección de Rostros**:
   - Se utiliza un clasificador preentrenado de cascada de Haar (`haarcascade_frontalface_default.xml`) para detectar rostros en el video capturado en tiempo real desde la cámara web.
   - El procesamiento de imágenes se realiza convirtiendo el fotograma a escala de grises y utilizando este modelo preentrenado para encontrar caras en el cuadro de video.

2. **Superposición de Sombrero**:
   - Una imagen de un sombrero con fondo transparente es cargada y redimensionada dinámicamente, ajustándose al tamaño del rostro detectado.
   - El sombrero se coloca justo por encima del rostro, alineado de acuerdo con las dimensiones y posición del rostro detectado.
   - La superposición se hace utilizando la transparencia del canal alfa de la imagen del sombrero para asegurar que se mezcle correctamente con el video.

3. **Proceso en Tiempo Real**:
   - El programa captura continuamente fotogramas de la cámara web y, en cada uno, busca rostros para superponer los sombreros.
   - Los resultados se muestran en una ventana de video en tiempo real, permitiendo una experiencia interactiva donde el sombrero sigue el rostro mientras se mueve.

4. **Interactividad**:
   - Al igual que los ejemplos en los videos mencionados, este demostrador permite una interacción en tiempo real con los usuarios, ofreciendo un toque lúdico y dinámico a través del procesamiento de imágenes.
   - Los usuarios pueden ver cómo el sombrero se ajusta a sus movimientos, creando una experiencia visual entretenida y dinámica, similar a las instalaciones interactivas vistas en los proyectos de referencia.

5. **Salida del Programa**:
   - El programa se ejecuta indefinidamente hasta que el usuario presiona la tecla 'q', momento en el cual se cierra la ventana y se libera el recurso de la cámara.

![alt text](assets/tarea4.png)
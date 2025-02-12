# Convolución, correlación y transformación
Este repositorio tiene como objetivo explicar, utilizar y reconocer, la convolución como una operación entre señal y sistema, la correlación como una operación entre señales y la transformada de Fourier. Todo esto visualizado en python por medio del compilador spyder.

## Partes del código
1.  Tendremos un sistema h[n], dada por cada dígito del código estudiantil y una señal de entrada x[n] dada por cada dígito del documento de identificación de cada uno. Para asi mismo  hacer el proceso de convolucion para  hallar la señal de salida y[n], imprimiendo esta señal y observando su respectiva grafica.
2. Se tienen dos señales definidas en un intervalo "n". Se calculará la correlación cruzada entre ellas y se visualizará en una gráfica para analizar su relación.
3. -Se obtiene una señal electromiográfica (EMG) desde la base de datos PhysioNet.
-Se calculan estadísticas descriptivas como la media, desviación estándar y frecuencia media (fm).
-Se describe la señal en términos de su clasificación y características fisiológicas.
-Se aplica la transformada de Fourier para obtener su representación en el dominio de la frecuencia.
-Finalmente, se grafican tanto la transformada de Fourier (espectro de magnitud) como la densidad espectral de potencia para analizar la distribución de energía en las diferentes frecuencias..

### Uso de librerias 

```
import matplotlib.pyplot as plt 
import numpy as np 
from scipy.io import loadmat
from scipy.fft import fft, fftfreq
```
`matplotlib.pyplot` Se usa para poder graficar la señal ECG y su histograma. 
`numpy (np)` Permite realizar las operaciones matemáticas. 
`scipy.io  loadmat` Esta nos permite cargar archivos de MATLAB, en este caso nuestra señal fue extraida de la base de datos Physionet en formato `.mat.scipy.fft` nos servara para poder aplicar y hacer la transformada de Fourier (fft, fftfreq)

#### Convolución 

Convolución en Tiempo Discreto. La respuesta y[n] de un sistema en tiempo discreto a una entrada x[n] se obtiene como la suma de convolución dada por: donde h[n], que se asume conocida, es la respuesta del sistema a un impulso unitario en la entrada. (electronica.guru)

```
sistema = np.array([5, 6, 0, 0, 7, 8, 1])
señal = np.array([1, 0, 7, 7, 3, 4, 0, 1, 8, 7])
```
En este codigo el `sistema` h[n] esta dado por los digitos del carnet estudiantil, y la `señal` de entrada x[n] esta dada por los digitos de la C.C.

declaramos una variable como convolucion
```
convolucion = np.convolve(señal, sistema)
```
Esta declaración nos sirve para poder usar la funcion  `np.convolve()` que nos permite hacer la convulucion en python.
Ahora imprimimos como nos dio la convolucion.
```
yn = "Secuencia resultante y[n]: " + str(convolucion.tolist())
print(yn)
```
Esta manera de imprimirlo ayuda a que los valores se vean divididos por comas, teniendo una mejor visualizacion en el terminal de esta manera. `Secuencia resultante y[n]: [5, 6, 10, 57, 107, 95, 77, 80, 122, 215, 136, 65, 48, 69, 48, 64]`
procedemos a graficar la convolución.
```
plt.figure(figsize=(10, 5)) # crea una figura de 10x5
plt.stem(convolucion, linefmt='b-', markerfmt='ro', basefmt='k-')
plt.xlabel('n', fontsize=12) #eje x
plt.ylabel('y[n]', fontsize=12) #eje y
plt.title('CONVOLUCION DE x[n] CON EL SISTEMA h[n]', fontsize=14) #titulo
plt.grid(alpha=0.3) #agrega una cuadricula opaca al 30%
plt.show() 
```
La línea `plt.stem()` en la segunda gráfica genera una representación detallada de una secuencia discreta, ideal para visualizar señales discretas como la convolución.

En esta función, la variable `convolucion` representa el conjunto de valores resultantes tras aplicar la operación de convolución entre las señales de entrada.

Dentro de `plt.stem()`, se configuran los siguientes parámetros para mejorar la visualización:

`linefmt='b-'`: Dibuja las líneas verticales en color azul, conectando cada muestra con la línea base.
`markerfmt='ro'`: Representa los puntos de la secuencia como marcadores rojos.
`basefmt='k-'`: Establece la línea base en color negro, proporcionando un punto de referencia claro en el gráfico.
 
La gráfica resultante es: 

![image](https://github.com/user-attachments/assets/f52c71f3-2faf-40d8-91c4-32c8074c151e)





























![image](https://github.com/user-attachments/assets/5680fe49-3633-4d5b-a919-7f979f539ee4)

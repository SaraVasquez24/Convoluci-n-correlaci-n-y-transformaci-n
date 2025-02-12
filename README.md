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

![image](https://github.com/user-attachments/assets/f786e4e4-98c0-45ce-a755-5435fc692c17)






























![image](https://github.com/user-attachments/assets/5680fe49-3633-4d5b-a919-7f979f539ee4)

##Bibliografía

[1]	P. y. Estadística, “Correlación”, Probabilidad y Estadística, 25-feb-2022. [En línea]. Disponible en: https://www.probabilidadyestadistica.net/correlacion/. [Consultado: 12-feb-2025].
[2]	“PhysioBank ATM”, Physionet.org. [En línea]. Disponible en: https://archive.physionet.org/cgi-bin/atm/ATM. [Consultado: 12-feb-2025].
[3]	P. S. Chischilly, “¿Qué Es Y Para Qué Sirve La Convolución?”, Electronica.guru. [En línea]. Disponible en: https://electronica.guru/app01/7599/que-es-y-para-que-sirve-la-convolucion. [Consultado: 12-feb-2025].
[4]	R. Python, “Fourier Transforms With scipy.fft: Python Signal Processing”, Realpython.com, 02-nov-2020. [En línea]. Disponible en: https://realpython.com/python-scipy-fft/. [Consultado: 12-feb-2025].
[5]	V. T. las E. De programacionpython, “APLICANDO LA ‘TRANSFORMADA DE FOURIER’ EN PYTHON, CON ‘numpy’”, El Programador Chapuzas, 06-dic-2023. [En línea]. Disponible en: https://programacionpython80889555.wordpress.com/2023/12/06/aplicando-la-transformada-de-fourier-en-python-con-numpy/. [Consultado: 12-feb-2025].



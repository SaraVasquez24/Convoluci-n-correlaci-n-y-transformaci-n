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


Como podemos observar podemos corroborar los datos impresos con la grafica, viendo y comprobando su veracidad.


#### Correlación
La correlación es una medida estadística que indica el grado de relación entre dos variables. En concreto, la correlación lineal sirve para determinar cuánto de correlacionadas linealmente están dos variables distintas.(probabilidadyestadistica.net)
En este caso no son variables sino dos señales, una sinusoidal y cosenosoidal.
Definir las señales s1[nTs] y s2[nTs] en el codigo
```
Ts = 1.25e-3  # Período de muestreo 1.25 ms
n_1 = np.arange(0, 9) #el rango de 0 a 9 de valores n
señal_1 = np.cos(2 * np.pi * 100 * n_1 * Ts)
señal_2 = np.sin(2 * np.pi * 100 * n_1 * Ts)
```
`Ts` el valor de esta esta dado en el ejercicio.
`np.cos()` y `np.sin()` nos ayudan a graficar señales del tipo seno y coseno, ademas lo que esta dentro de los parentesis de ambas son especificaciones dadas también en el ejercicio.
Calculamos la correlación:
```
correlacion = np.correlate(señal_1, señal_2, mode='full')
correlacion = np.round(correlacion, decimals=3) #redondeo no tantos decimales
```
El parámetro `mode='full'` en np.correlate() determina cómo se calcula la correlación entre las señales. Modos disponibles en np.correlate() mode='full' (modo completo, predeterminado)

Devuelve la correlación completa entre señal_1 y señal_2.
`np.correlate()` nos sirve para hallar la correlación entre las dos señales. 
El parámetro `mode='full'` en `np.correlate()` determina cómo se calcula la correlación entre las señales. Hay varios modos disponibles en `np.correlate()` siendo esta el modo completo, predeterminado.
`np.round()` permite hacer un redondeo de 3 decimales, esto con el fin de que sea mas limpio en la impresion de estos datos.
```
Correlacion_mostrar = "Correlación entre s1 y s2: " + str(correlacion.tolist())
print(Correlacion_mostrar)
```
Esto en el terminal se muestra asi: `Correlación entre s1 y s2: [-0.0, -0.707, -1.5, -1.414, -0.0, 2.121, 3.5, 2.828, 0.0, -2.828, -3.5, -2.121, 0.0, 1.414, 1.5, 0.707, 0.0]`, corroborando que son 3 decimales de aproximacion y viendo el valor (señal) resultante de la correlacion.

Procedemos a graficar, debemos tener en cuenta que se genera una figura y dentro de esta, se hacen tres graficas mostrando la señal_1, señal_2 y la respectiva correlación de estas dos señales. Debemos recordar que el rango `n_1` va de 0 a 9 valores n. exceptuando la correlacion, lo explicaremos mas adelante.

```
# los plt.subplot() se usa para crear múltiples subgráficos dentro del mismo "grafico".
plt.figure(figsize=(12, 5))
plt.subplot(3, 1, 1)  #3=numero de fila, 1=numero total de columnas, 1=es el primero de forma descendente 
plt.stem(n_1, señal_1, linefmt='b', markerfmt='bo', basefmt='k')
plt.xlabel("n")
plt.ylabel("s1[nTs]")
plt.title("Señal s1[nTs] = cos(2π100nTs)")
plt.grid(alpha=0.3)
```
```
plt.subplot(3, 1, 2)
plt.stem(n_1, señal_2, linefmt='r', markerfmt='ro', basefmt='k')
plt.xlabel("n")
plt.ylabel("s2[nTs]")
plt.title("Señal s2[nTs] = sin(2π100nTs)")
plt.grid(alpha=0.3)
```
```
plt.subplot(3, 1, 3)
plt.stem(range(-len(n_1) + 1, len(n_1)), correlacion, linefmt='g', markerfmt='go', basefmt='k')
plt.xlabel("n")
plt.ylabel("Correlación")
plt.title("Correlación entre s1 y s2")
plt.grid(alpha=0.3)

plt.tight_layout() #evita que se amontonen los titulos y ejes
plt.show()
```
En la gráfica de la correlación, notamos que no tomamos la variable `n_1` en el eje x como en las anteriores, ya que esta representa la correlación entre las dos señales. Como se mencionó anteriormente, la correlación indica la relación entre dos señales, lo que da como resultado una longitud determinada por **2N-1**. Dado que **N=9**, la longitud resultante es **17**.  

Para centrar el valor cero en el eje x, utilizamos `range(-len(n_1) - 1, len(n_1))`, lo que nos permite calcular el valor mínimo de x. Como **N=9**, el cálculo `-len(n_1) - 1` nos da **x = -8**, permitiendo que la secuencia pase por 0 y continúe hasta **8** en el lado positivo, asegurando así una representación simétrica.

![image](https://github.com/user-attachments/assets/256db264-19ac-4038-9345-cf5702a675f8)


![image](https://github.com/user-attachments/assets/5680fe49-3633-4d5b-a919-7f979f539ee4)


##Bibliografía

[1]	P. y. Estadística, “Correlación”, Probabilidad y Estadística, 25-feb-2022. [En línea]. Disponible en: https://www.probabilidadyestadistica.net/correlacion/. [Consultado: 12-feb-2025].
[2]	“PhysioBank ATM”, Physionet.org. [En línea]. Disponible en: https://archive.physionet.org/cgi-bin/atm/ATM. [Consultado: 12-feb-2025].
[3]	P. S. Chischilly, “¿Qué Es Y Para Qué Sirve La Convolución?”, Electronica.guru. [En línea]. Disponible en: https://electronica.guru/app01/7599/que-es-y-para-que-sirve-la-convolucion. [Consultado: 12-feb-2025].
[4]	R. Python, “Fourier Transforms With scipy.fft: Python Signal Processing”, Realpython.com, 02-nov-2020. [En línea]. Disponible en: https://realpython.com/python-scipy-fft/. [Consultado: 12-feb-2025].
[5]	V. T. las E. De programacionpython, “APLICANDO LA ‘TRANSFORMADA DE FOURIER’ EN PYTHON, CON ‘numpy’”, El Programador Chapuzas, 06-dic-2023. [En línea]. Disponible en: https://programacionpython80889555.wordpress.com/2023/12/06/aplicando-la-transformada-de-fourier-en-python-con-numpy/. [Consultado: 12-feb-2025].


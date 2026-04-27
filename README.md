# Método de mezcla natural

Existen diferentes métodos de ordenamiento externo; entre ellos se encuentra el de Mezcla Natural (o *Natural Merge Sort*).

Este método consiste en aprovechar la existencia de secuencias ya ordenadas dentro de los datos de un archivo. 
A diferencia de otros algoritmos, no divide los datos arbitrariamente, sino que identifica "runs" (subsecuencias ya ordenadas).

El algoritmo de ordenación por mezcla se basa en dividir recursivamente la lista de datos a ordenar en dos sublistas de tamaño similar, 
para posteriormente ordenarlas y fusionarlas, obteniendo así una lista final ordenada.

---

## Análisis de complejidad

La complejidad de un algoritmo describe cuánto trabajo se necesita realizar en función del tamaño de los datos de entrada (n). 
Se expresa mediante la notación Big O, que indica cómo crece el tiempo de ejecución conforme aumenta dicho tamaño.

Un concepto clave en la mezcla natural es el "run": una secuencia de elementos que ya están en orden dentro de la lista original. 
Cuantos más runs naturales existan, menos trabajo necesita realizar el algoritmo.

### Complejidad del método de mezcla natural


- 🟢 **Mejor caso — O(n)**  
  La lista ya está completamente ordenada. Solo existe un run; el algoritmo recorre los datos una sola vez y finaliza.

- 🔵 **Caso promedio — O(n log n)**  
  Existen varios runs de tamaño similar. Se realizan múltiples pasadas de fusión de forma logarítmica respecto al número de runs.

- 🔴 **Peor caso — O(n log n)**  
  Los datos están en orden inverso o completamente aleatorios. Cada elemento es su propio run (n runs de tamaño 1), por lo que se requiere el máximo número de pasadas.


---

## Casos de uso del método de mezcla natural

El método de mezcla natural es especialmente útil en situaciones donde los datos presentan cierto grado de orden o cuando se trabaja con grandes volúmenes de información almacenados en archivos. 
A diferencia de otros algoritmos de ordenamiento, este método no ignora el estado inicial de los datos, sino que lo aprovecha para optimizar el proceso.

Se recomienda utilizar este algoritmo en los siguientes casos:

- **Archivos muy grandes**  
  Cuando los datos no caben completamente en memoria principal, es necesario utilizar memoria secundaria (como disco). La mezcla natural está diseñada como un método de ordenamiento externo, por lo que permite trabajar eficientemente con archivos grandes sin necesidad de cargar toda la información en memoria.

-  **Datos parcialmente ordenados**  
  Si los datos contienen subsecuencias ya ordenadas (runs), el algoritmo puede identificarlas automáticamente y reducir significativamente el número de operaciones necesarias para ordenar el conjunto completo.

- **Procesamiento de datos externos**  
  Es ampliamente utilizado en sistemas que manejan grandes cantidades de información, como bases de datos, archivos de registros (logs) o sistemas de procesamiento masivo de datos, donde el acceso secuencial es más eficiente que el acceso aleatorio.

- **Optimización de recursos**  
  Permite disminuir el número de pasadas de fusión al aprovechar el orden existente en los datos, lo que reduce el costo computacional en comparación con métodos que siempre dividen los datos sin analizar su estructura.

  - **Procesos secuenciales de lectura**  
  Es ideal en contextos donde los datos se leen de manera continua (por ejemplo, desde archivos), ya que puede detectar y procesar runs en una sola pasada inicial.

### ¿Cuándo es mejor usarlo?

El método de mezcla natural es más eficiente cuando los datos no están completamente desordenados, ya que puede alcanzar un rendimiento cercano a O(n) si existen pocas subsecuencias desordenadas. 
En estos casos, el algoritmo requiere menos pasadas de fusión, lo que reduce el tiempo total de ejecución.


---
## Tabla comparativa entre otros métodos

| Características                     | Mezcla Natural                      | QuickSort                          | Bubble Sort                    |
|------------------------------------|------------------------------------|------------------------------------|--------------------------------|
| Tipo de ordenamiento               | Externo                            | Interno                            | Interno                        |
| Facilidad de paralelismo           | Alta (subarreglos independientes)  | Media (depende del pivote)         | Muy baja (cada paso depende del anterior) |
| Rendimiento medio                  | Levemente más lento por copias     | Más rápido en la práctica          | El más lento de los tres       |
| Estabilidad                        | Sí                                 | Depende de la implementación       | Sí                             |
| Espacio extra                      | O(n) (usa arreglo auxiliar)        | O(log n) (uso de pila)             | O(1) (no requiere extra)       |

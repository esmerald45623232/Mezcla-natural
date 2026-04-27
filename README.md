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

| Caso           | Complejidad  | Descripción |
|----------------|-------------|-------------|
| Mejor caso     | O(n)        | La lista ya está completamente ordenada. Solo existe 1 run; el algoritmo recorre los datos una sola vez y termina. |
| Caso promedio  | O(n log n)  | Existen varios runs de tamaño similar. Se realizan múltiples pasadas de fusión de forma logarítmica respecto al número de runs. |
| Peor caso      | O(n log n)  | Datos en orden inverso o completamente aleatorios. Cada elemento es su propio run (n runs de tamaño 1), requiriendo el máximo número de pasadas. |

#### Conclusión

Su complejidad varía entre O(n) y O(n log n), dependiendo del grado de orden presente en los datos de entrada.

---

## Tabla comparativa entre otros métodos

| Características                     | Mezcla Natural                      | QuickSort                          | Bubble Sort                    |
|------------------------------------|------------------------------------|------------------------------------|--------------------------------|
| Tipo de ordenamiento               | Externo                            | Interno                            | Interno                        |
| Facilidad de paralelismo           | Alta (subarreglos independientes)  | Media (depende del pivote)         | Muy baja (cada paso depende del anterior) |
| Rendimiento medio                  | Levemente más lento por copias     | Más rápido en la práctica          | El más lento de los tres       |
| Estabilidad                        | Sí                                 | Depende de la implementación       | Sí                             |
| Espacio extra                      | O(n) (usa arreglo auxiliar)        | O(log n) (uso de pila)             | O(1) (no requiere extra)       |

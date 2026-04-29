# Método de mezcla natural

Existen diferentes métodos de ordenamiento externo; entre ellos se encuentra el de Mezcla Natural (o *Natural Merge Sort*).

Este método consiste en aprovechar la existencia de secuencias ya ordenadas dentro de los datos de un archivo. 
A diferencia de otros algoritmos, no divide los datos arbitrariamente, sino que identifica "runs" (subsecuencias ya ordenadas).

El algoritmo de ordenación por mezcla se basa en dividir recursivamente la lista de datos a ordenar en dos sublistas de tamaño similar, 
para posteriormente ordenarlas y fusionarlas, obteniendo así una lista final ordenada.

---

### ¿Cómo funciona?

Es un método de ordenamiento que:

- Detecta runs o secuencias naturales de elementos ya ordenados.


- Divide la lista en estas subsecuencias.


- Luego las va mezclando (merge) sucesivamente hasta obtener una lista ordenada completa.


A diferencia del Merge Sort tradicional, no divide la lista a la mitad, sino que identifica automáticamente las porciones ya ordenadas para optimizar el número de pasadas.


---

## Análisis de complejidad

La complejidad de un algoritmo describe cuánto trabajo se necesita realizar en función del tamaño de los datos de entrada (n). 
Se expresa mediante la notación Big O, que indica cómo crece el tiempo de ejecución conforme aumenta dicho tamaño.

Un concepto clave en la mezcla natural es el "run": una secuencia de elementos que ya están en orden dentro de la lista original. 
Cuantos más runs naturales existan, menos trabajo necesita realizar el algoritmo.

### Complejidad del método de mezcla natural

El rendimiento del algoritmo Merge Sort se puede entender analizando dos aspectos principales: el tiempo que tarda en ejecutarse y la memoria que utiliza.

- Complejidad temporal:
Es de O(n log n), donde n representa el número de elementos a ordenar. Esto se debe a que el algoritmo divide repetidamente la lista en mitades (lo que genera aproximadamente log n niveles de división) y, en cada nivel, realiza un proceso de fusión que recorre todos los elementos, con un costo de O(n).

- Complejidad espacial:
Es de O(n), ya que el algoritmo requiere espacio adicional para almacenar las sublistas temporales durante el proceso de fusión.


---

## Aplicaciones

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

---
## Ejemplo sencillo

Dado el arreglo:

```bash
 [3, 4, 6, 1, 2, 8, 5, 7]
```

Paso 1.Identificación de runs naturales:

```bash
 [3, 4, 6]
```
```bash
 [1, 2, 8]
```
```bash
 [5, 7]
```
Paso 2. Distribución en archivos:

```bash
 A → [3,4,6], [5,7]
```
```bash
 B → [1,2,8]
```
Paso 3. Primera mezcla:

```bash
 Resultado → [1,2,3,4,6,8,5,7]
```
Paso 4. Segunda identificación de runs:

```bash
[1,2,3,4,6,8]
```
```bash
[5,7]
```
Paso 5. Segunda mezcla → lista final ordenada

```bash
[1,2,3,4,5,6,7,8]
```

## Ejemplo en Python 


```bash
import time
import sys

# Aumentar el limite de recursividad.
# ya que se divide muchas veces la lista.
sys.setrecursionlimit(100000)

def merge_sort(lista):
    """
    Funcion principal del metodo de Mezcla Natural (Merge Sort).
    Divide la lista recursivamente hasta llegar a elementos individuales.
    """
    if len(lista) > 1:
        # 1. DIVIDIR: Encontramos el medio de la lista
        medio = len(lista) // 2
        izquierda = lista[:medio]
        derecha = lista[medio:]

        # Llamadas recursivas para seguir dividiendo las mitades
        merge_sort(izquierda)
        merge_sort(derecha)

        # 2. MEZCLAR: Unimos las partes de forma ordenada
        i = j = k = 0

        # Comparamos los elementos de las dos sublistas
        while i < len(izquierda) and j < len(derecha):
            if izquierda[i] < derecha[j]:
                lista[k] = izquierda[i]
                i += 1
            else:
                lista[k] = derecha[j]
                j += 1
            k += 1

        # Si quedaron elementos en la sublista izquierda, los agregamos
        while i < len(izquierda):
            lista[k] = izquierda[i]
            i += 1
            k += 1

        # Si quedaron elementos en la sublista derecha, los agregamos
        while j < len(derecha):
            lista[k] = derecha[j]
            j += 1
            k += 1

def cargar_datos(nombre_archivo):
    """
    Lee el archivo .txt y convierte cada linea en un numero entero.
    """
    try:
        with open(nombre_archivo, 'r') as archivo:
            return [int(linea.strip()) for linea in archivo]
    except FileNotFoundError:
        print(f"Error: No se encontro el archivo '{nombre_archivo}'")
        return None

def ejecutar_benchmark():
    """
    Carga, ordena y mide el tiempo en milisegundos.
    """
    print("=== Wiki-Benchmark: Algoritmos de Ordenamiento ===")
    print("Metodo seleccionado: Mezcla Natural (Merge Sort)")

    # Cargar los 50,000 numeros
    datos = cargar_datos('datos.txt')

    if datos is not None:
        print(f"Exito: {len(datos)} numeros cargados.")
        print("Iniciando ordenamiento...")

        # --- INICIO DEL BENCHMARK ---
        inicio = time.time()

        merge_sort(datos)

        fin = time.time()
        # --- FIN DEL BENCHMARK ---

        tiempo_total_ms = (fin - inicio) * 1000

        print("\n¡Ordenamiento completado con exito!")
        print(f"Tiempo total de ejecucion: {tiempo_total_ms:.2f} ms")
        print(f"Primeros 5 numeros ordenados: {datos[:5]}")

if __name__ == "__main__":
    ejecutar_benchmark()
```
## Ejemplo de salida en consola

```bash
=== Wiki-Benchmark: Algoritmos de Ordenamiento ===
Metodo seleccionado: Mezcla Natural (Merge Sort)
Exito: 50000 numeros cargados.
Iniciando ordenamiento...

¡Ordenamiento completado con exito!
Tiempo total de ejecucion: 89.49 ms
Primeros 5 numeros ordenados: [5, 6, 7, 9, 10]
```

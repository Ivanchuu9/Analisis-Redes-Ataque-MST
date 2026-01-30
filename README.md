# Análisis de Redes de Ataque con Algoritmos Voraces

Este proyecto implementa una solución algorítmica basada en Teoría de Grafos para optimizar el análisis de una red de ciberataques. El objetivo es identificar la infraestructura crítica de conexión minimizando el impacto total (coste), garantizando que todos los nodos del sistema permanezcan monitorizados bajo una misma red lógica.

## 📋 Descripción del Proyecto

El script procesa un archivo CSV que modela una red de ataques donde los nodos representan sistemas y las aristas representan el vector de ataque con un "coste" asociado (impacto).

Se implementarán y compararán dos estrategias de **Algoritmos Voraces (Greedy Algorithms)** para hallar el Árbol de Recubrimiento Mínimo (MST):
1.  **Algoritmo de Prim:** Estrategia centrada en nodos (crecimiento orgánico de la red).
2.  **Algoritmo de Kruskal:** Estrategia centrada en aristas (unión de subconjuntos disjuntos).

El programa no solo calcula el coste numérico óptimo, sino que genera una visualización gráfica de la topología de red resultante.

## 🛠️ Requisitos Técnicos
* **Lenguaje:** Python 3 (Librerías estándar: `heapq`)
* **Librerías Externas:**
    * `pandas` (Lectura y manipulación de datos CSV)
    * `networkx` (Creación y manipulación de grafos complejos)
    * `matplotlib` (Visualización gráfica de la red)
* **Datos:** Archivo `Sample_data.csv`

## 🚀 Instrucciones de Ejecución

1.  Coloca el archivo CSV de datos en la misma ruta que el script principal (`main.py`).
2.  Ejecuta el script.
3.  **Salidas del programa:**

    * **Visualización Gráfica:** Se abrirá una ventana emergente mostrando el grafo del MST con los nodos conectados y sus costes.
    * **Archivo** `output_print.txt`: Reporte final que incluye:
        * Listado detallado de aristas seleccionadas por Prim.
        * Listado detallado de aristas seleccionadas por Kruskal.
        * Coste total del impacto mínimo calculado por ambos métodos.

## ⚠️ Estructura del Dataset

Para ejecutar el script correctamente, el archivo CSV de entrada debe contener la siguiente cabecera:

| Columna | Descripción |
| :--- | :--- |
| `source` | Identificador del nodo (sistema) de origen del ataque |
| `target` | Identificador del nodo (sistema) de destino |
| `cost` | Valor numérico del impacto o coste de la conexión |

## 📊 Análisis de Complejidad Algorítmica

A diferencia de los algoritmos "Divide y Vencerás", los algoritmos voraces se analizan en función de las estructuras de datos utilizadas (Colas de Prioridad y Ordenamiento).

### 1. Algoritmo de Prim
Se utiliza una **Min-Heap (Cola de Prioridad)** para seleccionar siempre la arista de menor peso conectada a los nodos visitados.

* **Operaciones:** Por cada arista $E$, realizamos operaciones de inserción/actualización en el Heap que contiene $V$ vértices.
* **Complejidad Temporal:**
  $$O(E \log V)$$
  Donde $E$ es el número de ataques (aristas) y $V$ el número de sistemas (nodos). Es óptimo para grafos densos.

### 2. Algoritmo de Kruskal
Se basa en el **ordenamiento** de todas las aristas y el uso de una estructura de conjuntos disjuntos (Union-Find) para detectar ciclos.

* **Ordenamiento:** Ordenar las aristas por coste toma $O(E \log E)$.
* **Union-Find:** Las operaciones de búsqueda y unión son casi constantes, denotadas como $\alpha(V)$ (inversa de Ackermann).
* **Complejidad Temporal:**
  $$O(E \log E)$$
  Dado que $\log E$ es proporcional a $\log V$, a menudo se simplifica también como $O(E \log V)$. Es óptimo para grafos dispersos.

### 3. Conclusión
Ambos algoritmos garantizan encontrar el MST óptimo con una eficiencia logarítmica, lo cual es escalable para redes de gran tamaño frente a soluciones de fuerza bruta que tendrían complejidad exponencial.
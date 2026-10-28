# Solving the Maximum Diversity Problem Using GRASP and GRASP with Path Relinking

Este repositorio contiene la formulación, implementación en **Python** y evaluación computacional de metaheurísticas aplicadas al **Maximum Diversity Problem (MDP)**, un problema de optimización combinatoria con aplicaciones en selección de carteras, localización de instalaciones e ingeniería genética.

---

## 📌 Contenido y Enfoque del Proyecto

1. **Greedy Randomized Adaptive Search Procedure (GRASP):**
   - **Fase de Construcción:** Generación incremental de soluciones factibles mediante una función voraz que evalúa la contribución marginal $c(e) := \sum_{s \in S} \text{dist}(e,s)$. Selección adaptativa sobre una lista restringida de candidatos (RCL) calibrada con el parámetro de aleatoriedad $\alpha \in [0,1]$.
   - **Fase de Búsqueda Local:** Exploración del vecindario basada en movimientos de intercambio 1 a 1 (*swap moves*: $S' := (S \setminus \{s\}) \cup \{e\}$), aplicando mejoras sucesivas hasta alcanzar un óptimo local.

2. **Intensificación mediante Path Relinking (GRASP+PR):**
   - **Gestión del Conjunto Élite ($E$):** Mantenimiento de una población de soluciones de alta calidad y suficiente diversidad obtenidas en la fase constructiva.
   - **Procedimiento de Path Relinking:** Exploración sistemática de trayectorias entre pares de soluciones élite (solución inicial $S_I$ y solución guía $S_G$), evaluando iterativamente intercambios de elementos entre $A := S_G \setminus S_I$ y $B := S_I \setminus S_G$ para descubrir óptimos de mayor calidad.

3. **Calibración Experimental de Hiperparámetros:**
   - Análisis de sensibilidad numérica sobre 15 instancias de prueba fijando semilla pseudoaleatoria.
   - Evaluación de $\alpha \in \{0.1, 0.2, \ldots, 0.9\}$ y tamaño de conjunto élite $|E| \in \{5, 10, 15\}$, seleccionando como configuración óptima $\alpha = 0.4$ y $|E| = 10$ para equilibrar codicia, diversidad y coste computacional.

4. **Comparativa y Rendimiento Algorítmico:**
   - Comparación del valor de la función objetivo sobre instancias pequeñas (100 elementos) y grandes (500 elementos) bajo un límite de tiempo estricto (30 y 60 segundos).
   - Análisis de convergencia y cuellos de botella computacionales: eficiencia de GRASP básico en instancias pequeñas frente a los requerimientos temporales de GRASP+PR para poblar el conjunto élite en instancias complejas.

---

## 📂 Estructura del Código

- `instance.py`: Lectura y procesamiento de las matrices de distancias e instancias del problema.
- `solution.py`: Estructura de datos para la representación y evaluación de soluciones.
- `cgrasp.py`: Heurística constructiva aleatorizada (construcción de la RCL).
- `lsbestimp.py`: Procedimiento de búsqueda local basado en el mejor intercambio (*best-improving swap*).
- `grasp.py`: Bucle principal de ejecución multiarranque del algoritmo GRASP.
- `elite.py`: Gestión, filtrado de duplicados y ordenación del conjunto de soluciones élite.
- `path_relinking.py`: Implementación del algoritmo voraz de Path Relinking.
- `grasp_pr.py`: Flujo integrado de GRASP con intensificación por Path Relinking y búsqueda local final.
- `project1.pdf`: Informe técnico completo con el desglose matemático, tablas de resultados y conclusiones.

---

## 👥 Autores
- **Juan José Berdejo**
- **Gemma López Coloma**

*Universitat de València — Enero 2026*
```[cite: 64, 65, 66, 67, 68, 70, 71]

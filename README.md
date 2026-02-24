# Estimaciones MNAR (Notebook local)

Este repositorio contiene el notebook `Estimaciones_MNAR_local.ipynb`, orientado a simulación y estimación bayesiana en escenarios **MNAR** (*Missing Not At Random*) mediante dos enfoques:

- **Modelo de mezcla de patrones**
- **Modelo de selección**

Además incluye ejecución iterativa, variantes con seguimiento, actualización de priors y esquema tipo Gibbs, junto con rutinas de análisis y exportación de resultados a CSV.

## Estructura general del notebook

El notebook está organizado en bloques:

1. **Generación**
   - Funciones auxiliares para definir parámetros y generar muestras.
   - Construcción de datos observados/no observados con mecanismos MNAR.
2. **Modelado**
   - Definición de priors y verosimilitudes con **PyMC**.
   - Implementación de modelos de mezcla y selección.
3. **Ejecución de modelos**
   - Estimación base.
   - Estimación con seguimiento.
   - Actualización de priors.
   - Variante Gibbs iterativa.
4. **Análisis**
   - Cálculo de errores de estimación y métricas resumen.
   - Exportación de tablas y resultados.
5. **Simulaciones**
   - Ejecución completa del pipeline desde datos generados hasta análisis.

## Ejecución

Pueden ejecutarse 6 versiones distintas del modelado:
- base: Una única estimación de los parámetros en cada ejecución 
- seguimiento: Una única estimación haciendo uso de datos de seguimiento
- updatepriors: n_iteraciones de la estimación usando la posterior como prior en cada ejecución
- gibbs: n_iteraciones de la estimación de parámetros y creación de datos sintéticos para la siguiente iteración
- seg_updatepriors: updatepriors haciendo uso de datos de seguimiento
- seg_gibbs: gibbs haciendo uso de datos de seguimiento en la primera iteración
  
## Entradas y salidas esperadas

- Entradas habituales:
  - Archivos de configuración (`Gen_<label>.csv`, `Hip_<label>.csv`) contenidos en una carpeta `Simulaciones_<label>`.
  - Parámetros de ejecución:
    - `n_ejecuciones`: veces que se ejecuta el modelado (de manera independiente)
    - `n_iteraciones`: dentro de cada ejecución
    - `pct`: porcentaje de los datos ausentes a los que se consigue hacer seguimiento
    - `P_R`: nivel de ausencia estimado (Fuerza las bases de datos generadas con Gibbs a acercarse a ese nivel de ausencia).
- Salidas:
  - Directorios con datos generados/observados.
  - Estimaciones de parámetros (`Estimaciones_theta*`).
  - Resúmenes por ejecución (`Ejecuciones/Resumen_*.csv`).
  - Tablas de análisis (`Analisis/...`).


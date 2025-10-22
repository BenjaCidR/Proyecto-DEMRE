# 👋 ¡Bienvenido al Periodo 2004-2011!

## 🏗 Estructura del Repositorio


| Carpeta / Archivo | Descripción |
| :--- | :--- |
| `data/` | Contiene los datasets originales (crudos) y las versiones limpias (`data_clean`). **¡Advertencia: Archivos grandes!** |
| `notebooks/` | Espacio de trabajo para la exploración de datos (`EDA`), análisis estadístico y visualizaciones. |
| `scripts/` | Scripts de Python/R para tareas específicas (ej: limpieza, normalización, modelado). |
| `docs/` | Documentación adicional, incluyendo el **Diccionario de Datos Completo**. |
| `README.md` | Este archivo. |
| `LICENSE` | Información sobre la licencia del proyecto. |

---

## 🔎 El Corazón de los Datos: La Estructura

La base de datos se presenta en formato tabular (como un DataFrame de `pandas`), donde cada fila es un registro de resultados de un postulante.

### Variables Clave de un Vistazo

| Columna | Significado | Tipo de Dato | Rol Analítico |
| :--- | :--- | :--- | :--- |
| `ID_aux` | Identificador único de registro (anonimizado). | Alfanumérico | Identificador |
| `GRUPO_DEPENDENCIA` | Tipo de dependencia del establecimiento de egreso. | Categórico | Socioeducativo |
| `RAMA` | Modalidad de egreso (Humanista-Científica vs. Técnico-Profesional). | Categórico |  Contextual |
| `SITUACION_EGRESO` | Condición del postulante al rendir la prueba. | Categórico | Contextual |
| `CODIGO_REGION` | Código de la región del establecimiento de egreso. | Categórico | Geográfico |
| `LENG_ACTUAL` | Puntaje en la prueba de Comprensión Lectora/Lenguaje. | Numérico | Puntaje Objetivo |
| `MATE_ACTUAL` | Puntaje en la prueba de Matemáticas. | Numérico | Puntaje Objetivo |
| `RBD` | Rol base de datos . | Numérico | Identificador |

# 📊 Estabilidad de Puntajes: El Fenómeno del Anclaje a 500

Este proyecto analiza puntajes que han sido sometidos a un proceso de **estandarización** con el objetivo de hacerlos comparables a lo largo del tiempo (2004-2025). El fenómeno más notable en la tendencia central es la estabilidad de los promedios de las pruebas cerca de los **500 puntos**.

---

## 1. ¿Por Qué los Promedios son Tan Estables?

La estabilidad no es una coincidencia de rendimiento nacional, sino un **efecto artificial y buscado** del diseño estadístico del sistema de acceso (PSU/PAES).

* **Punto de Anclaje ($\mu$):** El puntaje promedio de cada prueba (`LENG_ACTUAL`, `MATE_ACTUAL`, etc.) se **ajusta intencionalmente** en el proceso de escalamiento para que la media se sitúe siempre alrededor de los **500 puntos**.
* **Diseño Estadístico:** Se asume que el rendimiento promedio de la población que rinde la prueba es constante. El puntaje bruto (respuestas correctas) necesario para alcanzar 500 puntos **cambia cada año** en función de la dificultad de la prueba y el rendimiento real de la cohorte.

---

## 2. Propósito del Escalamiento (Comparabilidad)

El **DEMRE** utiliza el puntaje transformado (estandarizado) en lugar del puntaje bruto (respuestas correctas) por una razón fundamental: **garantizar la comparabilidad histórica**.

* **Valor Constante:** Al anclar la media en 500, el sistema asegura que un 650 en 2004 tenga el mismo **valor estadístico** (es decir, la misma posición relativa dentro de la distribución de puntajes de ese año) que un 650 en 2011.

**Conclusión:** Los datos son **transformados** por el motivo de ofrecer un standar a lo largo de los años. En futuras entregas del proyecto se investigará como puede influir esto en el análisis de los datos (que datos/medidas estadísticas son relevantes para establecer diferencias entre desempeño de distintos procesos de admisión).

> **IMPORTANTE:** El Rol Base de Datos (`RBD`) es el código que identifica a los establecimientos que forman parte del Sistema de Aseguramiento de la Calidad, siendo clave para la fiscalización y evaluación educativa. Para más información revise https://www.bcn.cl/leychile/navegar?idNorma=1093444.

---

### ⚠️ Consideraciones Éticas y de Uso

* Los datos están **anonimizados**. El uso de esta información está restringido al análisis estadístico y la investigación educativa.

---
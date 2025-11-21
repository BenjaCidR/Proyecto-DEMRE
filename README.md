# 📚 ¡Bienvenido al Proyecto de Análisis de Puntajes de Pruebas de Acceso! 📚

## Autores
| Nombre | Rol |
| :--- | :--- |
| Benjamín Cid Roblero | Responder preguntas 1 y 6, análisis preliminar años 2004-2011 |
| Martín Pérez Reveco |  Responder preguntas 3, 4 y 5, análisis preliminar años 2019-2025 |
| Felipe Serrano Salinas | Responder preguntas 2 y 7, análisis preliminar años 2012 - 2018 |

## 🏁 Objetivos principales
El propósito de este proyecto se basa en dar respuesta a las siguientes preguntas:
1. ¿Existen diferencias significativas en torno a los puntajes según el tipo de establecimiento (Municipal, Subvencionado, Particular), se han mantenido a lo largo del tiempo?
2. ¿Cómo se vieron afectados los puntajes durante la pandemia y el estallido social, considerando factores como la dificultad del acceso a las clases presenciales?
3. ¿En qué comunas de Santiago se concentran los mejores puntajes (>= 850) y cómo relacionamos esto a los tipos de colegios en cada comuna?
4. ¿Han cambiado los promedios de puntajes en el cambio de PSU, PDT y PAES, y si estos determinan un cambio en la forma de medir el rendimiento estudiantil o más bien un cambio real en el desempeño de estos? A considerar el cambio de escala de PSU a PAES.
5. ¿Qué factores académicos y socioeconómicos (NEM, Ranking, Tipo de Colegio) predicen la probabilidad de que un estudiante obtenga un Puntaje de Excelencia (Top 5%) a lo largo del periodo 2004-2025?
6. ¿Es posible identificar perfiles de colegios que compartan características comunes en su desempeño académico, de forma que algunos establecimientos enseñen resultados similares entre sí y se diferencien de otros grupos de colegios?
7. ¿Se puede establecer un perfil de estudiante que permita explicar su desempeño en la prueba de admisión, considerando variables como el promedio de notas de enseñanza media, la situación de egreso y otras condiciones académicas o socioeconómicas?



## 💾 Fuente de Datos del Proyecto (Data Source)

Este proyecto de análisis histórico se basa en datos públicos de resultados de las Pruebas de Acceso a la Educación Superior en Chile.

## 1. Origen Primario de los Datos

La base de datos se obtuvo a partir del **Portal de Bases de Datos del DEMRE**. Por más información, acceda a https://demre.cl/portales/portal-bases-datos.
* **Entidad Fuente:** Departamento de Evaluación, Medición y Registro Educacional (DEMRE), perteneciente a la Universidad de Chile.
* **Período Cubierto:** El *dataset* abarca los resultados de los procesos de admisión desde **2004 hasta 2025** (incluyendo la era PSU, PDT/PTU y PAES).
* **Contenido:** El *dataset* contiene los resultados individuales anonimizados, junto con variables contextuales y de procedencia del estudiante.


## 🏗 Estructura del Repositorio

| Carpeta / Archivo | Descripción |
| :--- | :--- |
| `data/` | Contiene archivos .parquet con el trabajo realizado y finalizado por cada uno de los integrantes de este proyecto en su primera fase (hasta la fecha 21 Octubre 2025) |
| `notebooks/` | Desarrollo del trabajo para la exploración de datos (`EDA`), análisis estadístico y visualizaciones. |
| `PROJECT_README.md` | Este archivo. |
| `.gitignore` | Archivos no relevantes para el proyecto. |

---

## 🔎 El Corazón de los Datos: La Estructura

La base de datos se presenta en formato tabular (como un DataFrame de `pandas`), donde cada fila es un registro de resultados de un postulante.

### Variables Clave

| Columna | Significado | Tipo de Dato | Rol Analítico |
| :--- | :--- | :--- | :--- |
| `id_estudiante` | Identificador único de registro (anonimizado). | Alfanumérico | Identificador |
| `dependencia_colegio` | Tipo de dependencia del establecimiento de egreso. | Categórico | Socioeducativo |
| `rama_educacional` | Modalidad de egreso (Humanista-Científica vs. Técnico-Profesional). | Categórico |  Contextual |
| `situacion_egreso` | Condición del postulante al rendir la prueba. | Categórico | Contextual |
| `cod_region` | Código de la región del establecimiento de egreso. | Categórico | Geográfico |
| `cod_comuna` | Código de la comuna del establecimiento de egreso. | Categórico | Geográfico |
| `puntaje_lectora` | Puntaje en la prueba de Comprensión Lectora/Lenguaje. | Numérico | Estadístico |
| `puntaje_m1` | Puntaje en la prueba de Matemáticas/M1. | Numérico | Estadístico |
| `id_colegio_rbd` | Rol base de datos | Numérico | Identificador |
| `promedio_notas`| El promedio de notas de enseñanza media | Numérico | Estadístico |
| `puntaje_nem`| Puntaje asociado al promedio de notas de enseñanza media | Numérico | Estadístico |
| `puntaje_ranking`| Puntaje asociado a una bonificación factor del desempeño del estudiante en su propio contexto escolar | Numérico | Estadístico |
| `year_proceso` | Año en el cual se rinde la prueba. | Categórico | Contextual |
| `%_de_logro_obligatorias`| Puntaje ponderado entre las pruebas Lectora/Lenguaje y Matemáticas/M1 | Numérico | Estadístico |

# 📊 Estabilidad de Puntajes: El Fenómeno del Anclaje a 500
Es fundamental recalcar (y contextualizar) que este proyecto analiza puntajes que han sido sometidos a un proceso de **estandarización** con el objetivo de hacerlos comparables a lo largo del tiempo (2004-2025). El fenómeno más notable en la tendencia central es la estabilidad de los promedios de las pruebas cerca de los **500 puntos**.

---

## 1. ¿Por Qué los Promedios son Tan Estables?

La estabilidad no es una coincidencia de rendimiento nacional, sino un **efecto artificial y buscado** del diseño estadístico del sistema de acceso (PSU/PAES).

* **Punto de Anclaje ($\mu$):** El puntaje promedio de cada prueba (`LENG_ACTUAL`, `MATE_ACTUAL`, etc.) se **ajusta intencionalmente** en el proceso de escalamiento para que la media se sitúe siempre alrededor de los **500 puntos**.
* **Diseño Estadístico:** Se asume que el rendimiento promedio de la población que rinde la prueba es constante. El puntaje bruto (respuestas correctas) necesario para alcanzar 500 puntos **cambia cada año** en función de la dificultad de la prueba y el rendimiento real de la cohorte.
* Véase en los gráficos adjuntos en la rama del repsitorio `Cid-2004_2011/notebooks/EDA_2004_2011.ipynb`

---

## 2. Propósito del Escalamiento (Comparabilidad)

El **DEMRE** utiliza el puntaje transformado (estandarizado) en lugar del puntaje bruto (respuestas correctas) por una razón fundamental: **garantizar la comparabilidad histórica**.

* **Valor Constante:** Al anclar la media en 500, el sistema asegura que un 650 en 2004 tenga el mismo **valor estadístico** (es decir, la misma posición relativa dentro de la distribución de puntajes de ese año) que un 650 en 2011.

**Conclusión:** Los datos son **transformados** por el motivo de ofrecer un standar a lo largo de los años. En futuras entregas del proyecto se investigará como puede influir esto en el análisis de los datos (que datos/medidas estadísticas son relevantes para establecer diferencias entre desempeño de distintos procesos de admisión), por lo que por esta entrega se presentan gráficos de variables descriptivas sin entrar más a detalle.

> **IMPORTANTE:** El Rol Base de Datos (`RBD`) es el código que identifica a los establecimientos que forman parte del Sistema de Aseguramiento de la Calidad, siendo clave para la fiscalización y evaluación educativa. Para más información revise https://www.bcn.cl/leychile/navegar?idNorma=1093444.

---

### 📚 Librerías implementadas 📚:

| Librería | Descripción |
|---------|-------------|
| **NumPy** | Manejo eficiente de arreglos multidimensionales y operaciones matemáticas de alto rendimiento. |
| **Pandas** | Manipulación, limpieza y análisis estructurado de datos mediante DataFrames. |
| **Scikit‑Learn (sklearn)** | Implementación de modelos estadísticos y de machine learning para clasificación, regresión y clustering. |
| **Seaborn** | Biblioteca para visualizaciones estadísticas de alto nivel y gráficos estilizados. |
| **Matplotlib** | Herramienta base para generar gráficos personalizados y visualizaciones detalladas. |

> **Nota:** Estas librerías deben ser utilizadas para el análisis y procesamiento de los datos del proyecto.


---
### ⚠️ Consideraciones Éticas y de Uso

* Los datos están **anonimizados**. El uso de esta información está restringido al análisis estadístico y la investigación educativa.

---

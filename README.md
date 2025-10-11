# 👋 ¡Bienvenido al Proyecto de Análisis de Puntajes de Pruebas de Acceso!

 **Todo esto es un ejemplo, modificar despues según corresponda**

Este repositorio alberga la base de datos y los scripts de análisis para el estudio histórico y longitudinal de los resultados de las pruebas de acceso a la educación superior, cubriendo un extenso periodo desde **2004 hasta 2025**.

El objetivo principal es generar *insights* profundos que permitan:

1.  **Evaluar la Evolución:** Entender cómo ha cambiado el rendimiento de los postulantes a lo largo de dos décadas.
2.  **Identificar Brechas:** Analizar las disparidades en los puntajes según variables clave como la dependencia escolar, la rama de egreso y la ubicación geográfica.
3.  **Informar Políticas:** Proporcionar evidencia sólida para la toma de decisiones en el ámbito de la política educativa.

---

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
| `ID_aux` | Identificador único de registro (anonimizado). | Alfanumérico | *Identificador* |
| `GRUPO_DEPENDENCIA` | Tipo de dependencia del establecimiento de egreso. | Categórico | **Socioeducativo** |
| `RAMA` | Modalidad de egreso (Humanista-Científica vs. Técnico-Profesional). | Categórico | **Contextual** |
| `SITUACION_EGRESO` | Condición del postulante al rendir la prueba. | Categórico | **Contextual** |
| `CODIGO_REGION` | Código de la región del establecimiento de egreso. | Categórico | **Geográfico** |
| `LENG_ACTUAL` | Puntaje en la prueba de Comprensión Lectora/Lenguaje. | Numérico | **Puntaje Objetivo** |
| `MATE_ACTUAL` | Puntaje en la prueba de Matemáticas. | Numérico | **Puntaje Objetivo** |

> **IMPORTANTE:** Los puntajes (`*_ACTUAL`) están en una escala estándar (generalmente entre 300 y 850). Para el detalle completo de los códigos (ej. el significado de `GRUPO_DEPENDENCIA = 1`), consulte el **[Diccionario de Datos Completo]** ubicado en la carpeta `docs/`.

---

## ⚙️ Primeros Pasos y Contribución

Para empezar a trabajar con el *dataset*:

1.  **Clonar el Repositorio:**
    ```bash
    git clone [URL_del_repositorio]
    ```
2.  **Configurar el Entorno:** Instalar las dependencias necesarias (usualmente `pandas`, `numpy`, `matplotlib`, `seaborn`, etc.).
3.  **Exploración Inicial:** Diríjase a la carpeta `notebooks/` y comience con el *notebook* de exploración de datos (ej. `01_EDA_Inicial.ipynb`).

### ⚠️ Consideraciones Éticas y de Uso

* Los datos están **anonimizados**. El uso de esta información está restringido al análisis estadístico y la investigación educativa.
* Trate las columnas de códigos (ej. `CODIGO_REGION`) como **variables categóricas** y no como variables continuas.

---

### **¡Tu contribución es clave para transformar datos en conocimiento educativo!**
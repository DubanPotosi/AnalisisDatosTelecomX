# Análisis de Evasión de Clientes (Churn) en TelecomX

## Descripción del Proyecto

Este proyecto tiene como objetivo principal analizar los datos de clientes de la empresa de telecomunicaciones **TelecomX** para identificar los factores clave que influyen en la evasión de clientes (Churn). A través de un proceso de extracción, transformación, carga (ETL) y análisis exploratorio de datos (EDA), buscamos comprender los patrones de comportamiento de los clientes, las características demográficas y de servicio que predicen la baja del servicio. El objetivo final es proporcionar *insights* accionables y recomendaciones estratégicas que permitan a TelecomX anticipar y mitigar la fuga de clientes, mejorando así la retención y la satisfacción general.

## Instalación y Configuración

Para ejecutar este proyecto, necesitarás tener instalado Python y las siguientes librerías. Se recomienda utilizar un entorno virtual para gestionar las dependencias.

### Requisitos Previos

*   **Python**: Versión 3.8 o superior.
*   **Librerías**: `pandas`, `requests`, `matplotlib`, `seaborn`.

### Pasos para la Instalación

1.  **Clonar el repositorio (si aplica)**:
    ```bash
    git clone <URL_DEL_REPOSITORIO>
    cd TelecomX_Churn_Analysis
    ```

2.  **Crear y activar un entorno virtual (recomendado)**:
    ```bash
    python -m venv venv
    source venv/bin/activate  # En Linux/macOS
    # venv\Scripts\activate  # En Windows
    ```

3.  **Instalar las dependencias**: 
    ```bash
    pip install pandas requests matplotlib seaborn
    ```

## Uso del Proyecto

Este proyecto está implementado como un Jupyter Notebook, lo que permite una ejecución paso a paso del análisis.

### Instrucciones para Ejecutar el Código

1.  **Iniciar Jupyter Notebook (o Jupyter Lab)**:
    ```bash
    jupyter notebook
    # o
    jupyter lab
    ```

2.  **Abrir el Notebook**: Navega hasta el archivo `TelecomX_Churn_Analysis.ipynb` (o el nombre de tu notebook) y ábrelo.

3.  **Ejecutar las Celdas**: Ejecuta las celdas del notebook en orden, desde la introducción hasta las conclusiones y recomendaciones. Cada celda contiene código Python y/o texto Markdown que detalla los pasos del análisis.

### Fragmentos de Código Clave

*   **Carga de Datos**:
    ```python
    import requests
    import pandas as pd

    url = "https://raw.githubusercontent.com/alura-cursos/challenge2-data-science-LATAM/refs/heads/main/TelecomX_Data.json"
    response = requests.get(url)
    df = pd.DataFrame(response.json())
    ```

*   **Limpieza de `Charges.Total`**:
    ```python
    df['Charges.Total'] = pd.to_numeric(df['Charges.Total'], errors='coerce')
    df['Charges.Total'] = df['Charges.Total'].fillna(0)
    ```

*   **Estandarización de `Churn` y `gender`**:
    ```python
    df['Churn'] = df['Churn'].replace('', 'No').replace({'Yes': 1, 'No': 0})
    df['gender'] = df['gender'].replace({'Female': 1, 'Male': 0})
    ```

## Estructura del Proyecto

El proyecto se organiza de la siguiente manera (asumiendo que es un único archivo Jupyter Notebook):

```
. # Directorio raíz del proyecto
├── TelecomX_Churn_Analysis.ipynb # Notebook principal con todo el análisis
└── README.md                    # Este archivo de documentación
```

*   **`TelecomX_Churn_Analysis.ipynb`**: Contiene la totalidad del análisis, desde la carga de datos hasta las conclusiones y recomendaciones. Está estructurado en secciones claras (Extracción, Transformación, Carga y Análisis, Informe Final).

## Problemas Comunes y Soluciones

*   **`KeyError` al acceder a columnas anidadas**: Si encuentras errores como `KeyError: 'customer'`, significa que las columnas originales con diccionarios anidados (`customer`, `phone`, `internet`, `account`) ya fueron aplanadas durante la carga inicial del DataFrame. Asegúrate de referirte a las nuevas columnas directamente (e.g., `df['gender']` en lugar de `df['customer']['gender']`).
*   **`FutureWarning` de Seaborn/Matplotlib**: Es común recibir advertencias sobre el uso de `palette` sin `hue` en funciones como `sns.countplot` o `sns.boxplot`. Esto es un aviso de que el comportamiento cambiará en futuras versiones. Para evitarlo, se recomienda añadir `hue='nombre_de_columna'` y `legend=False` cuando sea apropiado.

## Contribución y Licencia

### Contribución

¡Las contribuciones son bienvenidas! Si deseas mejorar este proyecto, puedes:

1.  Hacer un fork del repositorio.
2.  Crear una nueva rama (`git checkout -b feature/nueva-funcionalidad`).
3.  Realizar tus cambios y asegurarte de que el código pase las pruebas (si las hay).
4.  Hacer commit de tus cambios (`git commit -m 'feat: Añadir nueva funcionalidad X'`).
5.  Hacer push a la rama (`git push origin feature/nueva-funcionalidad`).
6.  Abrir un Pull Request.

### Licencia

Este proyecto está bajo la licencia [MIT](https://opensource.org/licenses/MIT). Puedes consultar el archivo `LICENSE` para más detalles.

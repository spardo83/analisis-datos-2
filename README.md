# Actividad 1: Interpretabilidad de Modelos
**Análisis de Datos 2 — 4B2026**

Repositorio con la resolución de la Actividad 1 sobre interpretabilidad, diagnóstico global (PFI), diagnóstico local (SHAP) y auditoría de modelos sobre el dataset de salarios en Data Science.

## Estructura del proyecto

- `actividad1_interpretabilidad.ipynb`: notebook con el flujo completo de entrenamiento, diagnóstico, auditoría de leakage y comparación del modelo corregido (con outputs ejecutados).
- `data/ds_salaries.csv`: dataset de [Data Science Salaries 2023](https://www.kaggle.com/datasets/arnabchaki/data-science-salaries-2023) (Kaggle).
- `requirements.txt`: librerías necesarias para ejecutar el notebook.

## Instrucciones para reproducir

```bash
# Crear y activar entorno virtual
python3 -m venv .venv
source .venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt

# Abrir el notebook
jupyter notebook actividad1_interpretabilidad.ipynb
```

## Resumen del análisis

1. **Modelo baseline:** Se entrenó un Random Forest con todas las variables disponibles, obteniendo un $R^2$ sospechosamente alto de 0.983 en test.
2. **Diagnóstico:** Tanto el análisis global (PFI) como el local (SHAP) mostraron que el modelo dependía de forma casi exclusiva de la columna `salary`.
3. **Auditoría:** Se comprobó que `salary_in_usd` es una conversión determinística fija de `salary` por año y moneda (*data leakage*). Además, se detectó una alta redundancia entre `employee_residence` y `company_location` (97.4% de coincidencia).
4. **Corrección:** Al remover `salary`, el modelo ($R^2 \approx 0.40$) redistribuye la importancia en factores laborales genuinos (`employee_residence`, `job_title`, `experience_level`).

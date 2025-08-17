# Telecom X — Análisis de Evasión de Clientes (Churn)

Este repositorio/notebook contiene un flujo **ETL + EDA** para analizar la evasión de clientes en **Telecom X**.  
El objetivo es **entender patrones de churn** y proponer acciones de retención basadas en datos.

---

## 🧭 Contenido

- **Objetivo**: medir y explicar la evasión (churn) y sus factores asociados.
- **Alcance**: extracción de datos, transformación/limpieza, análisis exploratorio, visualizaciones e informe final.
- **Stack**: Python (Google Colab), `pandas`, `numpy`, `matplotlib`.

---

## 📂 Estructura del Notebook

1. **EXTRACCIÓN**
   - Montaje de Google Drive.
   - Lectura del dataset en formato **JSON**.
   - **Aplanado** de campos anidados con `pd.json_normalize`.

2. **TRANSFORMACIÓN**
   - Tipificación: `customerID` como string; campos numéricos a `float/int`.
   - **Imputación mínima** de `account.Charges.Total`:
     - Si `tenure = 0` ⇒ Total = 0.
     - Si `tenure > 0` ⇒ Total ≈ Monthly × tenure.
   - Creación de variables:
     - `Churn_bin` (1 = yes, 0 = no).
     - `Cuentas_Diarias` = `account.Charges.Monthly` / 30.4375.
   - Normalización ligera de categóricas (minúsculas/espacios) y `category`.

3. **CARGA Y ANÁLISIS (EDA)**
   - Descriptivos globales y por churn (`describe`, `groupby`).
   - Distribución de churn (conteos y %).
   - **Churn por categoría**: contrato, método de pago, seguridad/soporte.
   - **Numéricas por churn**: `tenure`, `Monthly`, `Total`, `Cuentas_Diarias` (histogramas y boxplots).
   - Ranking rápido de relevancia:
     - Numéricas: |correlación| con churn.
     - Categóricas: **lift** (max − min de la tasa de churn por categoría).

4. **INFORME FINAL**
   - Introducción y contexto del problema.
   - Resumen de limpieza/tratamiento.
   - Hallazgos principales (tablas y gráficos clave).
   - Conclusiones e **insights** accionables.
   - **Recomendaciones** de retención (p. ej., migración a contrato anual, activar seguridad/soporte, foco en tenure bajo + monthly alto).

---


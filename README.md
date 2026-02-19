# Modelo de Predicción de ETFs

Aplicación de predicción para ETFs construida con **Streamlit** y modelos de **Deep Learning** (Keras/TensorFlow). El proyecto permite:

- Visualizar histórico de precios de ETFs.
- Generar predicciones a 5 días hábiles para ETFs seleccionados.
- Estimar el valor proyectado de una inversión en USD.
- Analizar métricas de evaluación del modelo (MAE, RMSE, R², MAPE).

> ⚠️ Este proyecto tiene fines educativos/informativos y **no constituye asesoramiento financiero**.

---

## ETFs soportados

- SPY
- DIA
- QQQ
- XLK
- IWV

---

## Estructura del repositorio

```text
.
├── Home.py                          # Página principal (selección de ETF, monto y rango histórico)
├── pages/
│   ├── Page_2.py                    # Predicción a 5 días + recomendación
│   └── Page_3.py                    # Visualización de métricas y gráficos de evaluación
├── Modelo_Predictivo.ipynb          # Notebook de entrenamiento/evaluación
├── generar_walk_forward_dias.py     # Script para generar archivos walk_forward_diaN.pkl
├── requirements.txt                 # Dependencias del proyecto
├── DataSet_General/
│   └── DATASET_LIMPIO_E_IMPUTADO.csv
├── modelos_directos_recientes/      # Modelos y scalers por horizonte (día1..día5)
├── datos_wf_testing.pkl             # Resultados de walk-forward (insumo para Page_3)
├── walk_forward_dia1.pkl            # Métricas por día de predicción (1..5)
├── walk_forward_dia2.pkl
├── walk_forward_dia3.pkl
├── walk_forward_dia4.pkl
├── walk_forward_dia5.pkl
└── logo.jpeg
```

---

## Requisitos

- Python 3.10+ recomendado
- Dependencias principales:
  - streamlit
  - yfinance
  - pandas
  - numpy
  - plotly
  - tensorflow
  - scikit-learn
  - matplotlib

---

## Instalación

1. Clona el repositorio.
2. (Opcional) Crea y activa un entorno virtual.
3. Instala dependencias:

```bash
pip install -r requirements.txt
```

---

## Ejecución de la app

Desde la raíz del proyecto:

```bash
streamlit run Home.py
```

La app abrirá una interfaz multipágina con:

- **Inicio (`Home.py`)**: selección del ETF, rango histórico y monto de inversión.
- **Predicción (`pages/Page_2.py`)**: proyección a 5 días hábiles y señal de oportunidad.
- **Métricas (`pages/Page_3.py`)**: comparación real vs predicho y métricas de desempeño.

---

## Flujo de datos y modelos

- La app usa precios de mercado desde **Yahoo Finance** (`yfinance`).
- Variables exógenas macro (p. ej. `DGS10`, `DGS2`, `VIXCLS`) se leen desde:
  - `DataSet_General/DATASET_LIMPIO_E_IMPUTADO.csv`
- Los modelos y escaladores se cargan desde `modelos_directos_recientes/`:
  - `modelo_dia1.h5` ... `modelo_dia5.h5`
  - `scaler_X_dia1.pkl` ... `scaler_X_dia5.pkl`
  - `scaler_y_dia1.pkl` ... `scaler_y_dia5.pkl`

---

## Archivos de evaluación

Para que la página de métricas (`pages/Page_3.py`) funcione correctamente, deben existir:

- `datos_wf_testing.pkl`
- `walk_forward_dia1.pkl` ... `walk_forward_dia5.pkl`

Si necesitas regenerar los archivos `walk_forward_diaN.pkl`, ejecuta:

```bash
python generar_walk_forward_dias.py
```

---

## Notas importantes

- Las predicciones dependen de la disponibilidad de datos externos (Yahoo Finance).
- Si faltan columnas/activos en la descarga, la app puede detenerse con mensajes de validación.
- El proyecto está orientado a análisis experimental y demostración de modelado predictivo.

---

## Autor

Repositorio: **carlos060495/Modelo_Prediccion_ETFS**

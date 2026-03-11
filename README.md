# Challenge Telecom X — Parte 2: Predicción de Cancelación de Clientes (Churn)

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completado-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

##  Descripción

Este repositorio contiene la solución completa al **Challenge Telecom X — Parte 2**, enfocado en la construcción de un pipeline de Machine Learning para predecir qué clientes tienen mayor probabilidad de **cancelar sus servicios (churn)**.

El proyecto forma parte de una serie de desafíos de Data Science sobre la empresa ficticia **Telecom X**, y continúa el análisis exploratorio realizado en la Parte 1, avanzando hacia el modelado predictivo.

---

## Estructura del Repositorio
```
├── Challenge_Telecom_X_parte_2.ipynb   # Notebook principal con el pipeline completo
└── README.md                           # Este archivo
```

---

## Objetivos del Proyecto

- Preparar los datos para el modelado (encoding, escalado, análisis de desbalance)
- Realizar análisis de correlación y selección de variables relevantes
- Entrenar y comparar múltiples modelos de clasificación
- Evaluar el rendimiento con métricas apropiadas para contextos de churn
- Interpretar la importancia de las variables en cada modelo
- Elaborar una conclusión estratégica orientada al negocio

---

## Dataset

| Característica | Detalle |
|---|---|
| Registros | 7.032 clientes |
| Variables | 22 (16 numéricas, 4 categóricas, 1 ID, 1 target) |
| Variable objetivo | `evasion` (1 = canceló, 0 = activo) |
| Desbalance de clases | 73.4% no canceló / 26.6% canceló |

### Variables principales

`id_cliente` · `genero` · `adulto_mayor` · `tiene_pareja` · `personas_a_cargo` · `meses_permanencia` · `tipo_internet` · `tipo_contrato` · `metodo_pago` · `cobro_mensual` · `cobro_total` · `cuentas_diarias` · `seguridad_online` · `soporte_tecnico` · entre otras.

---

## Pipeline de Machine Learning

### 1. Preparación de Datos
- Eliminación de `id_cliente`
- One-Hot Encoding sobre variables categóricas (`pd.get_dummies`)
- Análisis de desbalance de clases
- División Train/Test: **70% / 30%** con `stratify=y`
- Escalado con `StandardScaler` para modelos sensibles a escala

### 2. Análisis Exploratorio Enfocado en Churn
- Matriz de correlación con heatmap
- Tasa de cancelación por tipo de contrato
- Boxplots: `meses_permanencia` y `cobro_total` vs `evasion`
- Análisis de variables protectoras (soporte técnico, seguridad online)

### 3. Modelos Entrenados

| Modelo | Requiere Escalado |
|---|---|
| Regresión Logística | ✅ Sí |
| K-Nearest Neighbors (KNN) | ✅ Sí |
| Árbol de Decisión | ❌ No |
| Random Forest | ❌ No |

### 4. Ajuste de Hiperparámetros
- `GridSearchCV` con validación cruzada (cv=5)
- Métrica de optimización: **F1-Score**

---

## Resultados

### Comparación Final de Modelos (post GridSearchCV)

| Modelo | Accuracy | Precision | Recall | F1-Score |
|---|---|---|---|---|
| **Regresión Logística** ⭐ | **0.8024** | **0.6558** | **0.5401** | **0.5924** |
| Random Forest | 0.7905 | 0.6355 | 0.4973 | 0.5580 |
| Decision Tree | 0.7882 | 0.6307 | 0.4902 | 0.5517 |
| KNN | 0.7635 | 0.5576 | 0.5348 | 0.5460 |

>  **Modelo seleccionado: Regresión Logística** (`C=10`) — mejor F1-Score y sin signos de overfitting.

### Variables Más Importantes (consenso entre modelos)

1. `meses_permanencia` — menor permanencia, mayor riesgo
2. `tipo_contrato_Mes_a_mes` — tasa de churn del 42.7%
3. `cobro_total` y `cobro_mensual` — costo elevado sin valor percibido
4. `tipo_internet_Fiber optic` — segmento con alta insatisfacción
5. `metodo_pago_Electronic check` — asociado a menor compromiso

---

## Conclusión Estratégica

Los clientes con **contratos mensuales**, **pocos meses de permanencia** y **cobros elevados** representan el segmento de mayor riesgo. Las estrategias recomendadas incluyen:

- Programa de fidelización en los primeros 6 meses
- Incentivos para migrar a contratos anuales o bianuales
- Bundling de servicios adicionales (soporte técnico, seguridad online)
- Revisión de precios en el segmento Fiber optic
- Despliegue del modelo en producción para detección temprana

---

## Tecnologías Utilizadas

- **Python 3.10+**
- `pandas` · `numpy` — manipulación de datos
- `matplotlib` · `seaborn` — visualización
- `scikit-learn` — modelado, evaluación y ajuste de hiperparámetros
- **Google Colab** — entorno de ejecución

---

## Cómo Ejecutar

1. Clona el repositorio:
```bash
   git clone https://github.com/tu-usuario/challenge-telecom-x-parte-2.git
```
2. Abre el notebook en Google Colab o Jupyter:
```
   Challenge_Telecom_X_parte_2.ipynb
```
3. Ejecuta las celdas en orden secuencial.

> **Nota:** El notebook asume que el dataset ya fue procesado en la Parte 1 del challenge. Asegúrate de tener disponible el DataFrame `datos` con las columnas descritas.

---

## Autor

Desarrollado por: Houston Franz Gaona Jumpa
como parte del programa de formación en Data Science de Alura Latam.  
Si tienes preguntas o sugerencias, ¡no dudes en abrir un *issue* o un *pull request*!

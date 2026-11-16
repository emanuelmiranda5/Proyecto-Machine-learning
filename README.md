# Modelo predictivo NASDAQ-100
<img width="800" height="300" alt="image" src="https://github.com/user-attachments/assets/038bbea6-8d7c-495d-929f-67b812a05c65" />

# Autores: Emanuel Miranda Sinning, Mario José Moreno Remirez, Gabriel Alejandro Zambrano Herazo
Objetivo: Desarrollar y evaluar modelos de Machine Learning supervisados sobre un dataset de las 102 empresas más grandes de Estados Unidos para identificar y predecir cuál representa la mejor oportunidad de inversión.
#
Dataset: https://www.kaggle.com/datasets/ifuurh/nasdaq100-fundamental-data

### Modelos empleados
* **Clasificación Binaria:** Decision Tree Classifier, Random Forest Classifier, Support Vector Machine (SVC), Gaussian Naive Bayes, Dummy Classifier
* **Clasificación Multiclase (4 clases):** Random Forest Classifier, Decision Tree Classifier, Support Vector Machine (SVC), Gaussian Naive Bayes
* **Regresión:** Random Forest Regressor, Support Vector Regressor (SVR), Ridge Regression, Decision Tree Regressor
* **Redes Neuronales (MLP):** Multi-Layer Perceptron (MLPClassifier, MLPRegressor)
* **Optimización y Selección:** RandomizedSearchCV, Stratified K-Fold (5-fold), K-Fold (5-fold)



### ¿Qué contiene el dataset?
El dataset (`nasdaq100_metrics_ratios.csv`) recopila estados financieros y ratios fundamentales de **102 compañías** listadas en el índice **Nasdaq-100** (como Apple, Microsoft, NVIDIA, Amazon, Meta, Broadcom, Adobe, Qualcomm y PayPal), organizados en **283 columnas** divididas en las siguientes categorías:

* **Identificación y clasificación sectorial (4 columnas):** Código bursátil (`symbol`), nombre de la empresa (`company`), sector económico (`sector`, con 7 categorías lideradas por *Information Technology* con el 41,2 %) y subsector específico (`subsector`, con 41 industrias).
* **Historial financiero multianual (2017–2022) y métricas actuales (`_latest`):** Cada indicador fundamental se reporta de forma anualizada entre 2017 y 2022 junto con su valor consolidado más reciente (`_latest`), permitiendo analizar tanto la fotografía actual como la evolución histórica.
* **Múltiplos de valoración:** Ratios que comparan el precio de mercado o el valor empresa (*Enterprise Value*) frente a sus ganancias, ventas o flujos de caja (`price_to_earnings_ratio`, `enterprise_value_to_ebitda`, `enterprise_value_to_ebit`, `enterprise_value_to_revenue`, `price_to_free_cashflow`, `price_to_operating_cashflow`).
* **Rentabilidad y retorno al accionista:** Indicadores de rendimiento operativo y políticas de capital, incluyendo la variable objetivo `rate_of_return_latest` (rango de **-14,87 %** a **25,20 %**, con media de **9,82 %**), el rendimiento por recompra de acciones (`buyback_yield`) y la fórmula de rendimiento de ganancias de Greenblatt (`earning_yield_greenblatt`).
* **Crecimiento y estabilidad histórica:** Tasas de expansión interanual de ingresos y beneficios por acción (`yoy_revenue_growth`, `yoy_eps_growth`) y promedios de ganancias a 10 años (`e10`).
* **Solvencia, apalancamiento y salud financiera:** Métricas de estructura de capital y capacidad de pago de deuda (`debt_to_assets`, `debt_to_ebitda`, `equity_to_assets`, `interest_coverage`), además de puntajes compuestos de solidez financiera (`financial_strength`) y detección de manipulación contable (`mscore` de Beneish).
* **Eficiencia operativa:** Indicadores de gestión de activos, costos e inventarios (`asset_turnover`, `cogs_to_revenue`, `days_inventory`, `scaled_net_operating_assets`).

### Variables Seleccionadas

| Variable | Nombre | Significado |
| :--- | :--- | :--- |
| **Buyback Yield** | `buyback_yield_latest` | Porcentaje de recompra de acciones propias por parte de la empresa en el último periodo. |
| **Earning Yield (Greenblatt)** | `earning_yield_greenblatt_latest` | Rendimiento de las ganancias (EBIT / Enterprise Value) según la fórmula de Joel Greenblatt. |
| **Crecimiento de Ingresos YoY** | `yoy_revenue_growth_latest` | Crecimiento porcentual año a año de los ingresos o ventas netas recientes. |
| **EV / EBITDA** | `enterprise_value_to_ebitda_latest` | Múltiplo que evalúa el valor total de la empresa en relación con sus ganancias operativas antes de intereses, impuestos, depreciaciones y amortizaciones. |
| **EV / EBIT** | `enterprise_value_to_ebit_latest` | Múltiplo de valoración entre el valor total de la empresa y su beneficio operativo (EBIT). |
| **Precio / Flujo de Caja Libre** | `price_to_free_cashflow_latest` | Relación entre la cotización de la acción y el flujo de caja libre generado por acción (P/FCF). |
| **Precio / Flujo de Caja Operativo** | `price_to_operating_cashflow_latest` | Múltiplo entre el precio por acción y el flujo de caja generado por las actividades operativas. |
| **Deuda a Activos** | `debt_to_assets_latest` | Proporción de los activos totales de la empresa que está financiada mediante deuda total. |
| **E10** | `e10_latest` | Métrica de estabilidad o nivel de ganancias históricas promediadas a 10 años. |
| **Precio / Ganancias (P/E)** | `price_to_earnings_ratio_latest` | Ratio de valoración precio-beneficio (P/E), que indica cuántos dólares pagan los inversores por cada dólar de beneficio neto. |
| **Fortaleza Financiera** | `financial_strength_latest` | Score o puntaje integral que mide la salud del balance y la solvencia financiera general de la empresa. |
| **Cobertura de Intereses** | `interest_coverage_latest` | Capacidad de la empresa para pagar los intereses de su deuda acumulada a partir de sus ganancias operativas. |
| **Activos Operativos Netos Escalados** | `scaled_net_operating_assets_latest` | Proporción de activos operativos netos escalados respecto a los activos totales de la compañía. |
| **Deuda / EBITDA** | `debt_to_ebitda_latest` | Ratio de apalancamiento que mide cuántos años tardaría la empresa en pagar su deuda manteniendo su EBITDA actual. |
| **Rotación de Activos** | `asset_turnover_latest` | Eficiencia de la empresa en la utilización de sus activos para generar ventas de forma efectiva. |
| **Costo de Ventas a Ingresos** | `cogs_to_revenue_latest` | Porcentaje de las ventas que se destina directamente al costo de los bienes o servicios vendidos (COGS). |
| **M-Score (Beneish)** | `mscore_latest` | Modelo matemático de Beneish utilizado para detectar la probabilidad de manipulación en los estados financieros. |
| **Días de Inventario** | `days_inventory_latest` | Promedio de días que le toma a la empresa convertir su inventario en ventas reales. |
| **Patrimonio a Activos** | `equity_to_assets_latest` | Porcentaje del activo total de la compañía que pertenece a los accionistas (nivel de capital propio). |
| **EV / Ingresos** | `enterprise_value_to_revenue_latest` | Múltiplo de valoración que relaciona el valor total de la compañía (Enterprise Value) con sus ingresos o ventas netas totales. |

# Enlaces
Codigo: https://colab.research.google.com/drive/1k9hgYnrdWORM7-_G2bz1hNW_W-pH6kaT?usp=sharing
#
Video: https://youtu.be/ZYt6BgA_uiw
 

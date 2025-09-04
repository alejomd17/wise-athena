# Solución Prueba Técnica Data Scientist para Wise Athena

**Fecha**: 2025-09  
**Candidato**: Alejandro Moscoso Deossa  
**WhatsApp**: [+57 3122396942](http://wa.me/573122396942)  
**E-mail**: alejo-mdm@hotmail.com  
**Portafolio**: www.aleossa.com  
**Linkedin**: www.linkedin.com/in/alejomd17  
**Github**: www.github.com/alejomd17  

Este repositorio contiene mi solución a la Prueba Técnica Data Scientist pa Wise Athena.  
La solución aborda los dos problemas presentados en el desafío.

## Estructura del repositorio
```
wise-athena/
│
├── code/
│ ├── 01_exhibition_analysis.ipynb        # Análisis de efectividad de métodos de exhibición
│ └── 02_elasticity_forecasting.ipynb     # Cálculo de elasticidad precio y forecasting
│
├── presentation/
│ └── Data Scientist - Wise Athena.pdf    # 2 slides ejecutivos para el cliente
│
├── README.md                             # Instrucciones de Wise Athena
├── SOLUTION.md                           # Este archivo, detalle de la solución
└── requirements.txt                      # Librerías y dependencias
│
└── data/                                 # No se subieron datos por tamaño, confidencialidad y acuerdo de no divulgación
```

## Instrucciones de Ejecución
0. Crear ambiente virtual (opcional)  
1. Instalar dependencias: pip install -r requirements.txt  
2. Colocar los archivos de datos en la carpeta ./data:
  * sales_transactions.csv
  * store_exhibitions.csv  
  * store_metadata.csv  
3. Ejecutar los notebooks:
  * 01_exhibition_analysis.ipynb  
  * 02_elasticity_forecasting.ipynb  

## Resumen Ejecutivo
Este proyecto analizó datos de ventas y exhibiciones para una empresa CPG (Consumer Packaged Goods) con dos objetivos principales:  
* Evaluar la efectividad de tres métodos de exhibición en tiendas  
* Calcular la elasticidad precio y realizar forecasting para los productos más relevantes

## Solución
### 1. Análisis de Exhibiciones ([01_exhibition_analysis.ipynb](./code/01_exhibition_analysis.ipynb))
#### Preprocesamiento:
* Agregación de ventas a nivel semanal (Year-Week-Store-SKU)
* Eliminación de sku con más de un métodos
* Cálculo de precio ponderado por unidades vendidas
* Limpieza de duplicados en los datos de exhibición
* Merge de tablas de ventas y exhibiciones

#### Modelamiento Estadístico:
* Regresión OLS con variables: Price + Method_1 + Method_2 + Method_3
* Transformación logarítmica para interpretación en porcentajes
* Comparación de múltiples modelos de machine learning:
  * Decision Tree  
  + Random Forest  
  * XGBoost  
  * LightGBM  

#### Hallazgos Principales:
* Todos los métodos son estadísticamente significatos.  
* Por cobertura, el método 1 es el que más posee. Sin embargo, el de mayor importancia es el método 3.
* El Price, sigue siendo la variable más importante

| Variable | Promedio con método | Promedio Sin método | Variación | Coef | Coef % | p-value | E.S. | Importancia |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| Price | | | | -0.0856 | -0.04% | 0 | Si | 89.6% | 
| Method_1 | 152.49 | 118.57 | +28.61% | 28.4 | 21.1% | 0 | Si | 0.02% |
| Method_2 | 152.53 | 117.84 | +29.44% | 30.2 | 23.1% | 0 | Si | 0.8% |
| Method_3 | 163.35 | 98.97 | +65.06% | 68.41 | 54.3% | 0 | Si | 9.54% |

### 2. Elasticidad Precio y Forecasting ([02_elasticity_forecasting.ipynb](./code/02_elasticity_forecasting.ipynb))
#### Preprocesamiento:
* Agregación de ventas a nivel mensual (Year_Month-SKU)
* Cálculo de precio ponderado por unidades vendidas
#### Selección de Productos:
* Identificación de los 2 SKUs más relevantes por volumen de ventas
* Análisis individual para cada producto
#### Cálculo de Elasticidad:
* Modelo log-log: log(Units_Sold) ~ log(Price)
* Elasticidades significativas para ambos productos

| Sku | Elasticidad | Interpretación | p-value | E.S. | 
| --- | --- | --- | --- | --- | 
| 726 | -2.24 | 1% ↑ Price → -2.24% ↓ Units Sold | 0 | Si | 
| 850 | -2.08 | 1% ↑ Price → -2.08% ↓ Units Sold| 0.0007 | Si |

#### Forecasting (6 meses):
* Tres modelos comparados: Random Forest, XGBoost, Prophet
* Métricas de evaluación: RMSE, MAPE, R²
* Mejor modelo seleccionado por puntuación agregada (2 de 3 mejores métricas)

### Presentación para Cliente ([Data Scientist - Wise Athena.pdf](./presentation/Data%20Scientist%20-%20Wise%20Athena.pdf))
#### Slide 1: Efectividad de Exhibiciones
* Priorizar Method_3 en tiendas, ya que jalona considerablemente las ventas.
### Slide 2: Elasticidad y Forecasting
* Ambos elasticidad mayor a 2 (ignorando el signo negativo), indica que los consumidores son muy sensibles a los cambios en el precio de un bien o servicio.
* En concreto, un aumento o disminución del 1% en el precio generará un cambio en la cantidad demandada que será más del doble de ese porcentaje.
* Tendencias históricas similares en los productos, misma tendencia. Pronósticar con otros modelos.
* Sku 726 tiene pronóstico bajista, priorizar métodos para aumentar ventas. Sku 850 está alcista y acorde con la tendencia histórica.
* Monitorización continua recomendada para ajustar modelos
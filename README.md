# Optimización MILP de Comunidad Energética Local

Este repositorio contiene un modelo de optimización matemática basado en Programación Lineal Entera Mixta (MILP) desarrollado en Python para el dimensionamiento y gestión operativa de una comunidad energética de 7 consumidores (industriales y residenciales).
El código principal del modelo y la ejecución del solver se encuentran en el archivo Modelo_Optimizacion_MILP.ipynb

## Resumen del Proyecto
* Herramientas: Python, Pyomo, Solver HiGHS.
* Escenarios: Comparativa climática entre Esparragosa de Lares (España) y Helsinki (Finlandia).
* Hardware: Fotovoltaica (Techo y Suelo) y Almacenamiento Energético (BESS).

## Dimensionamiento Óptimo de la Instalación
El modelo dimensiona el sistema minimizando el coste total anualizado (CAPEX + OPEX). Se han utilizado variables binarias para discriminar entre instalación en tejados (límite físico) e instalación en suelo.

| Componente | Esparragosa de Lares (ES) | Helsinki (FI) |
| :--- | :--- | :--- |
| Fotovoltaica en Tejado | 9.000 Paneles (4.500 kWp) | 9.000 Paneles (4.500 kWp) |
| Fotovoltaica en Suelo | 3.333 Paneles (1.666,5 kWp) | 0 Paneles |
| Módulos de Batería (BESS) | 2.529 Módulos (12.645 kWh) | 800 Módulos (4.000 kWh)* |
| Ahorro Neto Común | 7,5% | 3,0% |

### El Coste de la Resiliencia en Helsinki
En el escenario de Finlandia, el solver óptimo sin restricciones sugería 0 baterías con un ahorro del 3,2%. Sin embargo, se impuso un mínimo de 800 módulos de batería para garantizar la resiliencia del Hospital (C2). 
* Resultado: El ahorro neto desciende al 3,0%. Esta diferencia del 0,2% se define como la "prima de seguro" que la comunidad asume para garantizar la seguridad energética de sus consumidores críticos, permitiendo además que el resto de miembros aproveche la infraestructura para arbitraje de precios.

## Optimización vs. Factor Social: Análisis de Criterios
Uno de los mayores hallazgos es que la optimización matemática pura (Criterios 1, 2, 3 y 5) no es socialmente viable en una comunidad real:
* Criterios 1-3: Generan grandes desigualdades; los consumidores pequeños suelen salir perjudicados mientras los grandes maximizan su ahorro.
* Criterio 5 (Flexible): Aunque permite un ajuste del +/- 5% en la inversión, el solver tiende a cargar más cuota de inversión a los pequeños para cuadrar el beneficio global del sistema.
* Criterio 4 (Social-Estático): Modelo seleccionado. Al fijar una inversión proporcional al consumo base, garantiza que todos ahorren exactamente el mismo porcentaje. Es la única vía que asegura la cohesión y aceptación social del proyecto.

## Análisis de Operación y Resultados

### Escenario: Esparragosa de Lares (España)
#### Operación Semanal (Verano e Invierno)
![Operación Verano](Analisis_Esparragosa_de_Lares_Verano.png)
![Operación Invierno](Analisis_Esparragosa_de_Lares_Invierno.png)
#### Impacto Económico Anualizado
![Impacto Económico Anual](Impacto_Economico_Anual_Esparragosa_de_Lares.png)

### Escenario: Helsinki (Finlandia)
#### Operación Semanal (Verano e Invierno)
![Operación Verano](Analisis_Helsinki_Verano.png)
![Operación Invierno](Analisis_Helsinki_Invierno.png)
#### Impacto Económico Anualizado
![Impacto Económico Anual](Impacto_Economico_Anual_Helsinki.png)

---
Contacto: jreyesmavs@gmail.com | [LinkedIn](https://www.linkedin.com/in/jorgereyesgon)

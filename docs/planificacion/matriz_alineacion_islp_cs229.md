# Matriz de alineación con ISLP y CS 229

## Criterios

La correspondencia se clasifica como **Alta**, **Parcial**, **Baja** o **Sin
correspondencia directa**. El nivel se clasifica como **Fundamental**,
**Intermedio**, **Avanzado**, **Complementario** o **Fuera del alcance actual**.

Para ISLP se usa la secuencia de *An Introduction to Statistical Learning, with
Applications in Python* (2023): capítulos 2 a 13. Para CS 229 se usan los bloques
publicados por Afshine y Shervine Amidi: *Supervised Learning*, *Unsupervised
Learning*, *Deep Learning*, *Tips and Tricks* y los repasos de probabilidad,
estadística, álgebra lineal y cálculo.

## Matriz

| Notebook | Tema actual | Sección propuesta | Referencia ISLP | Referencia CS 229 | Cobertura actual | Contenido ISLP faltante | Contenido CS 229 faltante | Contenido propio | Nivel | Acción editorial |
|---|---|---|---|---|---|---|---|---|---|---|
| `IntroduccionPython.ipynb` | Python y NumPy básicos | 1. Fundamentos computacionales | Laboratorios Python, apoyo transversal (**Baja**) | Prerrequisitos computacionales, sin bloque propio (**Baja**) | Tipos, estructuras, imports, arrays y ejercicio | Flujo de trabajo de los laboratorios, funciones, reproducibilidad | Convenciones de vectores/matrices y preparación para algoritmos | Introducción breve en español | Fundamental | Conservar; Ampliar; Reordenar internamente |
| `Pandas.ipynb` | Manipulación tabular | 1. Fundamentos computacionales | Laboratorios de todos los capítulos (**Parcial**) | Preparación de datos, apoyo transversal (**Baja**) | Series, selección, grupos, *reshape*, uniones y ejercicios | Patrones de preparación usados por los laboratorios ISLP | Separación limpia entre transformación y estimación | VAB cantonal ecuatoriano; cobertura extensa de pandas | Fundamental | Conservar; Reducir; Reordenar internamente; Sustituir ejemplos |
| `Visualizacion.ipynb` | Matplotlib, pandas y seaborn | 1. Fundamentos computacionales | Gráficos de laboratorios (**Parcial**) | Diagnóstico y visualización, apoyo transversal (**Baja**) | Galería amplia de gráficos y personalización | Principios de comunicación, gráficos de diagnóstico | Visualización de fronteras, errores y curvas de aprendizaje | Manual gráfico extenso | Fundamental | Conservar; Reducir; Reordenar internamente; Mover de sección |
| `Descriptiva.ipynb` | Descriptiva y distribuciones | 2. Fundamentos matemáticos y estadísticos | Prerrequisitos de caps. 2–5 y 13 (**Parcial**) | Repaso de probabilidad y estadística (**Parcial**) | Tendencia central, dispersión, variables aleatorias, CDF/PDF/cuantiles | Covarianza, esperanza condicional, muestreo, CLT, estimación | Bayes, independencia, MLE/MAP, notación consistente | Media/mediana como optimización | Fundamental | Conservar; Ampliar; Reordenar internamente |
| `PruebasHipotesis.ipynb` | t, Wilcoxon, KS y correlación | 2. Fundamentos matemáticos y estadísticos; 16 avanzado para pruebas múltiples | Cap. 13 Multiple Testing y prerrequisitos (**Parcial**) | Repaso estadístico y *tips* (**Baja**) | Pruebas de una/dos muestras y correlación | FDR/FWER, *p*-values múltiples, intervalos y tamaño de efecto | Estimación, potencia y relación con error de generalización | Ejemplos de energía y ventas | Intermedio | Conservar; Ampliar; Reordenar internamente |
| `IntroML.ipynb` | Aprendizaje estadístico, sesgo-varianza y remuestreo | 3. Fundamentos de ML | Cap. 2 Statistical Learning; cap. 5 Resampling (**Alta**) | Introducción, loss/cost y *tips* (**Parcial**) | Predicción/inferencia, error reducible, sesgo-varianza, bootstrap y CV | Flexibilidad, Bayes error, regresión frente a clasificación con más ejemplos | Riesgo empírico, pérdidas, likelihood, notación $h_\theta$ | Explicación detallada en español | Fundamental | Conservar; Ampliar; Mover parte de CV; Reordenar internamente |
| `Evaluacion.ipynb` | Métricas, ROC, CV y grid search | 5. Evaluación, validación y buenas prácticas | Cap. 5 y métricas de caps. 3–4 (**Parcial**) | *Tips and Tricks* (**Alta**) | Baselines, confusión, accuracy, precision, recall, ROC/AUC, CV, grid | Bootstrap/CV más rigurosos, métricas de regresión, error estándar | F1, especificidad, PR, calibración, error analysis, ablación | Problema binario desbalanceado con dígitos | Fundamental | Conservar; Ampliar; Revisar código; Reordenar internamente |
| `Regresion.ipynb` | Regresión lineal y múltiple econométrica | 6. Aprendizaje supervisado: regresión | Cap. 3 Linear Regression (**Alta**) | Supervised: linear regression (**Parcial**) | OLS manual, $R^2$, transformaciones, predicción y múltiples casos | Cualitativas, interacciones, diagnóstico integral, intervalos y no linealidad | Likelihood gaussiana, normal equations matriciales, LMS/gradiente, LWR | PPA, sueño, vivienda, CEO y educación | Fundamental | Conservar; Reordenar internamente; Ampliar; Sustituir ejemplos |
| `StepRegularization.ipynb` | Selección, ridge y lasso | 6. Regresión; después de evaluación | Cap. 6 Linear Model Selection and Regularization (**Alta**) | *Tips*: regularization; supervised linear models (**Parcial**) | Forward/backward, geometría L1/L2, ridge/lasso y grid search | Best subset real, $C_p$/AIC/BIC/adj. $R^2$, PCR/PLS, regla 1-SE | Elastic net, formulación de pérdida y optimización | Datos de empresas ecuatorianas | Intermedio | Conservar; Ampliar; Revisar código; Reordenar internamente |
| `ProbModels.ipynb` | Modelo lineal de probabilidad, logit y probit | 7. Aprendizaje supervisado: clasificación | Cap. 4 Classification (**Parcial**) | Supervised: logistic regression y modelos discriminativos (**Parcial**) | Logit/probit, inferencia, pipeline, ROC, umbral y tabla de ganancias | LDA, QDA, Naive Bayes, KNN, multicategoría y comparación común | Softmax, likelihood/gradiente, GDA, Naive Bayes, generativo vs. discriminativo | Caso UAFE y tabla de ganancias | Intermedio | Conservar; Dividir; Ampliar; Revisar código; Mover de sección |
| `AprendizajeSupervisado.ipynb` | KNN, lineales, regularización y árboles | 7. Clasificación (solo KNN); distribuir el resto | Caps. 3, 4, 6 y 8 (**Parcial**) | Supervised: KNN, linear models, trees (**Parcial**) | Encuesta práctica de cuatro familias | Marco comparativo y profundidad de cada capítulo | Pérdidas, likelihood, optimización y teoría | Dataset de frutas; fronteras y utilidades didácticas | Fundamental | Dividir; Reducir; Fusionar; Mover de sección; Renombrar |
| `Arboles.ipynb` | Árbol de clasificación y poda | 8. Árboles y métodos de ensamble | Cap. 8 Tree-Based Methods (**Parcial**) | Supervised: trees and ensemble methods (**Parcial**) | CART aplicado, preprocesamiento, interpretación y poda | Árboles de regresión, bagging, random forest, boosting y BART | Random forest, AdaBoost, gradient boosting y objetivos | Caso de riesgo de crédito | Intermedio | Conservar; Ampliar; Revisar código; Reordenar internamente |
| `SVM.ipynb` | SVM lineal, RBF, $C$ y $\gamma$ | 9. Métodos de margen y kernels | Cap. 9 Support Vector Machines (**Parcial**) | Supervised: SVM (**Parcial**) | Fronteras visuales y sensibilidad de hiperparámetros | Maximal margin, soft margin, support vectors, kernels y multicategoría | Hinge loss, primal/dual, Lagrangiano y kernel trick | Visualizaciones comparativas | Intermedio | Conservar; Ampliar; Revisar código; Reordenar internamente |
| `ACP.ipynb` | PCA teórico y aplicado | 10. No supervisado: reducción de dimensionalidad | Cap. 12 Unsupervised Learning (**Alta**) | Unsupervised: PCA (**Alta**) | Varianza máxima, autovectores, cargas, scree y biplot | Escalado, reconstrucción, datos faltantes y lab integrado | Teorema espectral, SVD, algoritmo/notación uniforme, ICA | Desarrollo basado en Peña y Husson | Intermedio | Conservar; Ampliar; Fusionar duplicados; Mover de sección |
| `NoSupervizado.ipynb` | K-means, k-medoides, jerárquico, DBSCAN y métricas | 11. No supervisado: clustering y mezclas | Cap. 12 Unsupervised Learning (**Alta**) | Unsupervised: clustering (**Alta**) | Amplia cobertura de clustering y evaluación interna | Clustering de variables, selección/estabilidad y lab más sistemático | EM, mezclas gaussianas, Jensen y variables latentes | K-medoides, DBSCAN, clientes y crimen | Intermedio | Conservar; Ampliar; Dividir; Revisar código; Renombrar |
| `RedesNeuronales.ipynb` | MLP introductorio | 12. Redes neuronales o puente al cap. 13 | Cap. 10 Deep Learning (**Parcial**) | Deep Learning: neural networks (**Parcial**) | Activaciones, capas, `alpha` y MLPClassifier | Pérdida, backprop, SGD, dropout, validación y lab moderno | Cross-entropy, gradientes, actualización de pesos | Fronteras 2D y cáncer de mama | Intermedio | Fusionar; Reducir; Mantener como contenido complementario |
| `AprendizajeProfundo.ipynb` | MLP, CNN, transferencia y entrenamiento | 13. Aprendizaje profundo | Cap. 10 Deep Learning (**Alta**) | Deep Learning (**Alta**) | Una/múltiples capas, CNN, augmentación, transferencia, gradiente, backprop, dropout y tuning | Secciones omitidas/renumeración, comparación más sistemática y documentación de cómputo | Batch norm, RNN/LSTM, inicialización, Adam con más detalle | Implementación propia en PyTorch y comparación tabular | Avanzado | Conservar; Reordenar internamente; Ampliar; Fusionar |
| `ReglasAso.ipynb` | Apriori y reglas de asociación | 14. Descubrimiento de patrones | Sin capítulo directo (**Sin correspondencia directa**) | Sin bloque directo (**Sin correspondencia directa**) | Soporte, confianza, lift y ejemplo sintético | No aplica; posible conexión general con no supervisado | No aplica; posible conexión con patrones latentes | Tema propio del curso | Complementario | Conservar; Ampliar; Mantener como contenido complementario |
| `DescriptivaRegresion.ipynb` | Agregado descriptiva–inferencia–regresión | No asignar; fuente temporal para fusión | Caps. 2, 3, 4 y 13 (**Parcial**) | Refresher estadístico y supervised linear models (**Parcial**) | Repite tres notebooks canónicos | Todo lo faltante en los capítulos canónicos, sin ventaja por agregación | Pérdidas, optimización, notación y validación | Algunos ejemplos aplicados adicionales | Complementario | Dividir; Fusionar; Reducir; Mantener como contenido complementario |
| `ProbACP.ipynb` | Agregado logit/probit–PCA | No asignar; fuente temporal para fusión | Caps. 4 y 12 (**Parcial**) | Supervised logistic + Unsupervised PCA (**Parcial**) | Duplica `ProbModels` y `ACP` | Mismos vacíos de ambos capítulos | Mismos vacíos de ambos bloques | Ninguno claramente exclusivo tras comparación inicial | Complementario | Dividir; Fusionar; Reducir; Mantener como contenido complementario |

## Temas comunes a ISLP y CS 229

La intersección debe formar el núcleo del curso:

- formulación de aprendizaje supervisado y distinción regresión/clasificación;
- regresión lineal y logística;
- sesgo-varianza, regularización y validación cruzada;
- KNN, árboles y ensambles;
- SVM y kernels;
- redes neuronales y aprendizaje profundo;
- PCA, k-means y clustering jerárquico;
- métricas de clasificación y buenas prácticas de evaluación.

El repositorio ya ofrece ejemplos de casi todos estos temas, pero la profundidad es
desigual. Regresión lineal, PCA, clustering y aprendizaje profundo son los bloques más
maduros. SVM, árboles/ensambles, clasificación comparada y evaluación rigurosa requieren
la mayor ampliación dentro del núcleo ya iniciado.

## Temas presentes principalmente en ISLP

- secuencia explícita entre inferencia y predicción;
- regresión lineal con diagnóstico y variables cualitativas;
- clasificación comparada con LDA, QDA, Naive Bayes y KNN;
- remuestreo con bootstrap y validación cruzada;
- selección de modelos, PCR y PLS;
- modelos no lineales: polinomios, *splines*, regresión local y GAM;
- tratamiento completo de árboles, bagging, random forests, boosting y BART;
- análisis de supervivencia;
- pruebas múltiples;
- laboratorios Python comparables entre familias.

Los vacíos de mayor prioridad para un curso principal son clasificación comparada,
ensambles y “más allá de la linealidad”. Supervivencia y pruebas múltiples pueden quedar
como avanzados; pruebas múltiples encaja mejor por existir ya un capítulo de hipótesis.

## Temas presentes principalmente en CS 229

- notación uniforme $h_\theta$, pérdidas y funciones de costo;
- likelihood, MLE/MAP y formulaciones generativas/discriminativas;
- descenso por gradiente, LMS y optimización;
- Lagrangianos, formulación primal/dual y *hinge loss* para SVM;
- GDA y Naive Bayes desde modelos generativos;
- teoría de aprendizaje (riesgo empírico, cotas, PAC/VC);
- EM, mezclas gaussianas, variables latentes e ICA;
- *batch normalization*, RNN/LSTM;
- MDP, ecuación de Bellman, iteración de valor/política y Q-learning.

Para el curso principal se recomiendan pérdidas, gradientes, likelihood,
generativo/discriminativo, formulación de SVM y EM/mezclas. Teoría PAC/VC, ICA, RNN y
aprendizaje por refuerzo deben marcarse como avanzados o futuros, salvo que aumente la
carga horaria.

## Temas propios del repositorio

- datos empresariales de la Superintendencia de Compañías del Ecuador;
- caso UAFE de clasificación y tablas de ganancias;
- VAB no petrolero cantonal;
- ejemplos econométricos de PPA, sueño, vivienda, salarios y educación;
- k-medoides y DBSCAN;
- reglas de asociación;
- capítulos extensos de pandas y visualización;
- utilidades visuales para fronteras de decisión.

Estos contenidos dan identidad aplicada al libro. Deben conservarse cuando tengan
procedencia documentada, licencia/permiso claro, una versión local o estable del dataset
y un flujo de validación correcto.

## Vacíos matemáticos

1. Un bloque común de álgebra lineal: vectores, matrices, norma, proyección,
   autovalores, SVD y matrices semidefinidas positivas.
2. Cálculo y optimización: gradiente, Hessiano, convexidad, descenso de gradiente,
   condiciones de primer orden y multiplicadores de Lagrange.
3. Probabilidad estadística: condicional, Bayes, esperanza condicional, MLE/MAP y
   familias exponenciales.
4. Funciones de pérdida y riesgo empírico como hilo conductor entre modelos.
5. Formulación matemática de regresión logística, SVM, árboles y redes.
6. Variables latentes y EM para mezclas.
7. Una notación editorial estable para muestra, observación, característica, parámetro,
   estimador, predicción y pérdida.

## Vacíos aplicados

1. Pipelines completos que encapsulen imputación, codificación, escala, selección y
   modelo dentro de cada fold.
2. Validación anidada o separación entrenamiento–validación–prueba.
3. Métricas de regresión, calibración, PR-AUC, costos y selección de umbral.
4. Comparaciones de varias familias sobre un mismo dataset y particiones idénticas.
5. Diagnóstico de regresión y análisis sistemático de errores.
6. Datos agrupados/temporales y particiones que respeten su estructura.
7. Reproducibilidad sin red, procedencia/licencia de datos y semillas.
8. Ejercicios con soluciones o criterios de evaluación en la mayoría de capítulos.

## Solapamientos

- `DescriptivaRegresion.ipynb` es una combinación histórica de
  `Descriptiva.ipynb`, `PruebasHipotesis.ipynb` y `Regresion.ipynb`.
- `ProbACP.ipynb` combina y duplica `ProbModels.ipynb` y `ACP.ipynb`.
- `AprendizajeSupervisado.ipynb` duplica regresión, regularización y árboles; KNN es su
  bloque diferenciador.
- `RedesNeuronales.ipynb` es una versión corta y menos rigurosa de contenidos ya
  desarrollados en `AprendizajeProfundo.ipynb`.
- `IntroML.ipynb` y `Evaluacion.ipynb` comparten bootstrap/CV y búsqueda de
  hiperparámetros.

## Capítulos que podrían dividirse

- `AprendizajeSupervisado.ipynb`: extraer KNN y distribuir los otros tres bloques.
- `NoSupervizado.ipynb`: separar fundamentos de clustering de mezclas/evaluación o
  mantener subunidades muy claras.
- `ProbModels.ipynb`: separar inferencia logit/probit del flujo predictivo UAFE.
- `Visualizacion.ipynb`: núcleo obligatorio breve más galería complementaria.
- `Pandas.ipynb`: fundamentos obligatorios más operaciones avanzadas.
- `DescriptivaRegresion.ipynb` y `ProbACP.ipynb`: dividir solo para rescatar contenido,
  no para crear nuevos capítulos.

## Capítulos que podrían fusionarse

- `RedesNeuronales.ipynb` con la introducción de `AprendizajeProfundo.ipynb`.
- El bloque PCA de `ProbACP.ipynb` con `ACP.ipynb`.
- El bloque de modelos binarios de `ProbACP.ipynb` con `ProbModels.ipynb`.
- Las celdas únicas de `DescriptivaRegresion.ipynb` con sus tres capítulos canónicos.
- El bloque operativo de CV de `IntroML.ipynb` con `Evaluacion.ipynb`, dejando en
  `IntroML.ipynb` la intuición y el sesgo-varianza.

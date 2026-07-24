# Mapa curricular objetivo

## Principios de diseño

Este mapa es una hipótesis editorial para discusión. No implica crear de inmediato todos
los capítulos ni cambiar el TOC. La secuencia principal sigue ISLP cuando coinciden los
temas; CS 229 profundiza notación, pérdidas, optimización y formulación algorítmica. Los
contenidos propios se mantienen cuando añaden contexto aplicado y cumplen criterios de
reproducibilidad.

Cada unidad debe distinguir:

- **intuición:** qué problema resuelve y cuándo es útil;
- **formulación:** datos, supuestos, notación, pérdida/objetivo y algoritmo;
- **práctica:** pipeline reproducible en Python;
- **evaluación:** métrica, partición y línea base;
- **lectura del resultado:** inferencia, predicción, límites y errores;
- **nivel:** fundamental, intermedio, avanzado o complementario.

## Partes propuestas

| Orden | Parte/área | Notebooks actuales candidatos | Notebook futuro posible | Nivel | Prerrequisitos | Referencia principal | Referencia complementaria | Carácter |
|---:|---|---|---|---|---|---|---|---|
| 1 | Fundamentos computacionales | `IntroduccionPython.ipynb`, `Pandas.ipynb`, `Visualizacion.ipynb` | `ReproducibilidadPython.ipynb` (rutas, entornos, semillas, pipelines) | Fundamental | Ninguno | Laboratorios ISLP | Convenciones computacionales CS 229 | Obligatorio |
| 2 | Fundamentos matemáticos y estadísticos | `Descriptiva.ipynb`, `PruebasHipotesis.ipynb` | `AlgebraLinealCalculoML.ipynb`; `ProbabilidadInferenciaML.ipynb` | Fundamental | Python/NumPy | Prerrequisitos ISLP caps. 2–5 | Refreshers CS 229 de probabilidad, estadística, álgebra y cálculo | Obligatorio |
| 3 | Fundamentos de Machine Learning | `IntroML.ipynb` | Integrar en el actual antes de crear otro | Fundamental | Partes 1–2 | ISLP cap. 2 | CS 229 Supervised: notación, loss/cost | Obligatorio |
| 4 | Optimización para Machine Learning | Bloques de `AprendizajeProfundo.ipynb` y `StepRegularization.ipynb` | `OptimizacionML.ipynb` | Intermedio | Álgebra, cálculo, fundamentos ML | Apoyo a ISLP caps. 6, 9 y 10 | CS 229: gradient descent, convexidad, Lagrangianos | Obligatorio en versión corta; ampliación opcional |
| 5 | Evaluación, validación y buenas prácticas | `Evaluacion.ipynb`; intuición de `IntroML.ipynb` | Ampliar el actual; quizá `ValidacionAvanzada.ipynb` | Fundamental | Fundamentos ML, probabilidad | ISLP cap. 5 | CS 229 Tips and Tricks | Obligatorio |
| 6 | Aprendizaje supervisado: regresión | `Regresion.ipynb`, parte lineal de `AprendizajeSupervisado.ipynb`, `StepRegularization.ipynb` | `ModelosNoLineales.ipynb` | Fundamental–intermedio | Partes 1–5 | ISLP caps. 3, 6 y 7 | CS 229 linear models, losses, gradient descent | Obligatorio |
| 7 | Aprendizaje supervisado: clasificación | `ProbModels.ipynb`; KNN de `AprendizajeSupervisado.ipynb` | `ClasificacionComparada.ipynb` | Fundamental–intermedio | Partes 1–6 | ISLP cap. 4 | CS 229 logistic, softmax, GDA, Naive Bayes | Obligatorio |
| 8 | Árboles y métodos de ensamble | `Arboles.ipynb`; bloque de `AprendizajeSupervisado.ipynb` | `Ensambles.ipynb` o ampliar `Arboles.ipynb` | Intermedio | Evaluación y clasificación/regresión | ISLP cap. 8 | CS 229 tree and ensemble methods | Obligatorio |
| 9 | Métodos de margen y kernels | `SVM.ipynb` | Ampliar el actual | Intermedio | Álgebra, optimización, clasificación | ISLP cap. 9 | CS 229 SVM, hinge loss, dualidad y kernels | Obligatorio o electivo según horas |
| 10 | No supervisado: reducción de dimensionalidad | `ACP.ipynb`; bloque duplicado de `ProbACP.ipynb` | `ReduccionDimensionalAvanzada.ipynb` solo si se aprueba | Intermedio | Álgebra lineal, descriptiva, escala | ISLP cap. 12 | CS 229 PCA e ICA | Obligatorio para PCA; ICA futura |
| 11 | No supervisado: clustering y mezclas | `NoSupervizado.ipynb` | `MezclasGaussianasEM.ipynb` | Intermedio–avanzado | Distancias, probabilidad, optimización, PCA | ISLP cap. 12 | CS 229 clustering, latent variables y EM | Clustering obligatorio; mezclas opcionales |
| 12 | Redes neuronales | `RedesNeuronales.ipynb`; primera parte de `AprendizajeProfundo.ipynb` | Preferible fusionar antes que crear | Intermedio | Modelos lineales, pérdidas, gradientes | ISLP cap. 10, secciones iniciales | CS 229 Neural Networks | Obligatorio como puente |
| 13 | Aprendizaje profundo | `AprendizajeProfundo.ipynb` | `ModelosSecuenciales.ipynb` solo a futuro | Avanzado | Redes, optimización, evaluación | ISLP cap. 10 | CS 229 Deep Learning | Núcleo avanzado o electivo |
| 14 | Descubrimiento de patrones | `ReglasAso.ipynb` | `PatronesSecuenciales.ipynb` solo si responde al programa | Complementario | Probabilidad, pandas, no supervisado | Contenido propio | Sin correspondencia directa en las hojas CS 229 | Opcional |
| 15 | Aprendizaje por refuerzo | Ninguno | `AprendizajeRefuerzo.ipynb` | Avanzado | Probabilidad, optimización, programación dinámica, redes | Sin capítulo directo en ISLP | CS 229: MDP, Bellman, value/policy iteration, Q-learning | Futuro |
| 16 | Temas avanzados y extensiones | Elementos aislados en varios notebooks | `Supervivencia.ipynb`, `PruebasMultiples.ipynb`, `TeoriaAprendizaje.ipynb`, `InterpretabilidadEtica.ipynb` | Avanzado/complementario | Núcleo completo | ISLP caps. 11 y 13 | CS 229 learning theory y tips | Futuro/electivo |

Los nombres de notebooks futuros son provisionales y describen funciones curriculares,
no una autorización para crearlos.

## Secuencia recomendada del curso principal

### Tramo A. Herramientas y lenguaje

1. `IntroduccionPython.ipynb`
2. `Pandas.ipynb`
3. Núcleo reducido de `Visualizacion.ipynb`
4. `Descriptiva.ipynb`
5. Fundamentos nuevos de probabilidad/álgebra/cálculo, integrados o en uno/dos notebooks
6. `PruebasHipotesis.ipynb` en versión enfocada

Resultado esperado: el estudiante puede representar datos, describir incertidumbre,
leer notación y seguir una derivación sencilla.

### Tramo B. Aprendizaje y evaluación

7. `IntroML.ipynb`
8. `Evaluacion.ipynb`
9. Optimización básica integrada: pérdida, gradiente, escala y regularización

Resultado esperado: el estudiante distingue inferencia/predicción, entrenamiento/
validación/prueba, parámetro/hiperparámetro y selección/evaluación.

### Tramo C. Aprendizaje supervisado

10. `Regresion.ipynb`
11. `StepRegularization.ipynb`
12. Futuro bloque de modelos no lineales
13. KNN extraído de `AprendizajeSupervisado.ipynb`
14. `ProbModels.ipynb` reestructurado como clasificación
15. `Arboles.ipynb`, seguido de ensambles
16. `SVM.ipynb`

Resultado esperado: el estudiante formula pérdidas, ajusta pipelines sin fuga, compara
familias bajo el mismo protocolo y comunica límites.

### Tramo D. Aprendizaje no supervisado

17. `ACP.ipynb`
18. `NoSupervizado.ipynb`
19. Mezclas gaussianas/EM si la duración lo permite

Resultado esperado: el estudiante comprende proyección, distancias, objetivos de
clustering, selección de hiperparámetros y limitaciones de evaluación sin etiquetas.

### Tramo E. Redes y extensiones

20. Introducción consolidada de redes neuronales
21. `AprendizajeProfundo.ipynb`
22. `ReglasAso.ipynb` como módulo opcional
23. Temas futuros/electivos

Resultado esperado: el estudiante conecta redes con modelos anteriores, entiende
retropropagación y regularización, y decide cuándo la complejidad adicional es
justificable.

## Dependencias curriculares

| Unidad | Debe dominar antes | Habilita después |
|---|---|---|
| Python/NumPy | — | pandas, visualización, matemática computacional |
| pandas/visualización | Python | todos los laboratorios |
| probabilidad/estadística | descriptiva y álgebra básica | inferencia, evaluación, modelos probabilísticos |
| álgebra/cálculo | Python/NumPy | regresión matricial, PCA, SVM, optimización, redes |
| fundamentos ML | probabilidad y programación | evaluación y todos los modelos |
| evaluación | fundamentos ML | selección, comparación y ajuste de modelos |
| regresión lineal | evaluación y álgebra | regularización, GAM, redes |
| clasificación | regresión/logit y evaluación | árboles, SVM, redes |
| optimización | cálculo y pérdidas | regularización, SVM, redes, EM |
| PCA | álgebra y escala | visualización de alta dimensión, clustering |
| clustering | distancias, evaluación no supervisada | mezclas y patrones |
| redes | clasificación, optimización | aprendizaje profundo y RL aproximado |

## Contenidos obligatorios

### Fundamentos

- Python, NumPy, pandas y visualización suficiente para los laboratorios.
- estadística descriptiva, probabilidad condicional, esperanza, varianza y muestreo;
- vectores, matrices, producto, norma, proyección, autovalores y gradiente;
- predicción frente a inferencia;
- sesgo-varianza y error reducible/irreducible;
- pérdida, costo, riesgo empírico y generalización;
- entrenamiento, validación, prueba, CV y pipelines sin fuga.

### Modelos

- regresión lineal y logística;
- KNN;
- selección, ridge y lasso;
- árboles, random forest y boosting;
- SVM lineal y kernel;
- PCA;
- k-means y clustering jerárquico;
- red multicapa, backpropagación y regularización.

### Práctica

- baseline;
- preparación dentro de pipeline;
- métrica alineada con la pregunta;
- selección sin tocar prueba;
- análisis de errores;
- interpretación y comunicación de incertidumbre;
- reproducibilidad de datos, dependencias y semillas.

## Contenidos opcionales

- pruebas no paramétricas en profundidad;
- probit y tablas de ganancias;
- k-medoides y DBSCAN;
- BART;
- PCR/PLS;
- GAM;
- mezclas gaussianas y EM;
- CNN y transferencia de aprendizaje, si el curso no es de especialización;
- reglas de asociación.

La condición para incluir un tema opcional es no desplazar evaluación, regresión,
clasificación, ensambles o fundamentos matemáticos.

## Contenidos futuros

- análisis de supervivencia;
- pruebas múltiples con FWER/FDR;
- teoría de aprendizaje PAC/VC;
- ICA;
- RNN/LSTM y modelos de secuencia;
- aprendizaje por refuerzo;
- explicabilidad e interpretabilidad;
- equidad, privacidad y uso responsable;
- incertidumbre, calibración y conformal prediction;
- deriva, monitoreo y fundamentos de MLOps.

No se recomienda incorporar estos temas hasta estabilizar la secuencia principal y el
entorno reproducible.

## Integraciones antes de crear capítulos nuevos

Se pueden cubrir vacíos iniciales dentro de notebooks actuales:

- añadir pérdidas, riesgo y notación común a `IntroML.ipynb`;
- añadir métricas de regresión, F1/PR-AUC, calibración y validación anidada a
  `Evaluacion.ipynb`;
- añadir likelihood, forma matricial y diagnóstico a `Regresion.ipynb`;
- añadir elastic net y validación correcta a `StepRegularization.ipynb`;
- añadir LDA/QDA/Naive Bayes como sección comparativa a `ProbModels.ipynb` antes de
  decidir si merece un notebook propio;
- añadir random forest y boosting a `Arboles.ipynb`;
- añadir margen, hinge loss y kernel trick a `SVM.ipynb`;
- añadir SVD a `ACP.ipynb`;
- añadir mezclas/EM de manera breve a `NoSupervizado.ipynb`;
- fusionar la introducción útil de `RedesNeuronales.ipynb` en
  `AprendizajeProfundo.ipynb`.

Solo después de medir extensión, tiempo de ejecución y carga cognitiva debe decidirse si
estas ampliaciones se convierten en notebooks separados.

## Referencias por función

### ISLP como referencia principal de secuencia

- cap. 2: fundamentos de aprendizaje estadístico;
- cap. 3: regresión lineal;
- cap. 4: clasificación;
- cap. 5: remuestreo;
- cap. 6: selección y regularización;
- cap. 7: más allá de la linealidad;
- cap. 8: árboles y ensambles;
- cap. 9: SVM;
- cap. 10: aprendizaje profundo;
- cap. 11: supervivencia;
- cap. 12: aprendizaje no supervisado;
- cap. 13: pruebas múltiples.

### CS 229 como referencia complementaria de profundidad

- *Supervised Learning*: pérdidas, likelihood, modelos lineales, SVM, generativos,
  árboles/ensambles, KNN y teoría;
- *Unsupervised Learning*: variables latentes, EM, k-means, jerárquico, evaluación,
  PCA e ICA;
- *Deep Learning*: arquitectura, activaciones, entropía cruzada, backprop, dropout,
  CNN, normalización por lotes, RNN y RL;
- *Tips and Tricks*: métricas, selección, regularización, sesgo-varianza y análisis de
  errores;
- *Refreshers*: probabilidad, estadística, álgebra lineal y cálculo.

## Prioridad de implementación futura

### Prioridad 1: estabilizar

- corregir fugas y errores de código;
- declarar dependencias;
- elegir datasets reproducibles;
- fijar plantilla editorial y notación;
- consolidar duplicaciones;
- mover evaluación antes de modelos;
- elegir un único pipeline de despliegue.

### Prioridad 2: completar el núcleo

- fundamentos matemáticos mínimos;
- clasificación comparada;
- modelos no lineales;
- ensambles;
- SVM matemático;
- métricas y validación rigurosas;
- mezclas/EM en nivel apropiado.

### Prioridad 3: extender

- supervivencia, pruebas múltiples, teoría de aprendizaje, secuencias, RL y temas de
  práctica responsable.

Cada prioridad requiere aprobación antes de modificar TOC, renombrar archivos, fusionar
notebooks o crear capítulos.

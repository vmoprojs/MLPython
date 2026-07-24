# Inventario de notebooks

## Alcance y método

Auditoría estática realizada el 24 de julio de 2026. Se inspeccionaron los 20 archivos
`.ipynb` de la raíz: celdas Markdown y de código, títulos, fórmulas, imports, fuentes de
datos, salidas almacenadas, errores almacenados, enlaces y relaciones de contenido. No se
ejecutaron notebooks ni se modificó su contenido.

Estado inicial obligatorio:

```text
git status --short
# sin salida: árbol de trabajo limpio

git branch --show-current
reorganizacion-islp-cs229

git log -1 --oneline
55b915f deep learning
```

El TOC incluye 18 notebooks. `DescriptivaRegresion.ipynb` y `ProbACP.ipynb` están
versionados, pero no aparecen en `myst.yml`.

## Resumen cuantitativo

| Notebook | Celdas Markdown/código | Tamaño aprox. | En TOC | Nivel estimado |
|---|---:|---:|---|---|
| `ACP.ipynb` | 8/13 | 105 KB | Sí | Intermedio |
| `AprendizajeProfundo.ipynb` | 34/31 | 535 KB | Sí | Intermedio–avanzado |
| `AprendizajeSupervisado.ipynb` | 27/30 | 883 KB | Sí | Fundamental–intermedio |
| `Arboles.ipynb` | 26/32 | 632 KB | Sí | Intermedio |
| `Descriptiva.ipynb` | 23/36 | 189 KB | Sí | Fundamental |
| `DescriptivaRegresion.ipynb` | 51/97 | 2.4 MB | No | Fundamental–intermedio |
| `Evaluacion.ipynb` | 10/16 | 159 KB | Sí | Fundamental |
| `IntroML.ipynb` | 21/8 | 268 KB | Sí | Fundamental |
| `IntroduccionPython.ipynb` | 15/8 | 8 KB | Sí | Fundamental |
| `NoSupervizado.ipynb` | 31/21 | 556 KB | Sí | Intermedio |
| `Pandas.ipynb` | 67/111 | 194 KB | Sí | Fundamental |
| `ProbACP.ipynb` | 23/29 | 144 KB | No | Intermedio |
| `ProbModels.ipynb` | 22/27 | 141 KB | Sí | Intermedio |
| `PruebasHipotesis.ipynb` | 17/24 | 41 KB | Sí | Fundamental–intermedio |
| `RedesNeuronales.ipynb` | 14/6 | 641 KB | Sí | Intermedio |
| `ReglasAso.ipynb` | 5/4 | 47 KB | Sí | Complementario |
| `Regresion.ipynb` | 24/48 | 376 KB | Sí | Fundamental–intermedio |
| `SVM.ipynb` | 9/9 | 578 KB | Sí | Intermedio |
| `StepRegularization.ipynb` | 17/17 | 641 KB | Sí | Intermedio |
| `Visualizacion.ipynb` | 21/81 | 5.3 MB | Sí | Fundamental/complementario |

## `ACP.ipynb`

- **Título y propósito:** “Análisis de Componentes Principales”. Presenta PCA desde la
  maximización de varianza, desarrolla la primera componente y lo conecta con una
  implementación de `sklearn`.
- **Contenido y estructura:** planteamiento, notación matricial, valores y vectores
  propios, varianza explicada, cargas, *scree plot* y *biplot*. La estructura teórica es
  breve y termina en varias funciones auxiliares.
- **Datasets y ejemplos:** datos construidos en el notebook y una figura local
  `images/fig1.png`; no depende de descargas remotas.
- **Dependencias:** `pandas`, `numpy`, `seaborn`, `matplotlib`, `sklearn`,
  `IPython`.
- **Prerrequisitos:** estadística descriptiva, estandarización, álgebra lineal
  (producto matricial, covarianza, autovalores y autovectores).
- **Problemas:** faltan objetivos, cierre, ejercicios y un criterio explícito para
  decidir entre covarianzas y correlaciones. Conviene unificar notación y explicar SVD,
  signo no identificable de las cargas, reconstrucción y riesgo de fuga al escalar antes
  de una partición. La bibliografía de Peña y Husson está como nota al pie, no en
  `references.bib`.
- **Relaciones:** su bloque PCA está duplicado casi por completo en `ProbACP.ipynb`;
  se relaciona con la reducción de dimensión aplicada de `NoSupervizado.ipynb`.
- **Acción recomendada:** conservar, ampliar y fusionar aquí el único bloque canónico de
  PCA; mover después de fundamentos de álgebra lineal y antes del ejemplo conjunto de
  clustering.

## `AprendizajeProfundo.ipynb`

- **Título y propósito:** “Redes neuronales y aprendizaje profundo”. Es el capítulo más
  cercano a una unidad universitaria autosuficiente y explícitamente se apoya en el
  capítulo 10 de ISLP.
- **Contenido y estructura:** objetivos, requisitos, red de una capa, activaciones,
  frontera no lineal, MLP, CNN, convolución, *pooling*, aumento, transferencia,
  comparación con modelos tabulares, descenso de gradiente, retropropagación, SGD,
  regularización, *dropout*, parada temprana, ajuste, resumen, ejercicios y referencias.
- **Datasets:** `make_moons`, `load_digits` y `load_diabetes` de scikit-learn; imagen
  `astronaut` de scikit-image solo en una demostración opcional. Los pesos de ResNet-18
  solo se descargan si `EJECUTAR_IMAGENET=True`, que actualmente es `False`.
- **Dependencias:** `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `torch`,
  `torchvision`; opcionalmente `Pillow` y `scikit-image`.
- **Prerrequisitos:** particiones de datos, métricas, modelos lineales, cálculo
  diferencial, regla de la cadena, álgebra lineal y optimización.
- **Problemas:** la numeración salta de 10.3 a 10.6 y luego 10.7 por imitar ISLP sin
  explicar las secciones omitidas. No cubre normalización por lotes, RNN/LSTM,
  inicialización, inestabilidad/semillas en GPU ni análisis de errores por clase. La
  importación opcional está en la celda global, por lo que esas librerías deben existir
  incluso si la descarga está desactivada. Es costoso de ejecutar y necesita marcar
  celdas opcionales y tiempos esperados.
- **Relaciones:** solapa ampliamente `RedesNeuronales.ipynb`; usa conceptos de
  `Evaluacion.ipynb`, `StepRegularization.ipynb` e `IntroML.ipynb`.
- **Acción recomendada:** conservar como capítulo principal, reordenar internamente y
  ampliar de forma selectiva; absorber solo los ejemplos útiles de
  `RedesNeuronales.ipynb`.

## `AprendizajeSupervisado.ipynb`

- **Título y propósito:** recorrido aplicado por KNN, regresión lineal, ridge, lasso y
  árboles. Funciona como encuesta de modelos, pero mezcla regresión y clasificación sin
  una arquitectura conceptual común.
- **Contenido y estructura:** KNN con frutas; sensibilidad a $k$ y al tamaño de la
  partición; regresión lineal sintética; regularización sobre *Communities and Crime*;
  árboles con Iris y cáncer de mama.
- **Datasets:** frutas descargadas de `raw.githubusercontent.com`; el dataset local
  `Data/CommViolPredUnnormalizedData.txt` se carga indirectamente desde
  `shared_utilities.py`; `make_regression`, Iris y cáncer de mama de scikit-learn.
- **Dependencias:** `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `graphviz` y
  `shared_utilities.py`.
- **Prerrequisitos:** `pandas`, visualización, partición entrenamiento/prueba, escala y
  métricas básicas.
- **Problemas:** no formula pérdidas ni objetivos; selecciona $k$ repetidamente mirando
  el mismo conjunto de prueba; no usa estratificación ni pipeline para KNN; depende de
  red pese a existir una copia local de frutas; mezcla demasiados temas y duplica
  `Regresion.ipynb`, `StepRegularization.ipynb` y `Arboles.ipynb`. Las cuentas de
  ejecución saltan de 47 a 143, señal de ejecución parcial histórica.
- **Relaciones:** KNN no tiene otro capítulo propio y es su contenido más singular; el
  resto ya cuenta con capítulos especializados.
- **Acción recomendada:** dividir. Conservar KNN como capítulo breve de clasificación
  no paramétrica; trasladar o reducir los bloques de regresión, regularización y árboles.

## `Arboles.ipynb`

- **Título y propósito:** árboles de decisión aplicados a riesgo de crédito, con
  preparación mixta de variables, interpretación y poda por costo-complejidad.
- **Contenido y estructura:** criterio de partición, caso German Credit, exploración,
  preprocesamiento con `ColumnTransformer`, entrenamiento, visualización, métricas y poda.
- **Datasets:** `credit.csv` remoto del repositorio `DataLectures`.
- **Dependencias:** `pandas`, `numpy`, `matplotlib`, `scikit-learn`; no requiere
  `shared_utilities.py`.
- **Prerrequisitos:** clasificación, entropía/impureza, partición de datos, variables
  categóricas y métricas.
- **Problemas:** el notebook llama “validación cruzada” a una comparación directa sobre
  prueba. Calcula los `test_scores` para cada `ccp_alpha` y elige el mejor con el conjunto
  de prueba, contaminando la evaluación final. La partición manual 90/10 no estratifica.
  Falta separar validación o usar CV dentro de entrenamiento. Solo cubre un árbol: no
  incluye bagging, random forests, boosting ni BART.
- **Relaciones:** duplica el bloque introductorio de árboles de
  `AprendizajeSupervisado.ipynb`; las métricas deben remitir a `Evaluacion.ipynb`.
- **Acción recomendada:** conservar el caso de crédito, corregir la validación,
  reordenar y ampliar hacia métodos de ensamble en una unidad posterior.

## `Descriptiva.ipynb`

- **Título y propósito:** fundamentos de estadística descriptiva y distribuciones para
  preparar el lenguaje probabilístico del curso.
- **Contenido y estructura:** tendencia central, interpretaciones de media y mediana
  como problemas de optimización, dispersión, cuantiles, variables aleatorias, masa,
  densidad, distribución acumulada y función cuantil.
- **Datasets:** ejemplos sintéticos; no usa archivos externos.
- **Dependencias:** `numpy`, `scipy`, `matplotlib`, `statsmodels`.
- **Prerrequisitos:** aritmética y Python/NumPy básicos.
- **Problemas:** el título “Medidas de tendencial central” y otros errores de redacción
  requieren corrección; hay un salto de encabezado de nivel 2 a nivel 4 antes de “La
  moda”. Falta distinguir población/muestra, notación de estimadores, covarianza,
  esperanza condicional, ley de grandes números, CLT y estimación. No incluye objetivos,
  ejercicios ni referencias MyST.
- **Relaciones:** parte del contenido está duplicado en `DescriptivaRegresion.ipynb`;
  prepara `PruebasHipotesis.ipynb`, `Regresion.ipynb`, `IntroML.ipynb` y `ACP.ipynb`.
- **Acción recomendada:** conservar y ampliar como fundamento estadístico, con una
  secuencia explícita hacia probabilidad e inferencia.

## `DescriptivaRegresion.ipynb`

- **Título y propósito:** cuaderno agregado que reúne descriptiva, pruebas, correlación y
  regresión. Parece ser un antecedente monolítico de tres capítulos actuales.
- **Contenido y estructura:** 148 celdas; descriptiva, distribuciones, pruebas de una y
  dos muestras, correlación, regresión simple y múltiple, transformaciones y predicción.
- **Datasets:** locales `Data/energy.csv` y `Data/company_sales_data.csv`, más diez CSV
  remotos de `DataLectures` (consumo, alimentos, PPA, sueño, telefonía, CEO, regresión al
  origen, vivienda y GPA).
- **Dependencias:** `numpy`, `pandas`, `scipy`, `statsmodels`, `matplotlib`, `seaborn`.
- **Prerrequisitos:** Python, estadística descriptiva e inferencia elemental.
- **Problemas:** duplica extensamente celdas de `Descriptiva.ipynb`,
  `PruebasHipotesis.ipynb` y `Regresion.ipynb`; no está en el TOC; conserva
  `%matplotlib notebook`, outputs HTML interactivos voluminosos y cuentas de ejecución
  desordenadas. Tiene 2.4 MB y muchas salidas históricas. La amplitud impide objetivos y
  cierres claros.
- **Relaciones:** es el solapamiento estructural más grande del repositorio.
- **Acción recomendada:** no convertirlo en capítulo. Comparar celda a celda y fusionar
  únicamente mejoras o ejemplos ausentes en los tres notebooks canónicos; mantenerlo
  temporalmente como material complementario hasta aprobar su retiro.

## `Evaluacion.ipynb`

- **Título y propósito:** evaluación de clasificación y selección de modelos con un
  problema binario desbalanceado derivado de `load_digits`.
- **Contenido y estructura:** *dummy classifiers*, matriz de confusión, exactitud,
  precisión, sensibilidad, reporte, ROC/AUC, validación cruzada y `GridSearchCV`.
- **Datasets:** `load_digits` de scikit-learn.
- **Dependencias:** `numpy`, `pandas`, `seaborn`, `matplotlib`, `scikit-learn` y
  `shared_utilities.py`.
- **Prerrequisitos:** clasificación, partición entrenamiento/prueba y probabilidad
  elemental.
- **Problemas:** guarda un `ImportError` porque `sklearn.metrics.SCORERS` ya no es API
  pública; debe usarse `sklearn.metrics.get_scorer_names()`. Una celda final no fue
  ejecutada. Faltan F1, especificidad, PR-AUC, calibración, umbrales/costos, métricas de
  regresión, validación anidada, series temporales/grupos, incertidumbre y prevención
  explícita de fuga. Hay repetición de particiones y ajustes sin pipeline.
- **Relaciones:** `IntroML.ipynb` ya introduce bootstrap y CV; `ProbModels.ipynb`,
  `Arboles.ipynb`, `SVM.ipynb` y `AprendizajeProfundo.ipynb` deberían remitir aquí.
- **Acción recomendada:** conservar y ampliar; convertirlo en una unidad central de
  evaluación y buenas prácticas, y dejar en `IntroML.ipynb` solo la intuición.

## `IntroML.ipynb`

- **Título y propósito:** introducción conceptual al aprendizaje estadístico, predicción
  frente a inferencia, error reducible/irreducible, sesgo-varianza y remuestreo.
- **Contenido y estructura:** IA/ML, terminología, aprendizaje supervisado, estimación de
  $f$, descomposición del error, bootstrap, validación cruzada, parámetros,
  hiperparámetros y ejercicios.
- **Datasets:** datos sintéticos e Iris de scikit-learn.
- **Dependencias:** `numpy`, `pandas`, `matplotlib`, `seaborn`, `scipy`,
  `scikit-learn`.
- **Prerrequisitos:** probabilidad, esperanza/varianza, Python y visualización.
- **Problemas:** cuentas de ejecución fuera de orden; el ejemplo de búsqueda de
  hiperparámetros invade `Evaluacion.ipynb`. Debe aclarar clasificación/regresión,
  aprendizaje supervisado/no supervisado, función de pérdida, riesgo empírico,
  generalización y el papel de un conjunto de prueba intacto. El enlace a Wikipedia para
  intervalos de confianza es débil como referencia académica.
- **Relaciones:** articula todo el bloque de ML y debe preceder a `Evaluacion.ipynb` y a
  los modelos. Tiene solapamiento específico con la validación de `Evaluacion.ipynb`.
- **Acción recomendada:** conservar, reordenar y ampliar en conceptos; trasladar la
  implementación detallada de CV y *grid search* a evaluación.

## `IntroduccionPython.ipynb`

- **Título y propósito:** introducción breve a Python para ciencia de datos.
- **Contenido y estructura:** objetivos, importaciones, tipos, listas, tuplas,
  diccionarios, NumPy, ejercicio y resumen.
- **Datasets:** ninguno.
- **Dependencias:** `numpy`, `pandas`.
- **Prerrequisitos:** ninguno más allá de uso básico de Jupyter.
- **Problemas:** las ocho celdas de código no tienen ejecución ni salidas guardadas;
  `pandas` se importa, pero casi no se desarrolla porque existe un capítulo propio.
  Faltan control de flujo, funciones, comprensión de errores, formas/dtypes, semillas,
  vectorización, rutas relativas y una mínima práctica reproducible.
- **Relaciones:** prerrequisito directo de `Pandas.ipynb` y `Visualizacion.ipynb`; debe
  evitar duplicar esos capítulos.
- **Acción recomendada:** conservar y ampliar solo con fundamentos computacionales
  imprescindibles; mantenerlo corto.

## `NoSupervizado.ipynb`

- **Título y propósito:** capítulo aplicado de clustering que cubre varios paradigmas y
  evaluación interna.
- **Contenido y estructura:** objetivos, k-means, k-medoides, jerárquico, dendrogramas,
  DBSCAN, reducción de dimensión más clustering, silueta, Calinski–Harabasz y ejercicio.
- **Datasets:** `make_blobs`; frutas y `Mall_Customers.csv` remotos; `crime2.dat` remoto
  de ETH; imágenes locales `images/10_fig1.png` y `images/dbscan.jpg`.
- **Dependencias:** `numpy`, `pandas`, `seaborn`, `matplotlib`, `scipy`,
  `scikit-learn`, `scikit-learn-extra`, `IPython`, `shared_utilities.py`.
- **Prerrequisitos:** escala/distancias, álgebra lineal elemental, PCA y visualización.
- **Problemas:** varios imports están repetidos y seis celdas de código no tienen cuenta
  de ejecución. Depende de tres recursos de red pese a existir copia local de frutas.
  Falta EM/mezclas gaussianas, selección razonada de $K$, estabilidad, evaluación
  externa, tratamiento de ruido y alta dimensión. PCA aparece como herramienta sin
  enlace pedagógico fuerte con `ACP.ipynb`. El nombre del archivo está mal escrito
  (“Supervizado”).
- **Relaciones:** complementa `ACP.ipynb`; no duplica otro capítulo de clustering.
- **Acción recomendada:** conservar, reordenar y dividir conceptualmente en clustering
  particional/densidad/jerárquico y mezclas; mantener k-medoides y DBSCAN como contenido
  propio valioso.

## `Pandas.ipynb`

- **Título y propósito:** manipulación tabular aplicada con pandas.
- **Contenido y estructura:** Series, selección/indexación, carga, agrupaciones, formatos
  ancho/largo, `pivot_table`, `melt`, *merge*, categorías, tablas dinámicas, `apply` y
  `concat`; contiene ejercicios integrados.
- **Datasets:** Gapminder, VAB no petrolero de cantones ecuatorianos y `cars.csv`,
  todos remotos. Existe un `Data/cars.csv` local que no se usa.
- **Dependencias:** `pandas`, `numpy`.
- **Prerrequisitos:** `IntroduccionPython.ipynb`.
- **Problemas:** 178 celdas y ejecución histórica desordenada; la progresión es larga y
  carece de objetivos/resumen visibles. Depende de red; faltan tipos nulos modernos,
  validación de uniones, copias/vistas, cadenas, fechas, lectura de rutas locales y
  buenas prácticas de memoria. Debe comprobarse la vigencia de ejemplos contra pandas
  actual.
- **Relaciones:** base para todos los notebooks con datos; `Visualizacion.ipynb` usa
  visualización integrada de pandas.
- **Acción recomendada:** conservar, reordenar internamente y reducir ejemplos
  redundantes; priorizar operaciones que reaparecen en el libro.

## `ProbACP.ipynb`

- **Título y propósito:** agregado de modelos binarios y PCA.
- **Contenido y estructura:** modelo lineal de probabilidad, logit, probit y después un
  capítulo PCA completo.
- **Datasets:** `mroz.csv` y `tabla15_7.csv` remotos; imágenes locales
  `images/RL_Im7.png` y `images/fig1.png`.
- **Dependencias:** `pandas`, `numpy`, `matplotlib`, `scipy`, `statsmodels`,
  `seaborn`, `scikit-learn`, `IPython`.
- **Prerrequisitos:** regresión, probabilidad, máxima verosimilitud y álgebra lineal.
- **Problemas:** no está en el TOC y duplica grandes bloques de `ProbModels.ipynb` y
  `ACP.ipynb`, incluidas celdas exactas. Mezcla dos áreas sin transición pedagógica.
  Presenta fórmulas con erratas como `\ mid`, jerarquía de encabezados irregular y
  notación inconsistente.
- **Relaciones:** es un antecedente combinado de dos notebooks canónicos.
- **Acción recomendada:** fusionar cualquier contenido único en `ProbModels.ipynb` o
  `ACP.ipynb` y mantenerlo temporalmente como complementario; no incorporarlo al TOC.

## `ProbModels.ipynb`

- **Título y propósito:** modelos para respuesta binaria, con énfasis econométrico y un
  caso aplicado de detección de actividades ilícitas.
- **Contenido y estructura:** modelo lineal de probabilidad, logit con dos ejemplos,
  partición de datos, exploración, pruebas univariadas, pipeline, ROC/umbral, tabla de
  ganancias y probit.
- **Datasets:** `mroz.csv`, `tabla15_7.csv` y `challengeTrainUafe.csv`, todos remotos;
  figura local `images/RL_Im7.png`.
- **Dependencias:** `pandas`, `numpy`, `matplotlib`, `scipy`, `statsmodels`,
  `scikit-learn`, `seaborn`, `sweetviz`.
- **Prerrequisitos:** regresión lineal, probabilidad condicional, Bernoulli, máxima
  verosimilitud y evaluación de clasificación.
- **Problemas:** el reporte Sweetviz genera `SWEETVIZ_REPORT.html` como efecto lateral;
  la variable se selecciona mediante pruebas univariadas sin validación integrada; el
  umbral se optimiza y evalúa sobre la misma validación; faltan calibración e
  incertidumbre. Hay cuentas de ejecución duplicadas/desordenadas, erratas LaTeX
  (`\ mid`) y redacción. Mezcla inferencia de `statsmodels` y predicción de
  scikit-learn sin separar sus objetivos.
- **Relaciones:** solapa con `ProbACP.ipynb`; evaluación debe centralizarse en
  `Evaluacion.ipynb`.
- **Acción recomendada:** conservar el caso UAFE y la comparación logit/probit; dividir
  explícitamente inferencia y predicción, revisar el flujo de validación y moverlo a
  “clasificación”.

## `PruebasHipotesis.ipynb`

- **Título y propósito:** introducción a pruebas paramétricas y no paramétricas y a la
  correlación.
- **Contenido y estructura:** pruebas t y Wilcoxon de una y dos muestras, comparación de
  varianzas, KS y correlación de Pearson.
- **Datasets:** `energy.csv` y `company_sales_data.csv` remotos, aunque existen copias
  locales de ambos.
- **Dependencias:** `numpy`, `pandas`, `scipy`, `statistics`.
- **Prerrequisitos:** `Descriptiva.ipynb`, distribuciones muestrales y Python básico.
- **Problemas:** ejecución fuera de orden y una cuenta duplicada; dependencia de red
  innecesaria. Faltan tamaño de efecto, intervalos de confianza, supuestos/diagnósticos,
  potencia, errores I/II, corrección por comparaciones múltiples y distinción entre
  significancia y relevancia. La formulación del KS requiere mayor precisión.
- **Relaciones:** gran parte aparece duplicada en `DescriptivaRegresion.ipynb`; se
  relaciona con el capítulo 13 de ISLP, pero actualmente solo de forma preliminar.
- **Acción recomendada:** conservar, ampliar y reordenar; considerar ubicar pruebas
  múltiples como bloque avanzado o complementario.

## `RedesNeuronales.ipynb`

- **Título y propósito:** introducción corta e intuitiva a MLP de scikit-learn.
- **Contenido y estructura:** noción de caja negra, batch/epoch, tasa de aprendizaje,
  activaciones, una y dos capas, regularización `alpha` y cáncer de mama.
- **Datasets:** `make_blobs` y cáncer de mama de scikit-learn; imágenes locales
  `images/im5.png`, `images/im6.png`, `images/im7.png`.
- **Dependencias:** `numpy`, `matplotlib`, `scikit-learn`, `shared_utilities.py`.
- **Prerrequisitos:** clasificación, escala, partición y optimización elemental.
- **Problemas:** guarda un `NameError` (`train_test_split` no definido en el orden
  ejecutado), tiene cuentas de ejecución duplicadas, poco desarrollo matemático y
  referencias principalmente divulgativas. No explica pérdida, gradientes ni
  retropropagación con rigor. El texto confunde tasa de aprendizaje con cantidad de
  actualizaciones.
- **Relaciones:** casi todo queda superado por `AprendizajeProfundo.ipynb`, aunque sus
  fronteras de decisión con `MLPClassifier` sirven como puente ligero.
- **Acción recomendada:** fusionar los mejores ejemplos en la introducción de
  `AprendizajeProfundo.ipynb` o conservarlo como prerequisito corto; no mantener dos
  tratamientos paralelos.

## `ReglasAso.ipynb`

- **Título y propósito:** introducción a minería de reglas de asociación y Apriori.
- **Contenido y estructura:** soporte, confianza, *lift*, ejercicios manuales y un
  ejemplo sintético con `mlxtend`.
- **Datasets:** transacciones construidas en el notebook; imágenes locales
  `images/im1_ar.png`, `images/im2_ar.png`, `images/im3_ar.png`.
- **Dependencias:** `numpy`, `pandas`, `mlxtend`, `matplotlib`, `seaborn`.
- **Prerrequisitos:** conjuntos, probabilidad condicional, tablas binarias y pandas.
- **Problemas:** solo nueve celdas; no discute preparación de datos reales,
  explosión combinatoria, redundancia/poda, validación o límites de interpretación
  causal. Las cuentas de ejecución están fuera de orden. `mlxtend` no está declarado en
  `requirements.txt`.
- **Relaciones:** contenido propio sin correspondencia directa en ISLP o las hojas CS
  229; pertenece a descubrimiento de patrones, no al núcleo de modelos predictivos.
- **Acción recomendada:** conservar como contenido complementario y ampliar solo si
  “descubrimiento de patrones” se aprueba como parte del curso.

## `Regresion.ipynb`

- **Título y propósito:** regresión lineal desde una perspectiva estadística/econométrica
  con derivación manual y numerosos casos aplicados.
- **Contenido y estructura:** regresión paso a paso, OLS, descomposición de sumas de
  cuadrados, PPA, sueño, transformaciones, modelo por el origen, regresión múltiple y
  predicción.
- **Datasets:** diez archivos remotos de `DataLectures` sobre consumo, gasto en
  alimentos, PPA, sueño, telefonía, vivienda, salarios ejecutivos, educación y GPA.
- **Dependencias:** `pandas`, `numpy`, `matplotlib`, `statsmodels`, `scipy`, `seaborn`.
- **Prerrequisitos:** descriptiva, correlación, inferencia básica, álgebra matricial
  elemental y pandas.
- **Problemas:** depende intensamente de red; una celda final no fue ejecutada. Falta una
  estructura clara de objetivos–teoría–laboratorio–ejercicios. Debe reforzar supuestos,
  diagnóstico residual, intervalos, variables categóricas/interacciones, colinealidad y
  distinción entre inferencia, causalidad y predicción. La notación de intercepto cambia
  entre $\beta_1$ y $\beta_0$.
- **Relaciones:** duplicado casi completo dentro de `DescriptivaRegresion.ipynb`;
  antecede `StepRegularization.ipynb` y se solapa parcialmente con
  `AprendizajeSupervisado.ipynb`.
- **Acción recomendada:** conservar los ejemplos propios, reordenar y ampliar con
  diagnóstico; reducir el bloque duplicado del cuaderno general.

## `SVM.ipynb`

- **Título y propósito:** demostración visual de SVM lineal y con kernels.
- **Contenido y estructura:** frontera lineal, efecto de $C$, cáncer de mama, RBF y
  polinomial, efecto de $\gamma$, cuadrícula $C$–$\gamma$ y ejemplo sin normalizar.
- **Datasets:** `make_classification`, `make_blobs` y cáncer de mama de scikit-learn.
- **Dependencias:** `matplotlib`, `scikit-learn`, `shared_utilities.py`.
- **Prerrequisitos:** clasificación, escala, geometría vectorial, regularización y
  validación.
- **Problemas:** no presenta margen, *hinge loss*, vectores soporte, formulación primal o
  dual ni el truco kernel. Ajusta hiperparámetros visualmente sin CV. El ejemplo final
  muestra datos sin normalizar, pero no completa la comparación con pipeline escalado.
  No hay objetivos, ejercicios ni referencias.
- **Relaciones:** usa evaluación básica y debe seguir a optimización/regularización; el
  concepto de kernel puede conectarse con transformaciones no lineales.
- **Acción recomendada:** conservar visualizaciones, ampliar con formulación gradual y
  validación, y mover a “métodos de margen y kernels”.

## `StepRegularization.ipynb`

- **Título y propósito:** selección de variables y regularización lineal con un caso de
  empresas grandes del Ecuador.
- **Contenido y estructura:** mejor subconjunto (conceptual), *forward/backward
  stepwise*, métricas, geometría de restricciones, ridge/lasso, partición, escalado y
  ajuste de $\lambda$ con `GridSearchCV`.
- **Datasets:** `superciasGrandes2023.csv` remoto, basado en la Superintendencia de
  Compañías del Ecuador; figura local `images/L1_fig1.png`.
- **Dependencias:** `pandas`, `numpy`, `statsmodels`, `matplotlib`, `scikit-learn`.
- **Prerrequisitos:** regresión lineal, álgebra lineal, sesgo-varianza, CV y escalado.
- **Problemas:** elimina predictores altamente correlacionados usando toda la muestra;
  la selección secuencial se ajusta y evalúa in-sample; por tanto las métricas son
  optimistas. Debe encapsular selección y escalado dentro de cada fold. Se formula
  *best subset*, pero el ejemplo usa selección secuencial. Falta elastic net, rutas de
  coeficientes, regla de un error estándar e incertidumbre posselección.
- **Relaciones:** duplica ridge/lasso de `AprendizajeSupervisado.ipynb`; se apoya en
  `Regresion.ipynb`, `IntroML.ipynb` y `Evaluacion.ipynb`.
- **Acción recomendada:** conservar el dataset ecuatoriano y la geometría, revisar el
  código de validación, ampliar y ubicar después de evaluación.

## `Visualizacion.ipynb`

- **Título y propósito:** manual amplio de matplotlib, pandas y seaborn.
- **Contenido y estructura:** dispersión, líneas, barras, subplots, histogramas,
  boxplots, mapas de calor, API de pandas, seaborn/Tips y personalización.
- **Datasets:** `Data/iris.csv` local y datos sintéticos. Menciona `pic.png`,
  `test.png` y `transparentback.png` como nombres de salida en ejemplos/documentación,
  no como entradas necesarias.
- **Dependencias:** `numpy`, `pandas`, `matplotlib`, `seaborn`, `mpl_toolkits`.
- **Prerrequisitos:** Python/NumPy y pandas.
- **Problemas:** 5.3 MB por abundantes outputs HTML históricos; cuentas de ejecución muy
  desordenadas. Tiene 102 celdas, pero solo 21 explicativas. Conviene actualizar estilos,
  separar principios de comunicación visual de la referencia de API y reducir ejemplos
  repetitivos. La visualización aparece al final del TOC aunque es prerrequisito de casi
  todos los capítulos.
- **Relaciones:** fundamento computacional junto con `Pandas.ipynb`; sus técnicas se
  usan en todo el libro.
- **Acción recomendada:** mover a fundamentos computacionales, reducir y reordenar;
  conservar una galería complementaria para detalles de API.

## Relaciones globales y datos

Los pares con mayor solapamiento son:

1. `DescriptivaRegresion.ipynb` con `Descriptiva.ipynb`,
   `PruebasHipotesis.ipynb` y `Regresion.ipynb`.
2. `ProbACP.ipynb` con `ProbModels.ipynb` y `ACP.ipynb`.
3. `AprendizajeSupervisado.ipynb` con `Regresion.ipynb`,
   `StepRegularization.ipynb` y `Arboles.ipynb`.
4. `RedesNeuronales.ipynb` con `AprendizajeProfundo.ipynb`.
5. `IntroML.ipynb` con el bloque de remuestreo de `Evaluacion.ipynb`.

Archivos locales utilizados directamente: `Data/energy.csv`,
`Data/company_sales_data.csv` y `Data/iris.csv`. `Data/CommViolPredUnnormalizedData.txt`
se usa indirectamente desde `shared_utilities.py`. Existe una copia local de frutas y de
`cars.csv`, pero los notebooks descargan las versiones remotas.

Datasets sin referencia activa detectada: `Data/Table2_1.xls`, `Data/census.csv` y
`Data/datasets_615098_1099843_Bank_churn_modelling.csv`. `Data/adspy_temp.dot` es un
artefacto generado/versionado. `Data/extra.py` y `Data/shared_utilities.py` no son
importados por los notebooks actuales; duplican o intentan incorporar utilidades.

No se detectaron enlaces Markdown internos a archivos inexistentes. Sí existe una
dependencia amplia de URLs remotas, lo que impide una ejecución totalmente reproducible
sin red y expone el curso a cambios de contenido externo.

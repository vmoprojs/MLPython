# Reorganización macro aplicada

## 1. Objetivo de la reorganización

Esta tarea reorganiza únicamente la arquitectura visible del libro para ofrecer una
secuencia pedagógica clara entre fundamentos, evaluación, aprendizaje supervisado,
aprendizaje no supervisado, redes neuronales y descubrimiento de patrones.

La intervención se limita a:

- reorganizar `project.toc` en `myst.yml`;
- convertir `intro.md` en una entrada editorial coherente con la nueva estructura;
- documentar las decisiones aplicadas y pospuestas;
- validar estáticamente el TOC.

No se modificó el contenido interno de notebooks, datos, imágenes, bibliografía,
dependencias, scripts, utilidades, workflows ni configuración de despliegue.

## 2. Estado Git inicial

La verificación se ejecutó antes de modificar archivos:

```text
git status --short
# sin salida: árbol de trabajo limpio

git branch --show-current
reorganizacion-islp-cs229

git log -1 --oneline
1076b03 docs: auditar estructura y alineación con ISLP y CS229
```

La rama activa coincidía con la requerida y no había cambios sin confirmar.

## 3. Estructura anterior del TOC

La estructura anterior publicaba `intro.md` y agrupaba 18 notebooks de la siguiente
manera:

1. **Fundamentos**
   - `IntroduccionPython.ipynb`
   - `Pandas.ipynb`
   - `Descriptiva.ipynb`
   - `PruebasHipotesis.ipynb`
2. **Machine Learning**
   - `IntroML.ipynb`
   - `AprendizajeSupervisado.ipynb`
   - `Regresion.ipynb`
   - `StepRegularization.ipynb`
   - `AprendizajeProfundo.ipynb`
3. **Modelos**
   - `Arboles.ipynb`
   - `SVM.ipynb`
   - `RedesNeuronales.ipynb`
4. **Evaluación**
   - `Evaluacion.ipynb`
5. **Modelos Probabilísticos**
   - `ProbModels.ipynb`
6. **Aprendizaje No Supervisado**
   - `ACP.ipynb`
   - `NoSupervizado.ipynb`
7. **Reglas de Asociación**
   - `ReglasAso.ipynb`
8. **Visualización**
   - `Visualizacion.ipynb`

Los principales problemas eran:

- visualización aparecía después de los modelos aunque es una herramienta
  prerrequisito;
- evaluación aparecía después de varios notebooks que ya la necesitan;
- aprendizaje profundo precedía a redes neuronales;
- `ProbModels.ipynb` quedaba separado del aprendizaje supervisado;
- “Machine Learning” y “Modelos” no expresaban una progresión conceptual precisa;
- reglas de asociación no estaban identificadas como contenido complementario de
  descubrimiento de patrones.

## 4. Nueva estructura

El TOC conserva `intro.md` como primera entrada y organiza los mismos 18 notebooks
publicados en siete partes:

```text
intro.md

Parte I. Fundamentos computacionales
  IntroduccionPython.ipynb
  Pandas.ipynb
  Visualizacion.ipynb

Parte II. Fundamentos matemáticos y estadísticos
  Descriptiva.ipynb
  PruebasHipotesis.ipynb

Parte III. Fundamentos y evaluación de Machine Learning
  IntroML.ipynb
  Evaluacion.ipynb

Parte IV. Aprendizaje supervisado
  AprendizajeSupervisado.ipynb
  Regresion.ipynb
  StepRegularization.ipynb
  ProbModels.ipynb
  Arboles.ipynb
  SVM.ipynb

Parte V. Aprendizaje no supervisado
  ACP.ipynb
  NoSupervizado.ipynb

Parte VI. Redes neuronales y aprendizaje profundo
  RedesNeuronales.ipynb
  AprendizajeProfundo.ipynb

Parte VII. Descubrimiento de patrones
  ReglasAso.ipynb
```

No se creó una parte vacía de temas avanzados ni se añadieron notebooks, páginas o
separadores ficticios.

## 5. Justificación pedagógica de cada parte

### Parte I. Fundamentos computacionales

Python es el punto de entrada. pandas depende de los conceptos básicos del lenguaje y
de NumPy. Visualización se ubica después de la manipulación de datos y antes de cualquier
capítulo analítico porque se utiliza en exploración, diagnóstico e interpretación a lo
largo del libro.

### Parte II. Fundamentos matemáticos y estadísticos

La estadística descriptiva introduce distribuciones, medidas de resumen e incertidumbre.
Las pruebas de hipótesis continúan esa base hacia la inferencia. La parte todavía no
constituye una cobertura completa de probabilidad, álgebra lineal, cálculo u
optimización; esa limitación se declara en la introducción.

### Parte III. Fundamentos y evaluación de Machine Learning

`IntroML.ipynb` precede a `Evaluacion.ipynb` porque primero deben comprenderse
aprendizaje estadístico, predicción, inferencia, sesgo-varianza y generalización. Después
se formalizan particiones, métricas, validación y selección de modelos. Esta ubicación
permite que los capítulos de modelos se lean bajo un protocolo de evaluación ya
presentado.

### Parte IV. Aprendizaje supervisado

La parte conserva temporalmente `AprendizajeSupervisado.ipynb` como entrada aplicada y
KNN. Regresión lineal aparece antes de selección y regularización. Los modelos de
probabilidad se interpretan como clasificación. Árboles y SVM se ubican después de los
modelos fundamentales y del capítulo de evaluación.

Esta asignación organiza los materiales existentes; no afirma que su contenido interno
ya esté consolidado.

### Parte V. Aprendizaje no supervisado

PCA aparece antes de clustering porque introduce reducción de dimensionalidad y una base
geométrica que puede apoyar la exploración posterior. `NoSupervizado.ipynb` reúne
k-means, k-medoides, clustering jerárquico, DBSCAN y evaluación interna. Se conserva el
nombre actual del archivo aunque su ortografía deba revisarse en otra fase.

### Parte VI. Redes neuronales y aprendizaje profundo

La introducción con `MLPClassifier` precede al tratamiento más amplio de redes
multicapa, CNN, entrenamiento y regularización. Ambos notebooks se mantienen separados;
su posible consolidación queda expresamente pospuesta.

### Parte VII. Descubrimiento de patrones

Las reglas de asociación se presentan como contenido complementario. Su objetivo es
identificar coocurrencias y conjuntos frecuentes, diferente de proyectar variables con
PCA o agrupar observaciones mediante clustering.

## 6. Asignación final de cada notebook

| Notebook | Parte visible | Posición dentro de la parte | Observación |
|---|---|---:|---|
| `IntroduccionPython.ipynb` | I. Fundamentos computacionales | 1 | Punto de entrada |
| `Pandas.ipynb` | I. Fundamentos computacionales | 2 | Manipulación tabular |
| `Visualizacion.ipynb` | I. Fundamentos computacionales | 3 | Herramienta transversal |
| `Descriptiva.ipynb` | II. Fundamentos matemáticos y estadísticos | 1 | Base descriptiva y probabilística |
| `PruebasHipotesis.ipynb` | II. Fundamentos matemáticos y estadísticos | 2 | Introducción a inferencia |
| `IntroML.ipynb` | III. Fundamentos y evaluación de ML | 1 | Conceptos de aprendizaje y generalización |
| `Evaluacion.ipynb` | III. Fundamentos y evaluación de ML | 2 | Métricas, validación y selección |
| `AprendizajeSupervisado.ipynb` | IV. Aprendizaje supervisado | 1 | Entrada temporal; futura concentración en KNN |
| `Regresion.ipynb` | IV. Aprendizaje supervisado | 2 | Regresión antes de regularización |
| `StepRegularization.ipynb` | IV. Aprendizaje supervisado | 3 | Selección y regularización |
| `ProbModels.ipynb` | IV. Aprendizaje supervisado | 4 | Tratado como clasificación |
| `Arboles.ipynb` | IV. Aprendizaje supervisado | 5 | Árboles después de modelos fundamentales |
| `SVM.ipynb` | IV. Aprendizaje supervisado | 6 | Métodos de margen y kernels |
| `ACP.ipynb` | V. Aprendizaje no supervisado | 1 | Reducción de dimensionalidad |
| `NoSupervizado.ipynb` | V. Aprendizaje no supervisado | 2 | Clustering |
| `RedesNeuronales.ipynb` | VI. Redes neuronales y aprendizaje profundo | 1 | Introducción a redes |
| `AprendizajeProfundo.ipynb` | VI. Redes neuronales y aprendizaje profundo | 2 | Profundización |
| `ReglasAso.ipynb` | VII. Descubrimiento de patrones | 1 | Contenido complementario |

## 7. Orden interno aprobado

La secuencia visible completa es:

1. `IntroduccionPython.ipynb`
2. `Pandas.ipynb`
3. `Visualizacion.ipynb`
4. `Descriptiva.ipynb`
5. `PruebasHipotesis.ipynb`
6. `IntroML.ipynb`
7. `Evaluacion.ipynb`
8. `AprendizajeSupervisado.ipynb`
9. `Regresion.ipynb`
10. `StepRegularization.ipynb`
11. `ProbModels.ipynb`
12. `Arboles.ipynb`
13. `SVM.ipynb`
14. `ACP.ipynb`
15. `NoSupervizado.ipynb`
16. `RedesNeuronales.ipynb`
17. `AprendizajeProfundo.ipynb`
18. `ReglasAso.ipynb`

## 8. Notebooks excluidos del TOC

Se mantienen fuera del TOC:

- `DescriptivaRegresion.ipynb`;
- `ProbACP.ipynb`.

No se eliminaron, movieron, renombraron ni modificaron. Se documentan como notebooks
históricos o agregados pendientes de consolidación. Sus contenidos únicos deberán
compararse con los notebooks canónicos antes de considerar una eventual eliminación,
archivo o fusión.

## 9. Separación entre descubrimiento de patrones y aprendizaje no supervisado

La separación responde a la finalidad de los métodos:

- PCA busca representar los datos en un espacio de menor dimensión;
- clustering busca formar grupos de observaciones según similitud o densidad;
- las reglas de asociación buscan coocurrencias, conjuntos frecuentes y relaciones entre
  ítems.

Aunque las tres familias pueden trabajar sin una variable respuesta, no resuelven el
mismo problema. Mantener reglas de asociación en una parte complementaria evita
presentarlas como una variante de clustering.

## 10. Papel de ISLP

ISLP guía principalmente:

- la progresión desde fundamentos de aprendizaje hacia evaluación y modelos;
- la distinción entre inferencia y predicción;
- el orden regresión, selección/regularización, clasificación, árboles y SVM;
- la orientación aplicada y la futura organización de laboratorios en Python.

La reorganización no copia texto, figuras ni ejercicios. Utiliza la referencia como
criterio de secuencia y cobertura.

## 11. Papel de Stanford CS 229

Los materiales de CS 229 complementan la estructura mediante:

- notación matemática común;
- funciones de pérdida y costo;
- gradientes y optimización;
- formulaciones algorítmicas;
- distinción entre modelos generativos y discriminativos;
- profundidad futura en aprendizaje supervisado, no supervisado, redes y temas
  avanzados.

Estos aportes se aplicarán durante la revisión interna de notebooks, no en esta
reorganización macro.

## 12. Limitaciones de MyST encontradas

No se encontró una limitación de sintaxis que impidiera la estructura aprobada.
`myst.yml` admite entradas con `title` y `children`, suficientes para las siete partes.

Se eligió deliberadamente un solo nivel de hijos:

- evita páginas vacías o archivos Markdown ficticios;
- evita una fragmentación excesiva;
- conserva una estructura fácil de validar;
- no depende de probar niveles anidados adicionales para subsecciones conceptuales.

No se modificaron configuraciones de MyST fuera de `project.toc`. La construcción HTML
no se ejecutó: ya existe un `_build/` previo y, para esta fase, las validaciones estáticas
son suficientes para comprobar sintaxis, rutas, unicidad y orden sin mezclar el resultado
con artefactos anteriores.

## 13. Validaciones ejecutadas

Se realizaron las siguientes validaciones estáticas:

1. carga de `myst.yml` con `yaml.safe_load`;
2. verificación de `intro.md` como primera entrada;
3. comparación exacta de los siete títulos aprobados;
4. comparación exacta del orden de las 19 entradas de archivo: una introducción y
   18 notebooks;
5. comprobación de existencia de todos los archivos referenciados;
6. comprobación de ausencia de duplicados;
7. comprobación de exclusión de `DescriptivaRegresion.ipynb` y `ProbACP.ipynb`;
8. comprobación de que no existen notebooks ficticios en el TOC;
9. `git diff --check`;
10. búsqueda de delimitadores matemáticos de corchete no permitidos;
11. revisión de `git diff --name-only` para controlar el alcance de archivos.

Resultados:

```text
YAML: OK
INTRO_FIRST: True
TITLES_MATCH: True
ORDER_MATCH: True
FILES_TOTAL: 19
NOTEBOOKS_TOTAL: 18
MISSING_PATHS: []
DUPLICATES: []
EXCLUDED_ABSENT: True
ALL_CHECKS: True
```

`git diff --check` no reportó errores y no se encontraron delimitadores matemáticos no
permitidos en los archivos editados.

Después de crear este informe se repitieron las validaciones de alcance y formato para
incluirlo entre los archivos permitidos.

## 14. Enlaces o configuraciones pendientes

Se conservan sin cambios:

- la acción “Open in Colab”;
- la acción Binder;
- la configuración Sphinx;
- bibliografía, tema, logo, favicon y acciones del sitio;
- workflow de GitHub Pages;
- pipeline manual de construcción y publicación.

La auditoría previa detectó que las URLs de Colab y Binder incluyen `MLPython/` como
subdirectorio aunque los notebooks están en la raíz. Esta posible inconsistencia sigue
pendiente porque la tarea prohibía corregirla.

También quedan pendientes la declaración reproducible de dependencias, la política de
datasets remotos y la unificación de los mecanismos de despliegue.

## 15. Archivos modificados

- `myst.yml`: solo la sección `project.toc`;
- `intro.md`: actualización editorial completa.

Archivo creado:

- `docs/planificacion/reorganizacion_macro_aplicada.md`.

No se modificó ningún `.ipynb`.

## 16. Decisiones pospuestas

- reorganización interna y corrección de notebooks;
- concentración de `AprendizajeSupervisado.ipynb` en KNN y fundamentos aplicados;
- consolidación de `RedesNeuronales.ipynb` y `AprendizajeProfundo.ipynb`;
- consolidación de `DescriptivaRegresion.ipynb` y `ProbACP.ipynb`;
- corrección del nombre `NoSupervizado.ipynb`;
- creación de fundamentos de álgebra lineal, cálculo, probabilidad u optimización;
- incorporación de modelos no lineales, mezclas/EM, supervivencia, pruebas múltiples,
  teoría del aprendizaje, modelos secuenciales y aprendizaje por refuerzo;
- interpretabilidad, equidad, uso responsable, monitoreo y MLOps;
- corrección de Colab/Binder;
- dependencias, datasets, workflows y despliegue;
- ejecución y validación de notebooks;
- construcción MyST sobre un artefacto limpio y controlado.

## 17. Orden recomendado para la revisión futura de notebooks

La revisión interna debería comenzar por:

1. `IntroML.ipynb`
2. `Evaluacion.ipynb`
3. `Regresion.ipynb`
4. `StepRegularization.ipynb`
5. `AprendizajeSupervisado.ipynb`
6. `ProbModels.ipynb`
7. `Arboles.ipynb`
8. `SVM.ipynb`
9. `ACP.ipynb`
10. `NoSupervizado.ipynb`
11. `RedesNeuronales.ipynb`
12. `AprendizajeProfundo.ipynb`

Después podrán revisarse los fundamentos computacionales, los fundamentos matemáticos y
estadísticos y los contenidos complementarios. Este orden prioriza primero el marco
conceptual y la evaluación, después los modelos supervisados, luego el aprendizaje no
supervisado y finalmente redes y aprendizaje profundo.

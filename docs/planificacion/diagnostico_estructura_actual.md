# Diagnóstico de la estructura actual

## 1. Resumen ejecutivo

El repositorio contiene material suficiente para sostener un curso universitario
aplicado, pero todavía no funciona como un libro con progresión uniforme. Hay 20
notebooks: 18 publicados en el TOC y dos agregados históricos fuera de él. La cobertura
es fuerte en fundamentos computacionales, regresión lineal, PCA, clustering y un capítulo
reciente de aprendizaje profundo. Es parcial en evaluación, clasificación, árboles,
regularización, SVM y redes neuronales. No existe cobertura sustantiva de optimización
general, ensambles, modelos generativos, mezclas/EM, aprendizaje por refuerzo ni varios
temas avanzados.

La arquitectura propuesta de 16 áreas es conveniente como mapa de largo plazo, no como
un TOC que deba materializarse de inmediato. Para el curso principal conviene consolidar
primero cinco hilos:

1. fundamentos computacionales;
2. probabilidad, estadística, álgebra lineal y cálculo mínimos;
3. fundamentos de aprendizaje y evaluación;
4. modelos supervisados con una notación común;
5. no supervisado y redes/aprendizaje profundo.

El problema técnico más serio no es un fallo de sintaxis aislado, sino la falta de una
frontera confiable entre selección de modelos y evaluación final. En
`Arboles.ipynb` se selecciona la poda con prueba; en `StepRegularization.ipynb` se
filtran y seleccionan variables con toda la muestra y se reporta ajuste in-sample. Estos
flujos enseñan, sin intención, fuga de información.

La auditoría no modificó `myst.yml`, `intro.md`, notebooks, configuración, datos ni
pipeline. Solo creó documentación dentro de `docs/planificacion/`.

### Estado Git inicial

```text
git status --short
# sin salida

git branch --show-current
reorganizacion-islp-cs229

git log -1 --oneline
55b915f deep learning
```

La rama de auditoría parte del mismo commit que `main` y `origin/main`. No tiene upstream
configurado. El remoto es `git@github.com:vmoprojs/MLPython.git`.

## 2. Fortalezas

### Pedagógicas

- La orientación aplicada es genuina: casi todos los capítulos combinan explicación y
  código.
- `IntroML.ipynb` desarrolla bien predicción frente a inferencia, error irreducible y
  sesgo-varianza.
- `Regresion.ipynb` conserva ejemplos econométricos ricos que diferencian el curso de
  una traducción de otro libro.
- `ACP.ipynb` ofrece un desarrollo matemático superior al promedio del resto del
  material.
- `NoSupervizado.ipynb` combina k-means, k-medoides, jerárquico, DBSCAN y evaluación
  interna; es un bloque propio valioso.
- `AprendizajeProfundo.ipynb` ya tiene objetivos, requisitos, intuición, matemática,
  ejemplos reproducibles, comparación de modelos, resumen, ejercicios y referencias.
  Puede servir como patrón editorial para otros capítulos.
- Los datos ecuatorianos de empresas y VAB aportan contexto local.
- Hay ejercicios en `IntroduccionPython.ipynb`, `Pandas.ipynb`, `IntroML.ipynb`,
  `NoSupervizado.ipynb`, `ReglasAso.ipynb` y `AprendizajeProfundo.ipynb`.

### Técnicas

- Todos los notebooks de la raíz tienen el mismo `kernelspec`
  `Python (env_global)`.
- `_build/`, `SWEETVIZ_REPORT.html`, caches y artefactos comunes están ignorados.
- Existe un flujo moderno de GitHub Actions que construye MyST y despliega Pages cuando
  se actualiza `main`.
- Los notebooks emplean en varios puntos `Pipeline`, `ColumnTransformer`,
  `GridSearchCV`, semillas y separación entrenamiento/prueba.
- Las imágenes Markdown locales referenciadas existen.
- No se encontraron enlaces Markdown internos a archivos locales inexistentes.

## 3. Debilidades

### Arquitectura editorial

- El TOC mezcla niveles y funciones. Visualización, que es prerrequisito, aparece al
  final; aprendizaje profundo aparece antes de árboles, SVM y redes neuronales; evaluación
  aparece después de varios modelos que ya la necesitan.
- “Machine Learning”, “Modelos”, “Evaluación” y “Modelos Probabilísticos” no forman una
  jerarquía pedagógica consistente.
- Regresión y clasificación no están separadas; `AprendizajeSupervisado.ipynb` mezcla
  cuatro familias.
- La optimización aparece tarde y solo dentro del capítulo profundo.
- No hay una plantilla editorial común de objetivos, prerrequisitos, notación,
  ejercicios, resumen, referencias y conexión con capítulos anteriores/siguientes.
- Los niveles fundamental/intermedio/avanzado/complementario no están señalados.

### Rigor y coherencia

- Cada notebook introduce notación de forma local. Cambian $X/x$, $y/Y$, índices,
  interceptos y símbolos de regularización.
- Las funciones de pérdida no son el hilo conductor de los modelos.
- Se mezclan objetivos de inferencia (`statsmodels`) y predicción
  (`scikit-learn`) sin explicitar el cambio de pregunta.
- Faltan prerrequisitos formales de álgebra lineal, cálculo y optimización.
- Hay pocos cierres y ejercicios con criterios de respuesta.
- Muchas fuentes externas aparecen solo como URLs; `references.bib` tiene once entradas,
  varias ajenas al contenido actual, y no incluye ISLP ni las hojas CS 229.

### Reproducibilidad

- Numerosos notebooks descargan datos en tiempo de ejecución desde
  `raw.githubusercontent.com` u otros dominios.
- Existen copias locales de frutas, `cars.csv`, energía y ventas, pero algunos notebooks
  siguen usando las copias remotas.
- No se documentan procedencia, licencia, hash o fecha de adquisición de los datasets.
- `requirements.txt` solo declara `jupyter-book`, `matplotlib` y `numpy`, pero el código
  usa además `pandas`, `scipy`, `statsmodels`, `seaborn`, `scikit-learn`, `graphviz`,
  `scikit-learn-extra`, `sweetviz`, `mlxtend`, `torch`, `torchvision`, `Pillow`,
  `scikit-image`, `nbformat` y `ghp-import`, entre otros.
- El entorno global actual contiene las dependencias, pero no es reproducible a partir
  del repositorio.

## 4. Duplicaciones

### Duplicación estructural

- `DescriptivaRegresion.ipynb` reproduce bloques de `Descriptiva.ipynb`,
  `PruebasHipotesis.ipynb` y `Regresion.ipynb`. Hay numerosas celdas exactamente
  iguales.
- `ProbACP.ipynb` reproduce el núcleo de `ProbModels.ipynb` y `ACP.ipynb`, también con
  celdas exactas.
- `AprendizajeSupervisado.ipynb` vuelve a cubrir regresión lineal, ridge/lasso y árboles.
- `RedesNeuronales.ipynb` queda casi completamente solapado por
  `AprendizajeProfundo.ipynb`.
- `IntroML.ipynb` y `Evaluacion.ipynb` comparten validación cruzada y búsqueda de
  hiperparámetros.

### Duplicación técnica

- `shared_utilities.py` y `Data/shared_utilities.py` son variantes del mismo módulo; solo
  el de la raíz se importa.
- `Data/extra.py` contiene una implementación copiada/incompleta de k-medoides y no se
  importa.
- Hay imports repetidos dentro de varios notebooks, especialmente
  `NoSupervizado.ipynb`.
- `Data/adspy_temp.dot` es un artefacto generado que quedó versionado.

La consolidación debe hacerse comparando contenidos, no eliminando de inmediato los
archivos agregados. Primero se debe identificar qué celdas únicas aportan valor y obtener
aprobación para retirar o archivar lo restante.

## 5. Vacíos temáticos

### Vacíos prioritarios del curso principal

- Álgebra lineal y cálculo orientados a ML.
- Optimización: objetivos, convexidad, gradientes, SGD y condiciones de primer orden.
- Funciones de pérdida y riesgo empírico.
- Clasificación comparada: LDA, QDA, Naive Bayes, logística y KNN sobre un marco común.
- Modelos no lineales: polinomios, *splines*, regresión local y GAM.
- Árboles de regresión y métodos de ensamble.
- Evaluación de regresión, calibración, PR-AUC, selección de umbral y validación anidada.
- Formulación matemática de SVM.
- Mezclas gaussianas y EM.

### Vacíos avanzados o futuros

- Teoría de aprendizaje PAC/VC y cotas.
- ICA.
- Análisis de supervivencia.
- RNN/LSTM y modelos de secuencia.
- Aprendizaje por refuerzo.
- Temas actuales como interpretabilidad, equidad, incertidumbre, deriva y MLOps.

### Cobertura por macroárea

| Macroárea propuesta | Diagnóstico |
|---|---|
| 1. Fundamentos computacionales | Alta, pero extensa y desordenada |
| 2. Fundamentos matemáticos y estadísticos | Parcial |
| 3. Fundamentos de ML | Alta en conceptos introductorios |
| 4. Optimización para ML | Baja; integrada solo en aprendizaje profundo |
| 5. Evaluación, validación y buenas prácticas | Parcial y con código obsoleto |
| 6. Supervisado: regresión | Alta en lineal; parcial en diagnóstico/no linealidad |
| 7. Supervisado: clasificación | Parcial |
| 8. Árboles y ensambles | Parcial en árboles; ensambles ausentes |
| 9. Margen y kernels | Parcial |
| 10. Reducción de dimensionalidad | Alta para PCA |
| 11. Clustering y mezclas | Alta para clustering; mezclas/EM ausentes |
| 12. Redes neuronales | Parcial; duplicada |
| 13. Aprendizaje profundo | Alta para MLP/CNN |
| 14. Descubrimiento de patrones | Parcial; solo reglas de asociación |
| 15. Aprendizaje por refuerzo | Sin cobertura |
| 16. Temas avanzados y extensiones | Sin estructura; elementos aislados |

## 6. Problemas de secuencia

La secuencia actual del TOC presenta estos conflictos:

1. `PruebasHipotesis.ipynb` aparece sin un bloque suficiente de probabilidad,
   muestreo e inferencia.
2. `IntroML.ipynb` introduce CV y después `AprendizajeSupervisado.ipynb` ajusta modelos
   mirando prueba, antes del capítulo formal de evaluación.
3. `AprendizajeProfundo.ipynb` aparece antes de árboles, SVM, redes neuronales y
   evaluación.
4. `Evaluacion.ipynb` llega después de modelos que ya deberían usar sus reglas.
5. `ProbModels.ipynb` aparece como categoría separada, cuando logit/probit son parte
   natural de clasificación.
6. PCA y clustering están correctamente cerca, pero el ejemplo conjunto no remite de
   forma clara al capítulo PCA.
7. Visualización está al final, aunque es fundamento de todos los laboratorios.
8. La selección/regularización aparece antes de una política madura de evaluación.

Secuencia mínima recomendada antes de ampliar contenidos:

```text
Python → pandas → visualización
→ descriptiva/probabilidad/inferencia + álgebra/cálculo mínimos
→ introducción a ML → evaluación
→ regresión → selección/regularización
→ clasificación → árboles/ensambles → SVM
→ PCA → clustering/mezclas
→ redes → aprendizaje profundo
→ patrones y temas opcionales
```

## 7. Contenidos propios a conservar

- Los casos ecuatorianos de empresas, VAB y UAFE.
- La orientación econométrica y los ejemplos PPA, sueño, vivienda, CEO y educación,
  siempre que se documente su origen.
- La explicación de media y mediana como soluciones de optimización.
- Las visualizaciones de fronteras de decisión.
- K-medoides y DBSCAN.
- Las reglas de asociación como módulo complementario.
- El experimento de modelos clásicos frente a red en datos tabulares.
- Las funciones de entrenamiento PyTorch, parada temprana y transferencia del capítulo
  profundo.
- Las tablas de ganancias, después de corregir su validación y explicar su ámbito de
  uso.

Conservar no implica mantener la ubicación o el código exactos. Estos contenidos deben
adoptar la notación común, pipelines reproducibles y la plantilla editorial del libro.

## 8. Riesgos técnicos

### Críticos para la validez didáctica

1. **Fuga en poda:** `Arboles.ipynb` evalúa todos los `ccp_alpha` sobre `X_test`,
   selecciona el mejor y vuelve a reportar sobre ese mismo test.
2. **Selección optimista:** `StepRegularization.ipynb` elimina variables correlacionadas
   y realiza selección secuencial con toda la muestra; después evalúa el modelo
   seleccionado sobre esos mismos datos.
3. **Selección de $k$ sobre prueba:** `AprendizajeSupervisado.ipynb` compara valores de
   $k$ usando repetidamente el conjunto de prueba.
4. **Selección de umbral:** `ProbModels.ipynb` optimiza y reporta el umbral sobre la misma
   partición de validación.

### Compatibilidad y ejecución

- `Evaluacion.ipynb` guarda un `ImportError`:
  `from sklearn.metrics import SCORERS`; la API actual es
  `get_scorer_names()`.
- `RedesNeuronales.ipynb` guarda un `NameError` por ejecutar una celda que usa
  `train_test_split` antes del import.
- Hay celdas sin ejecutar en `IntroduccionPython.ipynb`, `Evaluacion.ipynb`,
  `NoSupervizado.ipynb` y `Regresion.ipynb`.
- Muchos notebooks tienen cuentas de ejecución desordenadas o duplicadas.
- `%matplotlib notebook` permanece activo en `DescriptivaRegresion.ipynb`; sus outputs
  HTML inflan el archivo y son frágiles fuera de Jupyter clásico.
- `Visualizacion.ipynb` pesa 5.3 MB y `DescriptivaRegresion.ipynb` 2.4 MB por outputs
  históricos.
- El árbol completo ocupa aproximadamente 1 GB: `_build/` cerca de 602 MB y `.git/`
  cerca de 386 MB. Los archivos versionados actuales suman alrededor de 24 MB.
- El repositorio conserva más de 200 MB de objetos Git sueltos y paquetes; esto no
  afecta el contenido pedagógico, pero encarece clonación y mantenimiento.

### Configuración y enlaces

- `README.md` e `intro.md` tienen correos y enlaces diferentes; la introducción y el
  README no son una fuente única.
- Los enlaces de “Open in Colab” y Binder en `myst.yml` incluyen `MLPython/` como
  subdirectorio, aunque los notebooks están en la raíz del repositorio; requieren
  verificación antes de una publicación futura.
- El TOC omite dos notebooks versionados sin documentar si son borradores, archivos
  históricos o material complementario.
- No se encontraron scripts `.sh`; el pipeline manual solo está documentado como una
  secuencia de comandos.

## 9. Diagnóstico del pipeline de construcción y publicación

### `fix_kernels.py`

El script:

1. lista únicamente el directorio de trabajo con `os.listdir()`;
2. abre cada archivo cuyo nombre termina en `.ipynb`;
3. reemplaza `metadata.kernelspec` por:

   ```python
   {
       "name": "env_global",
       "display_name": "Python (env_global)",
       "language": "python",
   }
   ```

4. vuelve a escribir todos los notebooks mediante `nbformat.write()`.

En la estructura actual afecta los 20 notebooks de la raíz. No es recursivo: si en el
futuro se mueven notebooks a subdirectorios, dejará de encontrarlos. Tampoco compara la
metadata antes de escribir, por lo que puede generar diffs o normalizaciones de JSON aun
cuando el kernel ya sea correcto. Reescribir todos los notebooks justo antes de
`git add .` aumenta el riesgo de confirmar cambios mecánicos, outputs o metadata no
revisados. `nbformat` no está declarado en `requirements.txt`.

Recomendación futura: convertirlo en verificador por defecto; usar un modo `--check` que
falle si hay discrepancias y un modo explícito `--fix` que solo escriba archivos cuya
metadata cambie, con recorrido recursivo y resumen de cambios.

### Construcción MyST

`_build/` sí está ignorado por Git. También existe `MLPython/_build/` en `.gitignore`.
La construcción almacenada ocupa cientos de MB y puede contener restos de ejecuciones
anteriores.

El pipeline mostrado ejecuta comandos uno después de otro. Si se copian literalmente en
una terminal interactiva, un fallo de `myst build --html` no impide necesariamente que
el usuario ejecute después `ghp-import`. Además, MyST puede dejar archivos antiguos en
`_build/html`; publicar esa carpeta sin limpiarla/validarla puede mezclar una salida
parcial con artefactos previos.

No se ejecutó la construcción durante esta auditoría. Los errores guardados en notebooks
no prueban por sí solos que MyST falle, porque la construcción actual puede usar outputs
existentes sin ejecutar código. Esto crea un riesgo distinto: el sitio puede compilar
aunque el código ya no sea reproducible.

Recomendación futura:

- construir en un directorio de salida nuevo o limpio y temporal;
- capturar el código de salida;
- validar que existan las páginas esperadas y que no haya errores severos;
- ejecutar una muestra o todo el libro en CI separada cuando las dependencias sean
  reproducibles;
- publicar únicamente el artefacto que superó validación.

### Publicación y despliegue

`ghp-import -n -p -f _build/html` crea/reescribe y empuja la rama `gh-pages` de forma
inmediata. Por tanto, en el flujo manual la publicación ocurre **antes** de revisar y
confirmar los cambios fuente. `-f` hace el reemplazo de la historia de la rama de
publicación más agresivo.

Al mismo tiempo, `.github/workflows/deploy.yml` construye con `mystmd` instalado por npm
y despliega mediante GitHub Pages cuando se empuja `main`. Existen, por tanto, dos
mecanismos de despliegue: rama `gh-pages` manual y GitHub Actions. Según la configuración
de Pages, uno puede ser redundante o competir con el otro. Además, el flujo local usa el
entorno Python global y el ejecutable MyST del entorno, mientras CI instala la versión
más reciente de `mystmd` sin fijarla. Los resultados pueden divergir.

Recomendación futura: elegir un único mecanismo. La opción más segura es que `main`
active un workflow con versiones fijadas, construcción, validación, artefacto inmutable
y despliegue protegido. El despliegue manual debería quedar, si se conserva, como acción
de recuperación explícita y no como paso ordinario.

### Commit y push

- `git add .` incluye cualquier archivo nuevo no ignorado dentro del repositorio, no solo
  los archivos intencionales. Puede incorporar datasets pesados, credenciales, salidas,
  informes HTML o cambios mecánicos de `fix_kernels.py`.
- Un mensaje fijo como `deep learning` deja de describir el contenido real y dificulta
  auditoría, revisión y reversión.
- `git push origin main` en el ejemplo ignora que se puede estar trabajando en otra
  rama. En la auditoría la rama activa es `reorganizacion-islp-cs229`.
- Publicar antes de revisar hace que una versión defectuosa quede visible aunque después
  no se confirme la fuente.

Separación recomendada:

```text
1. preparar/editar
2. verificar kernels en modo lectura
3. ejecutar validaciones estáticas
4. construir en salida nueva
5. ejecutar pruebas/notebooks seleccionados
6. revisar artefacto y git diff
7. añadir archivos explícitos
8. commit descriptivo
9. push de la rama
10. revisión/aprobación
11. merge a main
12. despliegue automático del artefacto validado
```

## 10. Decisiones que requieren aprobación

1. Aprobar la arquitectura macro y decidir si las 16 áreas son partes visibles,
   capítulos futuros o etiquetas de planificación.
2. Definir duración del curso y profundidad matemática; esto determina si optimización,
   EM, teoría de aprendizaje y RL entran al núcleo.
3. Elegir los notebooks canónicos y autorizar la futura fusión/retiro de
   `DescriptivaRegresion.ipynb` y `ProbACP.ipynb`.
4. Decidir si `AprendizajeSupervisado.ipynb` se convierte en KNN o se conserva como
   encuesta inicial.
5. Decidir si `RedesNeuronales.ipynb` se fusiona con
   `AprendizajeProfundo.ipynb`.
6. Aprobar qué contenidos propios son obligatorios: econometría, UAFE, k-medoides,
   DBSCAN y reglas de asociación.
7. Elegir una política de datasets: copias locales versionadas, descarga con hash o
   paquete externo.
8. Elegir y fijar el entorno de dependencias, incluida la versión de Python y MyST.
9. Elegir un único mecanismo de despliegue: GitHub Actions o rama `gh-pages`.
10. Autorizar posteriormente cambios de TOC, nombres de archivos y correcciones de
    notebooks. Ninguna de esas acciones se realizó en esta fase.

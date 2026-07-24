# Plantilla adaptable para un capítulo en notebook

## Cómo usar esta plantilla

Esta es una estructura de partida, no un formulario rígido. Copie en el notebook solo
las secciones que ayuden a cumplir sus objetivos. Las marcas `{{...}}` son campos por
reemplazar. Las indicaciones entre comentarios editoriales no deben quedar en la versión
publicada.

Son normalmente obligatorios: orientación, problema, objetivos, prerrequisitos,
explicación conceptual, implementación o ejemplo, evaluación cuando haya un modelo,
interpretación, limitaciones, resumen y referencias. Las secciones identificadas como
opcionales pueden eliminarse sin romper el recorrido principal.

## Mapa sugerido de celdas

| Orden | Tipo de celda | Contenido | Carácter |
|---:|---|---|---|
| 1 | Markdown | Título, nivel y duración | Requerido |
| 2 | Markdown | Motivación y problema | Requerido |
| 3 | Markdown | Objetivos y prerrequisitos | Requerido |
| 4 | Markdown | Intuición y notación | Requerido |
| 5 | Markdown | Formulación matemática | Requerido para modelos |
| 6 | Código | Importaciones y configuración | Requerido si hay código |
| 7 | Markdown + código | Ejemplo mínimo | Recomendado |
| 8 | Markdown + código | Caso aplicado y datos | Recomendado |
| 9 | Markdown + código | Pipeline, selección y evaluación | Requerido para modelos |
| 10 | Markdown | Interpretación y limitaciones | Requerido |
| 11 | Markdown + código | Ejercicio guiado | Recomendado |
| 12 | Markdown | Ejercicios autónomos | Requerido |
| 13 | Markdown | Resumen y referencias | Requerido |
| 14 | Markdown + código | Extensión | Opcional |

## 1. Apertura y orientación

### Ejemplo de celda Markdown

```markdown
# {{Título del capítulo}}

**Nivel:** {{Fundamental | Intermedio | Avanzado | Complementario}}

**Tiempo de lectura:** {{rango orientativo}}

**Tiempo de ejecución:** {{rango y equipo de referencia}}

**Carácter:** {{Núcleo | Extensión opcional}}

## ¿Por qué estudiar este tema?

{{Plantee una situación, decisión o pregunta concreta. Explique su importancia en uno o
dos párrafos breves.}}

## Problema

Disponemos de {{tipo de datos y unidad de observación}} y queremos
{{describir | inferir | predecir | clasificar | agrupar | reducir dimensión}}.
La pregunta central es: **{{pregunta}}**.

Este capítulo se concentra en {{alcance}}. No permite concluir {{límite importante}}.
```

### Orientación editorial

- La motivación debe poder entenderse antes de conocer el algoritmo.
- Identifique si la meta es inferencia, predicción, descubrimiento de estructura o
  decisión.
- No anticipe causalidad si el diseño solo permite asociación.
- Si el título usa un término inglés, defina su equivalente en español.

## 2. Objetivos, prerrequisitos y conexiones

### Ejemplo de celda Markdown

```markdown
## Objetivos de aprendizaje

Al finalizar el capítulo, podrá:

- distinguir {{concepto A}} de {{concepto B}};
- formular {{objetivo o pérdida}};
- implementar {{procedimiento}} dentro de un pipeline reproducible;
- evaluar el resultado mediante {{métrica o protocolo}};
- interpretar {{resultado}} y reconocer {{limitación}}.

## Prerrequisitos

- {{concepto matemático}};
- {{concepto estadístico}};
- {{herramienta de Python}};
- {{capítulo previo}}.

## Conexiones

Este capítulo retoma {{idea previa}} y prepara {{tema posterior}}. La notación sigue la
guía matemática del libro.
```

No incluir como prerrequisito algo que el propio capítulo pretende enseñar. Si una
ampliación requiere más preparación, declararla al comienzo de esa ampliación.

## 3. Intuición

### Ejemplo de celda Markdown

```markdown
## Intuición

{{Explique el mecanismo con lenguaje directo. Use una analogía solo si conserva la
estructura relevante del problema.}}

La idea central es {{idea}}. Si {{condición}}, esperamos {{comportamiento}}; si
{{condición contraria}}, el método puede {{fallo}}.

> **Pregunta de lectura.** ¿Qué cambiaría si {{variación sencilla}}?
```

Una figura o tabla puede acompañar esta sección. Debe tener ejes, unidades, leyenda y
una interpretación inmediata.

## 4. Notación y formulación matemática

### Ejemplo de celda Markdown

```markdown
## Notación

Sea $\mathcal{D}=\{(\mathbf{x}_i,y_i)\}_{i=1}^{n}$ una muestra supervisada, donde
$\mathbf{x}_i\in\mathbb{R}^{p}$ contiene los predictores de la observación $i$ y $y_i$
es su respuesta. La función aprendida se denota por $\widehat f$.

## Formulación

La pérdida por observación es $\ell(y_i,f(\mathbf{x}_i))$. El riesgo empírico es

$$
\widehat R_n(f)=\frac{1}{n}\sum_{i=1}^{n}
\ell\left(y_i,f(\mathbf{x}_i)\right).
$$

Buscamos una función que equilibre ajuste y complejidad:

$$
\widehat f_\lambda
=
\underset{f\in\mathcal{F}}{\operatorname{arg\,min}}
\left\{\widehat R_n(f)+\lambda\Omega(f)\right\},
$$

donde $\mathcal{F}$ es {{familia}}, $\Omega(f)$ mide {{complejidad}} y $\lambda$
controla {{compromiso}}.

En la implementación, $\lambda$ corresponde a `{{nombre_del_parametro}}`. Se selecciona
con validación; el conjunto de prueba no interviene en esta decisión.
```

Adapte la formulación al método. No fuerce objetivos diferenciables para árboles ni una
notación supervisada para clustering. Toda ecuación central debe definir símbolos,
explicar su lectura y relacionarse con el código.

## 5. Algoritmo

### Ejemplo de celda Markdown

```markdown
## Algoritmo

**Entrada:** {{datos, hiperparámetros y estado inicial}}.

**Salida:** {{modelo, predicción, componentes o grupos}}.

1. {{Paso conceptual 1}}.
2. {{Paso conceptual 2}}.
3. {{Criterio de actualización}}.
4. Detener cuando {{criterio}}.

El costo dominante es {{tiempo/memoria}}. El algoritmo puede fallar o volverse inestable
cuando {{condición}}.
```

El pseudocódigo es opcional si una explicación breve y el código transparente ya hacen
visible el procedimiento.

## 6. Importaciones y configuración

### Ejemplo de celda de código

```python
from pathlib import Path
import random

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import ConfusionMatrixDisplay, classification_report
from sklearn.model_selection import GridSearchCV, train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import OneHotEncoder, StandardScaler

SEED = 42
random.seed(SEED)
np.random.seed(SEED)
rng = np.random.default_rng(SEED)

PROJECT_ROOT = Path.cwd()
DATA_DIR = PROJECT_ROOT / "datos"
```

Adapte y reduzca las importaciones. No conserve paquetes que no se utilizan. Si el
capítulo es de regresión, cambie estimador, métricas y estratificación.

## 7. Ejemplo mínimo o simulado

### Ejemplo de celda Markdown

```markdown
## Ejemplo mínimo

Este ejemplo aísla {{mecanismo}}. Generaremos {{datos}} con una semilla fija y
comprobaremos {{resultado esperado}}. No pretende representar una población real.
```

### Ejemplo de celda de código

```python
n_observaciones = 120
x = rng.normal(size=n_observaciones)
ruido = rng.normal(scale=0.4, size=n_observaciones)
y = 1.5 + 2.0 * x + ruido

datos_simulados = pd.DataFrame({"predictor": x, "respuesta": y})
datos_simulados.head()
```

### Ejemplo de celda Markdown para lectura

```markdown
### Lectura del ejemplo

{{Describa el patrón observado, conéctelo con la formulación y señale qué no puede
concluirse.}}
```

## 8. Caso aplicado y procedencia de datos

### Ejemplo de celda Markdown

```markdown
## Caso aplicado: {{nombre}}

**Pregunta:** {{pregunta sustantiva}}

**Unidad de observación:** {{unidad}}

**Fuente:** {{institución, publicación o URL estable}}

**Versión o fecha:** {{versión}}

**Licencia:** {{licencia o condición de uso}}

**Variable objetivo:** {{nombre, definición y unidades}}

**Predictores:** {{grupos de variables}}

**Limitaciones:** {{cobertura, medición, selección o representatividad}}
```

### Ejemplo de celda de código

```python
DATA_PATH = DATA_DIR / "archivo.csv"

if not DATA_PATH.exists():
    raise FileNotFoundError(
        f"No se encontró {DATA_PATH}. Consulte la sección de procedencia de datos."
    )

datos = pd.read_csv(DATA_PATH)

columnas_requeridas = {"objetivo", "predictor_numerico", "predictor_categorico"}
faltantes = columnas_requeridas.difference(datos.columns)
if faltantes:
    raise ValueError(f"Faltan columnas requeridas: {sorted(faltantes)}")

datos.info()
```

La exploración debe responder a la pregunta o verificar supuestos de preparación. No
usar el conjunto de prueba para decidir variables, transformaciones o umbrales.

## 9. Partición y pipeline

### Ejemplo de celda Markdown

```markdown
## Protocolo de evaluación

Reservaremos {{porcentaje}} para prueba final. La selección de hiperparámetros se
realizará mediante {{esquema}} dentro de entrenamiento. La métrica principal será
{{métrica}} porque {{justificación}}. La línea base será {{baseline}}.
```

### Ejemplo de celda de código

```python
TARGET = "objetivo"

X = datos.drop(columns=TARGET)
y = datos[TARGET]

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=SEED,
    stratify=y,
)

numeric_features = ["predictor_numerico"]
categorical_features = ["predictor_categorico"]

numeric_pipeline = Pipeline(
    steps=[
        ("imputer", SimpleImputer(strategy="median")),
        ("scaler", StandardScaler()),
    ]
)

categorical_pipeline = Pipeline(
    steps=[
        ("imputer", SimpleImputer(strategy="most_frequent")),
        (
            "encoder",
            OneHotEncoder(handle_unknown="ignore"),
        ),
    ]
)

preprocessor = ColumnTransformer(
    transformers=[
        ("numeric", numeric_pipeline, numeric_features),
        ("categorical", categorical_pipeline, categorical_features),
    ]
)

pipeline = Pipeline(
    steps=[
        ("preprocessor", preprocessor),
        ("model", LogisticRegression(max_iter=2_000)),
    ]
)
```

Para grupos, tiempo o espacio, sustituya `train_test_split` por el esquema apropiado.
Todo paso que aprenda de los datos debe quedar dentro del pipeline.

## 10. Selección del modelo

### Ejemplo de celda de código

```python
parameter_grid = {
    "model__C": [0.1, 1.0, 10.0],
}

search = GridSearchCV(
    estimator=pipeline,
    param_grid=parameter_grid,
    scoring="balanced_accuracy",
    cv=5,
    n_jobs=-1,
    refit=True,
)

search.fit(X_train, y_train)

print("Mejores hiperparámetros:", search.best_params_)
print("Validación media:", round(search.best_score_, 3))
```

No inspeccione `X_test` ni `y_test` durante esta etapa. Si se comparan procesos
completos de selección, use validación anidada y explique qué función cumple cada nivel.

## 11. Evaluación final

### Ejemplo de celda Markdown

```markdown
## Evaluación

Evaluaremos una sola vez el modelo seleccionado sobre prueba. Reportaremos
{{métrica principal}}, {{métricas secundarias}} y un análisis de {{tipo de errores}}.
Las cifras estiman desempeño bajo esta partición y población; no garantizan el mismo
resultado en otros periodos o contextos.
```

### Ejemplo de celda de código

```python
selected_model = search.best_estimator_
y_pred = selected_model.predict(X_test)

print(classification_report(y_test, y_pred, digits=3))
ConfusionMatrixDisplay.from_predictions(
    y_test,
    y_pred,
    cmap="Blues",
    colorbar=False,
)
plt.title("Matriz de confusión en el conjunto de prueba")
plt.tight_layout()
```

Incluya la línea base bajo la misma partición. Si el ejemplo es de regresión, reporte
errores en unidades de la respuesta y revise residuos. Si usa probabilidades, evalúe
discriminación y calibración antes de modificar el umbral.

## 12. Interpretación, limitaciones y errores frecuentes

### Ejemplo de celda Markdown

```markdown
## Interpretación

El modelo {{resultado principal}}. En términos del problema, esto significa
{{traducción sustantiva}}. Los errores se concentran en {{subgrupo o patrón}}, lo que
sugiere {{hipótesis que debe comprobarse}}.

## Supuestos y limitaciones

- {{supuesto del método}};
- {{limitación de los datos}};
- {{limitación del protocolo}};
- {{población o periodo fuera de alcance}}.

Estos resultados describen asociación o capacidad predictiva; no identifican un efecto
causal.

## Errores frecuentes

- ajustar el preprocesamiento antes de separar prueba;
- seleccionar hiperparámetros o umbrales con prueba;
- interpretar una puntuación como probabilidad;
- comparar modelos con particiones distintas;
- omitir la línea base;
- reportar una métrica sin explicar su costo de error.
```

Adapte los errores a la familia de métodos; no mantenga una lista genérica que nunca se
discute en el capítulo.

## 13. Ejercicio guiado

### Ejemplo de celda Markdown

```markdown
## Ejercicio guiado

**Objetivo:** {{habilidad}}.

**Producto:** {{tabla, figura, explicación o código}}.

1. Reemplace {{decisión}} por {{alternativa}}.
2. Mantenga la misma partición y vuelva a ajustar dentro del pipeline.
3. Compare {{métrica}} con la línea base.
4. Explique qué error cambió y por qué.

**Comprobación intermedia:** {{resultado cualitativo o rango esperado}}.

**Pista opcional:** {{pista que no entrega toda la solución}}.
```

### Ejemplo de celda de código

```python
# Complete sin consultar ni transformar el conjunto de prueba.
alternative_pipeline = None
```

## 14. Ejercicios para el estudiante

### Ejemplo de celda Markdown

```markdown
## Ejercicios

1. **Concepto.** Explique la diferencia entre {{A}} y {{B}} con un ejemplo propio.
2. **Matemática y código.** Identifique dónde aparece {{término de la ecuación}} en el
   pipeline.
3. **Evaluación.** Proponga una métrica diferente para {{costo}} y justifique la
   elección antes de calcularla.
4. **Análisis de errores.** Caracterice {{tipo de error}} sin usar prueba para ajustar
   el modelo.
5. **Crítica.** Señale dos límites para generalizar el resultado.
```

## 15. Resumen

### Ejemplo de celda Markdown

```markdown
## Resumen

- {{problema que resuelve el método}};
- {{idea matemática o algorítmica central}};
- {{decisión de preparación o evaluación}};
- {{interpretación principal}};
- {{limitación que debe recordarse}}.

### Antes de continuar

El lector debería poder {{resultado observable}}. El próximo capítulo utilizará
{{concepto}} para {{finalidad}}.
```

## 16. Referencias

### Ejemplo de celda Markdown

```markdown
## Referencias

- {{Referencia académica mediante una clave existente en `references.bib`}}:
  {cite:t}`{{clave_bibliografica}}`.
- {{Documentación oficial de la biblioteca y versión consultada}}.
- {{Fuente, licencia y versión de los datos}}.

La secuencia del tema se contrastó con ISLP y la formulación con materiales de CS229,
sin reproducir sus textos, figuras ni ejercicios.
```

Usar la sintaxis de citas MyST adoptada por el proyecto y comprobar que cada clave
exista antes de publicar.

## 17. Extensión opcional

### Ejemplo de celda Markdown

```markdown
## Extensión opcional: {{tema}}

**Nivel:** {{nivel}}

**Prerrequisitos adicionales:** {{lista}}

**Tiempo estimado:** {{lectura y ejecución}}

**Recursos:** {{CPU, GPU, memoria o red}}

**Dependencia opcional:** `{{paquete}}`

Esta sección amplía {{idea}}, pero no es necesaria para los ejercicios del núcleo.
Puede omitirse sin alterar el estado requerido por las celdas posteriores.
```

### Ejemplo de celda de código

```python
EJECUTAR_EXTENSION = False

if EJECUTAR_EXTENSION:
    # Importe aquí la dependencia y ejecute aquí cualquier descarga o cálculo costoso.
    pass
```

## Comprobación final del autor

Antes de considerar terminado el capítulo, aplicar
`checklist_revision_notebook.md`, reiniciar el kernel, ejecutar de arriba abajo, revisar
las salidas guardadas y confirmar el alcance con Git.

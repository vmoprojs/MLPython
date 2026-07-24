# Guía de notación matemática

## Propósito

Esta guía establece una notación compartida para que los notebooks puedan leerse como
un curso continuo. La consistencia debe facilitar el vínculo entre pregunta, ecuación,
algoritmo, implementación e interpretación. No se debe forzar una notación común cuando
oculte la convención natural de un método; toda excepción se declara localmente.

## Escritura matemática en MyST

- Usar `$...$` para matemática en línea.
- Usar `$$...$$` para ecuaciones centradas.
- No usar delimitadores matemáticos basados en corchetes.
- Escribir LaTeX compatible con MyST y evitar macros locales que no estén declaradas en
  la configuración del proyecto.
- Definir cada símbolo antes o inmediatamente después de su primera ecuación importante.
- Mantener la puntuación de la oración alrededor de la ecuación.
- No usar una ecuación como sustituto de una explicación verbal.

Ejemplo:

La pérdida cuadrática para la observación $i$ es

$$
\ell_i = \left(y_i-\widehat y_i\right)^2,
$$

donde $y_i$ es el valor observado y $\widehat y_i$ es la predicción. En código, esta
diferencia corresponde al residuo calculado antes de elevarlo al cuadrado.

## Datos, muestra y particiones

### Muestra supervisada

- $n$: número de observaciones.
- $p$: número de características o predictores.
- $\mathbf{X}\in\mathbb{R}^{n\times p}$: matriz de diseño.
- $\mathbf{x}_i\in\mathbb{R}^{p}$: vector de características de la observación $i$.
- $x_{ij}$: valor de la característica $j$ en la observación $i$.
- $y_i$: respuesta observada para la observación $i$.
- $\mathbf{y}=(y_1,\ldots,y_n)^\top$: vector de respuestas.
- $\mathcal{D}=\{(\mathbf{x}_i,y_i)\}_{i=1}^{n}$: conjunto de datos supervisado.

Cuando hay intercepto, se debe decir si $\mathbf{X}$ contiene una columna de unos o si
el intercepto se escribe por separado. No cambiar entre ambas convenciones dentro de
una derivación.

### Particiones

Usar:

- $\mathcal{D}_{\mathrm{train}}$: conjunto de entrenamiento;
- $\mathcal{D}_{\mathrm{val}}$: conjunto de validación;
- $\mathcal{D}_{\mathrm{test}}$: conjunto de prueba.

Si se usa validación cruzada, definir $K_{\mathrm{CV}}$ como el número de particiones
para no confundirlo con el número de clases. Puede usarse $\mathcal{I}_r$ para los
índices de la partición $r$, con $r=1,\ldots,K_{\mathrm{CV}}$.

### Variables aleatorias y observaciones

Usar mayúsculas para variables aleatorias y minúsculas para realizaciones:
$X$ y $Y$ representan variables aleatorias; $x_i$ y $y_i$, valores observados. Para
objetos vectoriales, usar negrita: $\mathbf{X}$ puede representar la matriz observada y
$\boldsymbol{X}$ un vector aleatorio solo si la distinción es necesaria y se explica.

## Funciones, parámetros y resultados del ajuste

- $f$: función poblacional o regla candidata, según se defina.
- $\widehat f$: función aprendida a partir de datos.
- $\boldsymbol{\beta}$: vector de parámetros de un modelo lineal.
- $\widehat{\boldsymbol{\beta}}$: estimador o vector estimado; el texto debe distinguir
  el procedimiento aleatorio de su valor en una muestra cuando esa diferencia importe.
- $\theta$: hiperparámetro escalar genérico.
- $\boldsymbol{\theta}$: conjunto de parámetros genérico solo cuando
  $\boldsymbol{\beta}$ no sea natural, por ejemplo en una red.
- $\widehat y_i=\widehat f(\mathbf{x}_i)$: valor ajustado o predicción, según el origen
  de $\mathbf{x}_i$.
- $e_i=y_i-\widehat y_i$: residuo observado.
- $\varepsilon_i$: error aleatorio no observable en un modelo de datos.

No usar “error” y “residuo” como sinónimos. En entrenamiento, $\widehat y_i$ es un valor
ajustado; para una observación no usada en el ajuste, es una predicción. Un parámetro se
aprende durante el ajuste; un hiperparámetro gobierna el procedimiento y se selecciona
con validación, no con prueba.

## Pérdida, riesgo y objetivo

### Convención general

- $\ell(y,f(\mathbf{x}))$: pérdida por observación.
- $R(f)$: riesgo poblacional.
- $\widehat R_n(f)$: riesgo empírico en una muestra de tamaño $n$.
- $\Omega(f)$ o $\Omega(\boldsymbol{\beta})$: penalización o medida de complejidad.
- $\lambda\geq 0$: intensidad de regularización.

El riesgo poblacional es

$$
R(f)=\mathbb{E}\left[\ell\left(Y,f(\boldsymbol{X})\right)\right].
$$

El riesgo empírico es

$$
\widehat R_n(f)=\frac{1}{n}\sum_{i=1}^{n}
\ell\left(y_i,f(\mathbf{x}_i)\right).
$$

Un objetivo regularizado puede escribirse como

$$
\widehat f_\lambda
=
\underset{f\in\mathcal{F}}{\operatorname{arg\,min}}
\left\{
\widehat R_n(f)+\lambda\Omega(f)
\right\}.
$$

Se debe explicar qué función cumple cada término: ajuste a los datos, control de
complejidad y compromiso gobernado por $\lambda$. La escala de la pérdida y la
penalización debe ser compatible; si una biblioteca usa suma en vez de promedio, se
documenta la correspondencia.

### Conexiones por familia

- **Regresión lineal.** Usar pérdida cuadrática y
  $\widehat y_i=\widehat\beta_0+\mathbf{x}_i^\top\widehat{\boldsymbol{\beta}}$.
  Declarar si se busca inferencia, predicción o ambas.
- **Clasificación probabilística.** Usar entropía cruzada o log-verosimilitud negativa y
  probabilidades de clase. Separar la estimación de probabilidades de la decisión por
  umbral.
- **SVM.** Usar margen, pérdida *hinge* y penalización. Explicar la equivalencia entre
  parámetros como $C$ y la intensidad de regularización según la implementación.
- **Árboles.** Usar impureza o error dentro de nodos y un criterio de partición. No
  representar artificialmente cada árbol como una minimización diferenciable.
- **Redes neuronales.** Usar $\boldsymbol{\theta}$ para pesos y sesgos, indicar la
  pérdida de la tarea y separar arquitectura, optimizador y regularización.

## Probabilidad y clasificación

### Clases y probabilidades

- $\mathcal{Y}=\{1,\ldots,K\}$: conjunto de $K$ clases.
- $\pi_k(\mathbf{x})=P(Y=k\mid\boldsymbol{X}=\mathbf{x})$: probabilidad condicional de
  la clase $k$.
- $\widehat\pi_k(\mathbf{x})$: probabilidad estimada.
- $\mathbb{1}\{A\}$: indicador del evento $A$.
- $s(\mathbf{x})$: puntuación continua de un clasificador.
- $t$: umbral de decisión.

La regla multiclase usual es

$$
\widehat y(\mathbf{x})
=
\underset{k\in\{1,\ldots,K\}}{\operatorname{arg\,max}}
\widehat\pi_k(\mathbf{x}).
$$

En clasificación binaria, si la clase positiva es $1$, una regla por umbral es

$$
\widehat y_t(\mathbf{x})
=
\mathbb{1}\left\{\widehat\pi_1(\mathbf{x})\geq t\right\}.
$$

El umbral debe seleccionarse con validación y con costos explícitos; no con el conjunto
de prueba.

### Logit y sigmoide

Definir la función sigmoide como

$$
\sigma(z)=\frac{1}{1+\exp(-z)}.
$$

Para regresión logística binaria:

$$
\operatorname{logit}\left(\pi_1(\mathbf{x})\right)
=
\log\left(\frac{\pi_1(\mathbf{x})}{1-\pi_1(\mathbf{x})}\right)
=
\beta_0+\mathbf{x}^{\top}\boldsymbol{\beta}.
$$

No llamar “probabilidad” a un *logit*, margen o puntuación sin calibración.

### Verosimilitud

- $L(\boldsymbol{\theta};\mathcal{D})$: verosimilitud.
- $\log L(\boldsymbol{\theta};\mathcal{D})$: log-verosimilitud.
- $\widehat{\boldsymbol{\theta}}_{\mathrm{MV}}$: estimador de máxima verosimilitud.

La verosimilitud se interpreta como función de los parámetros para datos observados, no
como probabilidad de esos parámetros. Si se minimiza log-verosimilitud negativa, mostrar
su correspondencia con la pérdida usada por el código.

### Modelos discriminativos y generativos

Un modelo discriminativo estima directamente $P(Y\mid\boldsymbol{X})$ o una frontera de
decisión. Un modelo generativo especifica $P(\boldsymbol{X}\mid Y)$ y $P(Y)$, o la
distribución conjunta, y obtiene la regla mediante Bayes. La notación debe hacer visible
qué distribución se modela; no basta con etiquetar el algoritmo.

## Álgebra lineal y cálculo

### Convenciones

- Escalares en cursiva: $a$, $\lambda$, $x_{ij}$.
- Vectores en negrita minúscula: $\mathbf{x}$, $\boldsymbol{\beta}$.
- Matrices en negrita mayúscula: $\mathbf{X}$, $\mathbf{W}$.
- Transpuesta: $\mathbf{X}^{\top}$.
- Producto interno: $\langle\mathbf{a},\mathbf{b}\rangle$ o
  $\mathbf{a}^{\top}\mathbf{b}$.
- Norma euclídea: $\lVert\mathbf{x}\rVert_2$.
- Norma uno: $\lVert\mathbf{x}\rVert_1$.
- Matriz identidad de dimensión $p$: $\mathbf{I}_p$.
- Gradiente: $\nabla_{\boldsymbol{\theta}}J(\boldsymbol{\theta})$.
- Hessiana: $\nabla^2_{\boldsymbol{\theta}}J(\boldsymbol{\theta})$.
- Derivada parcial: $\partial J/\partial\theta_j$.

Declarar dimensiones cuando ayuden a comprobar una operación. Por ejemplo, si
$\mathbf{X}\in\mathbb{R}^{n\times p}$ y
$\boldsymbol{\beta}\in\mathbb{R}^{p}$, entonces
$\mathbf{X}\boldsymbol{\beta}\in\mathbb{R}^{n}$.

### Autovalores, autovectores y SVD

Para una matriz cuadrada $\mathbf{A}$, usar

$$
\mathbf{A}\mathbf{v}_j=\lambda_j\mathbf{v}_j,
$$

donde $\lambda_j$ es un autovalor y $\mathbf{v}_j$ su autovector. No usar la misma
$\lambda$ para regularización y autovalores en una sección sin subíndices o una
aclaración.

Para la descomposición en valores singulares:

$$
\mathbf{X}=\mathbf{U}\boldsymbol{\Sigma}\mathbf{V}^{\top}.
$$

Indicar dimensiones, orden de valores singulares y relación concreta con PCA cuando se
utilice.

## Índices y símbolos reservados

| Símbolo | Uso preferido |
|---|---|
| $i$ | observación |
| $j$ | característica, coeficiente o componente |
| $k$ | clase |
| $g$ | grupo o *cluster* |
| $r$ | partición de validación cruzada o capa, según el capítulo |
| $b$ | lote de entrenamiento |
| $\ell$ | función de pérdida, no índice de capa |

Si una sección necesita simultáneamente particiones y capas, usar $r$ para la partición
y $q$ para la capa, o declarar otra convención sin ambigüedad. No reutilizar $k$ para
clase, vecino, grupo y partición en la misma explicación.

## Cómo presentar una ecuación importante

Cada ecuación central debe incluir:

1. definición previa o inmediata de todos los símbolos;
2. lectura verbal de qué optimiza, relaciona o mide;
3. interpretación del resultado en el contexto;
4. correspondencia con variables, funciones o parámetros del código;
5. unidades cuando las magnitudes las tengan;
6. supuestos y condiciones de validez relevantes.

Ejemplo de descenso por gradiente:

$$
\boldsymbol{\theta}^{(m+1)}
=
\boldsymbol{\theta}^{(m)}
-\eta\nabla_{\boldsymbol{\theta}}J\left(\boldsymbol{\theta}^{(m)}\right),
$$

donde $m$ es la iteración, $\eta>0$ es la tasa de aprendizaje y $J$ es el objetivo. En
código, $\eta$ corresponde al parámetro de aprendizaje del optimizador; el gradiente se
calcula con respecto a los parámetros del modelo, no a los hiperparámetros.

## Ejemplos de uso correcto e incorrecto

### Correcto

- “Sea $\mathbf{x}_i$ el vector de predictores de la observación $i$.”
- “El modelo produce $\widehat\pi_1(\mathbf{x})$; el umbral $t$ transforma esa
  probabilidad en una clase.”
- “El residuo $e_i$ se observa después del ajuste; el error
  $\varepsilon_i$ pertenece al modelo poblacional.”
- “Seleccionamos $\lambda$ mediante validación cruzada y evaluamos una vez en prueba.”

### Incorrecto

- Introducir $J$, $L$ o $\theta$ sin definirlos.
- Alternar $\mathbf{x}_i$ y $X_i$ para la misma observación sin explicar el cambio.
- Llamar error a todo residuo, o precisión a cualquier métrica de clasificación.
- Escribir que el conjunto de prueba “entrena” o “valida” el modelo.
- Comparar valores de pérdidas con escalas diferentes sin normalización ni explicación.
- Presentar una puntuación de decisión como probabilidad.
- Usar delimitadores matemáticos incompatibles con la política MyST del proyecto.

## Lista breve para revisión matemática

- Cada símbolo aparece definido.
- Mayúsculas aleatorias y minúsculas observadas son coherentes.
- Parámetros, estimadores, valores ajustados, predicciones, residuos e hiperparámetros
  están diferenciados.
- La pérdida coincide con la tarea y con el código.
- La muestra sobre la que se calcula cada riesgo o métrica está identificada.
- Las dimensiones matriciales son compatibles.
- La selección usa validación y la evaluación final usa prueba.
- La interpretación respeta unidades, supuestos y alcance.
- Todas las fórmulas usan delimitadores con signo de dólar compatibles con MyST.

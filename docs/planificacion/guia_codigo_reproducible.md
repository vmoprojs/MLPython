# Guía de código reproducible para notebooks

## Propósito

Esta guía define cómo escribir código que otro estudiante o docente pueda leer,
ejecutar y auditar en orden. La reproducibilidad incluye datos, entorno, semillas,
particiones, transformaciones, evaluación y salidas; no se limita a que una celda
funcione en la computadora de quien la escribió.

El código debe apoyar la explicación. Una implementación correcta pero opaca no cumple
el objetivo pedagógico, y una explicación clara no compensa un protocolo que contamine
la evaluación.

## Organización de celdas

Cada celda debe tener un propósito reconocible y producir una salida que se interpreta
o que prepara el siguiente paso. Preferir este flujo:

1. importaciones y versiones relevantes;
2. configuración reproducible;
3. carga y validación de datos;
4. exploración orientada por la pregunta;
5. partición de datos;
6. preparación y transformación;
7. entrenamiento y selección;
8. evaluación;
9. visualización y análisis de errores;
10. conclusiones computacionales.

No mezclar en una sola celda descargas, limpieza, entrenamiento y figuras. Una celda de
código extensa debe dividirse cuando sus partes tengan estados, fallos o explicaciones
independientes. Evitar también la fragmentación artificial de una operación breve en
muchas celdas que solo funcionan por efectos laterales invisibles.

Toda variable debe definirse antes de usarse en el orden de lectura. Reiniciar el kernel
y ejecutar de arriba abajo debe producir el mismo flujo, salvo variación explícitamente
documentada.

## Importaciones y dependencias

Agrupar las importaciones al inicio del recorrido ejecutable:

1. biblioteca estándar;
2. paquetes de terceros;
3. módulos locales del proyecto.

Ejemplo:

```python
from pathlib import Path
import random

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split

from herramientas.graficos import configurar_estilo
```

Reglas:

- usar alias convencionales: `np`, `pd`, `plt`, `sns`;
- no usar importaciones con asterisco;
- eliminar importaciones duplicadas o no utilizadas;
- declarar dependencias directas en el entorno del proyecto;
- no depender de funciones definidas en otro notebook;
- usar módulos locales solo si están versionados y su finalidad está documentada;
- tratar los avisos de bibliotecas de forma localizada y con justificación;
- usar APIs públicas y vigentes, no atributos internos o retirados.

### Dependencias opcionales

Una dependencia opcional debe importarse dentro de la sección que la necesita. La
sección debe indicar propósito, versión o requisito mínimo, tiempo, memoria y alternativa
sin esa dependencia. Si el bloque no se ejecuta, tampoco debe descargar pesos, datos ni
recursos.

```python
EJECUTAR_EXTENSION = False

if EJECUTAR_EXTENSION:
    import paquete_opcional

    # La descarga o el cálculo costoso se realiza únicamente aquí.
```

Una importación opcional fallida puede producir un mensaje breve y accionable; no debe
dejar una traza guardada en la versión publicada.

## Semillas y fuentes de aleatoriedad

Definir una sola constante visible:

```python
SEED = 42

random.seed(SEED)
np.random.seed(SEED)
rng = np.random.default_rng(SEED)
```

Pasar `random_state=SEED` a particiones, modelos y procedimientos que lo admitan. No
mezclar generadores sin explicar por qué. Si una biblioteca requiere su propia semilla,
configurarla en el mismo bloque.

Una semilla mejora la repetibilidad, pero no garantiza determinismo completo. En GPU
pueden existir operaciones no deterministas, diferencias entre controladores y cambios
numéricos entre versiones. Cuando el resultado dependa de GPU, registrar dispositivo,
versiones, precisión y cualquier configuración determinista usada. No prometer
reproducción bit a bit si no se comprobó.

## Datos y rutas

### Política de datos

Preferir, en este orden:

1. datos pequeños versionados en el repositorio con licencia compatible;
2. datos incluidos en una biblioteca estable;
3. datos simulados con semilla;
4. descarga desde una fuente institucional o repositorio estable.

Cada conjunto debe documentar:

- nombre y propósito;
- fuente original y enlace;
- licencia o condiciones de uso;
- fecha o versión de consulta;
- unidad de observación;
- variables utilizadas y unidades;
- valores faltantes o códigos especiales;
- transformaciones realizadas;
- limitaciones y población a la que no debe generalizarse.

Una URL remota debe ser estable. Cuando sea razonable, registrar versión, etiqueta de
lanzamiento o hash y ofrecer una copia local permitida o instrucciones de recuperación.
Si se descarga un archivo, validar su tipo, tamaño o checksum y su esquema antes de
usarlo. No usar enlaces temporales ni depender de una rama mutable sin advertencia.

No incluir datos personales, credenciales, tokens ni información sensible. Los datos
derivados deben conservar la atribución y las restricciones de la fuente.

### Rutas

Usar `pathlib` y rutas relativas a una raíz explícita del proyecto:

```python
from pathlib import Path

PROJECT_ROOT = Path.cwd()
DATA_DIR = PROJECT_ROOT / "datos"
DATA_PATH = DATA_DIR / "archivo.csv"

if not DATA_PATH.exists():
    raise FileNotFoundError(
        f"No se encontró {DATA_PATH}. Consulte las instrucciones de datos."
    )
```

No usar rutas absolutas del equipo del autor. Si el notebook puede abrirse desde
distintos directorios, incluir una función breve y verificable para localizar la raíz.
Las salidas generadas deben escribirse en una carpeta definida, con nombres estables, y
solo cuando sean necesarias. Evitar sobrescribir datos de entrada.

## Particiones y fuga de información

### Regla central

Separar primero los datos de prueba. Ajustar imputación, escala, selección de variables,
codificación, balanceo, reducción de dimensionalidad y modelo usando únicamente
entrenamiento. Seleccionar hiperparámetros con validación o validación cruzada dentro de
entrenamiento. Usar prueba una sola vez para estimar el desempeño final.

Todo preprocesamiento que aprende de los datos debe estar dentro de un pipeline o
ajustarse exclusivamente con la partición correspondiente. Esto incluye decisiones
aparentemente inocuas como elegir variables por correlación, fijar umbrales a partir de
la distribución completa o seleccionar épocas mediante la pérdida de prueba.
Usar `Pipeline` para encadenar transformaciones y modelo, y `ColumnTransformer` cuando
distintos grupos de columnas requieren tratamientos diferentes. La selección de
variables debe formar parte del pipeline para volver a ajustarse dentro de cada
partición.

Las particiones deben respetar el problema:

- estratificación para clases desbalanceadas cuando corresponda;
- grupos separados si varias filas pertenecen a la misma persona, entidad o unidad;
- paneles y jerarquías que mantengan juntas las observaciones relacionadas;
- orden temporal y validación hacia adelante en series de tiempo;
- particiones espaciales cuando la proximidad produzca dependencia;
- validación anidada si se compara de manera imparcial un proceso intensivo de
  selección.

### Aplicación a los notebooks inspeccionados

Estas observaciones orientan una revisión futura; no modifican los notebooks en esta
fase.

#### `IntroML.ipynb`

El capítulo combina fundamentos, *bootstrap*, validación cruzada y una búsqueda de
hiperparámetros. El ejemplo que coloca `GridSearchCV` dentro de una evaluación externa
es una base válida para explicar validación anidada, pero debe declarar claramente qué
particiones seleccionan y cuáles evalúan. Corrección editorial propuesta: conservar en
`IntroML.ipynb` la intuición de generalización y un ejemplo mínimo; desarrollar el
protocolo completo y la lectura de resultados en `Evaluacion.ipynb`. El generador de
`bootstrap` debe recibir una semilla explícita.

#### `Evaluacion.ipynb`

El notebook crea varias particiones con el mismo nombre y después presenta validación
cruzada y búsqueda en cuadrícula. También conserva una salida de error por importar
`SCORERS` desde una ubicación obsoleta. Corrección propuesta: definir un único protocolo
por experimento, preservar prueba desde el principio, realizar búsqueda solo dentro de
entrenamiento y evaluar una vez al modelo seleccionado. Consultar los *scorers* mediante
la API pública vigente y explicar si cada repetición usa exactamente la misma
partición.

#### `Regresion.ipynb`

Los ejemplos ajustan e interpretan modelos sobre varios conjuntos remotos, generalmente
sin una separación explícita entre finalidad inferencial y finalidad predictiva.
Corrección propuesta: para inferencia, declarar muestra, supuestos, estimando y
diagnósticos sin llamar “desempeño predictivo” al ajuste en muestra; para predicción,
crear entrenamiento y prueba antes de cualquier transformación y evaluar fuera de
muestra. La transformación de variables debe aprenderse con entrenamiento cuando
dependa de los datos. Las fuentes remotas deben versionarse o contar con una alternativa
reproducible.

#### `AprendizajeProfundo.ipynb`

El notebook ya separa entrenamiento, validación y prueba, configura varias semillas y
desactiva una demostración opcional con ImageNet. Corrección propuesta: mantener esa
separación como modelo interno, asegurar que escala, parada temprana y elección de
arquitectura usen solo entrenamiento/validación, y reservar prueba para la comparación
final. Cada bloque con PyTorch o `torchvision` debe declarar costo, dispositivo y
condición de ejecución; los experimentos clásicos y neuronales deben usar particiones y
métricas equivalentes.

### Corrección de errores de fuga ya auditados

Los cuatro casos siguientes son bloqueantes para una revisión futura. Se documentan
aquí sin modificar sus notebooks:

#### `Arboles.ipynb`

No se debe elegir `ccp_alpha`, la profundidad ni ningún otro hiperparámetro observando
el desempeño de prueba. Corrección propuesta: separar prueba al inicio, seleccionar
`ccp_alpha` mediante validación cruzada dentro de entrenamiento, reajustar el pipeline
con el valor elegido y evaluar una sola vez sobre prueba.

#### `StepRegularization.ipynb`

El filtrado y la selección de variables no deben calcularse con el conjunto completo,
ni el ajuste en muestra debe presentarse como evaluación de generalización. Corrección
propuesta: incluir selección, escala y regularización dentro de un pipeline que se
reajuste en cada partición; comparar *stepwise*, ridge, lasso u otras alternativas con
el mismo protocolo externo.

#### `AprendizajeSupervisado.ipynb`

No se debe escoger $k$ para KNN mediante inspecciones repetidas del conjunto de prueba.
Corrección propuesta: reservar prueba, normalizar dentro del pipeline y seleccionar $k$
con validación cruzada sobre entrenamiento. La curva de selección debe usar resultados
de validación; el punto de prueba aparece solo después de fijar el modelo.

#### `ProbModels.ipynb`

No se debe optimizar un umbral y reportar como final su desempeño sobre la misma
partición. Corrección propuesta: ajustar el modelo con entrenamiento, elegir el umbral
con validación según costos definidos previamente y estimar discriminación, calibración
y desempeño de la regla una sola vez en prueba. Si el tamaño muestral lo exige, usar un
procedimiento anidado.

## Evaluación reproducible

Todo experimento de modelos debe documentar:

- pregunta y unidad de análisis;
- línea base pertinente;
- métrica principal, elegida antes de observar prueba;
- métricas secundarias y qué error iluminan;
- esquema de partición;
- espacio de hiperparámetros;
- procedimiento de selección;
- estimación de incertidumbre o variabilidad cuando sea pertinente;
- análisis de errores;
- interpretación sustantiva y limitaciones.

Una línea base puede ser la media, mediana, clase mayoritaria, clasificador estratificado
o modelo simple. Debe competir bajo la misma partición y métrica que el modelo principal.

No comparar cifras obtenidas con particiones diferentes como si fueran directamente
equivalentes. Para una comparación justa, reutilizar índices o un objeto de validación
común. Si se reporta media de validación cruzada, incluir dispersión o distribución por
partición y evitar una precisión decimal que los datos no respaldan.

La métrica debe responder al costo del error. En clasificación desbalanceada, exactitud
puede ser insuficiente; considerar precisión, exhaustividad, F1, PR-AUC, ROC-AUC y
calibración según la decisión. En regresión, justificar MAE, RMSE, error relativo o
$R^2$ y mantener unidades interpretables.

## Estilo de código

- Preferir funciones pequeñas para operaciones repetidas o conceptualmente nombrables.
- Usar nombres descriptivos en español o inglés de forma consistente.
- Reservar comentarios para explicar decisiones y motivos, no traducir cada línea.
- Evitar repetir sintaxis si una función o bucle legible expresa la estructura.
- Evitar variables globales ocultas y mutaciones entre celdas.
- No sobrescribir un conjunto original con una versión transformada de significado
  distinto.
- Usar comprobaciones tempranas de columnas, tipos, rangos y clases.
- Mantener una única fuente de verdad para constantes, rutas y parámetros.
- Evitar capturar todas las excepciones; manejar solo fallos esperados.
- No silenciar avisos globalmente. Corregirlos o filtrar uno concreto con justificación.
- No acceder a atributos privados de bibliotecas.
- Eliminar código comentado, pruebas abandonadas y resultados no interpretados.

Una función debe recibir sus entradas y devolver su resultado:

```python
def calcular_rmse(y_real, y_predicha):
    """Calcula RMSE en las mismas unidades de la variable objetivo."""
    errores = np.asarray(y_real) - np.asarray(y_predicha)
    return float(np.sqrt(np.mean(errores**2)))
```

## Visualizaciones reproducibles y accesibles

- Crear figura y ejes de forma explícita.
- Aplicar estilos dentro del alcance de una figura o bloque controlado; no cambiar
  accidentalmente el estilo global para capítulos posteriores.
- Usar tamaños de figura, texto y marcadores legibles en pantalla y en el libro.
- Nombrar ejes, unidades, series y población.
- Mantener escalas comparables entre paneles.
- Indicar intervalos, variabilidad o tamaño de muestra cuando aporten a la lectura.
- Usar paletas accesibles y añadir marcadores, patrones o etiquetas si el color codifica
  información esencial.
- No truncar ejes de una manera que exagere efectos sin advertirlo.
- Fijar límites solo con una razón analítica.
- Cerrar figuras creadas dentro de bucles o procesos por lotes.
- Guardar archivos únicamente cuando el libro los necesite y con resolución, ruta y
  nombre definidos.
- Interpretar cada figura en el texto; una gráfica sin lectura no completa el análisis.

Ejemplo:

```python
fig, ax = plt.subplots(figsize=(7, 4))
ax.plot(epocas, perdida_entrenamiento, label="Entrenamiento")
ax.plot(epocas, perdida_validacion, label="Validación")
ax.set(
    xlabel="Época",
    ylabel="Pérdida media",
    title="Evolución de la pérdida",
)
ax.legend()
fig.tight_layout()
```

## Rendimiento y extensiones costosas

Toda celda que pueda tardar más de un minuto debe indicar un tiempo orientativo y el
equipo de referencia. Si requiere GPU, mucha memoria, descarga o acceso de red, debe
declararlo antes de ejecutarse.

Ofrecer dos modos cuando aporte valor:

- **rápido:** muestra menor, menos épocas o búsqueda acotada para recorrer el concepto;
- **completo:** experimento más costoso y marcado como opcional.

Ambos modos deben conservar el mismo objetivo pedagógico y no presentar resultados de
escalas incomparables como si fueran equivalentes. Una salida precalculada debe
identificarse como tal y explicar cómo se generó.

## Compatibilidad con MyST y citas

- Usar Markdown estándar y las extensiones MyST ya configuradas.
- Escribir matemática solo con delimitadores de signo de dólar.
- Mantener encabezados jerárquicos, sin saltar niveles por apariencia.
- Respetar el `tableofcontents` global y no crear entradas, archivos o índices locales
  ficticios para simular una estructura aún no aprobada.
- Dar texto alternativo o descripción útil a imágenes.
- Evitar HTML dependiente del tema cuando Markdown o MyST ofrecen una alternativa.
- Verificar que rutas de imágenes y archivos funcionen desde la raíz del proyecto.
- Usar claves existentes en `references.bib` y la sintaxis de citas adoptada por MyST.
- Registrar referencias nuevas para incorporarlas a `references.bib` en una tarea
  posterior autorizada, sin dejar claves rotas en el capítulo publicado.
- Citar la fuente del método, los datos y la documentación de APIs cuando corresponda.
- Preferir fuentes primarias y manuales oficiales; no sustentar un tema únicamente en
  blogs.
- No copiar texto, figuras, tablas ni ejercicios de las obras de referencia.

## Protocolo de revisión de un notebook

1. **Validación estructural.** Confirmar propósito, nivel, objetivos, prerrequisitos,
   orden de celdas, secciones obligatorias y opcionales, dependencias y datos.
2. **Ejecución limpia.** Reiniciar el kernel y ejecutar de arriba abajo en el entorno
   declarado, sin estado histórico ni variables futuras.
3. **Revisión de *warnings*.** Leer cada aviso, corregir su causa cuando sea relevante y
   justificar cualquier filtro local.
4. **Revisión de *outputs*.** Retirar trazas, errores y salidas masivas; conservar solo
   resultados necesarios, legibles e interpretados.
5. **Revisión matemática.** Comprobar notación, dimensiones, fórmulas, pérdidas,
   supuestos y correspondencia con el código.
6. **Revisión de enlaces.** Verificar datos, imágenes, referencias cruzadas, fuentes,
   licencias y claves bibliográficas sin depender de rutas personales.
7. **Validación MyST.** Revisar encabezados, tablas, figuras, citas, ecuaciones,
   `tableofcontents` y renderizado de salidas con la configuración admitida.
8. **Revisión de Git.** Confirmar que solo cambiaron archivos autorizados, ejecutar
   comprobaciones de formato y leer el diff completo antes de confirmar cambios.

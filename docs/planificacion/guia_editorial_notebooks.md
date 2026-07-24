# Guía editorial para los notebooks

## Propósito y alcance

Esta guía define el estándar común para revisar los capítulos de *Machine Learning con
Python*. Su finalidad es que cada notebook explique con claridad qué problema aborda,
por qué importa, qué aprenderá el estudiante, qué conocimientos requiere y cómo se
relaciona con los capítulos anteriores y posteriores.

La guía orienta decisiones editoriales; no exige que todos los capítulos tengan la
misma extensión ni que reproduzcan una plantilla de forma mecánica. La secuencia,
la distinción entre inferencia y predicción, la evaluación y el carácter aplicado se
alinean con ISLP. La notación, las pérdidas, la optimización, los gradientes y la
distinción entre modelos generativos y discriminativos se profundizan con criterios
inspirados en CS229. Los textos, ejemplos, figuras y ejercicios deben ser propios.

`AprendizajeProfundo.ipynb` es una referencia interna relativamente completa por su
combinación de objetivos, requisitos, intuición, matemática, código, interpretación,
resumen, ejercicios y referencias. No es una plantilla definitiva: su numeración
discontinua, su carga computacional, sus dependencias opcionales y la señalización de
tiempos todavía deben mejorarse.

## Preguntas que debe responder un capítulo

Al terminar la introducción, el lector debería saber:

1. ¿Qué problema se estudia?
2. ¿Por qué es relevante y en qué situaciones aparece?
3. ¿Qué resultados de aprendizaje se esperan?
4. ¿Qué conocimientos y herramientas se presuponen?
5. ¿Cómo se conecta el tema con el recorrido curricular?
6. ¿El objetivo principal es describir, inferir, predecir, descubrir estructura o tomar
   una decisión?
7. ¿Qué partes son nucleares y cuáles son ampliaciones?

## Estructura adaptable

El siguiente orden es el punto de partida. Una sección puede integrarse con otra cuando
la lectura mejore; no debe omitirse información esencial por mantener un formato breve.

1. **Título.** Específico, estable y consistente con el índice.
2. **Motivación.** Situación o pregunta que justifica el método.
3. **Objetivos de aprendizaje.** Entre tres y seis resultados observables, escritos con
   verbos como distinguir, formular, implementar, evaluar e interpretar.
4. **Prerrequisitos y conexiones.** Conceptos, paquetes y capítulos previos; anticipo
   breve de los capítulos que dependen del actual.
5. **Definición del problema.** Datos disponibles, variable objetivo si existe,
   pregunta analítica y tipo de tarea.
6. **Intuición.** Explicación verbal o visual antes de la formulación.
7. **Notación.** Símbolos necesarios y enlace a la guía común; no repetir un glosario
   completo si bastan dos o tres definiciones locales.
8. **Formulación matemática.** Supuestos, pérdida u objetivo y resultado que se busca.
9. **Algoritmo.** Pasos conceptuales, criterio de parada y costo relevante cuando
   corresponda.
10. **Ejemplo mínimo o simulado.** Aísla una idea y permite comprobarla con pocos datos.
11. **Caso aplicado.** Plantea una pregunta sustantiva con datos documentados.
12. **Preparación de datos.** Partición, limpieza, codificación y transformación sin
    fuga de información.
13. **Implementación en Python.** Código legible, reproducible y vinculado con la
    formulación.
14. **Evaluación.** Línea base, protocolo, métricas e incertidumbre.
15. **Interpretación.** Traducción de parámetros, predicciones, métricas o patrones al
    contexto del problema.
16. **Limitaciones y errores frecuentes.** Supuestos, fallos esperables y usos que el
    método no justifica.
17. **Ejercicio guiado.** Práctica con andamiaje y verificaciones intermedias.
18. **Ejercicios para el estudiante.** Transferencia a datos, métricas o supuestos
    diferentes.
19. **Resumen.** Ideas, decisiones y advertencias que deben permanecer.
20. **Referencias.** Fuentes académicas, documentación de software y procedencia de
    datos.

### Secciones requeridas, opcionales e integrables

Son requeridos en todo capítulo sustantivo: título, motivación o problema, objetivos,
prerrequisitos, explicación conceptual, implementación o ejemplo verificable,
interpretación, limitaciones, resumen y referencias. En capítulos de modelos también
son requeridos la formulación matemática, el protocolo de evaluación y al menos una
línea base pertinente.

Son opcionales cuando no aportan al objetivo: derivaciones extensas, pseudocódigo,
casos aplicados adicionales, comparaciones históricas y ampliaciones teóricas. Deben
marcarse como tales y no introducir dependencias necesarias para completar el núcleo.

Pueden integrarse:

- motivación y definición del problema;
- intuición y ejemplo mínimo;
- notación y formulación matemática;
- preparación e implementación dentro de un pipeline;
- evaluación e interpretación;
- limitaciones y errores frecuentes;
- resumen y preguntas de autoevaluación.

Conviene dividir una sección o un notebook cuando la ampliación introduce objetivos,
prerrequisitos o audiencia distintos; cuando impide recorrer el núcleo en una sesión;
cuando agrega dependencias pesadas; o cuando mezcla tareas que requieren protocolos de
evaluación diferentes. La división debe responder a una necesidad pedagógica, no solo
al número de celdas.

## Niveles de contenido

Cada notebook puede declarar un nivel dominante y marcar subsecciones de otro nivel.

| Nivel | Preparación matemática | Profundidad algorítmica | Carga computacional | Autonomía esperada | Papel en el curso |
|---|---|---|---|---|---|
| Fundamental | Álgebra y probabilidad elementales; cada símbolo nuevo se explica | Comprender el objetivo y usar una implementación guiada | Baja; ejecución normal en CPU | Seguir y adaptar ejemplos con apoyo | Indispensable para el recorrido principal |
| Intermedio | Notación matricial, derivadas y probabilidad aplicada | Comparar alternativas y razonar sobre hiperparámetros | Moderada; validación o búsqueda acotada | Construir un pipeline con decisiones justificadas | Profundiza el núcleo |
| Avanzado | Optimización, cálculo matricial o probabilidad más exigente | Derivar, diagnosticar y modificar el algoritmo | Media o alta; puede requerir GPU o más tiempo | Diseñar experimentos y evaluar supuestos con autonomía | Especialización o electivo |
| Complementario | Variable según el tema | Amplía el repertorio sin ser prerrequisito del núcleo | Debe declararse | Conectar el tema con el curso | No desplaza contenidos obligatorios |

La etiqueta depende de la combinación de estas dimensiones. Un ejemplo computacional
costoso no es automáticamente avanzado, y una derivación breve puede requerir
prerrequisitos avanzados.

## Criterios de redacción

### Lengua y tono

- Usar español académico claro, directo y preciso.
- Preferir párrafos cortos y una idea central por párrafo.
- Explicar la intuición antes de formalizar, sin sustituir la formalización cuando es
  necesaria.
- Mantener el ciclo intuición, matemática, código e interpretación.
- Evitar traducciones literales que resulten ajenas al uso técnico en español.
- Definir una sigla en su primera aparición y no acumular siglas innecesarias.
- Usar anglicismos solo cuando sean el término predominante o faciliten consultar la
  documentación; incluir el equivalente en español en la primera aparición.
- No presentar asociaciones, coeficientes o importancia predictiva como efectos
  causales sin un diseño que lo justifique.
- Distinguir explícitamente descripción, asociación, inferencia, predicción y causalidad.
- Declarar supuestos, alcance y limitaciones junto al método, no únicamente al final.

### Terminología preferida

| Primera aparición | Uso posterior recomendado | Observación |
|---|---|---|
| aprendizaje automático (*Machine Learning*) | aprendizaje automático; se admite *Machine Learning* en el título del proyecto | No alternar sin motivo |
| conjunto de datos (*dataset*) | conjunto de datos | `dataset` puede conservarse en nombres de API |
| característica (*feature*) | característica | Término general para una columna de entrada |
| predictor | predictor | Preferirlo cuando una variable se usa para predecir una respuesta |
| variable objetivo (*target*) | variable objetivo | También se admite respuesta en contexto estadístico |
| conjunto de entrenamiento (*training set*) | entrenamiento | No confundir con ajuste completo |
| conjunto de validación (*validation set*) | validación | Se usa para decisiones de modelado |
| conjunto de prueba (*test set*) | prueba | Se reserva para evaluación final |
| sobreajuste (*overfitting*) | sobreajuste | Evitar usarlo como sinónimo de cualquier mal resultado |
| subajuste (*underfitting*) | subajuste | Relacionarlo con complejidad insuficiente |
| sesgo (*bias*) | sesgo | Aclarar si es estadístico, algorítmico o social |
| varianza (*variance*) | varianza | Aclarar si se refiere a datos, estimador o error |

En clasificación, “clase positiva” debe definirse en el contexto. En aprendizaje no
supervisado, “grupo” puede usarse como explicación general y *cluster* cuando se hable
del objeto producido por un algoritmo o de una API.

## Recursos pedagógicos

### Ejemplos

El ejemplo mínimo debe aislar un mecanismo: pocos datos, una visualización legible y
una salida fácil de comprobar. El caso aplicado debe comenzar con una pregunta y
terminar con una interpretación, no con la mera ejecución de una biblioteca. Si ambos
ejemplos enseñan lo mismo, conservar solo el que aporte mayor claridad.

### Tablas y figuras

- Toda tabla o figura necesita propósito, título o pie y comentario en el texto.
- Los ejes deben tener nombres y unidades; la leyenda debe identificar las series.
- Los colores deben ser distinguibles y no ser el único canal de información.
- Las figuras no deben exagerar diferencias mediante escalas injustificadas.
- Las tablas comparativas deben usar el mismo conjunto de evaluación y la misma
  definición de métrica.

### Notas y advertencias

Las notas aclaran contexto, variantes o detalles de implementación. Las advertencias se
reservan para riesgos reales: fuga de información, uso indebido del conjunto de prueba,
interpretación causal injustificada, dependencia costosa o resultado sensible a una
decisión. No deben reemplazar una corrección que pertenece al flujo principal.

### Ejercicios

Combinar preguntas de:

- comprensión conceptual;
- lectura de ecuaciones y correspondencia con código;
- modificación controlada de un ejemplo;
- elección de métrica o protocolo;
- interpretación de resultados y análisis de errores;
- crítica de supuestos, limitaciones y afirmaciones.

Cada ejercicio debe indicar el producto esperado. Los ejercicios guiados pueden incluir
pistas; los ejercicios autónomos no deben depender de información no presentada.

### Resúmenes y referencias cruzadas

El resumen debe recuperar decisiones, no repetir el índice. Las referencias cruzadas
deben indicar qué conocimiento se reutiliza y para qué: “la partición se definió en el
capítulo de evaluación” es más útil que “véase el capítulo anterior”. Usar etiquetas
estables de MyST cuando existan y comprobar que el destino esté publicado.

## Control de extensión y carga

La extensión se evalúa con cuatro medidas: tiempo de lectura, tiempo de ejecución, carga
conceptual y cantidad de decisiones que se pide tomar al estudiante.

Rangos orientativos para el recorrido principal:

| Medida | Núcleo recomendado | Señal para revisar o dividir |
|---|---:|---:|
| Lectura activa | 45–90 minutos | Más de 120 minutos |
| Ejecución en CPU | Hasta 10 minutos | Más de 20 minutos |
| Conceptos nuevos principales | 3–6 | Más de 8 |
| Familias de modelos o protocolos | 1–2 | Más de 3 sin una pregunta integradora |
| Ejercicios del recorrido básico | 3–6 | Más de 8 obligatorios |

Son rangos de planificación, no límites automáticos. Una ampliación puede permanecer en
el notebook si está claramente marcada como opcional, no altera el estado requerido
para celdas posteriores y declara tiempo, memoria y dependencias. Si una sección
opcional representa más de un tercio del tiempo total, requiere otro nivel o cambia la
pregunta principal, debe evaluarse como capítulo separado.

Un notebook puede resultar demasiado corto si exige menos de 20 minutos de lectura,
solo presenta una definición aislada y no contiene práctica, interpretación ni una
función curricular autónoma. En ese caso se recomienda integrarlo con el capítulo del
que sea prerrequisito o aplicación. No debe ampliarse con contenido de relleno: un
capítulo breve es válido si resuelve una necesidad concreta y completa.

## Coherencia curricular

- Introducir evaluación antes de usarla para comparar modelos.
- Reservar prueba para una estimación final; seleccionar con entrenamiento y validación
  o validación cruzada.
- Presentar regresión antes de regularización, clasificación probabilística antes de
  margen y redes después de pérdidas y gradientes.
- Distinguir modelos discriminativos de generativos cuando la comparación ayude a
  comprender qué distribución modela cada uno.
- Mantener casos propios —incluidos ejemplos econométricos y datos ecuatorianos— si su
  procedencia, licencia, pregunta y protocolo son reproducibles.
- Conservar K-medoides, DBSCAN y reglas de asociación como contenidos propios cuando su
  nivel y carácter complementario estén claros y no desplacen el núcleo.
- No agregar contenido avanzado si desplaza fundamentos, evaluación, regresión,
  clasificación o buenas prácticas.

## Decisiones que requieren aprobación antes de editar IntroML.ipynb

| Decisión material | Recomendación concreta |
|---|---|
| Extensión máxima | Diseñar un núcleo de 60–90 minutos de lectura y menos de 10 minutos de ejecución; trasladar validación anidada y visualizaciones exhaustivas a `Evaluacion.ipynb`. |
| Admoniciones MyST | Aprobar un repertorio reducido: nota, advertencia y actividad; usarlas solo cuando la semántica aporte más que un párrafo normal. |
| Soluciones de ejercicios | Mantener pistas breves en la versión pública y soluciones completas en un recurso separado, enlazado solo cuando la política del curso lo permita. |
| Versiones para estudiante y docente | Conservar una única fuente canónica; generar variantes únicamente mediante un proceso reproducible, no mantener dos notebooks editados a mano. |
| Nivel matemático objetivo | Aprobar nivel fundamental con álgebra elemental, esperanza y varianza; explicar pérdida y riesgo empírico sin exigir cálculo matricial. |
| Política de datos locales | Preferir datos empaquetados o generados con semilla; permitir URL estable solo con fuente, licencia, fecha, copia verificable o mecanismo de recuperación. |
| `statsmodels` frente a `scikit-learn` | Usar `statsmodels` cuando la pregunta sea inferencial y `scikit-learn` cuando sea predictiva; explicar la diferencia y evitar duplicar el mismo ejemplo sin propósito. |
| Idioma de términos técnicos | Adoptar el glosario de esta guía: español como término principal y equivalente inglés en la primera aparición cuando facilite consultar APIs o bibliografía. |
| Salidas guardadas | Conservar únicamente resultados pequeños, deterministas y pedagógicamente interpretados; eliminar trazas, errores y salidas voluminosas antes de publicar. |
| Numeración de secciones | Usar numeración continua solo si se acuerda para todo el libro; mientras tanto, preferir encabezados semánticos sin imitar números de otra obra. |
| Emojis e iconos | No usarlos como estructura editorial ni como único indicador; admitirlos excepcionalmente si existe una convención accesible aprobada para todo el libro. |

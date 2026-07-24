# Checklist de revisión de un notebook

## Uso

Aplicar esta lista a un notebook a la vez. Un ítem marcado **BLOQUEANTE** impide aprobar
o publicar el capítulo hasta corregirlo y verificarlo. Registrar aparte las decisiones
editoriales que requieran autorización.

## Alcance

- [ ] El propósito y el nivel del notebook están identificados.
- [ ] El cambio corresponde a la fase y a los archivos autorizados.
- [ ] Se revisaron las relaciones con capítulos anteriores y posteriores.
- [ ] Las secciones opcionales están separadas del recorrido principal.
- [ ] No se introdujeron contenidos, dependencias o datos fuera del alcance aprobado.
- [ ] **BLOQUEANTE:** no se modificaron accidentalmente otros notebooks ni archivos
  ajenos a la tarea.

## Estructura

- [ ] El título coincide con el papel del capítulo en el índice.
- [ ] La motivación presenta una pregunta o problema reconocible.
- [ ] Hay objetivos de aprendizaje observables.
- [ ] Los prerrequisitos y conexiones curriculares son explícitos.
- [ ] La secuencia avanza de intuición a formulación, código e interpretación.
- [ ] El núcleo puede recorrerse sin ejecutar una extensión opcional.
- [ ] El resumen recupera decisiones, resultados y limitaciones.
- [ ] La numeración de encabezados es continua o se omite de forma consistente.

## Contenido

- [ ] Se distingue descripción, asociación, inferencia, predicción y causalidad.
- [ ] Se explica por qué el método es relevante y cuándo no conviene usarlo.
- [ ] Los supuestos aparecen cerca del resultado que condicionan.
- [ ] El nivel de profundidad coincide con los prerrequisitos declarados.
- [ ] ISLP orienta secuencia, evaluación y aplicación sin copiar contenido.
- [ ] CS229 aporta notación, pérdidas, optimización o formulación donde corresponde.
- [ ] Los ejemplos propios se conservan cuando son correctos, pertinentes y
  reproducibles.
- [ ] No hay afirmaciones causales sin diseño o evidencia que las sustente.

## Matemática

- [ ] Todos los símbolos se definen en su primera aparición.
- [ ] Variables aleatorias, observaciones, vectores y matrices siguen la guía común.
- [ ] Parámetros, estimadores, predicciones, residuos, errores e hiperparámetros están
  diferenciados.
- [ ] La pérdida, el riesgo o el objetivo corresponden al método y a la implementación.
- [ ] Las dimensiones de productos matriciales son compatibles.
- [ ] Cada ecuación importante incluye lectura, interpretación y vínculo con el código.
- [ ] Las unidades se declaran cuando las variables las tienen.
- [ ] Todas las fórmulas usan delimitadores de signo de dólar compatibles con MyST.
- [ ] **BLOQUEANTE:** no hay fórmulas matemáticamente incorrectas ni símbolos que
  cambien de significado sin explicación.

## Código

- [ ] Las celdas tienen un propósito y un orden de dependencia claros.
- [ ] Las importaciones están agrupadas, vigentes y sin duplicados innecesarios.
- [ ] No hay importaciones con asterisco ni acceso a APIs privadas.
- [ ] Las funciones son pequeñas, reciben entradas y devuelven resultados.
- [ ] Los nombres de variables son descriptivos y consistentes.
- [ ] Los comentarios explican decisiones, no traducen la sintaxis línea por línea.
- [ ] Las semillas están centralizadas y se pasan a cada componente aleatorio.
- [ ] Los avisos se corrigen o se filtran localmente con justificación.
- [ ] Las extensiones opcionales no importan ni descargan recursos al estar desactivadas.
- [ ] **BLOQUEANTE:** el código no contiene errores de sintaxis o ejecución de arriba
  abajo en el entorno declarado.
- [ ] **BLOQUEANTE:** no hay una dependencia usada pero no declarada.
- [ ] **BLOQUEANTE:** no quedan salidas de error o trazas guardadas.

## Datos

- [ ] La fuente, licencia, fecha o versión y unidad de observación están documentadas.
- [ ] Se describen variables, unidades, faltantes y códigos especiales.
- [ ] Las rutas son relativas y se construyen con `pathlib`.
- [ ] Las URLs son estables o existe una alternativa de recuperación verificable.
- [ ] Los datos derivados conservan atribución y transformaciones.
- [ ] No hay credenciales, tokens, datos sensibles ni rutas personales.
- [ ] Los archivos de salida se escriben en una ubicación controlada sin sobrescribir
  entradas.
- [ ] **BLOQUEANTE:** ningún archivo o URL requerido es inexistente o inaccesible bajo
  las condiciones declaradas.
- [ ] **BLOQUEANTE:** ningún conjunto de datos carece de procedencia suficiente para su
  uso y redistribución.

## Evaluación

- [ ] Hay una línea base pertinente.
- [ ] La métrica principal responde a la pregunta y se elige antes de observar prueba.
- [ ] Las métricas secundarias tienen una función interpretativa explícita.
- [ ] La partición respeta clases, grupos, tiempo o espacio cuando corresponde.
- [ ] Los modelos comparados usan las mismas observaciones y métricas.
- [ ] Se reporta variabilidad o incertidumbre cuando es pertinente.
- [ ] Se realiza análisis de errores, no solo comparación de puntuaciones.
- [ ] El conjunto de prueba se usa una sola vez para la evaluación final.
- [ ] **BLOQUEANTE:** no hay fuga de información en preparación, selección,
  transformación o evaluación.
- [ ] **BLOQUEANTE:** el conjunto de prueba no se usa para seleccionar variables,
  hiperparámetros, umbrales, épocas ni modelos.

## Interpretación

- [ ] Cada tabla y figura recibe una lectura en el texto.
- [ ] Las métricas se traducen a consecuencias del problema.
- [ ] Los coeficientes, probabilidades, márgenes o importancias se interpretan según su
  definición.
- [ ] Se diferencia desempeño en muestra de generalización fuera de muestra.
- [ ] Las limitaciones de datos, diseño, modelo y métrica son explícitas.
- [ ] No se generaliza más allá de la población y el periodo observados sin justificación.

## Ejercicios

- [ ] Existe al menos un ejercicio que comprueba comprensión conceptual.
- [ ] Los ejercicios de código pueden resolverse con lo presentado.
- [ ] Hay preguntas de interpretación o crítica, no solo cambios de parámetros.
- [ ] El producto esperado y los datos necesarios están claros.
- [ ] Las pistas y soluciones siguen la política aprobada para el curso.
- [ ] Ningún ejercicio exige una dependencia opcional no declarada.

## Referencias

- [ ] Los métodos, datos, figuras adaptadas y APIs relevantes están citados.
- [ ] Las claves bibliográficas existen en `references.bib`.
- [ ] Las referencias cruzadas apuntan a destinos publicados y estables.
- [ ] Las fuentes son primarias o académicamente adecuadas cuando es posible.
- [ ] No se copiaron párrafos, figuras, tablas ni ejercicios de ISLP, CS229 u otra obra.

## Ejecución

- [ ] Se reinició el kernel antes de la prueba final.
- [ ] Se ejecutaron todas las celdas en orden, sin depender de estado previo.
- [ ] Las cuentas de ejecución siguen el orden de lectura.
- [ ] Los resultados aleatorios son repetibles dentro de las limitaciones declaradas.
- [ ] Se registraron tiempo, memoria, dispositivo y red para bloques costosos.
- [ ] El modo rápido permite recorrer el núcleo en los recursos previstos.
- [ ] Las salidas guardadas son pequeñas, necesarias e interpretadas.
- [ ] **BLOQUEANTE:** el notebook completo no termina con una ejecución limpia.

## MyST

- [ ] Los encabezados siguen una jerarquía sin saltos.
- [ ] El Markdown y las fórmulas se renderizan con la configuración actual.
- [ ] Las imágenes tienen rutas válidas y texto alternativo o descripción.
- [ ] Las tablas son legibles y no dependen de HTML específico del tema.
- [ ] Las admoniciones, citas y referencias cruzadas usan sintaxis MyST admitida.
- [ ] No hay delimitadores matemáticos basados en corchetes.
- [ ] Las secciones opcionales están claramente señaladas.

## Git

- [ ] `git status --short` contiene solo archivos autorizados.
- [ ] `git diff --name-only` confirma el alcance esperado.
- [ ] `git diff --check` no reporta espacios o marcadores problemáticos.
- [ ] El diff fue leído completo antes de confirmar cambios.
- [ ] No se incluyeron cachés, datos descargados, entornos ni artefactos de construcción.
- [ ] No se ejecutaron acciones de publicación fuera de la fase aprobada.
- [ ] **BLOQUEANTE:** no aparece ningún notebook o archivo ajeno modificado por accidente.

## Cierre

- [ ] Todos los bloqueantes están resueltos y verificados.
- [ ] Las decisiones pendientes están documentadas con recomendación y responsable.
- [ ] El notebook cumple las guías editorial, matemática y de código reproducible.

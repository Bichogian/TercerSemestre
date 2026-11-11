# Ingeniería de Software — FastResumen

Guía para obtener una primera visión de la materia y repasar después. El [resumen completo](Ing_Soft.md) desarrolla cada explicación y sus ejemplos. Cada clase reúne las ideas centrales, qué significan y cómo se aplican. Los ejemplos extensos, diagramas y fuentes quedan en el documento completo. **Incluye las clases 1 a 5 y 7; la clase 6 fue una evaluación.**

## Cómo leer este resumen

El recorrido es: **construir software → organizar el equipo → probar y entregar cambios → diseñar su estructura → comunicar sus partes → preparar y actualizar datos**. Leé cada clase preguntándote qué problema resuelve y cómo se aplica el ejemplo.

## Índice

- [Clase 1 · Fundamentos y Git](#clase-1)
- [Clase 2 · Metodologías, GitHub y Docker](#clase-2)
- [Clase 3 · DevOps, CI/CD e IA](#clase-3)
- [Clase 4 · Arquitectura y patrones](#clase-4)
- [Clase 5 · Redes y APIs](#clase-5)
- [Clase 6 · Evaluación](#clase-6)
- [Clase 7 · Ingeniería de datos y orquestación](#clase-7)
- [Herramientas y plataformas: para qué sirve cada una](#herramientas)
- [Cómo se conecta todo](#recorrido)

<a id="clase-1"></a>
## Clase 1 · Fundamentos y Git

### Qué estamos construyendo

**Ingeniería de software:** desarrollar y mantener sistemas que resuelvan una necesidad y puedan evolucionar. Incluye entender requisitos, diseñar, programar, probar, desplegar y mantener.

En IA, **el modelo es una parte del sistema**: también hacen falta datos, código, una forma de usar sus predicciones y monitoreo. Se conectan tres flujos: preparar datos, entrenar/evaluar modelos y construir/operar software.

**CRISP-ML(Q)** organiza ese trabajo desde la comprensión del negocio y los datos hasta el desarrollo y la operación del modelo. Se itera y se controla la calidad durante todo el proceso.

### Qué hace que el software sea bueno

| Concepto | Qué significa en la práctica |
|---|---|
| Aceptabilidad | Que sus usuarios puedan usarlo y encaje en su entorno. |
| Confiabilidad y seguridad | Que funcione de manera previsible y proteja datos y accesos. |
| Eficiencia | Que use razonablemente tiempo y recursos. |
| Mantenibilidad | Que corregirlo o ampliarlo sea viable. |

**Complejidad esencial:** viene del problema. **Accidental:** la agregamos con herramientas o diseños innecesariamente complicados. Se busca reducir la segunda.

El ciclo de vida conecta **requisitos → diseño → implementación → pruebas → despliegue → mantenimiento**. No se recorre necesariamente una sola vez: el feedback hace volver y mejorar.

### Principios para diseñar y cambiar código

- **KISS:** elegir una solución simple de entender.
- **YAGNI:** implementar lo necesario hoy; evitar funciones hipotéticas.
- **DRY:** mantener una regla en un lugar común, evitando duplicaciones que luego diverjan.
- **SOLID:** separar responsabilidades, permitir extensiones, respetar los contratos de los subtipos, ofrecer interfaces específicas y depender de abstracciones.

Ejemplo: separar el cálculo de una factura de su lectura desde JSON permite cambiar la entrada sin reescribir las cuentas.

**Deuda técnica** es el costo futuro de decisiones que dificultan cambios. **Refactorizar** mejora la estructura interna conservando el comportamiento observable; las pruebas ayudan a comprobarlo.

### Git: guardar y organizar cambios

Git conserva versiones del proyecto. Cada **commit** registra una versión; una **rama** permite trabajar en una línea de cambios; un **merge** integra líneas de trabajo.

```text
Editar archivos → git add → git commit → git push
                 preparar   guardar     publicar
                            localmente  en el remoto
```

| Acción | Para qué sirve |
|---|---|
| `git clone URL` | Obtener una copia local de un repositorio existente. |
| `git status` / `git diff` | Ver el estado y revisar los cambios antes de guardarlos. |
| `git switch -c nombre` | Crear una rama y empezar a trabajar en ella. |
| `git pull` | Traer e integrar cambios del remoto en la rama actual. |
| `git log` | Consultar el historial. |
| Tag | Marcar una versión concreta, por ejemplo `v1.0.0`. |

**Commit no equivale a push:** guardar localmente no publica. `.gitignore` evita agregar archivos no versionados, como temporales o secretos; no deja de seguir archivos ya incluidos.

**Idea de la práctica:** hacer un cambio pequeño, comprobarlo, guardarlo con un mensaje claro y compartirlo.

[Ampliar Clase 1](Ing_Soft.md#clase-1) · [Volver al índice](#índice)

<a id="clase-2"></a>
## Clase 2 · Metodologías, GitHub y Docker

Con Git podemos conservar cambios. Ahora necesitamos **organizar el trabajo del equipo y compartir un entorno de ejecución**.

### Cómo se organiza el desarrollo

| Enfoque | Idea principal |
|---|---|
| Waterfall | Avanzar por etapas planificadas. Los cambios tardíos pueden resultar costosos. |
| Agile | Entregar valor en ciclos cortos y ajustar con feedback. También requiere planificación y documentación. |
| Iterativo | Mejorar una solución mediante sucesivas revisiones. |
| Incremental | Agregar capacidades utilizables por partes. |

**Scrum** organiza el trabajo en *sprints*. El **Product Owner** ordena prioridades y valor; el **Scrum Master** facilita el proceso y ayuda a resolver impedimentos; los **Developers** construyen y verifican el producto.

- **Product Backlog:** necesidades ordenadas del producto.
- **Sprint Backlog:** objetivo y trabajo elegido para el sprint.
- **Incremento:** resultado utilizable que cumple los criterios de terminado.
- **Planning:** acordar el objetivo y el trabajo. **Daily:** coordinar el avance. **Review:** revisar el producto con interesados. **Retrospectiva:** mejorar la forma de trabajar.

Un tablero muestra pendientes, trabajo en curso y terminado. Limitar el **WIP** —trabajo simultáneo— ayuda a terminar tareas. Una retrospectiva mejora el proceso; un **postmortem sin culpas** estudia un incidente y propone medidas para evitar su repetición.

### GitHub: colaborar sobre el repositorio

**Git es el control de versiones; GitHub aloja repositorios y ofrece herramientas de colaboración.**

```text
Issue → rama → cambios y commits → push → Pull Request → revisión y tests → merge
```

Una **issue** describe una tarea o problema. Un **Pull Request (PR)** propone integrar cambios y permite discutirlos y revisarlos. El **merge** realiza la integración. Después, cada integrante actualiza su copia con `pull`.

**PR y pull son distintos:** uno propone una integración en GitHub; el otro actualiza una rama local desde el remoto.

Si hay un **conflicto**, se revisan ambas versiones, se escribe el resultado correcto, se eliminan las marcas, se prueba y se confirma la resolución. No se resuelve eligiendo automáticamente todo un lado.

**Gitflow** es una convención: `main` contiene versiones oficiales, `develop` integra trabajo y las ramas `feature`, `release` y `hotfix` separan funcionalidades, preparación de versiones y arreglos urgentes.

### Docker: ejecutar con un entorno definido

Docker empaqueta aplicación y dependencias para ejecutar el mismo entorno de manera reproducible.

| Elemento | Qué es y cómo se usa |
|---|---|
| Dockerfile | Receta para construir una imagen. `RUN` ejecuta pasos de construcción; `CMD` define el comando por defecto al iniciar. |
| Imagen | Plantilla con código y dependencias. Se pueden crear varios contenedores desde ella. |
| Contenedor | Instancia de una imagen que se ejecuta con su propio entorno. |
| Volumen | Almacenamiento administrado por Docker para conservar datos al eliminar un contenedor. |
| Bind mount | Vincula una ruta de la computadora con una del contenedor; útil para trabajar con archivos locales. |
| Docker Compose | Define y arranca varios servicios relacionados desde un archivo YAML. |

```bash
docker build -t mi-app .
docker run -p 8080:80 mi-app
```

El primer comando construye la imagen. El segundo crea y ejecuta un contenedor: **puerto 8080 de la computadora → puerto 80 del contenedor**. La aplicación debe estar escuchando allí.

En Compose, una aplicación puede conectarse a la base usando el nombre del servicio, por ejemplo `db`. **`localhost` dentro de un contenedor apunta a ese mismo contenedor.**

Para trabajar: definir la imagen, configurar puertos y datos persistentes, iniciar y consultar logs. Un `.env` guarda configuración, pero no la vuelve secreta. Iniciar un servicio antes que otro tampoco garantiza que ya esté listo para aceptar conexiones.

[Ampliar Clase 2](Ing_Soft.md#clase-2) · [Volver al índice](#índice)

<a id="clase-3"></a>
## Clase 3 · DevOps, CI/CD e IA

Con equipo y entorno organizados, el siguiente paso es **comprobar los cambios y llevarlos a producción de forma repetible**.

### DevOps y ambientes

**DevOps** combina responsabilidad compartida entre desarrollo y operaciones, automatización y feedback rápido. No se consigue solamente instalando una herramienta.

Los ambientes separan usos: **desarrollo** para construir, **testing/QA** para verificar, **staging** para validar en condiciones similares a producción y **producción** para usuarios reales.

**Team Topologies** distingue equipos orientados a valor del producto, equipos que ayudan a otros a adquirir capacidades, especialistas en subsistemas complejos y equipos de plataforma que ofrecen servicios internos reutilizables.

### CI/CD: qué se automatiza

| Concepto | Qué garantiza el proceso |
|---|---|
| Integración continua — CI | Integrar frecuentemente y comprobar automáticamente los cambios con construcción y pruebas. |
| Entrega continua — Continuous Delivery | Mantener una versión lista para desplegar; puede existir una aprobación manual. |
| Despliegue continuo — Continuous Deployment | Desplegar automáticamente a producción los cambios que pasan los controles. |

Un **pipeline** encadena tareas: obtener código → instalar dependencias → analizar → probar → empaquetar → desplegar, según el proyecto.

**GitHub Actions** ejecuta esos flujos. Un *workflow* se define en `.github/workflows/`; un **evento** lo dispara; contiene **jobs**, ejecutados en **runners**, y cada job tiene **steps**.

**Idea de la práctica:** un push o PR ejecuta los tests de una calculadora. Si una suma devuelve una resta, el test falla y avisa antes de integrar. Publicar un tag puede generar una **GitHub Release** con notas y archivos; eso, por sí solo, no despliega la aplicación.

### Qué comprobar

- **Tests unitarios:** una unidad pequeña, como una función de cálculo.
- **Tests de integración:** colaboración entre componentes, como API y almacenamiento.
- **Tests de sistema o interfaz:** recorridos completos; suelen ser más costosos.

La pirámide propone muchas pruebas pequeñas y rápidas, algunas de integración y menos recorridos completos. Un **linter** detecta problemas de código; un **formateador** uniforma el estilo; un analizador de seguridad busca patrones riesgosos. Los controles locales de *pre-commit* complementan la CI.

### Desplegar y habilitar cambios

**Desplegar** instala una versión. **Liberar una funcionalidad** la habilita para usuarios: una *feature flag* permite separar ambos momentos.

| Estrategia | Cómo funciona |
|---|---|
| Big bang | Cambiar toda la versión de una vez. |
| Rolling | Reemplazar instancias gradualmente. |
| Blue-green | Mantener dos entornos y cambiar el tráfico al nuevo. |
| Canary | Enviar una parte del tráfico a la nueva versión y observar. |

Una prueba **A/B** compara variantes del producto; un **dark launch** ejercita una función sin mostrar su resultado al usuario. La elección depende del riesgo, el costo y la posibilidad de volver atrás.

**Infraestructura como código** describe recursos mediante archivos versionados. **GitOps** usa Git como referencia del estado deseado y un proceso que aplica o reconcilia esa configuración.

### Trabajar con IA

El autocompletado sugiere código, el chat ayuda a razonar y un agente puede actuar sobre archivos y herramientas. Cuanto más puede hacer, más importante es delimitar el objetivo y revisar resultados.

**Spec Driven Development:** definir comportamiento, restricciones, ejemplos y criterios de aceptación antes de implementar.

Flujo útil: **especificar → aportar contexto → planificar → implementar → validar → integrar**. Hay que revisar que código y tests cumplan el requisito: ambos pueden coincidir en una interpretación equivocada.

[Ampliar Clase 3](Ing_Soft.md#clase-3) · [Volver al índice](#índice)

<a id="clase-4"></a>
## Clase 4 · Arquitectura y patrones

La automatización ayuda a entregar cambios. La arquitectura busca que **el sistema siga siendo comprensible y modificable al crecer**.

### Cómo organizar un sistema

**Arquitectura** es la estructura de componentes, sus relaciones y las decisiones importantes. Se elige según requisitos y restricciones: no hay una solución universal. Un **ADR** registra una decisión, su contexto y sus consecuencias.

**Cohesión alta:** cada módulo reúne responsabilidades relacionadas. **Acoplamiento bajo:** cambiar un módulo exige pocos cambios en otros.

Se puede dividir por **responsabilidad técnica** —interfaz, negocio, datos— o por **dominio** —ventas, pagos, envíos—. Separar módulos no obliga a distribuirlos en máquinas distintas.

| Organización | Cuándo aporta valor |
|---|---|
| Capas | Separar responsabilidades y ordenar dependencias. |
| Pipeline | Procesar datos mediante etapas sucesivas. |
| Microkernel | Conservar un núcleo estable y extenderlo con plugins. |
| Servicios | Exponer capacidades mediante contratos de comunicación. |
| Eventos | Reaccionar a hechos publicados sin que el emisor coordine cada reacción. |
| Microservicios | Dar autonomía de desarrollo, despliegue y datos a servicios delimitados por dominio. |

Distribuir introduce red, fallas parciales, coordinación y problemas de consistencia. En eventos, un **broker** distribuye mensajes; un **mediador** coordina explícitamente un flujo.

### Patrones de diseño: resolver problemas recurrentes

Actúan a una escala más pequeña que la arquitectura. Se agrupan en **creación**, **estructura** y **comportamiento**.

| Patrón | Problema que resuelve | Ejemplo breve |
|---|---|---|
| Singleton | Controlar una única instancia en un ámbito definido. | Un recurso compartido; cuidado con dependencias globales difíciles de probar. |
| Chain of Responsibility | Pasar una solicitud entre manejadores. | Aplicar reglas de impuestos; si son acumulativas, deben continuar los manejadores correspondientes. |
| State | Cambiar comportamiento según el estado de un objeto. | Una factura en borrador permite cambios; publicada, tiene otras reglas. |
| Strategy | Intercambiar una política mediante un mismo contrato. | Elegir una regla de descuento sin modificar el calculador. |
| Template Method | Mantener un algoritmo común y variar ciertos pasos en subclases. | Un proceso de generación con pasos particulares para cada formato. |

**Strategy usa composición**: se entrega una política al objeto. **Template Method usa herencia**: una subclase redefine pasos.

### Aplicación en la práctica de facturación

Separar **entrada JSON → cálculo de negocio → salida**. El cálculo recibe políticas de descuentos e impuestos y se prueba sin depender de archivos ni de una interfaz.

La cuenta base es **total = subtotal − descuentos + impuestos**. Se debe explicitar sobre qué monto se calcula cada porcentaje y cómo se redondea. Si corresponden dos impuestos, no hay que detener la cadena después del primero.

### Comunicar y medir

**DDD** organiza el modelo alrededor del negocio y delimita contextos donde los conceptos tienen un significado preciso. **C4** permite explicar el sistema con distintos niveles de detalle: contexto, contenedores, componentes y código. Un contenedor de C4 es una aplicación o almacén de datos; no significa necesariamente Docker.

**MTBF:** tiempo medio de funcionamiento entre fallas. **MTTF:** tiempo medio hasta la falla. **MTTR:** tiempo medio de reparación o recuperación, según la definición usada; hay que aclarar qué intervalo mide.

Las métricas **DORA** relacionan velocidad y estabilidad: frecuencia de despliegue, tiempo de entrega de cambios, proporción de cambios fallidos y tiempo de restauración. Sirven para mejorar el sistema de trabajo, no para contar productividad individual.

[Ampliar Clase 4](Ing_Soft.md#clase-4) · [Volver al índice](#índice)

<a id="clase-5"></a>
## Clase 5 · Redes y APIs

Cuando los componentes se comunican por red, necesitamos entender **cómo llega un pedido, qué puede fallar y cómo se protege**.

### Dirección, transporte y protocolos

La pila **TCP/IP** separa aplicación —HTTP, DNS—, transporte —TCP, UDP—, internet —IP— y acceso a red —Ethernet, Wi-Fi—. OSI describe esa comunicación en siete capas. Cada capa agrega información para transportar los datos: **encapsulación**.

| Concepto | Qué identifica o hace |
|---|---|
| IP | Una dirección de una interfaz en la red. |
| Puerto | Un punto de comunicación del transporte asociado a un servicio o proceso. |
| Socket | Un extremo de comunicación que usa un programa. |
| DNS | Resuelve nombres y otros datos; permite obtener direcciones IP a partir de dominios. |
| TCP | Ofrece un flujo de bytes ordenado y confiable mediante controles y retransmisiones. La conexión puede fallar. |
| UDP | Envía datagramas sin garantizar entrega ni orden. |
| SMTP | Transfiere correo electrónico. |

En `http://localhost:8000/files`, `http` es el esquema, `localhost` el host, `8000` el puerto y `/files` la ruta del recurso. **`localhost` siempre refiere al propio entorno.** Escuchar en `0.0.0.0` permite recibir conexiones por las interfaces IPv4 disponibles; no es la dirección habitual para navegar.

### HTTP y el contrato de una API

Una **API** define cómo interactuar con un sistema. En HTTP, el cliente envía método, ruta, encabezados y, cuando corresponde, cuerpo; el servidor responde con estado, encabezados y cuerpo.

- **GET:** consultar. **POST:** enviar datos para procesar o crear. **PUT:** reemplazar un recurso. **DELETE:** eliminar.
- **2xx:** éxito. **4xx:** problemas relacionados con la solicitud, como un recurso inexistente. **5xx:** errores del servidor.
- **Content-Type:** formato enviado. **Accept:** formatos que el cliente acepta recibir.

**HTTPS** protege HTTP con TLS: cifra la comunicación, preserva su integridad y permite verificar la identidad del servidor mediante certificados. La aplicación todavía debe controlar quién puede acceder a cada recurso.

Recorrido típico: **resolver el nombre → establecer comunicación → negociar TLS si corresponde → enviar HTTP → procesar → responder**.

### Rendimiento, fallas y diagnóstico

**Latencia** es demora; **RTT**, tiempo de ida y vuelta; **ancho de banda**, capacidad del enlace; **throughput**, transferencia efectiva; **jitter**, variación de la demora.

Un *timeout* significa que no llegó respuesta a tiempo: la operación pudo haberse realizado. Reintentar una creación sin control puede duplicarla. Un ACK de TCP confirma recepción de bytes, no que el negocio haya terminado correctamente.

Para investigar: `ping` comprueba respuesta ICMP, `traceroute` observa saltos, `nslookup` consulta DNS y `curl` prueba HTTP. **Wireshark** inspecciona capturas PCAP; permite ver protocolos, direcciones y tiempos. Con TLS, el contenido de la aplicación está cifrado.

**SSH** permite acceso remoto seguro; una **VPN** crea un túnel protegido. Ninguno reemplaza los permisos de la aplicación.

### Práctica: API de archivos

**FastAPI** define las rutas y sus contratos en Python; **Pydantic** valida datos; **Uvicorn** ejecuta la aplicación como servidor ASGI.

| Operación | Función |
|---|---|
| `GET /files` | Listar archivos. |
| `POST /files` | Crear un archivo con nombre y contenido según el contrato definido. |
| `GET /files/{name}` | Leer un archivo. |

El trabajo consiste en definir entradas y errores, validar nombres y rutas, probar las operaciones y conservar los archivos. JSON y subida multipart son contratos diferentes: cliente y servidor deben coincidir.

Después se empaqueta con Docker y se monta almacenamiento persistente. **Recrear el contenedor** permite comprobar la persistencia. Para publicar el puerto se usa `-p`; `EXPOSE` por sí solo no lo publica.

**Render** puede alojar la API: obtiene el proyecto y ejecuta sus comandos de construcción e inicio. Los archivos que deban sobrevivir requieren almacenamiento persistente configurado.

[Ampliar Clase 5](Ing_Soft.md#clase-5) · [Volver al índice](#índice)

<a id="clase-6"></a>
## Clase 6 · Evaluación

La clase 6 fue una **evaluación**. No hay una clase teórica faltante para resumir; se conserva la numeración original.

<a id="clase-7"></a>
## Clase 7 · Ingeniería de datos y orquestación

**Idea central:** convertir datos dispersos en información útil y mantener ese proceso funcionando.

**Ejemplo que une la clase:** una empresa quiere ver cada mañana cuánto vendió ayer en cada sucursal. Para conseguirlo hay que traer las ventas, corregir formatos, quitar duplicados, sumar importes y publicar el reporte. Ese proceso debe repetirse y permitir detectar fallas.

### Del dato al producto

La **ingeniería de datos** permite capturar, mover, almacenar, transformar y servir datos. Un **producto de datos** resuelve una necesidad mediante una tabla, reporte, API, dashboard o modelo, con usuarios, continuidad, documentación y expectativas de calidad.

Debe ser descubrible, comprensible, accesible, confiable, interoperable y seguro. Tener datos guardados no garantiza que alguien pueda utilizarlos correctamente.

**Trabajar hacia atrás:** primero definir qué decisión se quiere tomar; después, qué datos hacen falta y con qué calidad y frescura. Se equilibran **costo, velocidad y precisión**. Un informe mensual y una alerta de fraude no necesitan la misma arquitectura.

| Nivel de análisis | Pregunta |
|---|---|
| Descriptivo | ¿Qué ocurrió? |
| Diagnóstico | ¿Por qué ocurrió? |
| Predictivo | ¿Qué podría ocurrir? |
| Prescriptivo | ¿Qué conviene hacer? |

### Qué características de los datos importan

Las **cinco V** ayudan a elegir cómo trabajar:

| Característica | Pregunta sencilla |
|---|---|
| Volumen | ¿Cuántos datos hay? |
| Velocidad | ¿Con qué ritmo llegan y cuán pronto deben estar disponibles? |
| Variedad | ¿De cuántas fuentes y formatos vienen? |
| Veracidad | ¿Podemos confiar en su calidad? |
| Valor | ¿Para qué decisión sirven? |

### Cómo llegan y cómo están organizados

- **Batch:** procesar lotes periódicos, como ventas de cada noche.
- **Streaming:** procesar eventos continuamente para reducir demora; no implica latencia cero.

El **esquema** define campos, tipos y reglas de los datos. Según su organización:

- **Estructurados:** esquema regular, como una tabla de ventas.
- **Semiestructurados:** estructura flexible, como JSON.
- **No estructurados:** imágenes o texto sin un esquema tabular directo para el análisis.

### Qué hacemos con los datos

El recorrido es **generación → ingesta → almacenamiento → transformación → consumo**. En el ejemplo: registrar la venta → traerla desde la sucursal → guardarla → limpiar y sumar → consultar el reporte. Calidad, gobierno y protección de datos atraviesan todas las etapas.

El Data Engineer prepara el movimiento y disponibilidad; el Analytics Engineer modela datos analíticos y su semántica; el analista interpreta y comunica; Data Science/ML desarrolla modelos; el Data Product Manager prioriza necesidades y valor. Los roles pueden superponerse.

### Operar el negocio y analizarlo

**OLTP** es procesamiento de transacciones: registra y consulta operaciones individuales. **OLAP** es procesamiento analítico: cruza y resume datos para responder preguntas.

**Para recordarlo:** la caja registra una venta mediante OLTP; el informe compara miles de ventas mediante OLAP.

### Dónde se guardan los datos para analizarlos

| Concepto | Idea central |
|---|---|
| Data warehouse | Datos preparados y modelados para análisis. |
| Data mart | Datos analíticos centrados en un área del negocio. |
| Data lake | Datos de múltiples formatos a escala, incluidos datos crudos. |
| Data lakehouse | Flexibilidad del lake con capacidades de gestión y análisis del warehouse. |

**OLTP/OLAP describen usos y cargas de trabajo; no se definen solo por tamaño.** Lake y warehouse pueden coexistir. Guardar datos crudos no garantiza calidad ni facilidad de consulta.

### ETL y ELT: cuándo se transforman los datos

**Extraer** es obtener los datos; **transformar** es prepararlos; **cargar** es guardarlos en el destino elegido.

| Flujo | Orden | Ejemplo de ventas |
|---|---|---|
| ETL | Extraer → transformar → cargar. | Leer archivos, limpiar y sumar, guardar el resultado. |
| ELT | Extraer → cargar → transformar. | Leer archivos, guardarlos en el destino, limpiar y sumar allí. |

Ambos transforman datos. Cambia **si esa preparación ocurre antes o después de la carga**.

Una plataforma conecta fuentes, ingesta, almacenamiento, transformaciones y consumo. Necesita infraestructura, gobierno, calidad y orquestación, además de herramientas.

### Orquestación y DAGs

Un **pipeline** organiza etapas de procesamiento. La **orquestación** coordina cuándo se ejecutan, de qué dependen y cómo se observa su resultado.

Un **DAG** es un grafo dirigido sin ciclos: las tareas son nodos y las dependencias son flechas.

```text
extraer_ventas ────┐
                  ├──> transformar → validar → publicar
extraer_clientes ─┘
```

Las extracciones pueden ejecutarse en paralelo si hay recursos; transformar espera ambas. Correr el mismo DAG todos los días genera nuevas ejecuciones y no crea un ciclo en el grafo.

- **Idempotencia:** repetir una operación mantiene el efecto final previsto; por ejemplo, cargar dos veces las mismas 100 ventas y terminar con 100 registros, no 200.
- **Reintentos con backoff:** volver a intentar fallas transitorias con esperas crecientes.
- **Observabilidad:** estados, logs, tiempos y controles sobre los datos producidos.

**Reintentar no evita duplicados por sí mismo.** Y que una tarea termine en éxito no garantiza que sus datos sean correctos.

### Airflow y la práctica

**Airflow** permite definir flujos de trabajo (*workflows*) en Python y coordinar sus ejecuciones. El **scheduler** programa las tareas y los **workers** las ejecutan. La **UI** es la interfaz visual; los **logs** son registros de lo ocurrido. La base de metadatos conserva información de las ejecuciones, como sus estados.

**DAG** es el plan «preparar el reporte diario». Una **ejecución del DAG** es aplicar ese plan a una corrida concreta, por ejemplo la de las ventas del lunes. Una **instancia de tarea** es un paso dentro de esa corrida, como validar esas ventas.

La práctica pide instalar y explorar Airflow, recrear el tutorial y observar sus ejecuciones:

1. Preparar un entorno virtual y seguir la documentación de una misma versión. En Windows, usar WSL según la consigna.
2. Comprobar `airflow version`, iniciar con `airflow standalone` y acceder a `http://localhost:8080` con las credenciales indicadas por la terminal.
3. Crear el archivo del tutorial en la carpeta de DAGs activa. Cambiar **nombre del archivo e identificador del DAG** para distinguirlo del ejemplo incluido.
4. Verificar que aparezca, ejecutar y revisar grafo, estados y logs; modificar y observar el resultado.

El tutorial coordina tareas didácticas; no construye todavía un producto de datos completo. Esta es una guía de estudio: la instalación y las ejecuciones no se realizaron al actualizar los apuntes.

**CI/CD comprueba y entrega cambios del código; Airflow coordina sus corridas sobre datos.** Ambos automatizan procesos, pero actúan en momentos diferentes.

### Comprobá que lo entendiste

- **¿Qué recibe el usuario?** Un producto de datos, como el reporte de ventas.
- **¿Qué lo produce?** Un pipeline con tareas de extracción, preparación y validación.
- **¿Qué representa el DAG?** Las tareas y sus dependencias.
- **¿Qué hace Airflow?** Coordina las ejecuciones y permite observar qué ocurrió.
- **¿Por qué importa la idempotencia?** Permite repetir trabajo sin duplicar su efecto.

[Ampliar Clase 7 y práctica](Ing_Soft.md#clase-7) · [Volver al índice](#índice)

<a id="herramientas"></a>
## Herramientas y plataformas: para qué sirve cada una

| Herramienta | Para qué la usaría |
|---|---|
| **Git** | Guardar versiones, crear ramas e integrar cambios. |
| **GitHub** | Compartir el repositorio, gestionar issues y revisar PRs. |
| **GitHub Actions** | Automatizar pruebas, empaquetado, releases o despliegues que configure. |
| **Docker** | Construir imágenes y ejecutar aplicaciones en contenedores. |
| **Docker Compose** | Coordinar varios contenedores, sus redes, configuración y volúmenes. |
| **FastAPI** | Programar una API HTTP en Python. |
| **Pydantic** | Definir y validar la estructura de los datos. |
| **Uvicorn** | Servir la aplicación ASGI y atender conexiones. |
| **Render** | Alojar y ejecutar una aplicación accesible por red. |
| **Apache Airflow** | Coordinar DAGs, programar tareas y observar sus ejecuciones. |
| **dbt** | Organizar transformaciones analíticas y sus comprobaciones. |
| **Wireshark** | Inspeccionar tráfico de red para entenderlo o diagnosticarlo. |
| **Jira / Trello / GitHub Projects** | Organizar tareas, prioridades y estados del trabajo. |

<a id="recorrido"></a>
## Cómo se conecta todo

1. **Entender y diseñar:** definir requisitos y elegir responsabilidades, arquitectura y patrones.
2. **Organizar y construir:** priorizar tareas, trabajar en ramas y revisar cambios mediante PRs.
3. **Comprobar:** ejecutar pruebas y análisis con CI.
4. **Empaquetar y entregar:** construir una imagen Docker y desplegarla en un entorno de ejecución.
5. **Preparar productos de datos:** conectar fuentes, definir transformaciones y validar calidad para el consumo.
6. **Operar y aprender:** atender pedidos por red, orquestar actualizaciones, observar errores y rendimiento y ajustar el sistema.

Ejemplo: para agregar un descuento a una API de facturas, se define la regla, se implementa como política, se prueba, se revisa el PR, pasa la CI y se despliega la nueva versión. Git conserva el cambio; GitHub organiza su revisión; Actions automatiza controles; Docker prepara el entorno; el servidor ejecuta la API. Si se necesita un reporte diario de facturación, un pipeline extrae las operaciones, las transforma y valida, y publica el resultado. Airflow coordina esas tareas; la CI comprueba los cambios del código que las define.

[Volver al índice](#índice)

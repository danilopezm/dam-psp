---
unit_title: "Unidad 1. Programación de Servicios y Procesos."
---
[Volver a Inicio](../README.md)

## Indice

1. [CONCEPTOS BÁSICOS](#1-conceptos-básicos)
2. [FORMAS DE EJECUCIÓN](#2-formas-de-ejecución)
3. [KERNEL Y LLAMADAS AL SISTEMA](#3-kernel-y-llamadas-al-sistema)
4. [ESTADOS DE UN PROCESO](#4-estados-de-un-proceso)
5. [COLAS DE PROCESOS](#5-colas-de-procesos)
6. [PLANIFICACIÓN](#6-planificación)
7. [CAMBIO DE CONTEXTO](#7-cambio-de-contexto)
8. [GESTIÓN DE PROCESOS](#8-gestión-de-procesos)
9. [PROCESOS EN JAVA](#9-procesos-en-java)
10. [ENTRADA, SALIDA Y STREAMS](#10-entrada-salida-y-streams)
11. [COMUNICACIÓN Y SINCRONIZACIÓN](#11-comunicación-y-sincronización)
12. [PROGRAMACIÓN MULTIPROCESO](#12-programación-multiproceso)
13. [MAPA CONCEPTUAL](#13-mapa-conceptual)
14. [IDEAS CLAVE](#14-ideas-clave)

## 1. CONCEPTOS BÁSICOS

### 1.1. PROGRAMA

Un **programa** es toda la información —código y datos— almacenada en disco que permite resolver una necesidad concreta de los usuarios.

- Es un elemento pasivo: no se está ejecutando.
- Puede convertirse en un proceso cuando el sistema operativo lo carga y lo ejecuta.

### 1.2. PROCESO

Un **proceso** es un programa que se encuentra en ejecución.

Además del código y los datos, un proceso incluye:

- Contador de programa.
- Imagen de memoria.
- Estado del procesador.
- Información necesaria para controlar su ejecución.

### 1.3. EJECUTABLE

Un **ejecutable** es un fichero que contiene la información necesaria para crear un proceso a partir de un programa almacenado.

### 1.4. DEMONIO

Un **demonio** es un proceso no interactivo que se ejecuta continuamente en segundo plano.

- Suele proporcionar servicios básicos al resto de procesos.
- No requiere interacción directa del usuario.

### 1.5. SISTEMA OPERATIVO

El **sistema operativo** actúa como intermediario entre el usuario, las aplicaciones y el hardware.

Sus funciones principales son:

- Proporcionar una interfaz para utilizar los recursos del ordenador.
- Gestionar los recursos de forma eficiente.
- Ejecutar programas de usuario.
- Administrar procesos, memoria, dispositivos y comunicaciones.

#### 📝 Actividades

> **Actividad 1. Programa vs proceso**.  
> 
> Elabora una tabla comparativa entre *programa* y *proceso*. Incluye al menos tres diferencias clave (por ejemplo: ubicación, estado, elementos que lo componen, etc.).

> **Actividad 2. Servicios en segundo plano**.  
> 
> Investiga qué es un demonio o servicio en segundo plano en tu sistema operativo (Windows, Linux o macOS). Elige un ejemplo concreto, describe brevemente qué función realiza y explica por qué es importante que esté siempre en ejecución.

---

## 2. FORMAS DE EJECUCIÓN

### 2.1. MULTIPROGRAMACIÓN

La **multiprogramación** permite que varios programas parezcan ejecutarse a la vez en un único procesador.

- Solo un proceso utiliza realmente la CPU en cada instante.
- El sistema operativo cambia rápidamente de un proceso a otro.
- El usuario percibe una ejecución simultánea.
- No mejora necesariamente el tiempo total de ejecución de un programa.

### 2.2. PROGRAMACIÓN CONCURRENTE

La **programación concurrente** consiste en alternar procesos en la CPU.

- Varios procesos progresan de forma aparentemente simultánea.
- El sistema operativo decide cuándo se intercambian.
- Es útil cuando algunos procesos deben esperar operaciones de entrada/salida.

### 2.3. PROGRAMACIÓN PARALELA

La **programación paralela** permite ejecutar varias instrucciones de forma real y simultánea.

- Requiere varios núcleos o procesadores.
- Puede mejorar el rendimiento de un programa.
- Los núcleos de un mismo procesador suelen compartir memoria.

### 2.4. PROGRAMACIÓN DISTRIBUIDA

La **programación distribuida** utiliza varios ordenadores conectados mediante una red.

- Cada ordenador posee su propia CPU y memoria.
- Permite aprovechar un gran número de recursos de forma paralela.
- La comunicación entre procesos es más costosa y compleja porque se realiza a través de la red.

#### 📝 Actividades

> **Actividad 3. Concurrencia en la vida cotidiana**.  
> 
> Describe dos situaciones de tu día a día en las que realices varias tareas alternándolas (no realmente a la vez). Explica cómo se relacionan con el concepto de *programación concurrente*.

> **Actividad 4. Paralelismo y núcleos**.  
> 
> Investiga cuántos núcleos tiene tu procesador. Busca un ejemplo de tarea informática que se beneficie claramente del paralelismo (varios núcleos trabajando a la vez) y explica por qué esa tarea mejora su rendimiento al ejecutarse en paralelo.

[Volver a Inicio](../README.md)

---

## 3. KERNEL Y LLAMADAS AL SISTEMA

### 3.1. KERNEL

El **kernel** es la parte central del sistema operativo.

Sus responsabilidades principales son:

- Gestionar los recursos del ordenador.
- Controlar la ejecución de los procesos.
- Atender llamadas al sistema.
- Permitir un acceso controlado al hardware.

El kernel funciona mediante **interrupciones**:

1. Se produce una interrupción.
2. El control pasa a la rutina que trata esa interrupción.
3. Durante su tratamiento se deshabilitan nuevas interrupciones.
4. Al finalizar, se reanuda el proceso en el punto donde se interrumpió.

### 3.2. LLAMADAS AL SISTEMA

Las **llamadas al sistema** son la interfaz entre los programas de usuario y el kernel.

Permiten realizar operaciones protegidas, como:

- Crear o finalizar procesos.
- Acceder a dispositivos.
- Gestionar archivos.
- Solicitar memoria.

### 3.3. MODO DUAL

El procesador dispone de dos modos de funcionamiento:

| Modo | Descripción |
|---|---|
| **Modo kernel** | También llamado modo supervisor o privilegiado. Permite operaciones protegidas del sistema operativo. |
| **Modo usuario** | Se utiliza para ejecutar programas de usuario con restricciones de seguridad. |

#### 📝 Actividades

> **Actividad 5. El kernel y sus funciones**.
> 
> Explica con tus propias palabras qué es el kernel de un sistema operativo y describe sus funciones principales (gestión de recursos, control de procesos, llamadas al sistema y acceso al hardware).

> **Actividad 6. Llamadas al sistema**.  
> 
> Investiga el nombre de al menos dos llamadas al sistema relacionadas con procesos (por ejemplo, en Linux o en documentación general). Para cada una, indica su nombre y describe brevemente qué acción realiza (crear proceso, terminar proceso, etc.).

---

## 4. ESTADOS DE UN PROCESO

Un proceso puede cambiar de estado durante su ejecución.

| Estado | Descripción |
|---|---|
| **Nuevo** | El proceso está siendo creado desde un fichero ejecutable. |
| **Listo** | Está preparado para ejecutarse, pero todavía no tiene asignada la CPU. |
| **En ejecución** | Está utilizando el procesador. |
| **Bloqueado** | Está esperando un evento, como una operación de entrada/salida. |
| **Terminado** | Ha finalizado y libera los recursos asignados. |

### Diagrama de estados

```text
                          ┌──────────────┐
                          │    Nuevo     │
                          └──────┬───────┘
                                 │ Creación
                                 ▼
                          ┌──────────────┐
                    ┌─────│    Listo     │◄────────────────┐
                    │     └──────┬───────┘                 │
                    │            │ Planificación           │ Interrupción
                    │            ▼                         │
                    │     ┌──────────────┐                 │
                    │     │ En ejecución │─────────────────┘
                    │     └───┬──────┬───┘      
                    │         │      │
                    │     E/S │      │ Finalización/Excepción
                    │         ▼      ▼
                    │  ┌──────────┐ ┌────────────┐
                    │  │Bloqueado │ │ Terminado  │
                    │  └────┬─────┘ └────────────┘
                    │       │
                    │       │ Evento recibido
                    └───────┘
```

#### 📝 Actividades

> **Actividad 7. Identificación de estados**.  
> 
> Lee los siguientes casos e indica en qué estado se encontraría el proceso en cada situación:
> - Un programa que está esperando a que el usuario pulse una tecla.  
> - Un programa que está calculando una operación en este instante.  
> - Un programa que ha finalizado y ha cerrado su ventana.  
> - Un programa que está cargado en memoria pero aún no ha recibido tiempo de CPU.

[Volver a Inicio](../README.md)

---

## 5. COLAS DE PROCESOS

El sistema operativo organiza los procesos en distintas colas:

| Cola | Contenido |
|---|---|
| **Cola de procesos** | Todos los procesos existentes en el sistema. |
| **Cola de preparados** | Procesos listos que esperan para utilizar la CPU. |
| **Cola de dispositivo** | Procesos que esperan una operación de entrada/salida en un dispositivo concreto. |

#### 📝 Actividades

> **Actividad 8. Diseñar una política de cola**.  
> 
> Imagina que eres el sistema operativo y tienes tres procesos: uno de alarma (muy prioritario), uno de usuario (prioridad media) y una copia de seguridad (prioridad baja). Describe cómo organizarías las colas y en qué orden atenderías cada proceso, justificando tu decisión.

---

## 6. PLANIFICACIÓN

### 6.1. PLANIFICACIÓN A CORTO PLAZO

El planificador de corto plazo:

- Selecciona qué proceso preparado pasa a ejecución.
- Se activa con mucha frecuencia, normalmente cada pocos milisegundos.
- Debe tomar decisiones rápidas.
- Utiliza algoritmos de planificación eficientes.

### 6.2. PLANIFICACIÓN A LARGO PLAZO

El planificador de largo plazo:

- Decide qué procesos nuevos pasan a la cola de preparados.
- Se ejecuta con menos frecuencia.
- Controla el grado de multiprogramación.
- Regula el número de procesos cargados en memoria.

### 6.3. TIPOS DE PLANIFICACIÓN

| Tipo | Funcionamiento |
|---|---|
| **Sin desalojo** | El proceso conserva la CPU hasta que termina o se bloquea. |
| **Apropiativa** | El sistema operativo puede retirar la CPU a un proceso si aparece otro de mayor prioridad. |
| **Tiempo compartido** | Cada proceso usa la CPU durante un intervalo llamado *cuanto* y después se selecciona otro. |

#### 📝 Actividades

> **Actividad 9. Verdadero o falso**.
> 
> Indica si las siguientes afirmaciones son verdaderas (V) o falsas (F).  
> Cuando sea falsa, corrígela brevemente en una línea.
> 
> A) El planificador de corto plazo selecciona qué proceso de la cola de preparados pasa a ejecución.  
> B) El planificador de largo plazo se activa cada pocos milisegundos para decidir qué proceso se ejecuta ahora.  
> C) El planificador de largo plazo controla el grado de multiprogramación regulando cuántos procesos hay cargados en memoria.  
> D) En la planificación sin desalojo, el sistema operativo puede quitar la CPU a un proceso si llega otro de mayor prioridad.  
> E) En la planificación apropiativa, el sistema operativo puede retirar la CPU a un proceso antes de que termine.  
> F) En la planificación por tiempo compartido, cada proceso usa la CPU durante un intervalo llamado *cuanto* antes de ceder el turno a otro proceso.

[Volver a Inicio](../README.md)

---

## 7. CAMBIO DE CONTEXTO

Un **cambio de contexto** se produce cuando el procesador interrumpe temporalmente la ejecución de un proceso para ejecutar otro.

Para realizar este cambio, el sistema operativo:

1. Guarda la información necesaria para continuar posteriormente el proceso actual.
2. Decide qué proceso se ejecutará a continuación.
3. Carga la información que tenía guardada del nuevo proceso.
4. Hace que el nuevo proceso continúe desde el punto en el que se había detenido.

El contexto incluye principalmente:

- El estado del proceso: indica si está preparado, en ejecución, bloqueado o terminado.
- El estado del procesador: contiene información como la siguiente instrucción que debe ejecutarse y los valores de los registros.
- La información de gestión de memoria: indica qué espacio de memoria utiliza el proceso y cómo está organizado.

> El cambio de contexto consume tiempo. Durante ese periodo, el procesador no realiza trabajo útil para los procesos de usuario.

#### 📝 Actividades

> **Actividad 10. Representación del cambio de contexto**.  
> 
> Dibuja un diagrama que represente el proceso de cambio de contexto.

---

## 8. GESTIÓN DE PROCESOS

### 8.1. CREACIÓN DE PROCESOS

Un proceso puede solicitar al sistema operativo la creación de otro proceso.

- El proceso que solicita la creación se denomina **proceso padre**.
- El proceso creado se denomina **proceso hijo** o subproceso.
- El padre y el hijo pueden ejecutarse de forma concurrente.
- Cada proceso tiene su propio espacio de memoria, aunque puede heredar algunos recursos o información del proceso padre.
- Un proceso hijo también puede crear nuevos procesos, formando una estructura jerárquica o **árbol de procesos**.

### 8.2. TERMINACIÓN DE PROCESOS

Un proceso termina cuando finaliza su trabajo o cuando se produce algún error que obliga a detenerlo.

Cuando termina un proceso:
- El sistema operativo libera los recursos que tenía asignados, como memoria, archivos y otros recursos.
- El proceso puede comunicar al sistema operativo un código de finalización.
- El proceso padre puede recibir información sobre el resultado de la terminación del proceso hijo.
- En muchos sistemas, la operación utilizada para indicar una terminación normal se denomina `exit`.

### 8.3. TERMINACIÓN FORZADA

Un proceso puede ser terminado antes de completar su ejecución. Esta terminación puede ser solicitada por el sistema operativo, por el usuario o por otro proceso con los permisos necesarios.

En Java, si se ha creado un proceso mediante `ProcessBuilder` o `Runtime.exec()`, se puede solicitar su terminación con:

```java
process.destroy();
```

Este método solicita la terminación del subproceso representado por el objeto `Process`. Después, se pueden utilizar métodos como `isAlive()`  o `waitFor()` para comprobar si realmente ha terminado. La documentación de Java describe `destroy()` como una operación que termina forzosamente el subproceso representado por `Process`.

[Volver a Inicio](../README.md)

---

## 9. PROCESOS EN JAVA

En Java, la clase `Process` representa un proceso creado en el sistema operativo.

### 9.1. ProcessBuilder

`ProcessBuilder` permite configurar y lanzar un proceso externo.

```java
ProcessBuilder pb = new ProcessBuilder("programa", "argumento");
Process proceso = pb.start();
```

Características:

- `start()` inicia el proceso.
- `command()` define el comando y sus argumentos.
- `directory()` permite establecer el directorio de trabajo.
- `environment()` permite consultar o modificar las variables de entorno.

### 9.2. Runtime.exec()

La clase `Runtime` también permite ejecutar comandos del sistema.

```java
Runtime runtime = Runtime.getRuntime();
Process proceso = runtime.exec("programa");
```

Puede recibir:

- Comando.
- Argumentos.
- Variables de entorno.
- Directorio de trabajo.

### 9.3. ESPERAR AL PROCESO HIJO

El método `waitFor()` bloquea el proceso padre hasta que termina el proceso hijo.

```java
int codigoRetorno = proceso.waitFor();
```

- Devuelve un código entero.
- Por convenio, `0` suele indicar que el proceso ha terminado correctamente.
- El código de retorno no representa los mensajes transmitidos mediante streams.

#### 📝 Actividades

> **Actividad 11. Predicción de comportamiento**.  
> 
> A partir del siguiente fragmento de código:  
> ```java
> ProcessBuilder pb = new ProcessBuilder("notepad");
> Process proceso = pb.start();
> int codigo = proceso.waitFor();
> System.out.println("Terminó con código: " + codigo);
> ```  
> Responde:  
> - ¿Qué ocurre cuando se ejecuta `start()`?  
> - ¿En qué momento se muestra el mensaje por pantalla?  
> - ¿Qué pasaría si se elimina la llamada a `waitFor()`?

> **Actividad 12. Modificación de código**.  
> 
> Partiendo del ejemplo anterior, describe cómo modificarías el código para:  
> - Ejecutar `calc.exe` en lugar de `notepad`.  
> - Ejecutar un programa con argumentos (por ejemplo, `miPrograma arg1 arg2`).  
> No es necesario que lo ejecutes, solo que expliques o escribas el código modificado.

---

## 10. ENTRADA, SALIDA Y STREAMS

Un proceso recibe datos, los transforma y genera resultados:

```text
Entrada ──► Proceso ──► Salida
```

| Canal | Nombre | Función habitual |
|---|---|---|
| Entrada estándar | `stdin` | Recibe datos, normalmente desde el teclado. |
| Salida estándar | `stdout` | Muestra resultados, normalmente en pantalla. |
| Salida de error | `stderr` | Envía mensajes de error. |

### Streams asociados a Process

Cuando Java crea un proceso hijo, el proceso padre se comunica con él mediante flujos:

| Stream | Función |
|---|---|
| `OutputStream` | Envía datos a la entrada estándar (`stdin`) del proceso hijo. |
| `InputStream` | Lee la salida estándar (`stdout`) generada por el proceso hijo. |
| `ErrorStream` | Lee los mensajes de error (`stderr`) generados por el proceso hijo. |

#### 📝 Actividades

> **Actividad 13. Identificación de canales**.  
> 
> Para cada uno de los siguientes programas, indica qué usaría como `stdin`, `stdout` y `stderr`:  
> - Una calculadora por consola que pide dos números y muestra el resultado.  
> - Un compilador que muestra errores de sintaxis.  
> - Un programa que lee un fichero y escribe el resultado en otro.

> **Actividad 14. Redirección de salida**.  
> 
> Investiga qué significan las siguientes órdenes en un sistema tipo Unix/Linux:  
> ```bash
> programa > salida.txt
> programa 2> errores.txt
> ```  
> Describe brevemente qué ocurre con `stdout` y `stderr` en cada caso y explica por qué puede ser útil separar la salida normal de los errores.

[Volver a Inicio](../README.md)

---

## 11. COMUNICACIÓN Y SINCRONIZACIÓN

### 11.1. COMUNICACIÓN ENTRE PROCESOS

Los procesos pueden intercambiar datos mediante varios mecanismos:

| Mecanismo | Utilidad |
|---|---|
| Streams | Comunicación mediante entrada, salida y errores estándar. |
| Pipes | Canal sencillo de comunicación, frecuente entre padre e hijo. |
| Sockets | Comunicación entre procesos, incluso en ordenadores distintos. |
| Memoria compartida | Región de memoria a la que acceden varios procesos. |
| Semáforos | Mecanismo de coordinación y bloqueo entre procesos. |
| JNI | Permite acceder desde Java a código escrito en otros lenguajes. |

### 11.2. SINCRONIZACIÓN

La **sincronización** permite coordinar el orden y el ritmo de ejecución de los procesos.

Un ejemplo es `waitFor()`:

```java
Process proceso = new ProcessBuilder(args).start();
int retorno = proceso.waitFor();

System.out.println("Código de retorno: " + retorno);
```

- El proceso padre queda bloqueado.
- El hijo continúa hasta finalizar.
- El padre recibe el código de retorno del hijo.

```text
Comunicación
│
├── Intercambio de datos
├── Coordinación del ritmo
└── Control de la ejecución
    │
    ▼
Sincronización
```

#### 📝 Actividades

> **Actividad 15. Esquema de comunicación**.  
> 
> Dibuja un esquema sencillo en el que un proceso padre y un proceso hijo se comunican mediante flujos de datos. Etiqueta los canales (puedes usar `stdin`, `stdout`, `stderr` o simplemente "canal de datos") y describe brevemente qué tipo de información viajaría en cada sentido.

> **Actividad 16. Sincronización con `waitFor()`**.  
> 
> A partir del siguiente fragmento:  
> ```java
> Process p = new ProcessBuilder("tarea").start();
> // línea A
> System.out.println("Terminó");
> // línea B
> p.waitFor();
> ```  
> Responde:  
> - Si `waitFor()` está en la línea B, ¿cuándo se imprime "Terminó"?  
> - ¿Dónde colocarías `waitFor()` si quieres que el mensaje se muestre solo cuando la tarea haya acabado realmente?  
> - ¿En qué situaciones te interesaría no usar `waitFor()`?

---

## 12. PROGRAMACIÓN MULTIPROCESO

La **programación multiproceso** permite que diferentes procesos cooperen para resolver una tarea.

El sistema operativo se encarga de:

- Gestionar la multiprogramación.
- Decidir qué proceso utiliza la CPU.
- Ocultar gran parte de la complejidad al usuario.

El programador debe encargarse de:

- Diseñar los procesos que cooperan.
- Implementar la comunicación.
- Sincronizar las operaciones.
- Gestionar posibles errores y finalizaciones.

### Fases de diseño

#### 1. Descomposición funcional

Identificar las tareas que debe realizar la aplicación y las relaciones entre ellas.

#### 2. Partición

Distribuir las tareas entre varios procesos.

Objetivos:

- Maximizar la independencia entre procesos.
- Minimizar la comunicación entre ellos.
- Definir cómo se intercambiarán los datos.

> La comunicación y la sincronización introducen un coste temporal y aumentan la complejidad de la aplicación.

#### 3. Implementación

Crear los procesos y programar los mecanismos necesarios de comunicación y sincronización.

#### 📝 Actividades

> **Actividad 17. División de una tarea en procesos**.  
> 
> Imagina una aplicación que:  
> - Lee un fichero grande.  
> - Procesa los datos (por ejemplo, los filtra o transforma).  
> - Guarda el resultado en otro fichero.  
> Propón cómo dividirías esta tarea en varios procesos, qué haría cada uno y qué procesos necesitarían comunicarse entre sí.

> **Actividad 18. Cuándo usar varios procesos**.  
> 
> Completa las siguientes frases con tus propias palabras:  
> - Usar varios procesos tiene sentido cuando…  
> - No merece la pena usar varios procesos cuando…  
> - Un riesgo de usar muchos procesos es…

[Volver a Inicio](../README.md)

---

## 13. MAPA CONCEPTUAL

```text
PROGRAMACIÓN DE SERVICIOS Y PROCESOS
│
├── Programa
│   └── Código y datos almacenados
│
├── Proceso
│   ├── Programa en ejecución
│   ├── Contador de programa
│   ├── Imagen de memoria
│   └── Estado del procesador
│
├── Sistema operativo
│   ├── Gestiona recursos
│   ├── Ejecuta programas
│   ├── Controla procesos
│   ├── Kernel
│   │   ├── Interrupciones
│   │   └── Llamadas al sistema
│   └── Modo dual
│       ├── Modo usuario
│       └── Modo kernel
│
├── Ejecución de programas
│   ├── Multiprogramación
│   ├── Programación concurrente
│   ├── Programación paralela
│   └── Programación distribuida
│
├── Estados del proceso
│   ├── Nuevo
│   ├── Listo
│   ├── En ejecución
│   ├── Bloqueado
│   └── Terminado
│
├── Planificación
│   ├── Corto plazo
│   ├── Largo plazo
│   ├── Sin desalojo
│   ├── Apropiativa
│   └── Tiempo compartido
│
├── Gestión de procesos
│   ├── Creación
│   │   ├── Padre
│   │   └── Hijo
│   ├── Árbol de procesos
│   ├── exit
│   ├── waitFor()
│   └── destroy()
│
├── Comunicación
│   ├── stdin
│   ├── stdout
│   ├── stderr
│   ├── Streams
│   ├── Sockets
│   ├── Pipes
│   ├── Memoria compartida
│   ├── Semáforos
│   └── JNI
│
└── Programación multiproceso
    ├── Descomposición funcional
    ├── Partición
    └── Implementación
```

---

## 14. IDEAS CLAVE

- Un **programa** es código y datos almacenados; un **proceso** es ese programa en ejecución.
- El **sistema operativo** administra recursos y controla los procesos.
- La **concurrencia** alterna procesos en la CPU; el **paralelismo** ejecuta instrucciones simultáneamente.
- Un proceso puede estar en estado nuevo, listo, ejecución, bloqueado o terminado.
- El **planificador** decide qué proceso utiliza la CPU.
- El **cambio de contexto** permite alternar procesos, pero consume tiempo.
- Los procesos pueden establecer relaciones de padre e hijo.
- En Java, `ProcessBuilder` y `Runtime.exec()` permiten crear procesos externos.
- `waitFor()` permite esperar a que un proceso hijo termine.
- `stdin`, `stdout` y `stderr` representan los canales estándar de un proceso.
- La **comunicación** intercambia datos; la **sincronización** coordina cuándo se ejecutan las operaciones.
- Una aplicación multiproceso debe minimizar la comunicación innecesaria entre procesos.

#### 📝 Actividades

> **Actividad 20. Autoevaluación**.  
> 
> Responde brevemente (sí/no o con una frase) a las siguientes preguntas:  
> - ¿Sabes explicar la diferencia entre programa y proceso?  
> - ¿Sabes describir los estados de un proceso sin mirar el tema?  
> - ¿Entiendes para qué sirve la planificación y los tipos principales?  
> - ¿Sabes qué hacen `ProcessBuilder`, `start()` y `waitFor()` en Java?  
> - ¿Puedes nombrar al menos tres mecanismos de comunicación entre procesos?

---

<small>Material de estudio elaborado a partir del Capítulo 1 de Programación de Servicios y Procesos.</small>

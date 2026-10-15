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

> **Diferencia entre multiprogramación y programación concurrente:**  
> La multiprogramación es una **técnica del sistema operativo** que alterna varios programas en la CPU para aprovecharla mejor.  
> La programación concurrente es un **concepto más general**: varias tareas progresan de forma aparentemente simultánea, aunque pueden alternarse en una sola CPU.  
> Por tanto, la multiprogramación es una forma de conseguir concurrencia, pero no la única.

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

Este método solicita la terminación del subproceso representado por el objeto `Process`. Después, se pueden utilizar métodos como `isAlive()`  o `waitFor()` para comprobar si realmente ha terminado.

[Volver a Inicio](../README.md)

---

## 9. PROCESOS EN JAVA

En Java, la clase `Process` representa un **proceso externo** creado por el sistema operativo: por ejemplo, el Bloc de notas, la calculadora o cualquier otro programa ejecutable.

Cuando un programa Java lanza otro programa, se producen dos procesos:
- **Proceso padre**: el programa Java.
- **Proceso hijo**: el programa externo ejecutado, como notepad.

La clase `Process` permite controlar ese proceso hijo: esperar a que termine, consultar su código de salida, enviarle datos o leer su salida.

### 9.1. ProcessBuilder

`ProcessBuilder` permite configurar y lanzar un proceso externo. Es la forma recomendada en Java para crear procesos.

```java
ProcessBuilder pb = new ProcessBuilder("notepad");
Process proceso = pb.start();
```

En este ejemplo:
1. Se crea un objeto `ProcessBuilder` con el programa notepad.
2. `start()` solicita al sistema operativo que ejecute Notepad.
3. `start()` devuelve un objeto Process, que representa al proceso hijo.

El método `start()` crea realmente el proceso utilizando el comando, los argumentos, el directorio de trabajo y las variables de entorno configurados en el `ProcessBuilder`.

### Métodos principales

| Método | Función |
|---|---|
| `start()` | Lanza el proceso y devuelve un objeto `Process`. |
| `command()` | Define o consulta el programa y sus argumentos. |
| `directory()` | Establece el directorio de trabajo del proceso hijo. |
| `environment()` | Permite consultar o modificar las variables de entorno. |

Por defecto, el proceso hijo utiliza el mismo directorio de trabajo y una copia de las variables de entorno del proceso Java que lo lanza.

### Ejemplo con argumentos

```java
ProcessBuilder pb = new ProcessBuilder("miPrograma", "arg1", "arg2");
Process proceso = pb.start();
```

Cada valor entre comillas es una parte independiente del comando:

- `"miPrograma"`: programa a ejecutar.
- `"arg1"`: primer argumento.
- `"arg2"`: segundo argumento.

Equivale a escribir en la consola:

```bash
miPrograma arg1 arg2
```

### 9.2. Runtime.exec()

La clase `Runtime` también permite ejecutar comandos del sistema.

```java
Runtime runtime = Runtime.getRuntime();
Process proceso = runtime.exec("notepad");
```

También puede recibir argumentos, variables de entorno y directorio de trabajo. Para pasar argumentos, se recomienda utilizar un array de `String`:

```java
Runtime runtime = Runtime.getRuntime();
Process proceso = runtime.exec(new String[] {"miPrograma", "arg1", "arg2"});
```

### ProcessBuilder o Runtime.exec()

| Aspecto | `ProcessBuilder` | `Runtime.exec()` |
|---|---|---|
| Recomendación actual | Opción moderna y más flexible. | Alternativa más antigua. |
| Configuración | Permite configurar comando, argumentos, directorio y entorno antes de lanzar. | Permite ejecutar directamente un comando. |
| Argumentos | Se indican como elementos separados. | Conviene usar un array de `String`. |
| Uso habitual | `new ProcessBuilder("programa", "arg1").start()` | `Runtime.getRuntime().exec("programa")` |

### 9.3. ESPERAR AL PROCESO HIJO

El método `waitFor()` bloquea el proceso padre hasta que termina el proceso hijo.

```java
int codigoRetorno = proceso.waitFor();
```

Mientras el proceso hijo sigue ejecutándose, el programa Java queda detenido en esa línea.
Cuando el hijo termina, `waitFor()` devuelve su código de salida.

### Código de retorno

Por convenio:

- `0`: el proceso terminó correctamente.
- Distinto de `0`: normalmente indica un error o una finalización anormal.

El código de retorno NO representa los mensajes que el proceso hijo escribe por pantalla. Esos mensajes se transmiten mediante los streams de salida o de error del proceso; el código de retorno es solo un número que indica cómo terminó

## Ejemplo completo

```java
import java.io.IOException;

public class EjemploProcesos {
    public static void main(String[] args) throws IOException, InterruptedException {
        ProcessBuilder pb = new ProcessBuilder("notepad");
        Process proceso = pb.start();

        System.out.println("Notepad abierto. Esperando a que se cierre...");

        int codigo = proceso.waitFor();

        System.out.println("Terminó con código: " + codigo);
    }
}
```

### ¿Qué ocurre paso a paso?

1. `pb.start()` abre Notepad.
2. Java muestra el mensaje `Notepad abierto. Esperando a que se cierre...`.
3. `waitFor()` detiene el programa Java.
4. El usuario utiliza Notepad.
5. Cuando el usuario cierra Notepad, `waitFor()` devuelve el código de salida.
6. Java muestra, por ejemplo, `Terminó con código: 0`.

#### 📝 Actividades

> **Actividad 11. Predicción de comportamiento y modificación de código**.  
> 
> Partiendo del ejemplo anterior
> 
> Responde:  
> - ¿Qué pasaría si se elimina la llamada a `waitFor()`?
> - ¿Cómo modificarías el código para ejecutar la calculadora en lugar del bloc de notas?

---

## 10. ENTRADA, SALIDA Y STREAMS

Un proceso recibe datos, los transforma y genera resultados:

```text
Entrada ──► Proceso ──► Salida
```

Un **stream** o flujo es un canal de comunicación por el que un proceso envía o recibe datos de forma secuencial.

Por defecto, todo proceso tiene tres canales estándar:

| Canal | Nombre | Descriptor | Función habitual |
|---|---|---:|---|
| Entrada estándar | `stdin` | `0` | Recibe datos, normalmente desde el teclado. |
| Salida estándar | `stdout` | `1` | Muestra resultados normales, normalmente en pantalla. |
| Salida de error | `stderr` | `2` | Envía mensajes de error o diagnóstico. |

Estos canales no están obligatoriamente conectados al teclado o a la pantalla: pueden redirigirse a ficheros, a otros procesos o a dispositivos.

### Streams asociados a `Process`

Cuando Java crea un proceso hijo, el proceso padre puede comunicarse con él mediante flujos.

**Importante:** la perspectiva es la del proceso padre.

| Método de `Process` | Tipo devuelto | Comunicación |
|---|---|---|
| `getOutputStream()` | `OutputStream` | El padre escribe datos que el hijo recibe por su `stdin`. |
| `getInputStream()` | `InputStream` | El padre lee la salida normal (`stdout`) generada por el hijo. |
| `getErrorStream()` | `InputStream` | El padre lee los mensajes de error (`stderr`) generados por el hijo. |

El nombre `getInputStream()` puede confundir: no se refiere a la entrada del proceso hijo, sino al flujo desde el cual el proceso padre lee la salida del hijo.

#### 📝 Actividades

> **Actividad 12. Identificación de canales**.  
> 
> Para cada uno de los siguientes programas, indica qué usaría como `stdin`, `stdout` y `stderr`:  
> - Una calculadora por consola que pide dos números y muestra el resultado.  
> - Un compilador que muestra errores de sintaxis.  
> - Un programa que lee un fichero y escribe el resultado en otro.

> **Actividad 13. Redirección de salida**.  
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

En el apartado anterior se han visto los streams estándar de un proceso: `stdin`, `stdout` y `stderr`.  
Estos streams no solo sirven para comunicarse con el teclado o la pantalla: también pueden utilizarse para que dos procesos se comuniquen entre sí.

Cada proceso tiene su propio espacio de memoria. Por eso, cuando varios procesos necesitan intercambiar información o coordinar su ejecución, el sistema operativo les proporciona mecanismos de **comunicación entre procesos** (*IPC, Inter-Process Communication*).

Hay dos necesidades relacionadas pero distintas:

- **Comunicación:** enviar o recibir datos entre procesos.
- **Sincronización:** coordinar el orden o el momento en que los procesos realizan sus acciones.

### 11.1. Comunicación entre procesos

Los procesos pueden intercambiar datos mediante varios mecanismos:

| Mecanismo | Utilidad | Ejemplo |
|---|---|---|
| **Streams** | Comunicación mediante la entrada, salida y error estándar de un proceso. | Un programa Java ejecuta un comando y lee su salida mediante `getInputStream()`. |
| **Pipes** | Canal de comunicación, normalmente unidireccional, que conecta la salida de un proceso con la entrada de otro. | En Linux: `comando1 | comando2`. |
| **Sockets** | Comunicación bidireccional entre procesos, incluso si están en ordenadores distintos conectados por red. | Un cliente y un servidor se comunican mediante TCP. |
| **Memoria compartida** | Varios procesos acceden a una misma región de memoria para intercambiar datos rápidamente. | Dos procesos comparten una variable o una estructura de datos. |
| **Semáforos** | Mecanismo de coordinación que controla el acceso a recursos compartidos y evita accesos simultáneos conflictivos. | Varios procesos acceden a una misma zona de memoria compartida. |
| **JNI** | Permite que código Java invoque o sea invocado por código escrito en otros lenguajes, como C o C++. | Una aplicación Java utiliza una librería nativa escrita en C. |

Los streams vistos en el apartado anterior son un mecanismo de comunicación entre procesos. Cuando un proceso padre crea un proceso hijo, puede escribir en el `stdin` del hijo o leer su `stdout` y `stderr`.

La memoria compartida es rápida, pero como varios procesos pueden leer y escribir a la vez, normalmente necesita mecanismos de sincronización, como semáforos, para evitar condiciones de carrera.

### 11.2. Sincronización

La **sincronización** permite coordinar el orden y el ritmo de ejecución de los procesos o hilos.

Sirve, por ejemplo, para:

- Esperar a que otro proceso termine antes de continuar.
- Evitar que dos procesos modifiquen el mismo recurso al mismo tiempo.
- Establecer qué proceso debe actuar primero.
- Coordinar el acceso a memoria compartida, ficheros, impresoras u otros recursos.

Un ejemplo sencillo en Java es `waitFor()`:

```java
Process proceso = new ProcessBuilder(args).start();

int retorno = proceso.waitFor();

System.out.println("Código de retorno: " + retorno);
```

En este ejemplo:

1. El proceso padre crea e inicia un proceso hijo.
2. El padre llama a `waitFor()`.
3. El proceso padre queda bloqueado hasta que el hijo termina.
4. Cuando el hijo finaliza, `waitFor()` devuelve su código de retorno.
5. Por convención, el código `0` indica que el proceso hijo terminó correctamente; un valor distinto de `0` suele indicar un error o una terminación anormal.

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

> **Actividad 14. Cuándo usar varios procesos**.  
> 
> Completa las siguientes frases con tus propias palabras:  
> - Usar varios procesos tiene sentido cuando…  
> - No merece la pena usar varios procesos cuando…  
> - Un riesgo de usar muchos procesos es…

[Volver a Inicio](../README.md)

---

## 💻 Ejemplos

### Ejemplo 1: Lanzar Paint y esperar a que termine

Todas las versiones realizan la misma tarea: ejecutar Paint, esperar a que el usuario lo cierre y mostrar el código con el que ha terminado.

La diferencia entre ellas está en cómo se gestionan las excepciones y en cómo se obtiene el código de salida.

#### Excepciones que pueden generarse

El método `start()` de `ProcessBuilder` puede lanzar una `IOException`. Esta excepción se produce, por ejemplo, cuando el sistema no puede encontrar o ejecutar el programa indicado.

El método `waitFor()` de `Process` puede lanzar una `InterruptedException`. Esta excepción se produce si el hilo que está esperando a que termine el proceso hijo es interrumpido.

**Versión 1**: sin `try-catch`

En esta versión, el método `main` no captura las excepciones. En su lugar, las declara con `throws` para que las gestione quien llame al método.

```java
public static void main(String[] args) throws IOException, InterruptedException {
    ProcessBuilder pb = new ProcessBuilder("mspaint.exe");
    Process proceso = pb.start();

    System.out.println("Paint abierto. Esperando a que se cierre...");

    int codigo = proceso.waitFor();

    System.out.println("Terminó con código: " + codigo);
}
```

Si ocurre una `IOException` o una `InterruptedException`, el programa se detiene y muestra el error. Es la versión más sencilla, pero no permite controlar qué hacer cuando falla la ejecución o la espera.

**Versión 2**: capturando solo `InterruptedException`

En esta versión se captura la excepción que puede lanzar `waitFor()`. La `IOException` sigue declarándose con `throws`.

```java
public static void main(String[] args) throws IOException {
    ProcessBuilder pb = new ProcessBuilder("mspaint.exe");
    Process proceso = pb.start();

    try {
        System.out.println("Paint abierto. Esperando a que se cierre...");

        int codigo = proceso.waitFor();

        System.out.println("Terminó con código: " + codigo);

    } catch (InterruptedException ex) {
        System.err.println("La espera del proceso fue interrumpida: " + ex.getMessage());
        Thread.currentThread().interrupt();
    }
}
```

Cuando se captura una `InterruptedException`, es buena práctica restaurar el estado de interrupción del hilo con `Thread.currentThread().interrupt()`. Así no se pierde la información de que otro hilo solicitó la interrupción.

**Versión 3**: capturando `IOException` y `InterruptedException`

Esta versión captura las dos excepciones que pueden producirse: la que puede lanzar `start()` y la que puede lanzar `waitFor()`.

```java
public static void main(String[] args) {
    ProcessBuilder pb = new ProcessBuilder("mspaint.exe");
    Process proceso = null;

    try {
        proceso = pb.start();

        System.out.println("Paint abierto. Esperando a que se cierre...");

        int codigo = proceso.waitFor();

        System.out.println("Terminó con código: " + codigo);

    } catch (IOException ex) {
        System.err.println("Error al iniciar el proceso: " + ex.getMessage());

    } catch (InterruptedException ex) {
        System.err.println("La espera del proceso fue interrumpida: " + ex.getMessage());
        Thread.currentThread().interrupt();
    }
}
```

Esta es la versión más completa para un programa sencillo, porque distingue dos situaciones diferentes: un fallo al intentar ejecutar el proceso y una interrupción mientras se espera a que termine.

**Diferencia** entre `waitFor()` y `exitValue()`

El método `waitFor()` bloquea el proceso padre hasta que el proceso hijo termina. Además, devuelve directamente el código de salida del hijo.

```java
int codigo = proceso.waitFor();

System.out.println("El proceso terminó con el código: " + codigo);
```

El método `exitValue()` también devuelve el código de salida, pero solo puede utilizarse cuando el proceso ya ha terminado. Si se llama mientras el proceso sigue en ejecución, lanza una `IllegalThreadStateException`.

```java
proceso.waitFor();

int codigo = proceso.exitValue();

System.out.println("El proceso terminó con el código: " + codigo);
```

Por tanto, la forma más directa es utilizar el valor devuelto por `waitFor()`. La forma con `exitValue()` también es correcta, pero solo después de haber llamado a `waitFor()` o cuando se sabe con seguridad que el proceso ya ha finalizado.

**Ejemplo comparativo**

```java
public static void main(String[] args) {
    ProcessBuilder pb = new ProcessBuilder("mspaint.exe");
    Process proceso = null;

    try {
        proceso = pb.start();

        System.out.println("Esperando a que se cierre Paint...");

        int codigoConWaitFor = proceso.waitFor();

        int codigoConExitValue = proceso.exitValue();

        System.out.println("Código obtenido con waitFor(): " + codigoConWaitFor);
        System.out.println("Código obtenido con exitValue(): " + codigoConExitValue);

    } catch (IOException ex) {
        System.err.println("No se pudo iniciar el proceso: " + ex.getMessage());

    } catch (InterruptedException ex) {
        System.err.println("La espera fue interrumpida.");
        Thread.currentThread().interrupt();
    }
}
```

En este ejemplo, `waitFor()` espera a que Paint se cierre y devuelve su código de salida. Después, `exitValue()` consulta ese mismo código, ya que el proceso ha terminado.

### Ejemplo 2: Mismo programa, pero crear un `ProcessBuilder` vacío y usar `command()`

```java
public static void main(String[] args) {
    ProcessBuilder pb = new ProcessBuilder();
    pb.command("mspaint.exe");
    Process proceso = null;

    try {
        proceso = pb.start();

        System.out.println("Esperando a que se cierre Paint...");

        int codigo = proceso.waitFor();

        System.out.println("El proceso terminó con el código: " + codigo);

    } catch (IOException ex) {
        System.err.println("No se pudo iniciar el proceso: " + ex.getMessage());

    } catch (InterruptedException ex) {
        System.err.println("La espera fue interrumpida.");
        Thread.currentThread().interrupt();
    }
}
```

### Ejemplo 3: Esperar, destruir el proceso y obtener su estado

```java
public static void main(String[] args) {
    ProcessBuilder pb = new ProcessBuilder();
    pb.command("mspaint.exe");

    try {
        Process process = pb.start();
        Thread.sleep(2000);
        process.destroy();

        int estado = process.waitFor();
        System.out.println("Estado del hijo: " + estado);
    } catch (Exception e) {
        System.out.println("Error ejecutando el hijo");
        System.out.println("Descripción: " + e.getMessage());
    }
}
```

`destroy()` solicita la terminación del proceso hijo. Como el proceso puede tardar un instante en finalizar, después se llama a `waitFor()` para esperar su finalización y obtener su código de salida.

Si el proceso no responde a `destroy()`, se puede utilizar `destroyForcibly()` para terminarlo de forma forzada.

### Ejemplo 4: Leer la salida estándar del proceso hijo

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class LeerSalidaProceso {
    public static void main(String[] args) throws IOException {
        ProcessBuilder pb = new ProcessBuilder("cmd.exe", "/c", "dir");
        Process process = pb.start();

        try (BufferedReader reader = new BufferedReader(
                new InputStreamReader(process.getInputStream()))) {

            String linea;

            while ((linea = reader.readLine()) != null) {
                System.out.println(linea);
            }

            int estado = process.waitFor();
            System.out.println("El proceso terminó con el código: " + estado);

        } catch (InterruptedException e) {
            System.err.println("Se interrumpió la espera del proceso.");
            Thread.currentThread().interrupt();
        }
    }
}
```

En este ejemplo, el proceso padre lee el `stdout` del proceso hijo mediante `getInputStream()`. Aunque el método se llame `getInputStream()`, representa la salida del hijo porque es la información que el padre recibe como entrada.

### Ejemplo 5: Redirigir la salida del proceso hijo a un fichero

```java
import java.io.File;
import java.io.IOException;

public class RedirigirSalida {
    public static void main(String[] args) throws IOException {
        ProcessBuilder pb = new ProcessBuilder("cmd.exe", "/c", "dir");
        pb.redirectOutput(new File("salida.txt"));

        Process process = pb.start();

        try {
            int estado = process.waitFor();
            System.out.println("El proceso terminó con el código: " + estado);
        } catch (InterruptedException e) {
            System.err.println("Se interrumpió la espera del proceso.");
            Thread.currentThread().interrupt();
        }
    }
}
```

`redirectOutput()` redirige el `stdout` del proceso hijo al fichero `salida.txt`. De esta forma, la salida normal del comando no aparece en la consola, sino que se guarda en el fichero.

### Resumen

- `ProcessBuilder` permite configurar y lanzar procesos hijos.
- `start()` crea el proceso y devuelve un objeto `Process`.
- `waitFor()` bloquea el proceso padre hasta que el hijo termina y devuelve su código de salida.
- `exitValue()` devuelve el código de salida, pero solo si el proceso ya ha terminado.
- `destroy()` solicita la terminación del proceso.
- `destroyForcibly()` termina el proceso de forma forzada.
- Los métodos `getInputStream()`, `getOutputStream()` y `getErrorStream()` permiten comunicarse con el proceso hijo mediante sus streams estándar.
- `redirectOutput()`, `redirectError()` y `redirectInput()` permiten redirigir los streams del proceso hijo.

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

---

<small>Material de estudio elaborado a partir del Capítulo 1 de Programación de Servicios y Procesos.</small>

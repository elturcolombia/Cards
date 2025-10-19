# 🧠 Configuración de Spec Kit — Framework de GitHub para desarrollo basado en especificaciones

## 📋 Descripción general

Spec Kit es un framework open source de GitHub que implementa el enfoque Spec-Driven Development (SDD): un modelo en el que el proyecto se define primero mediante especificaciones estructuradas, y luego esas especificaciones guían la planificación, tareas e implementación. Su herramienta principal, `specify-cli`, permite inicializar y gestionar las especificaciones de un proyecto directamente desde la terminal.

## ⚙️ Instalación del entorno

### 1. Instalar UV
`uv` es el gestor de entornos y herramientas que se usa para instalar la CLI de Spec Kit.

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Verificar la instalación:

```bash
uv --version
```

### 2. Instalar Spec Kit CLI

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

Verificar instalación:

```bash
specify --version
```

## 🏗️ Inicialización del proyecto

Dentro de la carpeta raíz del proyecto (no en `src/`, donde vive el código de Laravel):

```bash
cd ~/proyectos/Cards
specify init --here
```

Durante la inicialización:
*   Se elige el asistente IA (por ejemplo, Gemini, Copilot, Claude, etc.).
*   Se genera una carpeta `.spec/` con los archivos base:

```
.spec/
├── principles.md
├── specification.md
├── plan.md
├── tasks.md
└── README.md
```

Estos archivos representan los pilares del flujo SDD:

| Archivo          | Propósito                                            |
| ---------------- | ---------------------------------------------------- |
| `principles.md`  | Define los principios y valores técnicos del proyecto. |
| `specification.md`| Contiene la descripción funcional del sistema.      |
| `plan.md`        | Expone la estrategia y fases de implementación.      |
| `tasks.md`       | Lista tareas o hitos derivados de la especificación. |

## 🧩 Integración con IA y comandos clave

Una vez inicializado el proyecto, puedes usar comandos tipo slash (especialmente desde entornos compatibles con IA) para gestionar el ciclo completo:

| Comando                 | Propósito                                      |
| ----------------------- | ---------------------------------------------- |
| `/speckit.constitution` | Define los principios del proyecto.            |
| `/speckit.specify`      | Genera o actualiza la especificación base.     |
| `/speckit.plan`         | Construye el plan de implementación.           |
| `/speckit.tasks`        | Crea la lista de tareas derivadas.             |
| `/speckit.implement`    | Sincroniza las tareas con la ejecución.        |

Comandos opcionales para validación:
*   `/speckit.clarify` — reduce ambigüedades antes de planificar.
*   `/speckit.analyze` — verifica coherencia entre especificaciones.
*   `/speckit.checklist` — genera listas de control de calidad.

## 🧠 Recomendaciones

*   Añadir el directorio del agente (por ejemplo `.gemini/`) a `.gitignore` para evitar subir credenciales.
*   No ejecutar `specify init` dentro del código fuente (`src/` en proyectos Laravel).
*   Usar los archivos `.spec` como documentación viva del proyecto (principios, requisitos, plan y tareas).

## 📂 Análisis de la Estructura de Archivos

En conjunto, los archivos del proyecto forman un sistema de desarrollo de software llamado **Spec Kit**, configurado a medida. Este sistema utiliza un enfoque de **Desarrollo Basado en Especificaciones (Spec-Driven Development - SDD)**, donde la idea es definir claramente una funcionalidad en un lenguaje natural y luego usar herramientas y automatización (integradas con un asistente de IA) para generar planes, tareas e incluso guiar la implementación.

### 1. Directorio `.specify/` (El motor del framework)

Este es el corazón del sistema "Spec Kit". Contiene la lógica y las plantillas para que todo funcione.

*   **`.specify/memory/constitution.md`**: Este es el archivo más importante. Es la **"Constitución"** de tu proyecto. Define las reglas y principios técnicos innegociables que todo el desarrollo debe seguir. En tu caso, exige:
    *   Diseño modular.
    *   Desarrollo "API-First".
    *   **Test-Driven Development (TDD) obligatorio**.
    *   Tests de integración.
    *   Versionamiento Semántico.

*   **`.specify/scripts/bash/*.sh`**: Son los "músculos" del sistema. Son scripts de Bash que automatizan tareas clave:
    *   `create-new-feature.sh`: Crea la estructura de carpetas y la rama de Git para una nueva funcionalidad.
    *   `check-prerequisites.sh`: Verifica que todos los archivos necesarios existan antes de ejecutar un comando.
    *   `setup-plan.sh`: Prepara el archivo de planificación.
    *   `update-agent-context.sh`: Un script muy interesante que lee los planes y actualiza archivos de contexto para diferentes asistentes de IA (Gemini, Copilot, Claude) para que entiendan el stack tecnológico del proyecto.

*   **`.specify/templates/*.md`**: Son las plantillas o "moldes" que el sistema usa para generar los documentos de especificación, planificación y tareas. Esto asegura que todos los documentos tengan una estructura consistente.

### 2. Directorio `.gemini/commands/` (La integración con la IA)

Estos archivos `.toml` son **comandos personalizados para Gemini**. Cada archivo define un paso del flujo de desarrollo y da instrucciones muy detalladas sobre cómo ejecutarlo, qué scripts llamar y qué esperar.

*   `speckit.constitution.toml`: Para definir o actualizar la "Constitución" del proyecto.
*   `speckit.specify.toml`: Para tomar una descripción tuya y crear una **especificación** formal (`spec.md`).
*   `speckit.clarify.toml`: Para hacer preguntas y resolver ambigüedades en la especificación.
*   `speckit.plan.toml`: Para generar un **plan de implementación** técnico (`plan.md`) a partir de la especificación.
*   `speckit.tasks.toml`: Para crear una **lista de tareas** detallada (`tasks.md`) a partir del plan.
*   `speckit.implement.toml`: Para empezar a **ejecutar las tareas** y escribir el código.
*   `speckit.analyze.toml` y `speckit.checklist.toml`: Para analizar la calidad y consistencia de las especificaciones y generar listas de control.

### En resumen:

Has configurado un flujo de trabajo de desarrollo muy estructurado y automatizado. Le pides a un asistente de IA que realice una acción (ej. `/speckit.plan`), la IA lee el comando `.toml` correspondiente, ejecuta los scripts `.sh` necesarios, usa las plantillas `.md` y se guía por la `constitution.md` para generar los artefactos del proyecto de una manera consistente y predecible.
# Grupos Proyecto Integrador

---

## Grupos Proyecto Integrador
[Ver Grupos](https://docs.google.com/spreadsheets/d/18ZFiQJEN-VW94srzq7EdmxlNP2dLX4UZW6EMEjEICpk/edit?usp=sharing){target="_blank"} 

=== "Proyecto 1"

    # Sistema de Evaluación en Línea    

    ## Descripción del Sistema
    El sistema permite a profesores crear y gestionar exámenes en línea, mientras que los estudiantes pueden responderlos desde cualquier dispositivo. Las entidades principales son:

    - **Profesores**: Crean y gestionan cuestionarios.
    - **Estudiantes**: Responden los cuestionarios.
    - **Cuestionarios**: Contienen preguntas diseñadas por profesores.
    - **Preguntas**: Componentes de los cuestionarios.
    - **Respuestas**: Respuestas enviadas por los estudiantes a las preguntas.

    ## Modelo Relacional
    ### Tablas y Atributos
    1. **Profesores**
        - `id_profesor` (PK, INT): Identificador único del profesor.
        - `nombre` (VARCHAR): Nombre del profesor.
        - `email` (VARCHAR): Correo electrónico único.

    2. **Estudiantes**
        - `id_estudiante` (PK, INT): Identificador único del estudiante.
        - `nombre` (VARCHAR): Nombre del estudiante.
        - `email` (VARCHAR): Correo electrónico único.

    3. **Cuestionarios**
        - `id_cuestionario` (PK, INT): Identificador único del cuestionario.
        - `titulo` (VARCHAR): Título del cuestionario.
        - `id_profesor` (FK, INT): Referencia al profesor que creó el cuestionario.

    4. **Preguntas**
        - `id_pregunta` (PK, INT): Identificador único de la pregunta.
        - `texto` (TEXT): Texto de la pregunta.
        - `id_cuestionario` (FK, INT): Referencia al cuestionario al que pertenece.

    5. **Respuestas**
        - `id_respuesta` (PK, INT): Identificador único de la respuesta.
        - `id_pregunta` (FK, INT): Referencia a la pregunta respondida.
        - `id_estudiante` (FK, INT): Referencia al estudiante que respondió.
        - `texto_respuesta` (TEXT): Texto de la respuesta.

    ### Relaciones
    - Un **Profesor** puede crear múltiples **Cuestionarios** (1:N).
    - Un **Cuestionario** contiene múltiples **Preguntas** (1:N).
    - Una **Pregunta** puede tener múltiples **Respuestas** de diferentes **Estudiantes** (1:N).
    - Un **Estudiante** puede enviar múltiples **Respuestas** (1:N).

    ## Consultas SQL
    ### Creación de Tablas

    ```sql
    -- Tabla Profesores
    CREATE TABLE Profesores (
        id_profesor INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Estudiantes
    CREATE TABLE Estudiantes (
        id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Cuestionarios
    CREATE TABLE Cuestionarios (
        id_cuestionario INT AUTO_INCREMENT PRIMARY KEY,
        titulo VARCHAR(200) NOT NULL,
        id_profesor INT NOT NULL,
        FOREIGN KEY (id_profesor) REFERENCES Profesores(id_profesor)
    );

    -- Tabla Preguntas
    CREATE TABLE Preguntas (
        id_pregunta INT AUTO_INCREMENT PRIMARY KEY,
        texto TEXT NOT NULL,
        id_cuestionario INT NOT NULL,
        FOREIGN KEY (id_cuestionario) REFERENCES Cuestionarios(id_cuestionario)
    );

    -- Tabla Respuestas
    CREATE TABLE Respuestas (
        id_respuesta INT AUTO_INCREMENT PRIMARY KEY,
        id_pregunta INT NOT NULL,
        id_estudiante INT NOT NULL,
        texto_respuesta TEXT NOT NULL,
        FOREIGN KEY (id_pregunta) REFERENCES Preguntas(id_pregunta),
        FOREIGN KEY (id_estudiante) REFERENCES Estudiantes(id_estudiante)
    );
    ```

=== "Proyecto 2"



    # Sistema de Gestión de Eventos Escolares

    ## Descripción del Sistema
    La aplicación permite organizar y gestionar eventos escolares como ferias académicas, competencias deportivas o días culturales. Los organizadores pueden crear eventos, y los estudiantes pueden inscribirse para participar. Las entidades principales son:

    - **Organizadores**: Crean y gestionan eventos.
    - **Estudiantes**: Se inscriben en eventos.
    - **Eventos**: Actividades escolares planificadas.
    - **Inscripciones**: Registro de estudiantes en eventos.
   

    ## Modelo Relacional
    ### Tablas y Atributos
    1. **Organizadores**
        - `id_organizador` (PK, INT): Identificador único del organizador.
        - `nombre` (VARCHAR): Nombre del organizador.
        - `email` (VARCHAR): Correo electrónico único.

    2. **Estudiantes**
        - `id_estudiante` (PK, INT): Identificador único del estudiante.
        - `nombre` (VARCHAR): Nombre del estudiante.
        - `email` (VARCHAR): Correo electrónico único.

    3. **Eventos**
        - `id_evento` (PK, INT): Identificador único del evento.
        - `nombre` (VARCHAR): Nombre del evento.
        - `fecha` (DATE): Fecha del evento.
        - `id_organizador` (FK, INT): Referencia al organizador que creó el evento.

    4. **Inscripciones**
        - `id_inscripcion` (PK, INT): Identificador único de la inscripción.
        - `id_evento` (FK, INT): Referencia al evento.
        - `id_estudiante` (FK, INT): Referencia al estudiante inscrito.

    ### Relaciones
    - Un **Organizador** puede crear múltiples **Eventos** (1:N).
    - Un **Evento** puede tener múltiples **Inscripciones** (1:N).
    - Un **Estudiante** puede inscribirse en múltiples **Eventos** (N:M, implementado mediante la tabla **Inscripciones**).

    ## Consultas SQL
    ### Creación de Tablas

    ```sql
    -- Tabla Organizadores
    CREATE TABLE Organizadores (
        id_organizador INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Estudiantes
    CREATE TABLE Estudiantes (
        id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Eventos
    CREATE TABLE Eventos (
        id_evento INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(200) NOT NULL,
        fecha DATE NOT NULL,
        id_organizador INT NOT NULL,
        FOREIGN KEY (id_organizador) REFERENCES Organizadores(id_organizador)
    );

    -- Tabla Inscripciones
    CREATE TABLE Inscripciones (
        id_inscripcion INT AUTO_INCREMENT PRIMARY KEY,
        id_evento INT NOT NULL,
        id_estudiante INT NOT NULL,
        FOREIGN KEY (id_evento) REFERENCES Eventos(id_evento),
        FOREIGN KEY (id_estudiante) REFERENCES Estudiantes(id_estudiante),
        UNIQUE (id_evento, id_estudiante)
    );
    ```

=== "Proyecto 3"

    # Sistema de Gestión de Horarios de Clases

    ## Descripción del Sistema
    La aplicación permite crear y gestionar horarios de clases para estudiantes y profesores. Los administradores pueden asignar clases a profesores y estudiantes, especificando días y horas. Las entidades principales son:

    - **Profesores**: Imparten clases.
    - **Estudiantes**: Asisten a clases.
    - **Clases**: Sesiones programadas con día y hora.
    - **Horarios**: Asignaciones de clases a profesores y estudiantes.    

    ## Modelo Relacional
    ### Tablas y Atributos
    1. **Profesores**
        - `id_profesor` (PK, INT): Identificador único del profesor.
        - `nombre` (VARCHAR): Nombre del profesor.
        - `email` (VARCHAR): Correo electrónico único.

    2. **Estudiantes**
        - `id_estudiante` (PK, INT): Identificador único del estudiante.
        - `nombre` (VARCHAR): Nombre del estudiante.
        - `email` (VARCHAR): Correo electrónico único.

    3. **Clases**
        - `id_clase` (PK, INT): Identificador único de la clase.
        - `nombre` (VARCHAR): Nombre de la clase (ej. "Matemáticas").
        - `dia` (VARCHAR): Día de la semana (ej. "Lunes").
        - `hora_inicio` (TIME): Hora de inicio de la clase.
        - `hora_fin` (TIME): Hora de fin de la clase.

    4. **Horarios**
        - `id_horario` (PK, INT): Identificador único del horario.
        - `id_clase` (FK, INT): Referencia a la clase.
        - `id_profesor` (FK, INT): Referencia al profesor asignado.
        - `id_estudiante` (FK, INT): Referencia al estudiante asignado.

    ### Relaciones
    - Una **Clase** puede estar en múltiples **Horarios** (1:N).
    - Un **Profesor** puede estar asignado a múltiples **Horarios** (1:N).
    - Un **Estudiante** puede estar asignado a múltiples **Horarios** (1:N).
    - Un **Horario** asocia una **Clase** con un **Profesor** y un **Estudiante** (N:M entre Clases, Profesores y Estudiantes).

    ## Consultas SQL
    ### Creación de Tablas

    ```sql
    -- Tabla Profesores
    CREATE TABLE Profesores (
        id_profesor INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Estudiantes
    CREATE TABLE Estudiantes (
        id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Clases
    CREATE TABLE Clases (
        id_clase INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        dia VARCHAR(10) NOT NULL,
        hora_inicio TIME NOT NULL,
        hora_fin TIME NOT NULL
    );

    -- Tabla Horarios
    CREATE TABLE Horarios (
        id_horario INT AUTO_INCREMENT PRIMARY KEY,
        id_clase INT NOT NULL,
        id_profesor INT NOT NULL,
        id_estudiante INT NOT NULL,
        FOREIGN KEY (id_clase) REFERENCES Clases(id_clase),
        FOREIGN KEY (id_profesor) REFERENCES Profesores(id_profesor),
        FOREIGN KEY (id_estudiante) REFERENCES Estudiantes(id_estudiante),
        UNIQUE (id_clase, id_profesor, id_estudiante)
    );
    ```

=== "Proyecto 4"

    # Sistema de Gestión de Calificaciones

    ## Descripción del Sistema
    La aplicación permite a los profesores registrar y gestionar las calificaciones de los estudiantes por asignatura, generar informes y visualizar estadísticas de rendimiento. Las entidades principales son:

    - **Profesores**: Ingresan calificaciones.
    - **Estudiantes**: Reciben calificaciones.
    - **Asignaturas**: Materias evaluadas.
    - **Calificaciones**: Notas asignadas a estudiantes por asignatura.    

    ## Modelo Relacional
    ### Tablas y Atributos
    1. **Profesores**
        - `id_profesor` (PK, INT): Identificador único del profesor.
        - `nombre` (VARCHAR): Nombre del profesor.
        - `email` (VARCHAR): Correo electrónico único.

    2. **Estudiantes**
        - `id_estudiante` (PK, INT): Identificador único del estudiante.
        - `nombre` (VARCHAR): Nombre del estudiante.
        - `email` (VARCHAR): Correo electrónico único.

    3. **Asignaturas**
        - `id_asignatura` (PK, INT): Identificador único de la asignatura.
        - `nombre` (VARCHAR): Nombre de la asignatura (ej. "Matemáticas").
        - `id_profesor` (FK, INT): Referencia al profesor que imparte la asignatura.

    4. **Calificaciones**
        - `id_calificacion` (PK, INT): Identificador único de la calificación.
        - `id_estudiante` (FK, INT): Referencia al estudiante.
        - `id_asignatura` (FK, INT): Referencia a la asignatura.
        - `nota` (DECIMAL): Calificación numérica (ej. 0 a 100).
        - `fecha` (DATE): Fecha de registro de la calificación.

    ### Relaciones
    - Un **Profesor** puede impartir múltiples **Asignaturas** (1:N).
    - Una **Asignatura** puede tener múltiples **Calificaciones** (1:N).
    - Un **Estudiante** puede tener múltiples **Calificaciones** (1:N).
    - Una **Calificación** asocia un **Estudiante** con una **Asignatura** (N:M entre Estudiantes y Asignaturas).

    ## Consultas SQL
    ### Creación de Tablas

    ```sql
    -- Tabla Profesores
    CREATE TABLE Profesores (
        id_profesor INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Estudiantes
    CREATE TABLE Estudiantes (
        id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Asignaturas
    CREATE TABLE Asignaturas (
        id_asignatura INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        id_profesor INT NOT NULL,
        FOREIGN KEY (id_profesor) REFERENCES Profesores(id_profesor)
    );

    -- Tabla Calificaciones
    CREATE TABLE Calificaciones (
        id_calificacion INT AUTO_INCREMENT PRIMARY KEY,
        id_estudiante INT NOT NULL,
        id_asignatura INT NOT NULL,
        nota DECIMAL(5,2) NOT NULL CHECK (nota >= 0 AND nota <= 100),
        fecha DATE NOT NULL,
        FOREIGN KEY (id_estudiante) REFERENCES Estudiantes(id_estudiante),
        FOREIGN KEY (id_asignatura) REFERENCES Asignaturas(id_asignatura),
        UNIQUE (id_estudiante, id_asignatura, fecha)
    );
    ```

=== "Proyecto 5"

    # Sistema de Gestión de Salidas Pedagógicas

    ## Descripción del Sistema
    La aplicación permite organizar y gestionar salidas pedagógicas, como visitas a museos, parques naturales o empresas. Los organizadores pueden planificar salidas, y los estudiantes pueden inscribirse para participar. Las entidades principales son:

    - **Organizadores**: Planifican y gestionan las salidas.
    - **Estudiantes**: Se inscriben en las salidas.
    - **Salidas**: Actividades pedagógicas planificadas.
    - **Inscripciones**: Registro de estudiantes en las salidas.

    ## Modelo Relacional
    ### Tablas y Atributos
    1. **Organizadores**
        - `id_organizador` (PK, INT): Identificador único del organizador.
        - `nombre` (VARCHAR): Nombre del organizador.
        - `email` (VARCHAR): Correo electrónico único.

    2. **Estudiantes**
        - `id_estudiante` (PK, INT): Identificador único del estudiante.
        - `nombre` (VARCHAR): Nombre del estudiante.
        - `email` (VARCHAR): Correo electrónico único.

    3. **Salidas**
        - `id_salida` (PK, INT): Identificador único de la salida.
        - `destino` (VARCHAR): Lugar de la salida (ej. "Museo Nacional").
        - `fecha` (DATE): Fecha de la salida.
        - `id_organizador` (FK, INT): Referencia al organizador que planificó la salida.

    4. **Inscripciones**
        - `id_inscripcion` (PK, INT): Identificador único de la inscripción.
        - `id_salida` (FK, INT): Referencia a la salida.
        - `id_estudiante` (FK, INT): Referencia al estudiante inscrito.

    ### Relaciones
    - Un **Organizador** puede planificar múltiples **Salidas** (1:N).
    - Una **Salida** puede tener múltiples **Inscripciones** (1:N).
    - Un **Estudiante** puede inscribirse en múltiples **Salidas** (N:M, implementado mediante la tabla **Inscripciones**).

    ## Consultas SQL
    ### Creación de Tablas

    ```sql
    -- Tabla Organizadores
    CREATE TABLE Organizadores (
        id_organizador INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Estudiantes
    CREATE TABLE Estudiantes (
        id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Salidas
    CREATE TABLE Salidas (
        id_salida INT AUTO_INCREMENT PRIMARY KEY,
        destino VARCHAR(200) NOT NULL,
        fecha DATE NOT NULL,
        id_organizador INT NOT NULL,
        FOREIGN KEY (id_organizador) REFERENCES Organizadores(id_organizador)
    );

    -- Tabla Inscripciones
    CREATE TABLE Inscripciones (
        id_inscripcion INT AUTO_INCREMENT PRIMARY KEY,
        id_salida INT NOT NULL,
        id_estudiante INT NOT NULL,
        FOREIGN KEY (id_salida) REFERENCES Salidas(id_salida),
        FOREIGN KEY (id_estudiante) REFERENCES Estudiantes(id_estudiante),
        UNIQUE (id_salida, id_estudiante)
    );
    ```

=== "Proyecto 6"

    # Sistema de Registro de Asistencia

    ## Descripción del Sistema
    La aplicación permite a los profesores registrar la asistencia diaria de los estudiantes, marcando si están presentes o ausentes. Los administradores pueden generar informes de asistencia. Las entidades principales son:

    - **Profesores**: Registran la asistencia.
    - **Estudiantes**: Su asistencia es registrada.
    - **Asistencias**: Registros de presencia o ausencia por estudiante y fecha.

    ## Modelo Relacional
    ### Tablas y Atributos
    1. **Profesores**
        - `id_profesor` (PK, INT): Identificador único del profesor.
        - `nombre` (VARCHAR): Nombre del profesor.
        - `email` (VARCHAR): Correo electrónico único.

    2. **Estudiantes**
        - `id_estudiante` (PK, INT): Identificador único del estudiante.
        - `nombre` (VARCHAR): Nombre del estudiante.
        - `email` (VARCHAR): Correo electrónico único.

    3. **Asistencias**
        - `id_asistencia` (PK, INT): Identificador único del registro de asistencia.
        - `id_estudiante` (FK, INT): Referencia al estudiante.
        - `id_profesor` (FK, INT): Referencia al profesor que registró la asistencia.
        - `fecha` (DATE): Fecha del registro.
        - `estado` (ENUM): Estado de asistencia ("Presente", "Ausente").

    ### Relaciones
    - Un **Profesor** puede registrar múltiples **Asistencias** (1:N).
    - Un **Estudiante** puede tener múltiples **Asistencias** (1:N).
    - Una **Asistencia** asocia un **Estudiante** con un **Profesor** en una fecha específica.

    ## Consultas SQL
    ### Creación de Tablas

    ```sql
    -- Tabla Profesores
    CREATE TABLE Profesores (
        id_profesor INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Estudiantes
    CREATE TABLE Estudiantes (
        id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Asistencias
    CREATE TABLE Asistencias (
        id_asistencia INT AUTO_INCREMENT PRIMARY KEY,
        id_estudiante INT NOT NULL,
        id_profesor INT NOT NULL,
        fecha DATE NOT NULL,
        estado ENUM('Presente', 'Ausente') NOT NULL,
        FOREIGN KEY (id_estudiante) REFERENCES Estudiantes(id_estudiante),
        FOREIGN KEY (id_profesor) REFERENCES Profesores(id_profesor),
        UNIQUE (id_estudiante, fecha)
    );
    ```

=== "Proyecto 7"

    # Sistema de Encuestas de Bienestar Emocional

    ## Descripción del Sistema
    La aplicación permite medir el bienestar emocional y psicológico de los estudiantes mediante encuestas periódicas. Los administradores crean encuestas, y los estudiantes responden preguntas para evaluar su estado emocional. Las entidades principales son:

    - **Estudiantes**: Responden las encuestas.
    - **Encuestas**: Conjuntos de preguntas enviadas periódicamente.
    - **Preguntas**: Elementos individuales de las encuestas.
    - **Respuestas**: Respuestas de los estudiantes a las preguntas.    

    ## Modelo Relacional
    ### Tablas y Atributos
    1. **Estudiantes**
        - `id_estudiante` (PK, INT): Identificador único del estudiante.
        - `nombre` (VARCHAR): Nombre del estudiante.
        - `email` (VARCHAR): Correo electrónico único.

    2. **Encuestas**
        - `id_encuesta` (PK, INT): Identificador único de la encuesta.
        - `titulo` (VARCHAR): Título de la encuesta (ej. "Bienestar Semanal").
        - `fecha` (DATE): Fecha de la encuesta.

    3. **Preguntas**
        - `id_pregunta` (PK, INT): Identificador único de la pregunta.
        - `texto` (TEXT): Texto de la pregunta.
        - `id_encuesta` (FK, INT): Referencia a la encuesta a la que pertenece.

    4. **Respuestas**
        - `id_respuesta` (PK, INT): Identificador único de la respuesta.
        - `id_pregunta` (FK, INT): Referencia a la pregunta.
        - `id_estudiante` (FK, INT): Referencia al estudiante que respondió.
        - `valor` (INT): Valor de la respuesta (ej. 1 a 5 para escala Likert).

    ### Relaciones
    - Una **Encuesta** contiene múltiples **Preguntas** (1:N).
    - Una **Pregunta** puede tener múltiples **Respuestas** (1:N).
    - Un **Estudiante** puede enviar múltiples **Respuestas** (1:N).
    - Una **Respuesta** asocia un **Estudiante** con una **Pregunta** (N:M entre Estudiantes y Preguntas).

    ## Consultas SQL
    ### Creación de Tablas

    ```sql
    -- Tabla Estudiantes
    CREATE TABLE Estudiantes (
        id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(100) NOT NULL,
        email VARCHAR(100) NOT NULL UNIQUE
    );

    -- Tabla Encuestas
    CREATE TABLE Encuestas (
        id_encuesta INT AUTO_INCREMENT PRIMARY KEY,
        titulo VARCHAR(200) NOT NULL,
        fecha DATE NOT NULL
    );

    -- Tabla Preguntas
    CREATE TABLE Preguntas (
        id_pregunta INT AUTO_INCREMENT PRIMARY KEY,
        texto TEXT NOT NULL,
        id_encuesta INT NOT NULL,
        FOREIGN KEY (id_encuesta) REFERENCES Encuestas(id_encuesta)
    );

    -- Tabla Respuestas
    CREATE TABLE Respuestas (
        id_respuesta INT AUTO_INCREMENT PRIMARY KEY,
        id_pregunta INT NOT NULL,
        id_estudiante INT NOT NULL,
        valor INT NOT NULL CHECK (valor >= 1 AND valor <= 5),
        FOREIGN KEY (id_pregunta) REFERENCES Preguntas(id_pregunta),
        FOREIGN KEY (id_estudiante) REFERENCES Estudiantes(id_estudiante),
        UNIQUE (id_pregunta, id_estudiante)
    );
    ```


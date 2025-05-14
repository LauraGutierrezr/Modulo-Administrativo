# Modulo-Administrativo
Modulo 6 - Parte Administrativa de ECI Bienestar Total


## Descripción
El Módulo de Gestión de Usuarios centraliza las funciones administrativas del sistema de Bienestar Universitario, permitiendo al Administrador gestionar de forma integral los perfiles de usuario y la configuración de horarios para el uso de espacios, recursos y servicios. Facilita la asignación de roles, el control de accesos y la planificación eficiente de la operación diaria.


-- Características Principales--

## Gestión de usuarios

Registro completo: Creación de nuevos perfiles con toda la información requerida según tipo de usuario
Modificación y eliminación: Mantenimiento actualizado de la base de usuarios
Asignación de roles: Configuración de permisos según el perfil (Estudiante, Funcionario, Entrenador, etc.)
Historial de actividad: Seguimiento detallado de las acciones de cada usuario en el sistema

## Gestión de horarios

Configuración flexible: Definición de horarios para todos los espacios y servicios
Franjas personalizables: Control de duración, intervalos y disponibilidad
Gestión de pausas: Registro de tiempos no disponibles (almuerzos, reuniones)
Visualización integral: Consulta por espacio o por responsable

## Funcionalidades Detalladas
Para Administradores

-- Gestión completa de usuarios:

Crear, modificar y eliminar cualquier tipo de usuario
Asignar cualquier rol disponible en el sistema
Actualizar cualquier dato sin restricciones
Visualizar historial completo de actividad


-- Control total de horarios:

Configurar horarios para cualquier espacio o servicio
Modificar cualquier horario existente
Desactivar temporalmente horarios según necesidad
Gestionar pausas y excepciones



## Para Funcionarios de Bienestar

-- Gestión personal limitada:

Actualizar sus propios datos personales
Visualizar su historial de actividad
Configurar sus horarios de disponibilidad (con aprobación)
Gestionar sus propias pausas


-- Visualización de información:

Consultar horarios por espacio (solo lectura)
Consultar horarios por responsable (solo lectura)



## Estructura de Datos
Datos de Estudiantes

Código del estudiante (número de carné)
Tipo y número de identificación
Nombre completo
Programa académico
Correo institucional
Número de contacto
Fecha de nacimiento
Dirección de residencia
Contacto de emergencia:

Nombre completo
Número de teléfono
Tipo y número de identificación
Parentesco



## Datos de Funcionarios

Tipo y número de identificación
Nombre completo
Rol asignado
Especialidad (aplica solo para médicos)
Correo electrónico institucional
Número de contacto
Horarios de disponibilidad

## Datos de Registro de Horarios

ID del horario
Tipo de espacio o servicio
Usuario responsable (si aplica)
Día de la semana
Hora de inicio y hora de fin
Intervalos de atención configurables
Horario de almuerzo o pausa (si aplica)
Estado del horario (Activo / Inactivo)

## Diagramas

Diagrama de Clases
mermaidclassDiagram
    class Usuario {
        -int id
        -String tipoIdentificacion
        -String numeroIdentificacion
        -String nombreCompleto
        -String correoInstitucional
        -String numeroContacto
        -String direccion
        -Date fechaNacimiento
        -boolean estado
        +registrar()
        +modificar()
        +eliminar()
        +obtenerHistorialActividad()
    }

    class Estudiante {
        -String codigoEstudiante
        -String programaAcademico
        +actualizarDatosPersonales()
    }

    class ContactoEmergencia {
        -int id
        -String nombreCompleto
        -String numeroTelefono
        -String tipoIdentificacion
        -String numeroIdentificacion
        -String parentesco
        +registrar()
        +actualizar()
    }

    class Funcionario {
        -String rol
        -String especialidad
        -List~HorarioDisponibilidad~ horarios
        +actualizarDisponibilidad()
    }

    class HorarioDisponibilidad {
        -int id
        -TipoEspacio tipoEspacio
        -Usuario responsable
        -DiaSemana dia
        -Time horaInicio
        -Time horaFin
        -int intervaloMinutos
        -Time inicioPausa
        -Time finPausa
        -EstadoHorario estado
        +configurarHorario()
        +modificarHorario()
        +desactivarHorario()
        +verificarDisponibilidad(fecha, hora)
    }

    Usuario <|-- Estudiante
    Usuario <|-- Funcionario
    Estudiante "1" -- "1" ContactoEmergencia
    Funcionario "1" -- "0..*" HorarioDisponibilidad


## Diagrama de Casos de Uso
      - En astah

´´
<img width="443" alt="Captura de pantalla 2025-05-14 a la(s) 6 15 53 p m" src="https://github.com/user-attachments/assets/8c5106ec-8901-4d95-a18a-72bd424b1ebe" />
´´

´´
<img width="557" alt="Captura de pantalla 2025-05-14 a la(s) 6 16 07 p m" src="https://github.com/user-attachments/assets/65d67580-2a52-4632-b87c-c671b9776272" />
´´


## Flujos de Trabajo Principales
-- Registro de Nuevo Usuario

Administrador accede a la opción "Registrar Usuario"
Selecciona tipo de usuario (Estudiante, Funcionario, etc.)
Completa todos los campos requeridos según el tipo
Para estudiantes, agrega información de contacto de emergencia
Asigna rol específico y permisos
Guarda el nuevo registro, que queda activo en el sistema

-- Configuración de Horarios

Administrador o Funcionario accede a "Gestión de Horarios"
Selecciona el espacio o servicio a configurar
Define día de la semana y franjas horarias disponibles
Configura intervalos de atención si aplica
Establece pausas necesarias (almuerzo, descansos)
Guarda la configuración que queda disponible para reservas

## Tecnologías Utilizadas

  ´´
Frontend: HTML, CSS, JavaScript, React
Backend: Java, Spring Boot
Base de Datos: PostgreSQL
Seguridad: Spring Security, JWT
Documentación: Swagger/OpenAPI
  ´´

## Reglas de Negocio

Solo los administradores pueden crear nuevos usuarios
Los funcionarios solo pueden modificar sus propios datos
La eliminación de usuarios requiere confirmación doble
Los horarios no pueden tener conflictos para un mismo espacio
Todo usuario estudiante debe tener al menos un contacto de emergencia
Los horarios de pausa deben estar dentro del horario principal configurado

## Instalación y Configuración

Clonar el repositorio
bashgit clone https://github.com/tu-organizacion/bienestar-universitario.git
cd bienestar-universitario/modulo-gestion-usuarios

Instalamos las dependencias
bashmvn install

Configuramos la base de datos en application.properties
propertiesspring.datasource.url=jdbc:postgresql://localhost:5432/bienestar_db
spring.datasource.username=postgres
spring.datasource.password=...

EjecutamosD la aplicación
bashmvn spring-boot:run



© 2025 Sistema de Bienestar Universitario - Desarrollado por Equipo CVDS Juan Mejía - Laura Gutiérrez

# Diagrama de Clases - Módulo SOMA

## Descripción
Este diagrama muestra las clases principales del sistema SOMA y sus relaciones para la gestión de exámenes médicos ocupacionales.

```mermaid
classDiagram
    %% Clases principales
    class Empleado {
        +String nombres
        +String apellidos
        +String condicion
        +String obra
        +String dni
        +Date fechaNacimiento
        +String cargo
        +String detalleCargo
        +String celular
        +String ubicacion
        +int edad
        +String genero
        +validarDatos()
        +calcularEdad()
        +obtenerUbicacion()
    }
    
    class CapitalHumano {
        +String codigoArea
        +String nombreArea
        +String responsable
        +validarPersonal(Empleado)
        +aprobarSolicitud(SolicitudEMO)
        +rechazarSolicitud(SolicitudEMO)
    }
    
    class AreaSolicitante {
        +String codigoArea
        +String nombreArea
        +String responsable
        +crearSolicitud(Empleado)
        +enviarSolicitud(SolicitudEMO)
        +consultarEstado(String)
    }
    
    class SolicitudEMO {
        +String idSolicitud
        +Date fechaSolicitud
        +String estado
        +String motivo
        +String observaciones
        +aprobar()
        +rechazar()
        +programar()
    }
    
    class Clinica {
        +String codigoClinica
        +String nombreClinica
        +String direccion
        +String telefono
        +String email
        +List~Sede~ sedes
        +obtenerSedes()
        +verificarDisponibilidad()
    }
    
    class Sede {
        +String codigoSede
        +String nombreSede
        +String direccion
        +String telefono
        +String ubicacion
        +List~Examen~ examenesDisponibles
        +verificarCapacidad()
        +asignarCita()
    }
    
    class Examen {
        +String codigoExamen
        +String nombreExamen
        +String descripcion
        +int duracionMinutos
        +String tipoExamen
        +boolean requiereAyuno
        +List~String~ preparacion
        +validarRequisitos(Empleado)
    }
    
    class HistorialEMO {
        +String idHistorial
        +Date fechaExamen
        +String estado
        +String resultado
        +Date fechaVencimiento
        +String observaciones
        +verificarVigencia()
        +calcularVencimiento()
    }
    
    class CitaMedica {
        +String idCita
        +Date fechaCita
        +Time horaCita
        +String estado
        +String observaciones
        +confirmar()
        +cancelar()
        +reprogramar()
    }
    
    class Reporte {
        +String idReporte
        +Date fechaGeneracion
        +String tipoReporte
        +String contenido
        +generar()
        +exportar()
    }
    
    %% Relaciones
    Empleado ||--o{ SolicitudEMO : "genera"
    CapitalHumano ||--o{ SolicitudEMO : "valida"
    AreaSolicitante ||--o{ SolicitudEMO : "crea"
    
    SolicitudEMO ||--|| HistorialEMO : "consulta"
    SolicitudEMO ||--o| CitaMedica : "programa"
    
    Clinica ||--o{ Sede : "contiene"
    Sede ||--o{ Examen : "ofrece"
    Sede ||--o{ CitaMedica : "asigna"
    
    Empleado ||--o{ HistorialEMO : "tiene"
    Empleado ||--o{ CitaMedica : "asiste"
    
    Examen ||--o{ HistorialEMO : "genera"
    
    %% Relaciones de composición
    SolicitudEMO *-- Empleado : "empleado"
    HistorialEMO *-- Empleado : "empleado"
    HistorialEMO *-- Examen : "examen"
    CitaMedica *-- Empleado : "empleado"
    CitaMedica *-- Sede : "sede"
    
    %% Estilos
    classDef empleado fill:#e1f5fe
    classDef area fill:#fff2cc
    classDef clinica fill:#f8cecc
    classDef examen fill:#d5e8d4
    classDef sistema fill:#e1d5e7
    
    class Empleado empleado
    class CapitalHumano,AreaSolicitante area
    class Clinica,Sede clinica
    class Examen,HistorialEMO examen
    class SolicitudEMO,CitaMedica,Reporte sistema
```

## Descripción de Clases

### Empleado
Representa la información personal del empleado que pasará el EMO.
- **Atributos principales**: datos personales, ubicación, edad, género
- **Métodos clave**: validarDatos(), calcularEdad(), obtenerUbicacion()

### CapitalHumano
Área responsable de validar que el personal esté aprobado.
- **Responsabilidades**: Validación de personal, aprobación de solicitudes
- **Métodos**: validarPersonal(), aprobarSolicitud(), rechazarSolicitud()

### AreaSolicitante
Área que solicita el EMO para su personal.
- **Responsabilidades**: Crear y enviar solicitudes de EMO
- **Métodos**: crearSolicitud(), enviarSolicitud(), consultarEstado()

### SolicitudEMO
Representa una solicitud de examen médico ocupacional.
- **Estados**: Pendiente, Aprobada, Rechazada, Programada
- **Métodos**: aprobar(), rechazar(), programar()

### Clinica y Sede
Representan las instalaciones médicas donde se realizan los exámenes.
- **Clinica**: Información general de la clínica
- **Sede**: Ubicaciones específicas con capacidad y servicios

### Examen
Define los tipos de exámenes médicos disponibles.
- **Tipos**: Básico, Electrocardiograma, Test de Embarazo, etc.
- **Métodos**: validarRequisitos() según edad y género del empleado

### HistorialEMO
Registro histórico de exámenes médicos del empleado.
- **Información**: Fechas, resultados, vigencia
- **Métodos**: verificarVigencia(), calcularVencimiento()

### CitaMedica
Representa una cita programada para el examen.
- **Estados**: Programada, Confirmada, Cancelada, Completada
- **Métodos**: confirmar(), cancelar(), reprogramar()

### Reporte
Generación de reportes del sistema.
- **Tipos**: Reportes de solicitudes, exámenes realizados, estadísticas
- **Métodos**: generar(), exportar()

## Reglas de Negocio Implementadas

1. **Validación de Edad**: Si el empleado es mayor de 40 años, requiere electrocardiograma
2. **Validación de Género**: Si es mujer, puede requerir test de embarazo
3. **Ubicación**: La asignación de clínica/sede depende de la ubicación del empleado
4. **Vigencia**: Los EMO tienen una vigencia específica que debe verificarse
5. **Aprobación**: Toda solicitud debe ser aprobada por Capital Humano y Área Solicitante

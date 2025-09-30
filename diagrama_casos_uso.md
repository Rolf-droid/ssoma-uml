# Diagrama de Casos de Uso - Módulo SOMA

## Descripción
Este diagrama muestra los casos de uso principales del sistema SOMA para la gestión de exámenes médicos ocupacionales (EMO).

```mermaid
graph TD
    %% Actores
    CH[Capital Humano]
    AS[Área Solicitante]
    ADM[Administrador]
    CLI[Clínica]
    EMP[Empleado]
    
    %% Sistema SOMA
    SOMA[Sistema SOMA]
    
    %% Casos de Uso
    CH --> UC1[Validar Personal]
    AS --> UC2[Solicitar EMO]
    ADM --> UC3[Gestionar Sistema]
    CLI --> UC4[Programar Examen]
    CLI --> UC5[Realizar Examen]
    EMP --> UC6[Consultar Estado]
    
    %% Relaciones con el sistema
    UC1 --> SOMA
    UC2 --> SOMA
    UC3 --> SOMA
    UC4 --> SOMA
    UC5 --> SOMA
    UC6 --> SOMA
    
    %% Casos de uso internos del sistema
    SOMA --> UC7[Buscar Historial EMO]
    SOMA --> UC8[Verificar Vigencia]
    SOMA --> UC9[Asignar Clínica/Sede]
    SOMA --> UC10[Definir Exámenes Requeridos]
    SOMA --> UC11[Generar Reportes]
    SOMA --> UC12[Validar Condiciones Especiales]
    
    %% Estilos
    style CH fill:#e1f5fe
    style AS fill:#fff2cc
    style ADM fill:#d5e8d4
    style CLI fill:#f8cecc
    style EMP fill:#f0f0f0
    style SOMA fill:#e1d5e7
    style UC1 fill:#e8f5e8
    style UC2 fill:#e8f5e8
    style UC3 fill:#e8f5e8
    style UC4 fill:#e8f5e8
    style UC5 fill:#e8f5e8
    style UC6 fill:#e8f5e8
    style UC7 fill:#fff8e1
    style UC8 fill:#fff8e1
    style UC9 fill:#fff8e1
    style UC10 fill:#fff8e1
    style UC11 fill:#fff8e1
    style UC12 fill:#fff8e1
```

## Descripción de Actores

### Capital Humano
- **Responsabilidad**: Validar que el personal esté aprobado para pasar el EMO
- **Acciones**: Verificar datos del empleado, aprobar solicitudes

### Área Solicitante
- **Responsabilidad**: Solicitar EMO para personal nuevo o existente
- **Acciones**: Enviar datos del empleado, justificar necesidad

### Administrador
- **Responsabilidad**: Gestionar configuración del sistema
- **Acciones**: Configurar clínicas, sedes, tipos de exámenes

### Clínica
- **Responsabilidad**: Programar y realizar exámenes médicos
- **Acciones**: Asignar citas, realizar exámenes, reportar resultados

### Empleado
- **Responsabilidad**: Consultar estado de su EMO
- **Acciones**: Verificar fechas, ubicaciones, resultados

## Descripción de Casos de Uso

### UC1: Validar Personal
- **Actor Principal**: Capital Humano
- **Descripción**: Verificar que el empleado esté aprobado para pasar EMO
- **Precondiciones**: Empleado registrado en el sistema
- **Flujo Principal**: 
  1. Recibir datos del empleado
  2. Verificar aprobación
  3. Confirmar elegibilidad

### UC2: Solicitar EMO
- **Actor Principal**: Área Solicitante
- **Descripción**: Solicitar examen médico para empleado
- **Precondiciones**: Personal validado por Capital Humano
- **Flujo Principal**:
  1. Ingresar datos del empleado
  2. Seleccionar tipo de examen requerido
  3. Enviar solicitud

### UC7: Buscar Historial EMO
- **Actor Principal**: Sistema
- **Descripción**: Consultar si el empleado tiene EMO vigente
- **Precondiciones**: Empleado registrado
- **Flujo Principal**:
  1. Buscar en base de datos
  2. Verificar vigencia
  3. Retornar resultado

### UC9: Asignar Clínica/Sede
- **Actor Principal**: Sistema
- **Descripción**: Asignar clínica según ubicación del empleado
- **Precondiciones**: Empleado sin EMO vigente
- **Flujo Principal**:
  1. Determinar ubicación del empleado
  2. Seleccionar clínica más cercana
  3. Asignar sede disponible

### UC10: Definir Exámenes Requeridos
- **Actor Principal**: Sistema
- **Descripción**: Determinar exámenes según edad y género
- **Precondiciones**: Empleado asignado a clínica
- **Flujo Principal**:
  1. Verificar edad del empleado
  2. Verificar género
  3. Aplicar reglas de negocio
  4. Definir exámenes requeridos

# Diagrama de Secuencia - Flujo EMO

## Descripción
Este diagrama muestra la secuencia de interacciones entre los actores y el sistema SOMA durante el proceso completo de solicitud y programación de un EMO.

```mermaid
sequenceDiagram
    participant AS as Área Solicitante
    participant SOMA as Sistema SOMA
    participant CH as Capital Humano
    participant DB as Base de Datos
    participant CLI as Clínica
    participant EMP as Empleado
    
    %% Flujo principal de solicitud EMO
    Note over AS,EMP: Proceso de Solicitud y Programación EMO
    
    AS->>SOMA: 1. Crear solicitud EMO
    Note right of AS: Ingresa datos del empleado:<br/>Nombres, Apellidos, DNI,<br/>Fecha nacimiento, Cargo, etc.
    
    SOMA->>SOMA: 2. Validar datos del empleado
    SOMA->>SOMA: 3. Calcular edad
    SOMA->>SOMA: 4. Determinar género
    
    SOMA->>CH: 5. Enviar solicitud para validación
    Note right of SOMA: Solicitud pendiente de<br/>aprobación de Capital Humano
    
    CH->>SOMA: 6. Validar personal
    Note right of CH: Verifica que el empleado<br/>esté aprobado para EMO
    
    alt Personal aprobado
        CH->>SOMA: 7a. Aprobar solicitud
        SOMA->>DB: 8. Buscar historial EMO
        DB->>SOMA: 9. Retornar historial
        
        alt No tiene EMO vigente
            SOMA->>SOMA: 10a. Determinar exámenes requeridos
            Note right of SOMA: Si edad > 40: ECG<br/>Si es mujer: Test embarazo
            
            SOMA->>SOMA: 11a. Obtener ubicación empleado
            SOMA->>CLI: 12a. Consultar clínicas disponibles
            CLI->>SOMA: 13a. Retornar clínicas y sedes
            
            SOMA->>SOMA: 14a. Asignar clínica/sede
            Note right of SOMA: Según ubicación<br/>del empleado
            
            SOMA->>CLI: 15a. Programar cita médica
            CLI->>SOMA: 16a. Confirmar cita programada
            
            SOMA->>EMP: 17a. Notificar cita programada
            Note right of EMP: Recibe información de<br/>fecha, hora y ubicación
            
            SOMA->>AS: 18a. Confirmar programación exitosa
            
        else Tiene EMO vigente
            SOMA->>AS: 10b. Informar EMO vigente
            Note right of AS: No se requiere<br/>nueva programación
        end
        
    else Personal no aprobado
        CH->>SOMA: 7b. Rechazar solicitud
        SOMA->>AS: 8b. Notificar rechazo
        Note right of AS: Solicitud rechazada<br/>por Capital Humano
    end
    
    %% Flujo de realización del examen
    Note over EMP,CLI: Proceso de Realización del Examen
    
    EMP->>CLI: 19. Asistir a cita médica
    CLI->>CLI: 20. Realizar exámenes médicos
    
    alt Exámenes completados
        CLI->>SOMA: 21a. Reportar resultados
        SOMA->>DB: 22a. Guardar historial EMO
        SOMA->>EMP: 23a. Notificar resultados disponibles
        SOMA->>AS: 24a. Confirmar EMO completado
        
    else Exámenes incompletos
        CLI->>SOMA: 21b. Reportar examen incompleto
        SOMA->>CLI: 22b. Programar nueva cita
        CLI->>EMP: 23b. Notificar reprogramación
    end
    
    %% Flujo de consulta de estado
    Note over AS,EMP: Consultas de Estado
    
    AS->>SOMA: 25. Consultar estado solicitud
    SOMA->>DB: 26. Buscar estado actual
    DB->>SOMA: 27. Retornar estado
    SOMA->>AS: 28. Informar estado actual
    
    EMP->>SOMA: 29. Consultar estado EMO
    SOMA->>DB: 30. Buscar historial empleado
    DB->>SOMA: 31. Retornar historial
    SOMA->>EMP: 32. Informar estado EMO
```

## Descripción del Flujo

### Fase 1: Solicitud Inicial
1. **Área Solicitante** crea la solicitud ingresando todos los datos del empleado
2. **Sistema SOMA** valida los datos y calcula edad/género automáticamente
3. Se envía la solicitud a **Capital Humano** para validación

### Fase 2: Validación
4. **Capital Humano** revisa y valida que el empleado esté aprobado
5. Si es aprobado, el sistema busca el historial EMO en la base de datos
6. Si no tiene EMO vigente, se procede con la programación

### Fase 3: Programación
7. El sistema determina los exámenes requeridos según reglas de negocio:
   - Si edad > 40 años: incluir electrocardiograma
   - Si es mujer: incluir test de embarazo
8. Se obtiene la ubicación del empleado
9. Se consultan las clínicas disponibles
10. Se asigna la clínica/sede más cercana
11. Se programa la cita médica
12. Se notifica al empleado y área solicitante

### Fase 4: Realización del Examen
13. El empleado asiste a la cita programada
14. La clínica realiza los exámenes médicos
15. Se reportan los resultados al sistema
16. Se actualiza el historial EMO

### Fase 5: Consultas
17. Tanto el área solicitante como el empleado pueden consultar el estado en cualquier momento

## Puntos de Decisión Clave

- **Validación de Capital Humano**: Determina si el proceso continúa
- **Historial EMO**: Si existe uno vigente, no se requiere nueva programación
- **Exámenes Requeridos**: Se determinan automáticamente según edad y género
- **Asignación de Clínica**: Se basa en la ubicación del empleado
- **Resultados del Examen**: Pueden requerir reprogramación si están incompletos

## Manejo de Errores

- **Solicitud Rechazada**: Se notifica inmediatamente al área solicitante
- **EMO Vigente**: Se informa que no se requiere nueva programación
- **Examen Incompleto**: Se programa automáticamente una nueva cita
- **Clínica No Disponible**: Se busca alternativa o se reprograma

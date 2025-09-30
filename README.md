# 📊 Diagramas UML - Módulo SOMA

Este repositorio contiene los diagramas UML completos para el sistema de gestión de exámenes médicos ocupacionales (EMO) del módulo SOMA.

## 📁 Archivos incluidos

| Archivo | Tipo de Diagrama | Descripción |
|---------|------------------|-------------|
| `diagrama_casos_uso.md` | Casos de Uso | Actores y funcionalidades principales del sistema |
| `diagrama_clases.md` | Clases | Entidades y relaciones del sistema |
| `diagrama_secuencia.md` | Secuencia | Flujo completo de interacciones para EMO |
| `diagrama_actividad.md` | Actividad | Proceso detallado de programación de citas |
| `diagrama_componentes.md` | Componentes | Arquitectura del sistema con capas |

## 🎯 Funcionalidades del Sistema

### Actores Principales
- **Capital Humano**: Valida personal aprobado para EMO
- **Área Solicitante**: Solicita EMO para su personal
- **Administrador**: Gestiona configuración del sistema
- **Clínica**: Programa y realiza exámenes médicos
- **Empleado**: Consulta estado de su EMO

### Reglas de Negocio Implementadas
- ✅ **Validación por edad**: Empleados >40 años requieren Electrocardiograma
- ✅ **Validación por género**: Mujeres requieren Test de Embarazo
- ✅ **Aprobación dual**: Capital Humano + Área Solicitante
- ✅ **Verificación de historial**: Búsqueda de EMO vigente
- ✅ **Asignación automática**: Clínica más cercana según ubicación

### Datos del Empleado
- Nombres y Apellidos
- Condición y Obra
- DNI y Fecha de Nacimiento
- Cargo y Detalle de Cargo
- Celular y Ubicación

## 🔧 Tecnologías Utilizadas

- **Lenguaje**: Mermaid
- **Formato**: Markdown (.md)
- **Visualización**: Compatible con GitHub, GitLab, VS Code

## 📖 Cómo visualizar los diagramas

### En GitHub/GitLab
Los diagramas se renderizan automáticamente al abrir los archivos `.md`

### En VS Code
1. Instala la extensión `Mermaid Preview`
2. Abre cualquier archivo `.md`
3. Presiona `Ctrl+Shift+P` → `Mermaid Preview`

### Online
- **Mermaid Live Editor**: https://mermaid.live/
- Copia el código del diagrama y pégalo en el editor

## 🚀 Instalación de Extensiones

### VS Code
```bash
# Mermaid Preview
code --install-extension vstirbu.vscode-mermaid-preview

# Markdown Mermaid Support
code --install-extension bierner.markdown-mermaid
```

## 📊 Estadísticas del Proyecto

- **Total de archivos**: 5 diagramas UML
- **Líneas de código**: 959+ líneas
- **Tipos de diagramas**: 5 (Casos de Uso, Clases, Secuencia, Actividad, Componentes)
- **Actores definidos**: 5
- **Clases principales**: 10+
- **Reglas de negocio**: 5

## 🔄 Flujo del Sistema

1. **Solicitud**: Área Solicitante crea solicitud EMO
2. **Validación**: Capital Humano aprueba el personal
3. **Verificación**: Sistema busca historial EMO vigente
4. **Programación**: Si no tiene EMO vigente, se programa cita
5. **Asignación**: Se asigna clínica según ubicación del empleado
6. **Exámenes**: Se determinan exámenes según edad y género
7. **Notificación**: Se notifica al empleado y área solicitante

## 📝 Licencia

Este proyecto está bajo la licencia MIT. Ver archivo `LICENSE` para más detalles.

## 👥 Contribuidores

- **Desarrollador**: Rolf-droid
- **Fecha**: 2024
- **Versión**: 1.0.0

---

**Nota**: Todos los diagramas están optimizados para visualización en GitHub y editores compatibles con Mermaid.

# Testing

El backend de GoalApp implementa una estrategia de pruebas exhaustiva para asegurar la estabilidad y calidad del sistema.

### 1. Estructura de Pruebas

Las pruebas están organizadas en la carpeta `tests/`, divididas en tres categorías principales:

* **Pruebas Unitarias**: Validan la lógica de funciones y servicios individuales de forma aislada.
* **Pruebas de Integración**: Verifican la interacción correcta entre múltiples componentes (ej. Router $\rightarrow$ Service $\rightarrow$ DB).
* **Pruebas Compartidas (Shared)**: Contienen fixtures y utilidades comunes para todas las pruebas.

### 2. Implementación Actual

El proyecto cuenta con una suite de **28 archivos de prueba**, lo que garantiza una cobertura significativa de los flujos críticos:

* **Fixtures**: Uso de `conftest.py` para definir datos de prueba reutilizables.
* **Aislamiento**: Cada prueba utiliza una sesión de base de datos independiente para evitar efectos secundarios.

### 3. Ejecución de Pruebas

Las pruebas se ejecutan utilizando el framework `pytest`.

```bash
# Ejecutar todas las pruebas
pytest

# Ejecutar pruebas de un módulo específico
pytest tests/unit/test_usuario.py
```

***

### 4. Cobertura de Escenarios

Se han implementado pruebas para los siguientes casos críticos:
- Validaciones de esquemas Pydantic.
- Control de acceso basado en roles (RBAC).
- Gestión de errores en servicios.
- Persistencia de datos mediante SQLAlchemy.

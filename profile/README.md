# GermanVR Mule Libraries

Colección de librerías reutilizables para **Mule 4** enfocadas en estandarizar el manejo de errores y la resiliencia en arquitecturas multicapa.

---

## 🚀 Proyectos

### 📦 global-error-handler-lib

Biblioteca para construir respuestas de error uniformes entre APIs.

**Características**

- Formato estándar de errores.
- Propagación entre capas.
- Conservación del `errorChain`.
- Identificación del `failingComponent`.
- Configuración mediante `errorConfig`.
- Compatible con cualquier conector Mule.

---

### 📦 resilient-request-lib

Biblioteca para centralizar llamadas a sistemas externos.

**Características**

- Logging uniforme.
- Reintentos automáticos.
- Ejecución dinámica de flows.
- Compatible con HTTP, Database, Salesforce, SAP, etc.
- Configuración mediante `requestConfig`.
- Integración con `global-error-handler-lib`.

---

## 🏗 Arquitectura de referencia

```text
EAPI
 │
 ▼
PAPI
 │
 ▼
SAPI
 │
 ▼
Sistema Externo
```

Cada capa conserva el contexto del error hasta llegar al consumidor final.

---

# 📚 Ejemplos incluidos

Este repositorio contiene proyectos de ejemplo completamente funcionales.

---

## germanvr-example-eapi

Experience API encargada de exponer el servicio al cliente.

**Responsabilidades**

- Exposición al consumidor.
- Consumo de PAPI.
- Construcción de la respuesta final.

```text
Cliente
   ↓
EAPI
```

---

## germanvr-example-papi

Process API encargada de la orquestación.

**Responsabilidades**

- Reglas de proceso.
- Consumo de SAPI.
- Propagación del contexto del error.

```text
EAPI
   ↓
PAPI
```

---

## germanvr-example-sapi

System API encargada de la integración con sistemas externos.

**Responsabilidades**

- Consumo del sistema externo.
- Configuración específica del conector.
- Generación del error original.

```text
PAPI
   ↓
SAPI
   ↓
Sistema Externo
```

---

# 🔄 Flujo completo

```text
Cliente
    │
    ▼
EAPI
    │
    ▼
PAPI
    │
    ▼
SAPI
    │
    ▼
Sistema Externo
```

Si ocurre un error:

```text
Sistema Externo
        ↑
SAPI
        ↑
PAPI
        ↑
EAPI
        ↑
Cliente
```

El contexto se conserva entre capas mediante `errorChain`.

---

# 🎯 Filosofía

## Una responsabilidad por capa

### resilient-request-lib

Responsable de:

- Requests externos.
- Reintentos.
- Resiliencia.

### global-error-handler-lib

Responsable de:

- Formato uniforme.
- Trazabilidad.
- Contexto de errores.

### APIs consumidoras

Responsables de:

- Reglas de negocio.
- Transformaciones.
- Orquestación.

---

# 📦 Repositorios

- `global-error-handler-lib`
- `resilient-request-lib`
- `germanvr-example-eapi`
- `germanvr-example-papi`
- `germanvr-example-sapi`

---

# ⚙ Compatibilidad

- Mule Runtime 4.x
- Mule Maven Plugin 4.x

---

# Objetivo

Reducir código duplicado y mantener implementaciones consistentes entre proyectos Mule.

> "Una librería no debería contener lógica de negocio; debería evitar que tengas que resolver el mismo problema veinte veces."

# ER DIAGRAMS

## Definición

Un ER Diagram (Entity-Relationship Diagram) o Diagrama Entidad-Relación es una representación gráfica de una base de datos.

Permite visualizar:

- Entidades
- Atributos
- Relaciones
- Primary Keys
- Foreign Keys
- Cardinalidad

antes de construir físicamente la base de datos.

---

## ¿Por qué existen los ER Diagrams?

Diseñar directamente tablas suele generar errores.

Un ER Diagram permite:

```text
Visualizar el negocio.
Detectar problemas de diseño.
Validar relaciones.
Comunicar ideas.
```

antes de escribir SQL.

---

# Componentes principales

## Entidades

Representan objetos o conceptos del negocio.

Ejemplos:

```text
Cliente
Cuenta
Transacción
```

---

## Atributos

Representan información sobre una entidad.

Ejemplo:

```text
Cliente

IdCliente
Nombre
Apellido
Email
```

---

## Relaciones

Conectan entidades.

Ejemplo:

```text
Cliente
↓
Cuenta
```

---

## Cardinalidad

Describe cuántos registros participan en la relación.

Ejemplos:

```text
1:1
1:N
N:M
```

---

# Ejemplo básico

## Requerimiento

Un banco necesita almacenar:

```text
Clientes
Cuentas
```

---

## Modelo Conceptual

```text
Cliente posee Cuenta
```

---

## ER Diagram

```text
┌─────────────┐
│  CLIENTE    │
├─────────────┤
│ IdCliente   │ PK
│ Nombre      │
│ Apellido    │
└─────────────┘
        │
        │ 1:N
        │
        ▼
┌─────────────┐
│   CUENTA    │
├─────────────┤
│ IdCuenta    │ PK
│ IdCliente   │ FK
│ Saldo       │
└─────────────┘
```

---

# Identificando componentes

## Entidad

```text
CLIENTE
```

---

## Atributos

```text
IdCliente
Nombre
Apellido
```

---

## Primary Key

```text
IdCliente
```

---

## Foreign Key

```text
IdCliente en Cuenta
```

---

## Cardinalidad

```text
1:N
```

---

# Ejemplo Bancario Completo

## Entidades

```text
Cliente
Cuenta
Transacción
```

---

## Relaciones

```text
Cliente → Cuenta

1:N
```

---

```text
Cuenta → Transacción

1:N
```

---

## ER Diagram

```text
┌─────────────┐
│ CLIENTES    │
├─────────────┤
│ IdCliente PK│
│ Nombre      │
│ Apellido    │
└─────────────┘
        │
        │ 1:N
        ▼
┌─────────────┐
│ CUENTAS     │
├─────────────┤
│ IdCuenta PK │
│ IdCliente FK│
│ Saldo       │
└─────────────┘
        │
        │ 1:N
        ▼
┌────────────────┐
│ TRANSACCIONES  │
├────────────────┤
│ IdTrans PK     │
│ IdCuenta FK    │
│ Fecha          │
│ Monto          │
└────────────────┘
```

---

# Relación 1:1

## Ejemplo

```text
Persona
Pasaporte
```

---

```text
┌───────────┐
│ PERSONA   │
└───────────┘
      │
      │ 1:1
      ▼
┌───────────┐
│ PASAPORTE │
└───────────┘
```

---

# Relación 1:N

## Ejemplo

```text
Cliente
Cuenta
```

---

```text
Cliente
   1
   │
   │
   N
Cuenta
```

---

# Relación N:M

## Ejemplo

```text
Estudiante
Curso
```

---

## Problema

Las bases de datos relacionales no implementan N:M directamente.

---

## Solución

Tabla intermedia.

---

```text
┌──────────────┐
│ ESTUDIANTE   │
└──────────────┘
        │
        │ 1:N
        ▼
┌──────────────┐
│ INSCRIPCION  │
└──────────────┘
        ▲
        │ N:1
        │
┌──────────────┐
│ CURSO        │
└──────────────┘
```

---

# ER Diagram vs Base de Datos

## ER Diagram

Representa:

```text
Diseño
```

---

## Base de Datos

Representa:

```text
Implementación
```

---

# Flujo profesional

```text
Requerimientos
↓
Modelo Conceptual
↓
ER Diagram
↓
Modelo Lógico
↓
Modelo Físico
↓
SQL
```

---

# Herramientas populares

## Gratuitas

- Draw.io
- DBeaver
- dbdiagram.io

---

## Profesionales

- SQL Server Management Studio
- ERwin Data Modeler
- Lucidchart
- Visual Paradigm

---

# Caso práctico

## Universidad

Entidades:

```text
Estudiante
Curso
Profesor
```

---

Relaciones:

```text
Profesor → Curso

1:N
```

```text
Estudiante → Curso

N:M
```

---

ER Diagram:

```text
Profesor
    │
    │ 1:N
    ▼
Curso
    ▲
    │
    │ N:M
    ▼
Estudiante
```

---

# Error común

Muchos principiantes comienzan creando tablas sin realizar un diagrama.

Resultado:

```text
Relaciones incorrectas.
Duplicación de datos.
Problemas de mantenimiento.
```

---

# Error conceptual frecuente

Muchos creen que:

```text
ER Diagram = Base de Datos
```

Incorrecto.

El ER Diagram es:

```text
Un plano.
```

La base de datos es:

```text
La construcción.
```

---

# Pensamiento de Arquitectura de Datos

Antes de construir una base de datos pregúntate:

1. ¿Qué entidades existen?
2. ¿Qué atributos tiene cada entidad?
3. ¿Cuál es la Primary Key?
4. ¿Existen Foreign Keys?
5. ¿Cuál es la cardinalidad?
6. ¿Puedo representarlo en un ER Diagram?

---

# Relación con los siguientes módulos

```text
DATABASE FUNDAMENTALS
↓
DATABASE DESIGN LIFECYCLE
↓
ENTITIES AND ATTRIBUTES
↓
PRIMARY KEYS
↓
FOREIGN KEYS
↓
CARDINALITY
↓
ER DIAGRAMS
↓
NORMALIZATION
```

---

# Resumen

Los ER Diagrams permiten representar visualmente una base de datos antes de implementarla.

Elementos fundamentales:

- Entidades
- Atributos
- Primary Keys
- Foreign Keys
- Cardinalidad

Son una herramienta esencial para:

- Database Engineers
- DBAs
- Data Architects
- Data Engineers

y constituyen la base de todo diseño relacional profesional.

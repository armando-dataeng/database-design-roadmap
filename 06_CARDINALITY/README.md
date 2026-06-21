# CARDINALITY

## Definición

La Cardinalidad define cuántos registros de una entidad pueden relacionarse con registros de otra entidad.

Permite describir las reglas del negocio antes de implementar tablas y relaciones.

Pregunta fundamental:

> ¿Cuántos registros pueden participar en esta relación?

---

# ¿Por qué existe la cardinalidad?

Supongamos:

```text
Cliente
Cuenta
```

Sabemos que están relacionados.

Pero necesitamos responder:

```text
¿Un cliente puede tener una cuenta?

¿Puede tener varias?

¿Una cuenta puede pertenecer a varios clientes?
```

La cardinalidad responde estas preguntas.

---

# Tipos principales

Existen tres tipos fundamentales:

```text
1:1
1:N
N:M
```

---

# Relación Uno a Uno (1:1)

## Definición

Un registro de la primera tabla se relaciona con un único registro de la segunda tabla.

Y viceversa.

---

## Ejemplo

```text
Persona
↓
Pasaporte
```

---

## Regla

```text
Una persona tiene un pasaporte.

Un pasaporte pertenece a una persona.
```

---

## Visualización

```text
Persona
    1
    │
    │
    1
Pasaporte
```

---

## Tablas

### Personas

| IdPersona | Nombre |
|------------|---------|
| 1 | Pedro |
| 2 | Ana |

---

### Pasaportes

| IdPasaporte | IdPersona |
|-------------|------------|
| 100 | 1 |
| 101 | 2 |

---

# Relación Uno a Muchos (1:N)

## Definición

Un registro de la tabla principal puede relacionarse con muchos registros de otra tabla.

Pero cada registro de la segunda tabla pertenece a uno solo de la primera.

---

## Ejemplo bancario

```text
Cliente
↓
Cuenta
```

---

## Regla

```text
Un cliente puede tener muchas cuentas.

Una cuenta pertenece a un solo cliente.
```

---

## Visualización

```text
Cliente
    1
    │
    │
    N
Cuenta
```

---

## Tablas

### Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |

---

### Cuentas

| IdCuenta | IdCliente |
|-----------|-----------|
| 101 | 1 |
| 102 | 1 |
| 103 | 1 |

---

## Interpretación

```text
Pedro tiene tres cuentas.
```

---

# Relación Muchos a Muchos (N:M)

## Definición

Muchos registros de una tabla pueden relacionarse con muchos registros de otra tabla.

---

## Ejemplo universitario

```text
Estudiante
↓
Curso
```

---

## Regla

```text
Un estudiante puede tomar muchos cursos.

Un curso puede tener muchos estudiantes.
```

---

## Visualización

```text
Estudiante
    N
    │
    │
    M
Curso
```

---

# Problema

Las bases de datos relacionales no implementan directamente N:M.

---

# Solución

Crear una tabla intermedia.

---

## Ejemplo

### Estudiantes

| IdEstudiante |
|--------------|
| 1 |
| 2 |

---

### Cursos

| IdCurso |
|---------|
| 101 |
| 102 |

---

### Inscripciones

| IdEstudiante | IdCurso |
|--------------|----------|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

---

## Resultado

```text
Estudiante
↓
Inscripciones
↓
Curso
```

---

# Cardinalidad en Diagramas ER

## Uno a Uno

```text
Persona ───── Pasaporte
   1             1
```

---

## Uno a Muchos

```text
Cliente ───── Cuenta
   1            N
```

---

## Muchos a Muchos

```text
Estudiante ── Curso

      N:M
```

---

# Ejemplos reales

## Banco

```text
Cliente → Cuenta

1:N
```

---

## E-commerce

```text
Cliente → Pedido

1:N
```

---

## Hospital

```text
Médico → Paciente

N:M
```

---

## Universidad

```text
Alumno → Curso

N:M
```

---

# Cómo identificar la cardinalidad

Haz estas preguntas:

---

## Uno a Uno

```text
¿Cada registro tiene exactamente uno relacionado?
```

---

## Uno a Muchos

```text
¿Uno puede tener varios?

¿El otro pertenece a uno solo?
```

---

## Muchos a Muchos

```text
¿Ambos lados pueden tener múltiples relaciones?
```

---

# Error común

Muchos principiantes modelan todo como:

```text
1:N
```

---

Sin analizar las reglas reales del negocio.

---

# Error conceptual frecuente

Muchos creen que:

```text
Foreign Key = Cardinalidad
```

Incorrecto.

La Foreign Key implementa la relación.

La Cardinalidad describe la regla del negocio.

---

## Ejemplo

```text
Cliente
↓
Cuenta
```

Cardinalidad:

```text
1:N
```

Implementación:

```sql
FOREIGN KEY (IdCliente)
REFERENCES Clientes(IdCliente)
```

---

# Caso Bancario Completo

## Cliente

Puede tener:

```text
Cuenta Corriente
Cuenta Ahorro
Cuenta Empresarial
```

---

Cardinalidad:

```text
Cliente → Cuenta

1:N
```

---

## Cuenta

Puede registrar:

```text
Miles de transacciones.
```

---

Cardinalidad:

```text
Cuenta → Transacción

1:N
```

---

## Resultado

```text
Cliente
   │
   │ 1:N
   ▼

Cuenta
   │
   │ 1:N
   ▼

Transacción
```

---

# Pensamiento de Modelado de Datos

Antes de crear relaciones pregúntate:

1. ¿Cuántos registros pueden relacionarse?
2. ¿Existe una relación 1:1?
3. ¿Existe una relación 1:N?
4. ¿Existe una relación N:M?
5. ¿Necesito una tabla intermedia?

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
```

---

# Resumen

La Cardinalidad describe cuántos registros pueden relacionarse entre entidades.

Tipos principales:

```text
1:1
Uno a Uno

1:N
Uno a Muchos

N:M
Muchos a Muchos
```

Comprender la cardinalidad es esencial para:

- Modelado de datos.
- Diseño relacional.
- Diagramas ER.
- Normalización.
- Arquitectura de bases de datos.

Es uno de los conceptos más importantes del diseño de bases de datos.

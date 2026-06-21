# ENTITIES AND ATTRIBUTES

## Definición

Las Entidades y los Atributos son los bloques fundamentales del modelado de datos.

Permiten representar objetos, personas, lugares o conceptos del mundo real dentro de una base de datos.

Todo diseño de base de datos comienza identificando:

```text
Entidades
↓
Atributos
```

---

# ¿Qué es una Entidad?

Una entidad es cualquier objeto o concepto sobre el cual necesitamos almacenar información.

Pregunta clave:

> ¿De qué quiero guardar datos?

---

## Ejemplos

### Banco

```text
Cliente
Cuenta
Transacción
Sucursal
Empleado
```

---

### Universidad

```text
Alumno
Profesor
Materia
Carrera
```

---

### E-commerce

```text
Cliente
Producto
Pedido
Proveedor
```

---

## Regla práctica

Si puedes responder:

```text
Quiero almacenar información sobre...
```

probablemente estás frente a una entidad.

---

# ¿Qué es un Atributo?

Un atributo es una característica o propiedad de una entidad.

Pregunta clave:

> ¿Qué información necesito guardar sobre esta entidad?

---

## Ejemplo

Entidad:

```text
Cliente
```

Atributos:

```text
IdCliente
Nombre
Apellido
FechaNacimiento
Telefono
Email
```

---

## Visualización

```text
Cliente
│
├── IdCliente
├── Nombre
├── Apellido
├── FechaNacimiento
├── Telefono
└── Email
```

---

# Ejemplo Bancario

## Entidad

```text
Cliente
```

---

## Atributos

| Atributo | Descripción |
|-----------|-------------|
| IdCliente | Identificador único |
| Nombre | Nombre del cliente |
| Apellido | Apellido del cliente |
| Telefono | Número telefónico |
| Email | Correo electrónico |

---

## Representación en tabla

| IdCliente | Nombre | Apellido | Telefono |
|------------|----------|------------|------------|
| 1 | Pedro | López | 5551234 |
| 2 | Ana | García | 5559876 |

---

# Múltiples Entidades

## Banco

```text
Cliente
Cuenta
Transacción
```

---

### Cliente

```text
IdCliente
Nombre
Apellido
```

---

### Cuenta

```text
IdCuenta
NumeroCuenta
Saldo
```

---

### Transacción

```text
IdTransaccion
Fecha
Monto
Tipo
```

---

# Tipos de Atributos

## Atributo Simple

No puede dividirse.

Ejemplo:

```text
Nombre
Edad
Salario
```

---

## Atributo Compuesto

Puede dividirse en partes más pequeñas.

Ejemplo:

```text
NombreCompleto
```

Puede dividirse en:

```text
Nombre
Apellido
```

---

## Atributo Multivaluado

Puede contener múltiples valores.

Ejemplo:

```text
Telefonos
```

Un cliente puede tener:

```text
5551111
5552222
5553333
```

---

## Atributo Derivado

Se calcula a partir de otros atributos.

Ejemplo:

```text
Edad
```

calculada desde:

```text
FechaNacimiento
```

---

# Identificando Entidades

Supongamos el requerimiento:

```text
Un banco necesita almacenar
clientes, cuentas y transacciones.
```

---

## Entidades

```text
Cliente
Cuenta
Transacción
```

---

## Atributos

### Cliente

```text
IdCliente
Nombre
Apellido
Email
```

---

### Cuenta

```text
IdCuenta
NumeroCuenta
Saldo
```

---

### Transacción

```text
IdTransaccion
Fecha
Monto
```

---

# Buenas prácticas

## Utilizar nombres claros

✔ Correcto

```text
Cliente
Cuenta
Transaccion
```

---

❌ Evitar

```text
Tabla1
RegistroA
ObjetoX
```

---

## Utilizar atributos significativos

✔ Correcto

```text
Nombre
Apellido
FechaNacimiento
```

---

❌ Evitar

```text
Dato1
CampoA
ValorX
```

---

# Error común

Muchos principiantes confunden:

```text
Entidad
```

con

```text
Atributo
```

---

❌ Incorrecto

```text
Nombre
```

como entidad.

---

✔ Correcto

```text
Cliente
```

Entidad.

```text
Nombre
```

Atributo.

---

# Error conceptual frecuente

Muchos principiantes intentan modelar directamente tablas.

Incorrecto.

Primero se identifican:

```text
Entidades
```

y

```text
Atributos
```

Después se crean las tablas.

---

# Caso práctico

## Requerimiento

Una universidad necesita almacenar información sobre:

```text
Estudiantes
Profesores
Cursos
```

---

## Entidades

```text
Estudiante
Profesor
Curso
```

---

## Atributos

### Estudiante

```text
IdEstudiante
Nombre
Correo
```

---

### Profesor

```text
IdProfesor
Nombre
Especialidad
```

---

### Curso

```text
IdCurso
NombreCurso
Creditos
```

---

# Pensamiento de Modelado de Datos

Antes de crear una tabla pregúntate:

1. ¿Qué entidad estoy modelando?
2. ¿Qué información debo almacenar?
3. ¿Qué atributos son realmente necesarios?
4. ¿Qué atributos son derivados?
5. ¿Existen atributos multivaluados?

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

Una Entidad representa un objeto o concepto sobre el cual almacenamos información.

Un Atributo representa una característica de una entidad.

Ejemplo:

```text
Entidad:
Cliente

Atributos:
IdCliente
Nombre
Apellido
Telefono
Email
```

Identificar correctamente entidades y atributos es el primer paso para diseñar bases de datos profesionales y escalables.

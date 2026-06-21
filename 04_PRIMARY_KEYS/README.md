# PRIMARY KEYS

## Definición

Una Primary Key (Clave Primaria) es una columna o conjunto de columnas que identifica de manera única cada registro dentro de una tabla.

Su propósito es evitar duplicados y garantizar que cada fila pueda identificarse de forma inequívoca.

---

## ¿Por qué existen las Primary Keys?

Imagina una tabla de clientes:

| Nombre | Apellido |
|----------|-----------|
| Pedro | López |
| Pedro | López |

Pregunta:

```text
¿Cómo sabemos cuál de los dos clientes es cuál?
```

No podemos.

Necesitamos un identificador único.

---

## Solución

Agregar una Primary Key.

| IdCliente | Nombre | Apellido |
|------------|----------|-----------|
| 1 | Pedro | López |
| 2 | Pedro | López |

Ahora cada registro es único.

---

# Características de una Primary Key

Una Primary Key debe cumplir:

### Unicidad

No puede repetirse.

✔ Correcto

| IdCliente |
|------------|
| 1 |
| 2 |
| 3 |

---

❌ Incorrecto

| IdCliente |
|------------|
| 1 |
| 1 |
| 3 |

---

### No permite NULL

Cada registro debe tener una clave.

✔ Correcto

| IdCliente |
|------------|
| 1 |
| 2 |

---

❌ Incorrecto

| IdCliente |
|------------|
| 1 |
| NULL |

---

### Estabilidad

Idealmente no debería cambiar.

✔ Correcto

```text
IdCliente
IdCuenta
IdProducto
```

---

❌ Mala práctica

```text
Email
Telefono
Nombre
```

porque pueden cambiar.

---

# Sintaxis

## Crear una tabla con Primary Key

```sql
CREATE TABLE Clientes
(
    IdCliente INT PRIMARY KEY,
    Nombre VARCHAR(100),
    Apellido VARCHAR(100)
);
```

---

# Ejemplo Bancario

## Tabla Clientes

```sql
CREATE TABLE Clientes
(
    IdCliente INT PRIMARY KEY,
    Nombre VARCHAR(100),
    Apellido VARCHAR(100)
);
```

---

## Datos

| IdCliente | Nombre |
|------------|----------|
| 1 | Pedro |
| 2 | Ana |
| 3 | Luis |

---

Cada cliente posee un identificador único.

---

# Primary Key Compuesta

## Definición

En algunos casos una sola columna no es suficiente.

Se utilizan varias columnas para formar una clave única.

---

## Ejemplo

Tabla:

```text
Inscripciones
```

---

| IdAlumno | IdCurso |
|-----------|----------|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

---

Primary Key:

```sql
PRIMARY KEY (IdAlumno, IdCurso)
```

---

## SQL

```sql
CREATE TABLE Inscripciones
(
    IdAlumno INT,
    IdCurso INT,

    PRIMARY KEY
    (
        IdAlumno,
        IdCurso
    )
);
```

---

# Clave Natural

## Definición

Proviene del negocio.

Ejemplo:

```text
Número de Seguro Social
CURP
RFC
Número de Pasaporte
```

---

## Ventaja

Ya existe.

---

## Desventaja

Puede cambiar.

Puede tener reglas complejas.

---

# Clave Sustituta (Surrogate Key)

## Definición

Se crea únicamente para identificar registros.

Ejemplo:

```text
IdCliente
IdProducto
IdCuenta
```

---

## Ventajas

- Simple.
- Pequeña.
- Estable.
- Fácil de relacionar.

---

## Ejemplo

```sql
IdCliente INT
```

---

# Identity

En SQL Server es común:

```sql
CREATE TABLE Clientes
(
    IdCliente INT IDENTITY(1,1)
        PRIMARY KEY,

    Nombre VARCHAR(100)
);
```

---

## ¿Qué hace?

Genera automáticamente:

```text
1
2
3
4
5
...
```

---

# Error común

Intentar utilizar columnas no únicas.

❌ Incorrecto

```sql
Nombre
```

como Primary Key.

---

¿Por qué?

Puede haber:

```text
Pedro
Pedro
Pedro
```

---

✔ Correcto

```sql
IdCliente
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
Primary Key = Índice
```

Incorrecto.

Una Primary Key:

```text
Identifica registros.
```

Aunque normalmente genera un índice, su propósito principal es garantizar unicidad.

---

# Caso práctico

## Requerimiento

Un banco necesita almacenar cuentas.

---

## Diseño incorrecto

| NumeroCuenta | Saldo |
|--------------|--------|
| NULL | 5000 |

---

Problema:

```text
No existe forma de identificar la cuenta.
```

---

## Diseño correcto

| IdCuenta | NumeroCuenta | Saldo |
|-----------|--------------|--------|
| 1 | 123456 | 5000 |

---

# Buenas prácticas

### Utilizar claves numéricas

✔

```text
INT
BIGINT
```

---

### Mantenerlas simples

✔

```text
IdCliente
```

---

❌ Evitar

```text
Nombre_Apellido_FechaNacimiento
```

---

### Una Primary Key por tabla

Cada tabla debe tener una única clave primaria.

---

# Pensamiento de Modelado de Datos

Antes de definir una Primary Key pregúntate:

1. ¿Identifica cada registro de forma única?
2. ¿Puede contener NULL?
3. ¿Puede cambiar en el futuro?
4. ¿Es simple de utilizar?
5. ¿Es adecuada para relaciones futuras?

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

Una Primary Key identifica de forma única cada registro dentro de una tabla.

Características:

- Única.
- No permite NULL.
- Estable.
- Fácil de relacionar.

Tipos principales:

- Clave Natural.
- Clave Sustituta (Surrogate Key).
- Clave Compuesta.

Las Primary Keys son el fundamento de todas las relaciones en una base de datos relacional.

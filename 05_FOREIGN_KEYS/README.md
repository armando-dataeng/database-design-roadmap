# FOREIGN KEYS

## Definición

Una Foreign Key (Clave Foránea) es una columna que crea una relación entre dos tablas.

Su función es garantizar que los datos relacionados sean consistentes.

Una Foreign Key apunta a una Primary Key de otra tabla.

---

## ¿Por qué existen las Foreign Keys?

Supongamos que tenemos dos tablas:

```text
Clientes
Cuentas
```

Un cliente puede tener una o varias cuentas.

Necesitamos una forma de relacionarlas.

---

## Tabla Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |
| 2 | Ana |

---

## Tabla Cuentas

| IdCuenta | Saldo |
|-----------|--------|
| 101 | 5000 |
| 102 | 10000 |

---

Pregunta:

```text
¿De quién es cada cuenta?
```

No podemos saberlo.

---

## Solución

Agregar una Foreign Key.

### Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |
| 2 | Ana |

---

### Cuentas

| IdCuenta | IdCliente | Saldo |
|-----------|-----------|--------|
| 101 | 1 | 5000 |
| 102 | 2 | 10000 |

---

Ahora podemos identificar:

```text
Cuenta 101 pertenece a Pedro.

Cuenta 102 pertenece a Ana.
```

---

# Relación entre tablas

```text
Clientes
─────────────
IdCliente (PK)

        │
        │
        ▼

Cuentas
─────────────
IdCliente (FK)
```

---

# Sintaxis

## Crear tablas relacionadas

### Tabla principal

```sql
CREATE TABLE Clientes
(
    IdCliente INT PRIMARY KEY,
    Nombre VARCHAR(100)
);
```

---

### Tabla relacionada

```sql
CREATE TABLE Cuentas
(
    IdCuenta INT PRIMARY KEY,

    IdCliente INT,

    Saldo DECIMAL(10,2),

    FOREIGN KEY (IdCliente)
        REFERENCES Clientes(IdCliente)
);
```

---

# ¿Qué garantiza una Foreign Key?

## Integridad Referencial

Impide relaciones inválidas.

---

### Ejemplo válido

Clientes:

| IdCliente |
|------------|
| 1 |
| 2 |

---

Cuentas:

| IdCuenta | IdCliente |
|-----------|-----------|
| 101 | 1 |

---

SQL permite el registro.

---

### Ejemplo inválido

Clientes:

| IdCliente |
|------------|
| 1 |
| 2 |

---

Cuentas:

| IdCuenta | IdCliente |
|-----------|-----------|
| 101 | 999 |

---

Resultado:

```text
Error.
```

Porque:

```text
El cliente 999 no existe.
```

---

# Ejemplo Bancario Completo

## Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |
| 2 | Ana |

---

## Cuentas

| IdCuenta | IdCliente | Saldo |
|-----------|-----------|--------|
| 101 | 1 | 5000 |
| 102 | 1 | 12000 |
| 103 | 2 | 8000 |

---

Interpretación:

```text
Pedro tiene dos cuentas.

Ana tiene una cuenta.
```

---

# Foreign Key y JOIN

Gracias a la Foreign Key podemos utilizar JOINs.

```sql
SELECT
    c.Nombre,
    cu.IdCuenta,
    cu.Saldo
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Resultado

| Nombre | IdCuenta | Saldo |
|----------|-----------|--------|
| Pedro | 101 | 5000 |
| Pedro | 102 | 12000 |
| Ana | 103 | 8000 |

---

# Relaciones comunes

## Cliente → Cuenta

```text
Cliente
↓
Cuenta
```

---

## Pedido → DetallePedido

```text
Pedido
↓
DetallePedido
```

---

## Departamento → Empleado

```text
Departamento
↓
Empleado
```

---

## Curso → Estudiante

```text
Curso
↓
Inscripción
```

---

# ON DELETE

Controla qué ocurre cuando se elimina un registro padre.

---

## CASCADE

```sql
FOREIGN KEY (IdCliente)
REFERENCES Clientes(IdCliente)
ON DELETE CASCADE
```

---

### Ejemplo

Eliminar:

```text
Cliente 1
```

---

Resultado:

```text
Se eliminan automáticamente
sus cuentas.
```

---

# ON DELETE SET NULL

```sql
ON DELETE SET NULL
```

---

Resultado:

```text
La Foreign Key se vuelve NULL.
```

---

# ON UPDATE CASCADE

Si cambia la Primary Key:

```sql
ON UPDATE CASCADE
```

Las Foreign Keys se actualizan automáticamente.

---

# Error común

❌ Insertar registros huérfanos.

```sql
INSERT INTO Cuentas
VALUES
(
    101,
    999,
    5000
);
```

---

Problema:

```text
Cliente 999 no existe.
```

---

✔ Correcto

Primero:

```sql
INSERT INTO Clientes
VALUES
(
    999,
    'Pedro'
);
```

Luego:

```sql
INSERT INTO Cuentas
VALUES
(
    101,
    999,
    5000
);
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
La Foreign Key almacena datos de otra tabla.
```

Incorrecto.

La Foreign Key únicamente almacena:

```text
La referencia.
```

---

Ejemplo:

```text
Cuentas.IdCliente = 1
```

No almacena:

```text
Pedro
López
Correo
```

Solo:

```text
1
```

---

# Caso práctico

## Universidad

### Estudiantes

| IdEstudiante | Nombre |
|---------------|---------|
| 1 | Juan |
| 2 | María |

---

### Cursos

| IdCurso | NombreCurso |
|----------|-------------|
| 101 | SQL |
| 102 | Python |

---

### Inscripciones

| IdEstudiante | IdCurso |
|---------------|----------|
| 1 | 101 |
| 2 | 102 |

---

Foreign Keys:

```text
IdEstudiante → Estudiantes

IdCurso → Cursos
```

---

# Pensamiento de Modelado de Datos

Antes de crear una Foreign Key pregúntate:

1. ¿Qué tablas deben relacionarse?
2. ¿Cuál es la tabla padre?
3. ¿Cuál es la tabla hija?
4. ¿Qué ocurre si se elimina un registro?
5. ¿Necesito integridad referencial?

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

Una Foreign Key conecta dos tablas mediante una relación.

Características:

- Apunta a una Primary Key.
- Garantiza integridad referencial.
- Evita registros huérfanos.
- Permite realizar JOINs.
- Mantiene consistencia entre tablas.

Sin Foreign Keys tendríamos tablas aisladas.

Con Foreign Keys obtenemos una verdadera base de datos relacional.

# DATABASE FUNDAMENTALS

## Definición

Una Base de Datos (Database) es un sistema diseñado para almacenar, organizar y gestionar información de manera estructurada.

Su objetivo es permitir que los datos puedan ser:

- Almacenados.
- Consultados.
- Modificados.
- Eliminados.
- Protegidos.

de forma eficiente.

---

## ¿Por qué existen las bases de datos?

Imagina un banco que guarda información de:

- Clientes
- Cuentas
- Transacciones
- Empleados

Sin una base de datos:

```text
La información estaría dispersa.
Sería difícil encontrar datos.
Aumentarían los errores.
```

Las bases de datos resuelven estos problemas.

---

## Conceptos clave

Una base de datos permite:

### Persistencia

Los datos permanecen almacenados incluso después de apagar el sistema.

Ejemplo:

```text
Cliente:
Pedro López

Cuenta:
123456

Saldo:
5000
```

La información sigue existiendo mañana.

---

### Integridad

Los datos deben ser correctos y consistentes.

Ejemplo:

```text
No puede existir una cuenta
sin un cliente asociado.
```

---

### Seguridad

Permite controlar quién puede:

```text
Leer datos
Insertar datos
Modificar datos
Eliminar datos
```

---

### Escalabilidad

Puede manejar:

```text
100 registros
1000 registros
1 millón de registros
100 millones de registros
```

---

## Componentes principales

### Datos

Información almacenada.

Ejemplo:

```text
Nombre
Apellido
Saldo
Fecha
```

---

### Tablas

Estructuras donde se almacenan los datos.

Ejemplo:

```text
Clientes
Cuentas
Transacciones
```

---

### Filas

Representan registros individuales.

Ejemplo:

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |
| 2 | Ana |

Cada fila representa un cliente.

---

### Columnas

Representan atributos.

Ejemplo:

| IdCliente | Nombre | Apellido |
|------------|---------|-----------|

---

## Ejemplo bancario

Tabla:

```text
Clientes
```

| IdCliente | Nombre | Apellido |
|------------|---------|-----------|
| 1 | Pedro | López |
| 2 | Ana | García |

---

Tabla:

```text
Cuentas
```

| IdCuenta | IdCliente | Saldo |
|-----------|-----------|--------|
| 101 | 1 | 5000 |
| 102 | 2 | 12000 |

---

## Sistemas Gestores de Bases de Datos (DBMS)

Un DBMS es el software que administra la base de datos.

Ejemplos:

### Relacionales

- SQL Server
- PostgreSQL
- MySQL
- Oracle

---

### No Relacionales

- MongoDB
- Cassandra
- Redis
- DynamoDB

---

## Bases de Datos Relacionales

Organizan los datos en tablas relacionadas entre sí.

Ejemplo:

```text
Clientes
↓
Cuentas
↓
Transacciones
```

Utilizan:

```text
Primary Keys
Foreign Keys
Relaciones
```

---

## Bases de Datos No Relacionales

Organizan datos mediante:

```text
Documentos
Grafos
Clave-Valor
Columnas
```

Ejemplo:

```json
{
  "cliente": "Pedro",
  "saldo": 5000
}
```

---

## ¿Qué es SQL?

SQL significa:

```text
Structured Query Language
```

Es el lenguaje utilizado para interactuar con bases de datos relacionales.

Permite:

```sql
SELECT
INSERT
UPDATE
DELETE
```

---

## Ciclo de vida de los datos

1. Crear datos.

```text
Cliente abre una cuenta.
```

2. Almacenar datos.

```text
Base de datos registra la cuenta.
```

3. Consultar datos.

```sql
SELECT *
FROM Clientes;
```

4. Actualizar datos.

```sql
UPDATE Clientes
```

5. Eliminar datos.

```sql
DELETE FROM Clientes
```

---

## Casos de uso reales

### Banco

```text
Clientes
Cuentas
Transacciones
```

---

### E-commerce

```text
Productos
Pedidos
Clientes
```

---

### Hospital

```text
Pacientes
Médicos
Citas
```

---

### Universidad

```text
Alumnos
Profesores
Materias
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```text
Base de datos = Tabla
```

Incorrecto.

Una tabla es solo una parte de una base de datos.

Una base de datos puede contener:

```text
Tablas
Vistas
Procedimientos
Funciones
Índices
Triggers
```

---

## Pensamiento de Arquitectura de Datos

Antes de diseñar una base de datos pregúntate:

1. ¿Qué información debo almacenar?
2. ¿Qué entidades existen?
3. ¿Cómo se relacionan?
4. ¿Cuánto crecerán los datos?
5. ¿Quién utilizará la información?

---

## Relación con los siguientes módulos

En este roadmap aprenderás:

```text
DATABASE FUNDAMENTALS
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
↓
DATA WAREHOUSE DESIGN
```

---

## Resumen

Una base de datos es un sistema diseñado para almacenar y gestionar información de forma estructurada.

Conceptos fundamentales:

- Datos
- Tablas
- Filas
- Columnas
- Relaciones
- Integridad
- Seguridad
- Escalabilidad

Comprender estos conceptos es el primer paso para convertirse en:

- Database Engineer
- DBA
- Data Engineer
- Data Architect
- Analytics Engineer

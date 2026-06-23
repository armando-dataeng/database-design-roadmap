# NORMALIZATION

## Definición

La Normalización es el proceso de organizar los datos dentro de una base de datos para reducir la redundancia y mejorar la integridad de la información.

Su objetivo es:

- Evitar duplicación de datos.
- Reducir inconsistencias.
- Facilitar el mantenimiento.
- Mejorar la calidad de los datos.

---

## ¿Por qué existe la normalización?

Supongamos una tabla:

| Cliente | Cuenta | Saldo |
|----------|---------|--------|
| Pedro | 123 | 5000 |
| Pedro | 456 | 10000 |
| Pedro | 789 | 7000 |

Observa:

```text
Pedro aparece repetido tres veces.
```

Esto genera problemas:

- Duplicación de información.
- Mayor almacenamiento.
- Riesgo de inconsistencias.

---

## Problemas que resuelve

### Anomalía de Inserción

No podemos registrar un cliente si aún no tiene cuenta.

---

### Anomalía de Actualización

Si Pedro cambia su nombre:

```text
Pedro → Pedro López
```

debemos actualizar múltiples filas.

---

### Anomalía de Eliminación

Si eliminamos la última cuenta:

```text
Cuenta 789
```

podríamos perder información del cliente.

---

## Solución

Separar los datos.

### Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |

---

### Cuentas

| IdCuenta | IdCliente | Saldo |
|-----------|-----------|--------|
| 123 | 1 | 5000 |
| 456 | 1 | 10000 |
| 789 | 1 | 7000 |

---

## Formas Normales

### Primera Forma Normal (1NF)

Elimina grupos repetitivos.

Garantiza:

```text
Valores atómicos.
```

---

### Segunda Forma Normal (2NF)

Elimina dependencias parciales.

Garantiza:

```text
Dependencia completa de la clave.
```

---

### Tercera Forma Normal (3NF)

Elimina dependencias transitivas.

Garantiza:

```text
Cada atributo depende únicamente de la clave.
```

---

### Boyce-Codd Normal Form (BCNF)

Versión más estricta de 3NF.

Resuelve casos especiales de dependencias funcionales.

---

## Flujo de Normalización

```text
Datos sin normalizar
        ↓
1NF
        ↓
2NF
        ↓
3NF
        ↓
BCNF
```

---

## Beneficios

- Menor redundancia.
- Mejor integridad.
- Menor riesgo de errores.
- Mejor mantenimiento.
- Diseño profesional.

---

## Desventajas

Una base de datos altamente normalizada puede requerir:

```text
Más tablas
Más JOINs
Consultas más complejas
```

Por esta razón existe:

```text
DENORMALIZATION
```

que estudiarás posteriormente.

---

## Caso Bancario

Sistema:

```text
Clientes
Cuentas
Transacciones
```

La normalización permite:

- Separar clientes.
- Separar cuentas.
- Separar transacciones.

y relacionarlas mediante claves.

---

## Relación con los siguientes módulos

```text
NORMALIZATION
│
├── 1NF
├── 2NF
├── 3NF
├── BCNF
└── CASE STUDY
```

---

## Resumen

La normalización es una técnica de diseño de bases de datos que busca reducir redundancia y mejorar integridad.

Formas normales:

- 1NF
- 2NF
- 3NF
- BCNF

Es uno de los pilares fundamentales del diseño relacional y la arquitectura de datos.

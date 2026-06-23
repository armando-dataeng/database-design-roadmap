# FIRST NORMAL FORM (1NF)

## Definición

La Primera Forma Normal (1NF) establece que cada columna debe contener valores atómicos e indivisibles.

Una tabla cumple 1NF cuando:

- Cada celda contiene un único valor.
- No existen grupos repetitivos.
- No existen listas dentro de una columna.
- Cada fila puede identificarse de forma única.

---

## ¿Por qué existe 1NF?

Las bases de datos relacionales están diseñadas para almacenar datos estructurados.

Cuando una columna contiene múltiples valores:

```text
SQL no puede relacionar los datos correctamente.
```

Esto dificulta:

- Consultas.
- Actualizaciones.
- Eliminaciones.
- Relaciones entre tablas.

---

# ¿Qué significa valor atómico?

Atómico significa:

```text
Un solo valor por celda.
```

---

## Incorrecto

| IdCliente | Nombre | Telefonos |
|------------|---------|------------|
| 1 | Pedro | 5551111,5552222 |

---

Problema:

```text
La columna Telefonos contiene múltiples valores.
```

---

## Correcto

| IdCliente | Nombre | Telefono |
|------------|---------|----------|
| 1 | Pedro | 5551111 |
| 1 | Pedro | 5552222 |

o mejor:

### Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |

---

### Telefonos

| IdTelefono | IdCliente | Telefono |
|------------|------------|----------|
| 1 | 1 | 5551111 |
| 2 | 1 | 5552222 |

---

# Grupos repetitivos

## Incorrecto

| Cliente | Cuenta1 | Cuenta2 | Cuenta3 |
|----------|----------|----------|----------|
| Pedro | 123 | 456 | 789 |

---

Problema:

```text
Las columnas representan grupos repetitivos.
```

---

## Correcto

### Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |

---

### Cuentas

| IdCuenta | IdCliente |
|-----------|-----------|
| 123 | 1 |
| 456 | 1 |
| 789 | 1 |

---

# Caso Bancario

## Diseño NO normalizado

| Cliente | Cuentas |
|----------|----------|
| Pedro | 123,456,789 |
| Ana | 999,888 |

---

Problemas:

### Consultas difíciles

¿Cómo buscar la cuenta 456?

---

### Actualizaciones complejas

¿Cómo eliminar únicamente la cuenta 456?

---

### Integridad deficiente

No existe una relación clara entre cliente y cuenta.

---

# Diseño en 1NF

### Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |
| 2 | Ana |

---

### Cuentas

| IdCuenta | IdCliente |
|-----------|-----------|
| 123 | 1 |
| 456 | 1 |
| 789 | 1 |
| 999 | 2 |
| 888 | 2 |

---

Ahora:

```text
Cada valor es atómico.
```

---

# Otro ejemplo

## Incorrecto

| IdPedido | Productos |
|-----------|------------|
| 100 | Laptop,Mouse,Teclado |

---

Problema:

```text
Una celda contiene múltiples productos.
```

---

## Correcto

### Pedidos

| IdPedido |
|-----------|
| 100 |

---

### DetallePedido

| IdPedido | Producto |
|-----------|----------|
| 100 | Laptop |
| 100 | Mouse |
| 100 | Teclado |

---

# Cómo identificar violaciones a 1NF

Pregúntate:

### ¿Existe una lista dentro de una columna?

Ejemplo:

```text
Rojo, Azul, Verde
```

---

### ¿Existen columnas repetidas?

Ejemplo:

```text
Telefono1
Telefono2
Telefono3
```

---

### ¿Existe más de un valor por celda?

Ejemplo:

```text
123,456
```

---

Si la respuesta es:

```text
Sí
```

la tabla probablemente no cumple 1NF.

---

# Beneficios de 1NF

## Consultas más simples

```sql
SELECT *
FROM Cuentas
WHERE IdCuenta = 456;
```

---

## Mejor integridad

Cada dato ocupa una única ubicación.

---

## Relaciones más claras

Las Foreign Keys funcionan correctamente.

---

## Base para la normalización

2NF y 3NF dependen de 1NF.

---

# Error común

Muchos principiantes crean columnas como:

```text
Telefono1
Telefono2
Telefono3
```

---

Problema:

```text
No sabemos cuántos teléfonos existirán.
```

---

Solución:

```text
Tabla Telefonos
```

relacionada mediante Foreign Key.

---

# Error conceptual frecuente

Muchos creen que:

```text
1NF significa una tabla por entidad.
```

Incorrecto.

1NF significa:

```text
Valores atómicos.
```

La separación en múltiples tablas ocurre como consecuencia del diseño, pero no es la definición de 1NF.

---

# Caso práctico

## Requerimiento

Un cliente puede tener múltiples correos electrónicos.

---

## Diseño incorrecto

| IdCliente | Correos |
|------------|----------|
| 1 | a@email.com,b@email.com |

---

## Diseño correcto

### Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |

---

### Correos

| IdCorreo | IdCliente | Correo |
|-----------|-----------|---------|
| 1 | 1 | a@email.com |
| 2 | 1 | b@email.com |

---

# Pensamiento de Modelado de Datos

Antes de diseñar una tabla pregúntate:

1. ¿Cada celda contiene un único valor?
2. ¿Existen listas dentro de columnas?
3. ¿Existen columnas repetidas?
4. ¿Puedo relacionar los datos fácilmente?
5. ¿La estructura funcionará si crecen los datos?

---

# Relación con las siguientes formas normales

```text
1NF
↓
2NF
↓
3NF
↓
BCNF
```

---

# Resumen

La Primera Forma Normal (1NF) exige que los datos sean atómicos.

Reglas principales:

- Un valor por celda.
- Sin listas.
- Sin grupos repetitivos.
- Sin columnas duplicadas conceptualmente.

1NF es la base sobre la cual se construyen todas las demás formas normales.

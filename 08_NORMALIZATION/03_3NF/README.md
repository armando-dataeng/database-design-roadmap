# THIRD NORMAL FORM (3NF)

## Definición

La Tercera Forma Normal (3NF) elimina las dependencias transitivas.

Una tabla cumple 3NF cuando:

1. Cumple 2NF.
2. Ningún atributo no clave depende de otro atributo no clave.

En otras palabras:

```text
Todos los atributos deben depender
únicamente de la clave primaria.
```

---

## ¿Qué es una dependencia transitiva?

Ocurre cuando:

```text
Clave Primaria
        ↓
Atributo A
        ↓
Atributo B
```

Es decir:

```text
Atributo B depende de A
en lugar de depender directamente
de la clave primaria.
```

---

# Ejemplo sencillo

## Tabla Empleados

| IdEmpleado | Nombre | IdDepartamento | NombreDepartamento |
|------------|---------|----------------|-------------------|
| 1 | Pedro | 10 | Finanzas |
| 2 | Ana | 20 | Tecnología |
| 3 | Luis | 10 | Finanzas |

---

Clave primaria:

```text
IdEmpleado
```

---

Observemos:

```text
NombreDepartamento
```

---

¿Depende de:

```text
IdEmpleado?
```

No.

---

Depende de:

```text
IdDepartamento
```

---

Tenemos:

```text
IdEmpleado
        ↓
IdDepartamento
        ↓
NombreDepartamento
```

Esto es una:

```text
Dependencia Transitiva
```

---

# ¿Por qué es un problema?

## Redundancia

La palabra:

```text
Finanzas
```

aparece muchas veces.

---

## Actualizaciones complejas

Si:

```text
Finanzas
```

cambia a:

```text
Finanzas Corporativas
```

debemos modificar múltiples filas.

---

## Riesgo de inconsistencias

Podrían existir registros como:

```text
Finanzas
```

y otros como:

```text
Finanzas Corp.
```

---

# Solución

Separar la entidad Departamento.

---

## Empleados

| IdEmpleado | Nombre | IdDepartamento |
|------------|---------|----------------|
| 1 | Pedro | 10 |
| 2 | Ana | 20 |
| 3 | Luis | 10 |

---

## Departamentos

| IdDepartamento | NombreDepartamento |
|----------------|--------------------|
| 10 | Finanzas |
| 20 | Tecnología |

---

Ahora:

```text
NombreDepartamento
```

depende de:

```text
IdDepartamento
```

dentro de su propia tabla.

---

No existe dependencia transitiva.

---

# Caso Bancario

## Diseño incorrecto

| IdCuenta | Saldo | IdSucursal | NombreSucursal |
|-----------|--------|-------------|----------------|
| 100 | 5000 | 1 | Centro |
| 101 | 10000 | 1 | Centro |
| 102 | 3000 | 2 | Norte |

---

Clave:

```text
IdCuenta
```

---

Problema:

```text
NombreSucursal
```

depende de:

```text
IdSucursal
```

---

No depende directamente de:

```text
IdCuenta
```

---

Violación de 3NF.

---

# Diseño correcto

## Cuentas

| IdCuenta | Saldo | IdSucursal |
|-----------|--------|-------------|
| 100 | 5000 | 1 |
| 101 | 10000 | 1 |
| 102 | 3000 | 2 |

---

## Sucursales

| IdSucursal | NombreSucursal |
|------------|----------------|
| 1 | Centro |
| 2 | Norte |

---

Ahora:

```text
Cada atributo depende
de la clave de su propia tabla.
```

---

# Regla práctica

Pregunta:

```text
¿Este atributo depende
directamente de la clave primaria?
```

---

Si responde:

```text
No
```

entonces probablemente existe una dependencia transitiva.

---

# Comparación

## 1NF

Elimina:

```text
Valores múltiples.
```

---

## 2NF

Elimina:

```text
Dependencias parciales.
```

---

## 3NF

Elimina:

```text
Dependencias transitivas.
```

---

# Ejemplo Universitario

## Diseño incorrecto

| IdAlumno | NombreAlumno | IdCarrera | NombreCarrera |
|-----------|-------------|-----------|---------------|
| 1 | Juan | 10 | Ingeniería |
| 2 | María | 10 | Ingeniería |
| 3 | Luis | 20 | Medicina |

---

Problema:

```text
NombreCarrera
```

depende de:

```text
IdCarrera
```

---

No depende directamente de:

```text
IdAlumno
```

---

# Diseño correcto

## Alumnos

| IdAlumno | NombreAlumno | IdCarrera |
|-----------|-------------|-----------|
| 1 | Juan | 10 |
| 2 | María | 10 |
| 3 | Luis | 20 |

---

## Carreras

| IdCarrera | NombreCarrera |
|-----------|---------------|
| 10 | Ingeniería |
| 20 | Medicina |

---

# Beneficios de 3NF

## Menor redundancia

Información almacenada una sola vez.

---

## Mayor integridad

Menos riesgo de inconsistencias.

---

## Actualizaciones simples

Un cambio se realiza en un único lugar.

---

## Mejor mantenimiento

Diseño más limpio y escalable.

---

# Error común

Muchos principiantes almacenan:

```text
NombreCliente
NombreSucursal
NombreDepartamento
```

en tablas donde ya existe:

```text
IdCliente
IdSucursal
IdDepartamento
```

---

Esto suele indicar una violación de 3NF.

---

# Error conceptual frecuente

Muchos creen que:

```text
Más tablas = mejor diseño.
```

Incorrecto.

El objetivo no es crear más tablas.

El objetivo es:

```text
Eliminar dependencias incorrectas.
```

---

# Pensamiento de Modelado de Datos

Antes de aceptar una tabla pregúntate:

1. ¿Todos los atributos dependen de la clave primaria?
2. ¿Existe algún atributo que dependa de otro atributo?
3. ¿Hay información repetida?
4. ¿Puedo separar una nueva entidad?
5. ¿Existe una dependencia transitiva?

---

# Relación con la siguiente forma normal

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

## ¿Qué elimina cada una?

```text
1NF → Valores no atómicos

2NF → Dependencias parciales

3NF → Dependencias transitivas

BCNF → Dependencias funcionales complejas
```

---

# Resumen

La Tercera Forma Normal (3NF) elimina dependencias transitivas.

Requisitos:

- Cumplir 2NF.
- Los atributos no clave deben depender únicamente de la clave primaria.

Objetivos:

- Reducir redundancia.
- Evitar inconsistencias.
- Mejorar mantenimiento.
- Crear modelos relacionales sólidos.

3NF es la forma normal más utilizada en sistemas OLTP profesionales.

# SECOND NORMAL FORM (2NF)

## Definición

La Segunda Forma Normal (2NF) busca eliminar las dependencias parciales.

Una tabla cumple 2NF cuando:

1. Ya cumple 1NF.
2. Todos los atributos no clave dependen de la clave primaria completa.

---

## Conceptos clave

Para comprender 2NF primero debemos entender:

```text
Clave primaria compuesta
```

---

## Clave primaria compuesta

Una clave compuesta utiliza más de una columna para identificar un registro.

Ejemplo:

```text
(IdAlumno, IdCurso)
```

---

Tabla:

| IdAlumno | IdCurso |
|-----------|----------|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

---

La combinación:

```text
(IdAlumno, IdCurso)
```

identifica cada fila.

---

# ¿Qué es una dependencia parcial?

Ocurre cuando una columna depende únicamente de una parte de la clave compuesta.

No depende de toda la clave.

---

## Problema

Tabla:

| IdAlumno | IdCurso | NombreAlumno | NombreCurso |
|-----------|----------|---------------|-------------|
| 1 | 101 | Pedro | SQL |
| 1 | 102 | Pedro | Python |
| 2 | 101 | Ana | SQL |

---

Clave primaria:

```text
(IdAlumno, IdCurso)
```

---

Observemos:

```text
NombreAlumno
```

depende solamente de:

```text
IdAlumno
```

---

No necesita:

```text
IdCurso
```

---

También:

```text
NombreCurso
```

depende solamente de:

```text
IdCurso
```

---

No necesita:

```text
IdAlumno
```

---

Esto es una:

```text
Dependencia Parcial
```

---

# ¿Por qué es un problema?

## Redundancia

Pedro aparece múltiples veces.

---

## Actualizaciones complejas

Si Pedro cambia de nombre:

```text
Pedro → Pedro López
```

debemos actualizar varias filas.

---

## Riesgo de inconsistencias

Una fila podría quedar:

```text
Pedro
```

y otra:

```text
Pedro López
```

---

# Solución

Separar la información.

---

## Alumnos

| IdAlumno | NombreAlumno |
|-----------|---------------|
| 1 | Pedro |
| 2 | Ana |

---

## Cursos

| IdCurso | NombreCurso |
|----------|-------------|
| 101 | SQL |
| 102 | Python |

---

## Inscripciones

| IdAlumno | IdCurso |
|-----------|----------|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

---

Ahora:

```text
NombreAlumno
```

depende de:

```text
IdAlumno
```

---

Y:

```text
NombreCurso
```

depende de:

```text
IdCurso
```

---

No existe dependencia parcial.

---

# Caso bancario

## Diseño incorrecto

| IdCliente | IdCuenta | NombreCliente | Saldo |
|------------|-----------|----------------|--------|
| 1 | 100 | Pedro | 5000 |
| 1 | 101 | Pedro | 12000 |
| 2 | 102 | Ana | 3000 |

---

Clave:

```text
(IdCliente, IdCuenta)
```

---

Problema:

```text
NombreCliente
```

depende solamente de:

```text
IdCliente
```

---

Violación de 2NF.

---

# Diseño correcto

## Clientes

| IdCliente | NombreCliente |
|------------|----------------|
| 1 | Pedro |
| 2 | Ana |

---

## Cuentas

| IdCuenta | IdCliente | Saldo |
|-----------|-----------|--------|
| 100 | 1 | 5000 |
| 101 | 1 | 12000 |
| 102 | 2 | 3000 |

---

Ahora:

```text
Cada atributo depende
de su clave correspondiente.
```

---

# Regla práctica

Pregunta:

```text
¿Este atributo depende
de TODA la clave?
```

---

Si responde:

```text
No
```

existe una dependencia parcial.

---

# Cómo detectar una violación de 2NF

Supongamos:

Clave:

```text
(IdProducto, IdProveedor)
```

---

Atributo:

```text
NombreProducto
```

---

Pregunta:

```text
¿Necesita IdProveedor?
```

---

Respuesta:

```text
No
```

---

Entonces:

```text
Violación de 2NF.
```

---

# Beneficios de 2NF

## Menos redundancia

Información almacenada una sola vez.

---

## Menos errores

Actualizaciones más simples.

---

## Mejor mantenimiento

Cambios realizados en un único lugar.

---

## Diseño más limpio

Relaciones más claras.

---

# Error común

Muchos estudiantes creen:

```text
2NF aplica a todas las tablas.
```

---

Realmente:

```text
2NF se vuelve importante
cuando existen claves compuestas.
```

---

# Error conceptual frecuente

Muchos creen que:

```text
Eliminar columnas
es normalizar.
```

---

Incorrecto.

Normalizar significa:

```text
Mover atributos
a entidades correctas.
```

---

# Comparación

## 1NF

Resuelve:

```text
Valores múltiples.
```

---

## 2NF

Resuelve:

```text
Dependencias parciales.
```

---

# Flujo de normalización

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

# Pensamiento de Modelado de Datos

Antes de aceptar una tabla pregúntate:

1. ¿Existe una clave compuesta?
2. ¿Todos los atributos dependen de toda la clave?
3. ¿Hay datos repetidos?
4. ¿Existen dependencias parciales?
5. ¿Puedo separar entidades?

---

# Relación con la siguiente forma normal

```text
1NF
↓
2NF
↓
3NF
```

1NF elimina:

```text
Valores no atómicos.
```

---

2NF elimina:

```text
Dependencias parciales.
```

---

3NF eliminará:

```text
Dependencias transitivas.
```

---

# Resumen

La Segunda Forma Normal (2NF) elimina dependencias parciales.

Requisitos:

- Cumplir 1NF.
- Todos los atributos no clave deben depender de la clave completa.

Objetivos:

- Reducir redundancia.
- Mejorar consistencia.
- Facilitar mantenimiento.

2NF es especialmente importante cuando existen claves primarias compuestas.

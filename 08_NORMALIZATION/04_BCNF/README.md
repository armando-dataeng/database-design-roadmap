# BOYCE-CODD NORMAL FORM (BCNF)

## Definición

La Forma Normal de Boyce-Codd (BCNF) es una versión más estricta de la Tercera Forma Normal (3NF).

Una tabla cumple BCNF cuando:

```text
Todo determinante debe ser una clave candidata.
```

---

## ¿Qué significa determinante?

Un determinante es una columna o conjunto de columnas que determina el valor de otra columna.

Ejemplo:

```text
IdCliente → NombreCliente
```

Esto significa:

```text
Conociendo IdCliente
puedo conocer NombreCliente.
```

---

# ¿Por qué existe BCNF?

Existen tablas que cumplen:

```text
1NF
2NF
3NF
```

pero todavía presentan redundancia y anomalías.

BCNF fue creada para resolver esos casos especiales.

---

# Conceptos clave

## Clave candidata

Es cualquier columna o conjunto de columnas que puede identificar un registro de forma única.

Ejemplo:

```text
IdCliente
```

o

```text
NumeroDocumento
```

si ambos son únicos.

---

# Caso clásico

## Asignación de profesores

Supongamos la siguiente regla:

```text
Un profesor imparte una única materia.

Una materia puede ser impartida por varios profesores.
```

---

## Tabla

| Profesor | Materia | Aula |
|-----------|----------|------|
| Juan | SQL | A101 |
| Pedro | Python | A102 |
| Ana | SQL | A101 |

---

Supongamos además:

```text
Cada materia tiene un aula fija.
```

---

Entonces:

```text
Materia → Aula
```

---

# Dependencias funcionales

Tenemos:

```text
Profesor → Materia
```

y

```text
Materia → Aula
```

---

Por lo tanto:

```text
Profesor → Aula
```

---

Problema:

```text
Materia
```

determina:

```text
Aula
```

pero:

```text
Materia
```

no es clave candidata.

---

Violación de BCNF.

---

# ¿Qué problemas genera?

## Redundancia

La información del aula se repite.

---

| Profesor | Materia | Aula |
|-----------|----------|------|
| Juan | SQL | A101 |
| Ana | SQL | A101 |

---

## Actualizaciones

Si:

```text
SQL cambia de aula
```

deben actualizarse varias filas.

---

## Inconsistencias

Podríamos tener:

| Profesor | Materia | Aula |
|-----------|----------|------|
| Juan | SQL | A101 |
| Ana | SQL | A105 |

---

¿Cuál es correcta?

No lo sabemos.

---

# Solución

Separar las entidades.

---

## Materias

| Materia | Aula |
|----------|------|
| SQL | A101 |
| Python | A102 |

---

## Profesores

| Profesor | Materia |
|-----------|----------|
| Juan | SQL |
| Ana | SQL |
| Pedro | Python |

---

Ahora:

```text
Cada dependencia
se almacena una sola vez.
```

---

# Caso Bancario

Supongamos:

```text
Cada sucursal tiene un único gerente.
```

---

Tabla:

| Cuenta | Sucursal | Gerente |
|---------|-----------|----------|
| 100 | Centro | Laura |
| 101 | Centro | Laura |
| 102 | Norte | Pedro |

---

Dependencia:

```text
Sucursal → Gerente
```

---

Problema:

```text
Gerente
```

se repite muchas veces.

---

Violación potencial de BCNF.

---

# Solución

## Sucursales

| IdSucursal | Gerente |
|-------------|----------|
| Centro | Laura |
| Norte | Pedro |

---

## Cuentas

| Cuenta | Sucursal |
|---------|-----------|
| 100 | Centro |
| 101 | Centro |
| 102 | Norte |

---

# Regla práctica

Pregunta:

```text
¿Existe algún atributo
que determine otro atributo
sin ser clave candidata?
```

---

Si la respuesta es:

```text
Sí
```

puede existir una violación de BCNF.

---

# Comparación

## 3NF

Permite algunas dependencias funcionales.

---

## BCNF

Es más estricta.

Exige que:

```text
Todo determinante
sea una clave candidata.
```

---

# Beneficios

## Menos redundancia

Información almacenada una sola vez.

---

## Mayor consistencia

Menor riesgo de contradicciones.

---

## Diseño más sólido

Especialmente en modelos complejos.

---

# Desventajas

En algunos casos:

```text
Más tablas.
Más JOINs.
Mayor complejidad.
```

---

Por eso muchas bases de datos empresariales:

```text
3NF
```

es suficiente.

---

# Error común

Muchos estudiantes creen que:

```text
BCNF siempre es necesaria.
```

---

Incorrecto.

La mayoría de los sistemas operan correctamente en:

```text
3NF
```

---

# Error conceptual frecuente

Muchos creen que:

```text
BCNF reemplaza 3NF.
```

---

Incorrecto.

BCNF:

```text
Extiende 3NF.
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

# Pensamiento de Arquitectura de Datos

Antes de aplicar BCNF pregúntate:

1. ¿Existen dependencias funcionales complejas?
2. ¿Hay redundancia que 3NF no elimina?
3. ¿Existen anomalías de actualización?
4. ¿El beneficio justifica más tablas?
5. ¿Estoy diseñando un sistema OLTP o analítico?

---

# Relación con el siguiente módulo

```text
NORMALIZATION
│
├── 1NF
├── 2NF
├── 3NF
├── BCNF
└── NORMALIZATION_CASE_STUDY
```

---

# Resumen

BCNF (Boyce-Codd Normal Form) es una versión más estricta de 3NF.

Regla principal:

```text
Todo determinante
debe ser una clave candidata.
```

Objetivos:

- Reducir redundancia.
- Evitar anomalías.
- Mejorar consistencia.

BCNF es especialmente útil en modelos complejos donde 3NF no elimina todas las dependencias problemáticas.

# NORMALIZATION CASE STUDY

## Objetivo

Aplicar todo el proceso de normalización utilizando un caso práctico.

Analizaremos cómo una estructura inicial con redundancia evoluciona hasta un diseño normalizado.

---

# Caso de estudio

## Universidad

La universidad necesita almacenar:

- Estudiantes
- Cursos
- Profesores
- Aulas

---

# Diseño Inicial (Sin Normalizar)

| IdEstudiante | NombreEstudiante | Cursos | Profesor | Aula |
|-------------|------------------|---------|-----------|------|
| 1 | Juan | SQL,Python | Pedro | A101 |
| 2 | María | SQL | Pedro | A101 |

---

## Problemas

### Valores múltiples

```text
SQL,Python
```

---

### Información repetida

```text
Pedro
A101
```

---

### Difícil de consultar

¿Cómo saber cuántos estudiantes toman Python?

---

### Difícil de actualizar

Si SQL cambia de aula:

```text
A101 → A201
```

deben modificarse múltiples registros.

---

# Paso 1: Primera Forma Normal (1NF)

## Regla

```text
Un valor por celda.
```

---

## Resultado

| IdEstudiante | NombreEstudiante | Curso | Profesor | Aula |
|-------------|------------------|--------|-----------|------|
| 1 | Juan | SQL | Pedro | A101 |
| 1 | Juan | Python | Ana | A102 |
| 2 | María | SQL | Pedro | A101 |

---

## Mejoras

✔ Sin listas

✔ Valores atómicos

---

## Problema restante

La información sigue duplicada.

---

# Paso 2: Segunda Forma Normal (2NF)

## Clave compuesta

```text
(IdEstudiante, Curso)
```

---

Observemos:

```text
NombreEstudiante
```

depende únicamente de:

```text
IdEstudiante
```

---

Existe:

```text
Dependencia Parcial
```

---

# Solución

## Estudiantes

| IdEstudiante | NombreEstudiante |
|-------------|------------------|
| 1 | Juan |
| 2 | María |

---

## Inscripciones

| IdEstudiante | Curso |
|-------------|--------|
| 1 | SQL |
| 1 | Python |
| 2 | SQL |

---

## Problema restante

```text
Profesor
Aula
```

siguen dependiendo del curso.

---

# Paso 3: Tercera Forma Normal (3NF)

Observemos:

```text
Curso
↓
Profesor
```

---

y

```text
Curso
↓
Aula
```

---

Tenemos:

```text
Dependencias Transitivas
```

---

# Solución

## Cursos

| IdCurso | NombreCurso | Profesor | Aula |
|----------|------------|-----------|------|
| 101 | SQL | Pedro | A101 |
| 102 | Python | Ana | A102 |

---

## Estudiantes

| IdEstudiante | Nombre |
|-------------|---------|
| 1 | Juan |
| 2 | María |

---

## Inscripciones

| IdEstudiante | IdCurso |
|-------------|----------|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

---

## Mejoras

✔ Menos redundancia

✔ Menos actualizaciones

✔ Mayor consistencia

---

# Paso 4: BCNF

Supongamos la siguiente regla:

```text
Cada profesor utiliza
siempre la misma aula.
```

---

Entonces:

```text
Profesor
↓
Aula
```

---

En la tabla:

| IdCurso | Curso | Profesor | Aula |
|----------|--------|-----------|------|
| 101 | SQL | Pedro | A101 |
| 102 | Python | Ana | A102 |

---

Existe una dependencia funcional:

```text
Profesor → Aula
```

---

BCNF detecta este problema.

---

# Solución BCNF

## Profesores

| IdProfesor | NombreProfesor | Aula |
|------------|----------------|------|
| 1 | Pedro | A101 |
| 2 | Ana | A102 |

---

## Cursos

| IdCurso | NombreCurso | IdProfesor |
|----------|-------------|------------|
| 101 | SQL | 1 |
| 102 | Python | 2 |

---

Ahora:

```text
Cada dependencia
se almacena una sola vez.
```

---

# Modelo Final

## Estudiantes

| IdEstudiante | Nombre |
|-------------|---------|
| 1 | Juan |
| 2 | María |

---

## Profesores

| IdProfesor | NombreProfesor | Aula |
|------------|----------------|------|
| 1 | Pedro | A101 |
| 2 | Ana | A102 |

---

## Cursos

| IdCurso | NombreCurso | IdProfesor |
|----------|-------------|------------|
| 101 | SQL | 1 |
| 102 | Python | 2 |

---

## Inscripciones

| IdEstudiante | IdCurso |
|-------------|----------|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

---

# Comparación

## Sin Normalizar

```text
Redundancia alta
Actualizaciones complejas
Datos inconsistentes
```

---

## 1NF

```text
Valores atómicos
```

---

## 2NF

```text
Sin dependencias parciales
```

---

## 3NF

```text
Sin dependencias transitivas
```

---

## BCNF

```text
Sin dependencias funcionales problemáticas
```

---

# Resumen

Este caso práctico mostró la evolución completa de un diseño:

```text
Sin normalizar
        ↓
1NF
        ↓
2NF
        ↓
3NF
        ↓
BCNF
```

Cada forma normal elimina un tipo específico de problema:

- 1NF → Valores múltiples
- 2NF → Dependencias parciales
- 3NF → Dependencias transitivas
- BCNF → Dependencias funcionales complejas

El objetivo final es construir modelos consistentes, mantenibles y escalables.

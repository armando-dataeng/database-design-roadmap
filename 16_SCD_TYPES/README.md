# SLOWLY CHANGING DIMENSIONS (SCD)

## Definición

Slowly Changing Dimensions (SCD) son técnicas utilizadas en Data Warehouses para gestionar cambios en los atributos de una dimensión a lo largo del tiempo.

Permiten responder preguntas como:

```text
¿Qué información tenía el cliente
cuando ocurrió una venta?
```

---

# ¿Por qué existen?

Supongamos:

## DimCliente

| ClienteKey | Nombre | Ciudad |
|------------|---------|---------|
| 10 | Pedro | Madrid |

---

Meses después:

```text
Pedro se muda a Barcelona.
```

---

Pregunta:

```text
¿Qué hacemos con Madrid?
```

Opciones:

1. Sobrescribir.
2. Mantener historial.
3. Guardar ambas versiones.

---

Los SCD definen la estrategia.

---

# Tipos principales

Los más utilizados son:

```text
SCD Type 0
SCD Type 1
SCD Type 2
SCD Type 3
```

---

# SCD Type 0

## Definición

No se permiten cambios.

---

Ejemplo:

```text
Fecha de nacimiento
```

---

Tabla:

| ClienteKey | Nombre | FechaNacimiento |
|------------|---------|-----------------|
| 10 | Pedro | 1990-01-01 |

---

Si cambia:

```text
No se actualiza.
```

---

## Uso típico

Datos históricos permanentes.

---

# SCD Type 1

## Definición

Sobrescribe el valor anterior.

No mantiene historial.

---

## Antes

| ClienteKey | Nombre | Ciudad |
|------------|---------|---------|
| 10 | Pedro | Madrid |

---

## Cambio

```text
Madrid → Barcelona
```

---

## Después

| ClienteKey | Nombre | Ciudad |
|------------|---------|---------|
| 10 | Pedro | Barcelona |

---

## Ventaja

Simple.

---

## Desventaja

Se pierde historial.

---

## SQL

```sql
UPDATE DimCliente
SET Ciudad = 'Barcelona'
WHERE ClienteKey = 10;
```

---

# SCD Type 2

## Definición

Mantiene historial completo.

Cuando ocurre un cambio:

```text
Se crea una nueva fila.
```

---

## Antes

| ClienteKey | Nombre | Ciudad |
|------------|---------|---------|
| 10 | Pedro | Madrid |

---

## Después

| ClienteSK | ClienteID | Nombre | Ciudad |
|------------|------------|---------|---------|
| 1 | 10 | Pedro | Madrid |
| 2 | 10 | Pedro | Barcelona |

---

Observa:

```text
ClienteID
```

permanece igual.

---

Pero:

```text
ClienteSK
```

cambia.

---

# Columnas típicas

## FechaInicio

```text
Inicio de vigencia.
```

---

## FechaFin

```text
Fin de vigencia.
```

---

## RegistroActual

```text
Indica versión vigente.
```

---

## Ejemplo

| ClienteSK | ClienteID | Ciudad | FechaInicio | FechaFin | Actual |
|------------|------------|---------|-------------|----------|---------|
| 1 | 10 | Madrid | 2023-01-01 | 2024-05-01 | N |
| 2 | 10 | Barcelona | 2024-05-02 | NULL | Y |

---

## Ventaja

Historial completo.

---

## Desventaja

Mayor complejidad.

---

# SCD Type 3

## Definición

Guarda el valor actual y el anterior.

---

## Ejemplo

| ClienteKey | CiudadActual | CiudadAnterior |
|------------|--------------|----------------|
| 10 | Barcelona | Madrid |

---

## Ventaja

Permite comparar cambios recientes.

---

## Desventaja

Historial limitado.

---

# Comparación

| Tipo | Historial |
|--------|------------|
| Type 0 | No cambia |
| Type 1 | No |
| Type 2 | Sí |
| Type 3 | Parcial |

---

# Caso Retail

## Cliente cambia de ciudad

### Pregunta

```text
¿Dónde vivía el cliente
cuando realizó la compra?
```

---

## Type 1

No puede responder.

---

## Type 2

Sí puede responder.

Porque conserva versiones históricas.

---

# Caso Bancario

## Cliente

| ClienteID | Nombre | Segmento |
|------------|---------|-----------|
| 100 | Pedro | Silver |

---

Cambio:

```text
Silver → Gold
```

---

## Type 1

Reemplaza:

```text
Gold
```

---

## Type 2

Mantiene:

```text
Silver
Gold
```

como registros separados.

---

# ¿Cuál es el más utilizado?

En Data Warehousing:

```text
SCD Type 2
```

es el más común.

---

Porque permite:

```text
Auditoría
Historial
Análisis temporal
```

---

# Star Schema y SCD

```text
FactVentas
      |
      ▼
DimCliente (SCD Type 2)
```

---

La Fact Table se relaciona con la versión correcta de la dimensión.

---

# Buenas prácticas

## Utilizar Surrogate Keys

Especialmente en Type 2.

---

## Registrar fechas de vigencia

```text
FechaInicio
FechaFin
```

---

## Marcar registro actual

```text
IsCurrent
```

---

## Documentar estrategia SCD

Cada dimensión debe tener una política clara.

---

# Error común

Usar Type 1 para todos los cambios.

---

Resultado:

```text
Pérdida de historial.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Todos los cambios deben ser Type 2.
```

---

Incorrecto.

Depende del negocio.

---

Ejemplo:

```text
Corrección ortográfica
```

normalmente:

```text
Type 1
```

---

Cambio de segmento comercial:

```text
Type 2
```

---

# Pensamiento de Data Engineering

Antes de elegir un SCD pregúntate:

1. ¿Necesito historial?
2. ¿Qué preguntas de negocio debo responder?
3. ¿La dimensión cambia frecuentemente?
4. ¿Necesito auditoría?
5. ¿Vale la pena almacenar múltiples versiones?

---

# Relación con los siguientes módulos

```text
FACT TABLES
↓
DIMENSION TABLES
↓
SCD TYPES
↓
DATA WAREHOUSE DESIGN
```

---

# Resumen

Los Slowly Changing Dimensions (SCD) permiten gestionar cambios en dimensiones a través del tiempo.

Tipos principales:

```text
Type 0 → Sin cambios

Type 1 → Sobrescribe

Type 2 → Historial completo

Type 3 → Historial parcial
```

En la práctica:

```text
Type 1
```

y

```text
Type 2
```

son los más utilizados.

Especialmente:

```text
SCD Type 2
```

porque permite mantener el historial completo de los datos.

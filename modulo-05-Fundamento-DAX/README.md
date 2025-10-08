# 💻 Módulo 5: Fundamentos de DAX - Lenguaje de Análisis
Acabas de construir una casa sólida (el modelo de datos). Ahora es el momento de llenar esa casa con vida: las métricas de negocio. DAX (Data Analysis eXpressions) es el lenguaje que Power BI utiliza para crear cálculos. Es la herramienta que te permite ir más allá de la simple suma y responder a preguntas complejas de negocio.


## 1. ¿Qué es DAX? Contexto de Fila vs. Contexto de Filtro
DAX es un lenguaje de fórmulas, similar a las fórmulas avanzadas de Excel, pero diseñado específicamente para modelos de datos relacionales.

**Contexto de Fila:** Es la acción que ocurre fila por fila dentro de una tabla. Cuando creas una columna calculada, Power BI mira el valor de la fila actual para realizar el cálculo.

**Contexto de Filtro (El concepto clave):** Es la colección de filtros que se aplica a los datos. Cuando arrastras una columna a un gráfico (Ej: Categoría al Eje X), estás aplicando un filtro a todas las medidas. DAX calcula el resultado después de aplicar esos filtros. omprender esto es vital para el Módulo 6.


## 2. Creación de Columnas Calculadas
Las Columnas Calculadas se crean en la Vista de Datos de Power BI. Su uso es limitado y debe ser estratégico, ya que consumen memoria y espacio en el archivo .PBIX.

**Uso:** Ideal para cálculos que se definen fila por fila y no cambian con el contexto del filtro. Por ejemplo, concatenar campos o crear una clasificación sencilla.

**Sintaxis:**

Fragmento de código
```m
NombreColumna = [Columna1] * [Columna2]
```

**Ejemplo:** Calcular la edad de un paciente basado en su fecha de nacimiento.

Fragmento de código
```m
EdadPaciente = DATEDIFF('DimPaciente'[FechaNacimiento], TODAY(), YEAR)
```

**Advertencia:** Si puedes hacer el cálculo en Power Query (Módulo 3) o en una Vista SQL (Módulo 2), hazlo allí. Reserva las columnas calculadas para lógica que realmente necesite estar en el modelo.


## 3. Creación de Medidas (Measures)
Las Medidas son el corazón del análisis y la razón principal para usar DAX.

**Uso:** Las medidas no almacenan valores en el modelo; se calculan al momento de ser usadas en una visualización. Esto significa que no consumen memoria como una columna calculada. Las medidas responden a la pregunta: "¿Cuál es la suma, promedio, o conteo filtrado que debo mostrar en este momento?"

**Sintaxis:**

Fragmento de código
```m
NombreMedida = FUNCION_DE_AGREGACION([Columna])
```

**Ubicación:** Las medidas deben ser creadas preferiblemente en la Tabla de Hechos, o en una tabla dedicada a medidas.


## 4. Funciones de Agregación Básicas
Estas funciones son las más sencillas de DAX y son la base para todas las medidas. Operan sobre un contexto de filtro ya aplicado.

| **Función**         | **Descripción**                                                                                  | **Ejemplo**                                           |
|----------------------|--------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| SUM()                | Suma todos los números en una columna.                                                          | `Venta Total = SUM('HechosVenta'[Monto])`            |
| AVERAGE()            | Calcula el promedio de una columna.                                                             | `TicketPromedio = AVERAGE('HechosVenta'[Monto])`     |
| COUNTROWS()          | Cuenta el número de filas en una tabla (útil para contar transacciones).                        | `TotalPedidos = COUNTROWS('HechosVenta')`            |
| DISTINCTCOUNT()      | Cuenta el número de valores únicos en una columna (útil para contar clientes únicos).           | `ClientesUnicos = DISTINCTCOUNT('HechosVenta'[IdPaciente])` |



## 5. Funciones de Iteración (X-Functions)
Las funciones que terminan en X (como `SUMX`, `AVERAGEX`, `MAXX`) permiten realizar una operación fila por fila dentro de una tabla y luego aplicar una agregación. Son esenciales para evitar errores en cálculos de ratio.

Sintaxis:

Fragmento de código
```m
SUMX(Tabla, Expresión_a_aplicar_fila_por_fila)
```

**Problema Común:** Si usas `SUM('Ventas'[Precio]) * SUM('Ventas'[Cantidad])`, estás multiplicando la Suma de los precios por la Suma de las cantidades, lo cual es incorrecto.

**Solución (SUMX):**

Fragmento de código
```m
CostoVentaReal = SUMX(
    'HechosVenta', 
    'HechosVenta'[Precio] * 'HechosVenta'[Cantidad] 
)
```

**La función SUMX le dice a DAX:** "Ve a cada fila de la tabla HechosVenta, multiplica Precio por Cantidad en esa fila, y luego suma esos resultados."


## 6. Ejercicio Práctico: Creación de Medidas Fundamentales

**Objetivo:** Crear las tres métricas esenciales de negocio para tu sistema de ventas/clínica.

**Medida 1: Monto Total Facturado**

- Crea una nueva medida en la tabla HechosVenta.
- Fórmula: Total Ingresos = SUM('HechosVenta'[Monto])

**Medida 2: Conteo de Eventos**

- Crea otra medida.
- Fórmula: Num Citas = COUNTROWS('HechosVenta')

**Medida 3: Uso de Función X**

- Supón que tienes Precio y Costo por artículo vendido en la tabla HechosVenta.
- Crea la medida de Ganancia por Artículo usando SUMX.
- Fórmula: Ganancia = SUMX('HechosVenta', 'HechosVenta'[Precio] - 'HechosVenta'[Costo])
- Visualización: Arrastra las tres medidas a la Vista de Informe usando una visualización de Tarjeta (Card) para ver el resultado total. Luego, agrega la columna DimProducto[Categoría] a un gráfico de barras para ver cómo las medidas se filtran por contexto.

## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ Contexto DAX: La diferencia entre el Contexto de Fila (Columnas Calculadas) y el Contexto de Filtro (Medidas).
- ✅ Medidas vs. Columnas: Por qué las Medidas son más eficientes y el estándar de BI.
- ✅ Agregaciones: Uso de SUM(), COUNTROWS(), AVERAGE() para métricas básicas.
- ✅ Iteración: La función SUMX() para realizar cálculos fila por fila antes de agregarlos, esencial para cálculos de ratio como Ganancia.


## 🎯 Ejercicios de Práctica

**Ejercicio 1: Cálculo de Ratio Básico**

Usando las medidas que creaste:
- Crea una nueva medida llamada Promedio Ingreso por Cita.
- La fórmula debe dividir [Total Ingresos] entre [Num Citas].

**Ejercicio 2: El Peligro de las Columnas Calculadas**

- Crea una Columna Calculada en la tabla DimProducto llamada Flag Costoso.
- La fórmula debe ser Flag Costoso = IF('DimProducto'[Costo Promedio] > 500, "Sí", "No").
- **Reflexiona:** Si arrastras esta nueva columna Flag Costoso al Eje X de un gráfico y la medida [Total Ingresos] al Eje Y, ¿funciona el filtro correctamente? ¿Por qué esta columna no causa el mismo problema de memoria que una columna calculada de alto volumen de datos?


📖 **[Ir al Módulo 06: DAX Intermedio - El Poder de CALCULATE](/modulo-06-DAX-Intermedio/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*
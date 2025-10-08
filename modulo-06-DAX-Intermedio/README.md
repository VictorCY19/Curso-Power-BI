# 💻 Módulo 6: DAX Intermedio - El Poder de CALCULATE
Si el Módulo 5 te enseñó a sumar y promediar, este módulo te enseñará a hacerlo inteligentemente. La función CALCULATE es, sin duda, la función más importante y poderosa de todo el lenguaje DAX. Te permite manipular el Contexto de Filtro para crear métricas avanzadas como comparaciones de tiempo, porcentajes sobre el total y análisis condicionales.


## 1. La Función CALCULATE: El Motor de DAX
La función CALCULATE evalúa una expresión (generalmente una medida) en un contexto de filtro modificado. Es lo que te permite responder preguntas como: "¿Cuál fue el total de ingresos, pero solo para la categoría 'Laptop'?"

**Sintaxis:**

Fragmento de código
```m
CALCULATE ( <Expresión_a_evaluar>, <Modificador_Filtro_1>, <Modificador_Filtro_2>, ... )
```

**¿Qué hace? CALCULATE realiza dos acciones clave:**

**Evaluación:** Calcula la `<Expresión_a_evaluar>` (casi siempre una medida que ya creaste, como `[Total Ingresos]`).

**Modificación del Contexto:** Elimina o añade filtros según los Modificadores de Filtro que le proporciones.

**Ejemplo Básico:** Calcular las ventas para una región específica, ignorando el filtro del gráfico.

Fragmento de código
```m
Ingresos_RegionNorte = CALCULATE(
    [Total Ingresos],
    'DimSede'[Region] = "Norte"
)
```


### 2. Modificadores de Filtro (Ignorar y Restablecer)
Aquí es donde usas las funciones `ALL`, `ALLEXCEPT` y `ALLSELECTED` para cambiar el contexto de filtro que normalmente aplicaría Power BI.

| **Función**             | **Descripción**                                                                                                   | **Ejemplo de Uso**                                                                                         | **Propósito**                                                                                                                |
|--------------------------|-------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ALL(Tabla)               | Remueve todos los filtros de la tabla especificada.                                                              | `CALCULATE([Total Ingresos], ALL('DimProducto'))`                                                          | Calcula el Total Global de ingresos, sin importar lo que se filtre en el gráfico o la página.                                |
| ALLEXCEPT(Tabla, Columna)| Remueve todos los filtros de la tabla excepto los aplicados a la columna especificada.                           | `CALCULATE([Total Ingresos], ALLEXCEPT('DimDoctor', 'DimDoctor'[Especialidad]))`                           | Muestra el total de ingresos, manteniendo solo el filtro de **Especialidad**, pero ignorando filtros como **Sede** o **Doctor**. |
| ALLSELECTED()            | Remueve todos los filtros de la visualización, excepto los aplicados por el usuario en slicers o filtros de página. | —                                                                                                          | Calcula el total del conjunto de datos seleccionado por el usuario (útil para porcentajes sobre subtotales).                  |



## 3. Funciones de Inteligencia de Tiempo (Time Intelligence)
Las funciones de Inteligencia de Tiempo permiten comparaciones de rendimiento a lo largo del tiempo, cruciales en cualquier informe de negocio. Requieren una Tabla Calendario (Módulo 4) marcada como tabla de fechas.

**Cálculos Clave:**

**Acumulado Año a la Fecha (YTD):** Suma la métrica desde el inicio del año hasta la fecha actual, considerando los filtros de fecha.

Fragmento de código
```m
Ingresos YTD = CALCULATE(
    [Total Ingresos],
    DATESYTD('DimFecha'[Fecha])
)
```

**Mismo Periodo del Año Anterior:** Compara el periodo seleccionado (día, mes, trimestre) con el mismo periodo del año anterior.

Fragmento de código
```m
Ingresos Año Anterior = CALCULATE(
    [Total Ingresos],
    SAMEPERIODLASTYEAR('DimFecha'[Fecha])
)
```

**Desplazamiento de Periodo:** Desplaza el contexto de filtro hacia adelante o hacia atrás.

Fragmento de código
```m
Ingresos Mes Anterior = CALCULATE(
    [Total Ingresos],
    DATEADD('DimFecha'[Fecha], -1, MONTH) // Desplaza un mes atrás
)
```


## 4. Creación de Métricas Complejas: Porcentaje de Crecimiento
Una vez que tienes las medidas de tiempo, puedes combinarlas para crear métricas de desempeño.

**Porcentaje de Crecimiento Anual (YoY - Year over Year):**

Fragmento de código
```m
% Crecimiento YoY = DIVIDE(
    [Ingresos YTD] - [Ingresos Año Anterior], // Numerador: Diferencia
    [Ingresos Año Anterior]                    // Denominador: Base
)
```

**Nota sobre DIVIDE:** En lugar de usar la división simple (/), se usa `DIVIDE` en DAX para manejar automáticamente la división por cero, devolviendo un valor alternativo (o BLANK) en lugar de un error.


## 5. Uso de Variables en DAX
Las Variables (VAR) mejoran la legibilidad y el rendimiento de tus medidas. Una vez que se calcula una variable, su valor se almacena y se reutiliza, evitando que DAX tenga que calcular la misma expresión varias veces.

**Sintaxis (para la medida de Crecimiento):**

Fragmento de código
```m
% Crecimiento YoY V2 = 
VAR IngresosActual = [Ingresos YTD]
VAR IngresosAnterior = [Ingresos Año Anterior]

RETURN
    DIVIDE(
        IngresosActual - IngresosAnterior,
        IngresosAnterior
    )
```

**RETURN:** Toda expresión DAX que usa VAR debe terminar con la palabra clave `RETURN`, que indica el resultado final de la medida.


## 6. Ejercicio Práctico: Creación de un Análisis de Crecimiento

**Objetivo:** Crear una métrica de comparación de mes a mes para el sistema de ventas/clínica.

**Prerrequisito:** Debes tener una Tabla Calendario y la medida [Total Ingresos].

**Medida 1: Ingresos del Mes Anterior**

Usa DATEADD para calcular los ingresos del mes inmediatamente anterior.

Fragmento de código
```m
Ingresos Mes Anterior = CALCULATE(
    [Total Ingresos],
    DATEADD('DimFecha'[Fecha], -1, MONTH)
)
```

**Medida 2: Diferencia vs. Mes Anterior**

Crea una medida que reste los ingresos actuales menos los del mes anterior.

Fragmento de código
```m
Diferencia Mes Anterior = [Total Ingresos] - [Ingresos Mes Anterior]
```

**Visualización:** Crea un gráfico de línea. Coloca la columna Mes de tu tabla Calendario en el Eje X, y las medidas [Total Ingresos] y [Ingresos Mes Anterior] en el Eje Y. Observa cómo [Ingresos Mes Anterior] está siempre rezagada un mes.


## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ El Motor DAX: La función CALCULATE y su rol como modificador del contexto de filtro.
- ✅ Manipulación de Filtros: Uso de ALL() para calcular totales globales y porcentajes sobre el total.
- ✅ Inteligencia de Tiempo: Las funciones clave como DATESYTD y SAMEPERIODLASTYEAR para análisis de series temporales.
- ✅ Optimización: El uso de Variables (VAR) para mejorar la legibilidad y el rendimiento del código DAX.


## 🎯 Ejercicios de Práctica

**Ejercicio 1: Porcentaje Sobre el Total Global**

- Crea una nueva medida: Total Ingresos Global. Usa la medida base [Total Ingresos] y la función ALL() en tu tabla de hechos para obtener la suma de ingresos sin filtros.
- Crea la medida final: Pct Sobre Total. Esta medida debe dividir [Total Ingresos] entre [Total Ingresos Global].
- Visualización: Muestra esta nueva medida en un gráfico de barras por DimDoctor[Especialidad] y observa cómo la suma de los porcentajes siempre da 100%.

**Ejercicio 2: El Poder de ALLEXCEPT**

- Crea una medida: Total Sede Actual.
- Usa CALCULATE con ALLEXCEPT para calcular [Total Ingresos], removiendo todos los filtros de la tabla DimDoctor excepto el filtro aplicado a la columna DimDoctor[NombreDoctor].
- Reflexiona: Si aplicas un filtro de página a la columna DimDoctor[Especialidad], ¿esta medida se ve afectada? ¿Por qué?


📖 **[Ir al Módulo 07: Diseño y Visualización de Reportes](/modulo-07-Diseño-Visualizacion-Reportes/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*
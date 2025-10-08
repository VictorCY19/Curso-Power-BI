# 💻 Módulo 7: Diseño y Visualización de Reportes
Ya sabes extraer, transformar y calcular. Este módulo te saca del back-end (SQL y DAX) para llevarte al front-end: el diseño y la comunicación. Un análisis brillante es inútil si el informe no es claro, intuitivo y atractivo. Aprenderás a contar la historia de tus datos para que los líderes tomen decisiones correctas.


## 1. Principios de Visualización de Datos: ¿Qué Gráfico Usar y Por Qué?
La elección del gráfico no es estética; es funcional. El objetivo es reducir la carga cognitiva del usuario.

| **Tarea Analítica**                                 | **Visualización Recomendada**                                   | **Razón**                                                                                                                     |
|-----------------------------------------------------|------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Comparar categorías o ítems.                        | Gráfico de Barras (horizontales) o Columnas (verticales).        | Permiten una comparación precisa de longitudes. Barras si hay muchos ítems.                                                   |
| Mostrar Tendencias o cambios a lo largo del tiempo. | Gráfico de Líneas.                                               | Ideal para fechas (tu Dimensión de Tiempo) ya que el ojo sigue la dirección del cambio.                                       |
| Mostrar la Distribución de datos.                   | Histograma (Barras) o Gráfico de Dispersión (Scatter Plot).      | Muestran la frecuencia de valores o la relación entre dos variables.                                                          |
| Mostrar la Composición (partes de un todo).         | Gráfico de Donut o Árbol/Treemap (con precaución).               | Mejor usar barras apiladas, ya que los pie charts dificultan la comparación visual.                                           |
| Mostrar KPIs (Métricas Clave).                      | Tarjeta (Card) o Indicador (Gauge).                              | Muestra un único número crucial de manera prominente.                                                                         |


## 2. Tipos de Visualizaciones Clave

**Gráficos de Barras/Columnas:** Usa barras agrupadas para comparar múltiples métricas dentro de una categoría (Ej: Ingresos y Costo por Producto). Usa barras apiladas al 100% para ver la distribución porcentual.

**Mapas:** Útiles para datos geográficos (Ej: DimSede[Latitud] y DimSede[Longitud] de tu proyecto SQL). Power BI tiene mapas integrados que detectan países/ciudades.

**Tablas y Matrices:** Nunca las subestimes. Son esenciales para el detalle (Drill-Down) y para mostrar muchas métricas a la vez. Las matrices permiten mostrar una jerarquía flexible (Ej: Año > Mes > Día).

**Slicers (Segmentaciones de Datos):** Permiten al usuario final aplicar filtros directamente sin ir al Panel de Filtros. Ideal para filtros de uso frecuente (Ej: Filtrar por DimDoctor[Especialidad] o por un rango de fechas).


## 3. Interacción y Navegación (Drill-Through)
Un informe eficaz es interactivo, permitiendo al usuario navegar desde un resumen hacia el detalle.

**Filtros Cruzados:** Por defecto, al hacer clic en un elemento de un gráfico (Ej: una barra de la categoría "Laptop"), el resto de las visualizaciones en la página se filtran automáticamente.

**Drill-Through (Profundización):** Esta es la mejor técnica para ir del resumen al detalle.

- Crea una Página de Detalle con una tabla o matriz que muestre información granular.

- En esa página, activa el campo "Drill-through" en el panel de Visualizaciones (Ej: IdPaciente).

- En la página de resumen, al hacer clic derecho en un visual que contenga el campo IdPaciente, el usuario verá la opción de ir a la página de detalle, llevando consigo los filtros aplicados.


## 4. Mejores Prácticas de Diseño
El diseño debe apoyar, no distraer, a los datos.

**Jerarquía Visual y Contraste:** Los KPIs (Tarjetas) deben ir siempre arriba, ya que son lo más importante. Usa títulos claros y mantén los filtros en un lugar consistente.

**Uso del Color:** Utiliza el color para resaltar o comparar, no solo para decorar.

**Consistencia:** Usa el mismo color para la misma métrica en todo el informe (Ej: Ingresos siempre verde, Costos siempre rojo).

**Accesibilidad:** Evita combinaciones de alto contraste que puedan ser difíciles para usuarios con daltonismo. Usa paletas de colores accesibles.

**Narrativa (The Story):** El informe debe tener una historia o un flujo. No tires gráficos al azar. Las páginas deben responder a preguntas específicas (Ej: Página 1: Rendimiento Ejecutivo, Página 2: Análisis por Doctor, Página 3: Detalle de Citas).


## 5. Ejercicio Práctico: Creación del Primer Dashboard Interactivo

**Objetivo:** Diseñar una página de resumen de ventas/clínica que aplique varios principios de visualización.

**Paso 1: Diseño de Encabezado y KPIs**

- Crea una nueva página en Power BI Desktop.

- Agrega 3-4 visualizaciones de Tarjeta (Card) en la parte superior. Arrastra las medidas clave creadas en el Módulo 6 (Ej: [Total Ingresos], [Num Citas], [Ingresos YTD]).

**Paso 2: Filtro de Usuario**

- Añade una visualización de Segmentación de datos (Slicer).

- Arrastra la columna DimDoctor[Especialidad] a ese slicer.

- Asegúrate de que al hacer clic en una especialidad, todos los KPIs se actualicen inmediatamente.

**Paso 3: Análisis de Tendencia y Distribución**

- Crea un Gráfico de Líneas debajo de los KPIs.

- En el Eje X, usa la jerarquía de Fecha de tu tabla Calendario.

- En el Eje Y, usa la medida [Total Ingresos]. Esto te muestra la tendencia a lo largo del tiempo.

- Crea un Gráfico de Barras (horizontal) al lado.

- En el Eje Y, coloca DimProducto[Nombre] y en el Eje X, coloca la medida [Total Ingresos]. Esto te muestra qué productos/servicios dominan los ingresos.


## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ Elección de Gráficos: Cuándo usar Barras, Líneas o Mapas para tareas analíticas específicas.
- ✅ Interactividad: Uso de Slicers para la navegación del usuario y la técnica de Drill-Through para el detalle.
- ✅ Diseño: Aplicar la jerarquía visual, el contraste y el uso consistente del color para la narrativa de datos.


## 🎯 Ejercicios de Práctica

**Ejercicio 1: Configuración de Drill-Through**

- Crea una nueva página llamada "Detalle Pacientes".
- Añade una visualización de Matriz que muestre Paciente[Nombre], Cita_Consulta[Fecha] y la medida [Total Ingresos].
- En el panel de Visualizaciones, arrastra el campo Paciente[IdPaciente] al área de "Drill-through".
- Vuelve a tu página principal de resumen. Haz clic derecho en uno de los gráficos que contenga datos de pacientes. ¿Aparece la opción para ir a "Detalle Pacientes"?

**Ejercicio 2: Ajuste del Eje Y**

- Observa tu gráfico de líneas ([Total Ingresos] a lo largo del tiempo).
- En el Panel de Formato (pincel), ve al formato del Eje Y.
- Cambia la Posición de Inicio (Start) del Eje Y para que no comience en cero (puedes iniciar en 500000 o un valor similar).
- **Reflexiona:** ¿Cómo cambia la percepción de la volatilidad o el crecimiento de la tendencia cuando manipulas el eje? (Nota: Aunque a veces es útil para los ejecutivos, generalmente se recomienda que los gráficos de barras/columnas comiencen en cero).


📖 **[Ir al Módulo 08: Analítica Avanzada en Power BI](/modulo-08-Analitica-Avanzada/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*


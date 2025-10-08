# 💻 Módulo 8: Analítica Avanzada en Power BI
Has dominado la creación de modelos, el cálculo de métricas con DAX y el diseño de informes. Este módulo se enfoca en las capacidades analíticas de Power BI que te permiten ir más allá de la simple visualización, descubriendo por qué suceden las cosas en tus datos y utilizando herramientas que te preparan para la ciencia de datos.

## 1. Agrupación y Binning
A menudo, los datos numéricos (como el precio, la edad o el monto de la cita) necesitan ser clasificados en rangos para un análisis efectivo.

**Agrupación (Grouping):** Se utiliza en datos categóricos. Por ejemplo, si tienes 50 tipos de productos, puedes agrupar los menos relevantes bajo una categoría única llamada "Otros" para simplificar un gráfico.

**Binning (Agrupamiento por Rangos):** Se utiliza en datos numéricos. Crea grupos de igual tamaño a partir de una columna continua (Ej: crear rangos de edad de 10 años en 10 años: "20-29", "30-39", etc.).

**Creación en Power BI:** Se hace directamente en el panel Datos (haciendo clic derecho en la columna deseada) o en el panel de Visualizaciones para crear los bins (contenedores) o grupos personalizados.


## 2. Uso de Parámetros de Campo (Field Parameters)
Los Parámetros de Campo son una función avanzada que permite al usuario final seleccionar dinámicamente qué dimensiones o qué medidas se muestran en una visualización. Esto reduce drásticamente el número de gráficos que necesitas crear.

**Función:** Permite que una segmentación de datos (Slicer) controle qué columnas aparecen en un gráfico de barras.

**Ejemplo:** En un Slicer, el usuario puede elegir ver la barra por DimProducto[Categoría], por DimDoctor[Especialidad] o por DimSede[Región]. El gráfico se actualiza sin requerir tres gráficos separados.

**Creación:** Se crea desde la pestaña Modelado → Nuevo parámetro → Campos. Luego, se inserta en el Eje X o Y del gráfico, y el usuario interactúa a través de un Slicer.


## 3. Visualizaciones Avanzadas (R, Python, o Custom Visuals)
Power BI no se limita a sus gráficos predeterminados. Puedes extender su funcionalidad:

**Visualizaciones de R/Python:** Si sabes programar en R o Python, puedes escribir código que genere visualizaciones extremadamente personalizadas (Ej: gráficos de densidad o nubes de palabras) utilizando tus datos del modelo de Power BI. Requieren la instalación de los motores de R/Python en tu máquina.

**Custom Visuals (Visualizaciones Personalizadas):** Power BI tiene una tienda (AppSource) donde puedes descargar visualizaciones creadas por terceros que no vienen por defecto (Ej: Gráficos de Gantt, Gráficos Sankey, etc.). Advertencia: Siempre verifica la fuente y la licencia.


## 4. Implementación de Tooltips (Información sobre herramientas) de Página
El tooltip (información sobre herramientas) es el pequeño cuadro de texto que aparece cuando pasas el ratón sobre un punto de datos. Puedes convertir una página completa de tu informe en un tooltip para mostrar más información detallada.

**Función:** Cuando el usuario pasa el ratón sobre una barra del gráfico (Ej: la barra del Doctor "García"), el tooltip aparece, mostrando un KPI adicional, un minigráfico de línea de su tendencia de ingresos en los últimos 6 meses, o sus 3 clientes más valiosos.

**Pasos:**

- Crea una página pequeña y nomínala (Ej: "Tooltip Doctor").

- En el formato de la página, activa la opción "Permitir el uso como información sobre herramientas".

- En la página de tu informe principal, selecciona la visualización (Ej: el gráfico de barras por Doctor) y en el panel Formato → Información sobre herramientas → elige "Tooltip Doctor" como página de informe.


## 5. Funcionalidades de IA: Análisis de Influenciadores Clave
Power BI integra herramientas basadas en Inteligencia Artificial que te ayudan a encontrar los factores que impulsan un valor en una métrica sin necesidad de escribir código complejo de ciencia de datos.

**Gráfico de Influenciadores Clave (Key Influencers):** Una visualización incorporada que analiza tu modelo y te muestra qué dimensiones (Factores) tienen la mayor probabilidad de aumentar o disminuir un resultado.

**Ejemplo:** ¿Qué factores aumentan la probabilidad de que una cita clínica se cancele? (Factores: Doctor[Novato], Sede[Rural], Paciente[Edad < 25]).


## 6. Ejercicio Práctico: Crear un Análisis de Distribución y un Tooltip Avanzado

**Objetivo:** Aplicar la agrupación de datos y la funcionalidad de tooltip de página.

**Paso 1: Agrupamiento (Binning) de Montos**

- En tu tabla HechosVenta, haz clic derecho en la columna Monto.
- Selecciona "Nuevo grupo" o "Nuevo agrupamiento".
- Crea bins con un tamaño de 1000 (Ej: $0-1000, $1000-2000, etc.). Nombra la nueva columna Rango Monto Cita.
- Crea un Gráfico de Barras (Histograma) con el nuevo campo Rango Monto Cita en el Eje X y [Num Citas] en el Eje Y.

**Paso 2: Creación del Tooltip Avanzado**

- Crea una nueva página y formatéala como "Información sobre herramientas".
- En esta página, inserta un Gráfico de Líneas que muestre la medida [Total Ingresos] a lo largo del tiempo (Meses).
- Vuelve a la página de tu informe principal y asigna esta nueva página como tooltip de tu gráfico de barras que muestra [Total Ingresos] por DimDoctor[Nombre].
**Verificación:** Pasa el ratón sobre la barra de un doctor específico y observa cómo aparece la tendencia mensual filtrada para ese doctor.


## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ Estructuración: Usar Agrupación y Binning para clasificar datos numéricos y categóricos.
- ✅ Flexibilidad: Implementar Parámetros de Campo para dejar que el usuario final elija las dimensiones y medidas del gráfico.
- ✅ Navegación Avanzada: Crear Tooltips de Página para mostrar información de detalle valiosa de manera contextual.
- ✅ IA en BI: Conocer el uso de la visualización Influenciadores Clave para descubrir los drivers del negocio.


## 🎯 Ejercicios de Práctica

**Ejercicio 1: Aplicación del Parámetro de Campo**

- Crea un Nuevo Parámetro de Campo con las siguientes dos medidas: [Total Ingresos] y [Ganancia] (creadas en el Módulo 5). Nómbralo Selector de Metrica.
- Crea un Gráfico de Barras simple. En el Eje Y, usa el nuevo parámetro Selector de Metrica.
- Añade el Slicer del parámetro a la página.
**Verificación:** Al hacer clic en el Slicer en "Total Ingresos", el gráfico debe cambiar su valor, mostrando la métrica seleccionada.

**Ejercicio 2: El Gráfico de Influenciadores**

- Añade la visualización de Influenciadores Clave a tu informe.
- Configura el gráfico para "Analizar qué impacta a la [Medida: Total Ingresos] para que [aumente]".
- En el cuadro "Explicar por", arrastra las columnas DimDoctor[Especialidad] y DimPaciente[Edad].
**Reflexión:** ¿Qué factor identificó Power BI como el de mayor impacto para el aumento de los ingresos?

📖 **[Ir al Módulo 09: Seguridad y Publicación](/modulo-09-Seguridad-Publicacion/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*

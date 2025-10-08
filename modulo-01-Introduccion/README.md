# 💻 Módulo 1: Introducción a Power BI y Preparación del Entorno
¡Bienvenido al inicio de tu viaje con Power BI! Este módulo te establecerá los fundamentos teóricos y prácticos para entender el ecosistema de Power BI y preparar tu computadora para comenzar a analizar datos.

## 1. ¿Qué es Power BI? Componentes
Power BI es una colección de servicios de software, apps y conectores que funcionan juntos para convertir fuentes de datos no relacionadas en información coherente, visualmente inmersiva e interactiva.

| **Componente**               | **Descripción**                                         | **Función**                                                                                                                                          |
|------------------------------|---------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| Power BI Desktop             | Aplicación gratuita para PC con Windows.                | Herramienta principal para desarrollo: conectar, transformar, modelar y crear informes.                                                             |
| Power BI Service (la nube)   | Servicio en línea basado en SaaS (Software as a Service). | Herramienta para publicación y colaboración: compartir informes, configurar actualizaciones automáticas y gestionar seguridad (Módulo 9).           |
| Power BI Mobile              | Apps para dispositivos iOS, Android y Windows.          | Herramienta para consumo: ver e interactuar con informes y paneles desde cualquier lugar.                                                            |


## 2. El Rol del Analista de Datos y la Importancia del BI

**Business Intelligence (BI):** Es el proceso de recopilar, almacenar y analizar datos de operaciones comerciales para optimizar el rendimiento.

**Conexión con SQL Server:** Como ya sabes construir y consultar datos estructurados, el BI te permite llevar esos datos al "último kilómetro": convertirlos en tableros de control (Dashboards) que los líderes de negocio usan para tomar decisiones.

**Analista de Datos:** Eres el traductor. Tomas los datos técnicos que extraes con SQL y los conviertes en una narrativa clara y visual que cualquier persona puede entender.


## 3. Instalación de Power BI Desktop
Power BI Desktop es el punto de partida. Es completamente gratuito para el desarrollo.

**Requisito:** Power BI Desktop requiere Windows 10/11 o una versión moderna de Windows Server.

**Método Recomendado (Microsoft Store):** Buscar Power BI Desktop en la Microsoft Store. Esto garantiza actualizaciones automáticas y una instalación más sencilla.

**Método Alternativo (Sitio Web):** Descargar el instalador desde el sitio oficial de Microsoft Power BI.

**Verificación:** Una vez instalado, ábrelo. Deberías ver la pantalla de inicio con opciones para "Obtener datos" o "Abrir otros informes".


## 4. Navegación por la Interfaz
La interfaz de Power BI Desktop está dividida en tres vistas principales, accesibles mediante íconos a la izquierda, y es crucial familiarizarse con ellas desde el inicio:

| **Vista**           | **Ícono** | **Propósito**                                                                 | **Conexión con SQL**                                                        |
|----------------------|-----------|--------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| Vista de Informe     | 📊        | Donde se diseñan las visualizaciones, gráficos y tablas que componen el informe final. | El resultado de las consultas de SQL.                                      |
| Vista de Datos       | 📑        | Muestra las tablas y datos cargados, permitiendo inspeccionar filas y columnas.        | Similar a ver las tablas en SSMS (Módulo 2 de SQL).                        |
| Vista de Modelo      | 🔗        | Donde se define la estructura relacional entre las tablas (el corazón del modelado).   | Similar al Diagrama Entidad-Relación (ER) de SSMS (Módulo 3 de SQL).      |


**Además, tienes tres paneles clave a la derecha:**

**Filtros:** Para aplicar filtros a toda la página, visualización o informe.

**Visualizaciones:** Contiene la lista de gráficos disponibles (barra, línea, mapa, etc.).

**Datos:** Muestra todas las tablas y campos (columnas y medidas) disponibles en tu modelo.


## 5. Conexión Inicial: Cargar Datos
La forma más básica de cargar datos es mediante archivos planos. Esto te permite entender el flujo de trabajo antes de conectar a tu base de datos SQL.

- Hacer clic en "Obtener datos" en la pestaña Inicio.
- Seleccionar "Libro de Excel" o "Texto/CSV".
- Seleccionar el archivo y hacer clic en "Cargar".
- El sistema de Power BI te mostrará una vista previa.

  **Cargar vs. Transformar Datos:**
- Si los datos están listos, haz clic en Cargar.
- Si los datos necesitan limpieza o ajustes (lo más común), haz clic en Transformar datos (esto te llevará al Editor de Power Query, tema del Módulo 3).


## 6. Ejercicio Práctico: Crear el Primer Informe Sencillo

**Objetivo:** Cargar unos datos y crear un gráfico básico para familiarizarte con el flujo de trabajo.

- Descarga un archivo CSV o Excel sencillo (puedes usar el archivo csv del curso de SQL o algun otro por ejemplo uno de ventas).
- En Power BI Desktop, haz clic en Obtener datos y carga el archivo.
- Ve a la Vista de Informe.
- Selecciona un gráfico de Columnas apiladas del panel de Visualizaciones.
- Arrastra el campo "Nombre del Producto" al eje X.
- Arrastra el campo "Cantidad Vendida" (o similar) al eje Y.

**¡Felicidades! Has creado tu primera visualización en Power BI.**

## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ Ecosistema de Power BI: Los tres componentes (Desktop, Service, Mobile) y su propósito.
- ✅ Instalación: Tienes Power BI Desktop listo para trabajar.
- ✅ Interfaz: Estás familiarizado con las tres vistas clave (Informe, Datos, Modelo).
- ✅ Carga de Datos: Sabes cómo cargar datos iniciales y el concepto de Cargar vs. Transformar.


## 🎯 Ejercicio de Práctica

**Ejercicio 1: Inspección de la Interfaz**

- Abre Power BI Desktop.
- En la Vista de Datos, haz clic en el nombre de tu tabla cargada. ¿Qué información te muestra la barra superior sobre el número de filas y columnas?
- Navega a la Vista de Modelo. Aunque solo tienes una tabla, ¿dónde se ubica el panel de Propiedades si haces clic en la tabla?

**Ejercicio 2: Creación de un Indicador**

- Carga la tabla de datos de tu ejercicio anterior si no la tienes.
- En la Vista de Informe, selecciona el tipo de visualización llamado "Tarjeta" (Card).
- Arrastra el campo "Precio Total" (o similar) al área de Campo de la Tarjeta.
- Observa cómo Power BI aplica automáticamente una agregación (como Suma o Cuenta). Cambia la agregación a Promedio directamente en el panel de Visualizaciones.

📖 **[Ir al Módulo 02: Conexión Estratégica con SQL Server](/modulo-02-Conexion-SQL/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*

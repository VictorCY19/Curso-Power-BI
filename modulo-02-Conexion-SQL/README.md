# 💻 Módulo 2: Conexión Estratégica con SQL Server
Ahora que ya tienes Power BI Desktop instalado y conoces su interfaz, el siguiente paso es conectar esta poderosa herramienta de análisis directamente a tus datos estructurados. Este módulo te enseñará las mejores prácticas para enlazar tu proyecto de SQL Server con Power BI de manera eficiente y segura.


## 1. Tipos de Conexión: Importar vs. DirectQuery
Al conectar Power BI a SQL Server, tienes que elegir cómo Power BI manejará los datos. La elección afecta el rendimiento, el tamaño del archivo y la latencia de la información.

| **Tipo de Conexión**     | **Características**                                                                                                      | **Cuándo usarlo**                                                                                                                                                                                                                     |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Importar (Recomendado)    | Los datos se copian y se almacenan en el archivo de Power BI (.PBIX). Se comprime en memoria.                            | Cuando los datos no cambian frecuentemente (baja latencia no es crucial). Permite usar el 100% de las funciones de Power Query y DAX. Requiere actualización manual o programada.                                                     |
| DirectQuery               | Power BI no copia los datos. Cada acción del usuario (filtrar, hacer clic) genera una consulta SQL en tiempo real.       | Cuando los datos cambian constantemente (alta latencia es crucial) y el volumen de datos es demasiado grande para caber en memoria. Tiene limitaciones en funciones de DAX y Power Query.                                             |


## 2. Conexión a SQL Server
El proceso de conexión es directo y se realiza desde la interfaz de Power BI Desktop.

- En la pestaña Inicio, haz clic en "Obtener datos".
- Selecciona "Base de datos de SQL Server".

**Ingresa los parámetros de conexión:**
- **Servidor:** El nombre o la IP de tu servidor SQL (Ej: localhost o el nombre de instancia).
- **Base de Datos (Opcional):** El nombre de la base de datos (Ej: ProyectoDB). Si lo omites, se listarán todas las bases de datos.

- En la pantalla siguiente, selecciona el Modo de Conectividad de Datos (Importar o DirectQuery).
- **Credenciales:** Elige la autenticación. Generalmente, usarás "Windows" (si tu SQL Server usa la autenticación integrada) o "Base de datos" (si usas un usuario y contraseña de SQL Server, como el sa o un usuario creado en tu Módulo 8 de SQL).


## 3. Ventaja SQL: Usar Vistas para Optimizar la Carga (Conexión con Módulo 6 de SQL)
Un error común es importar todas las columnas de una tabla. El poder de SQL Server reside en que puedes preparar los datos antes de que lleguen a Power BI, mejorando el rendimiento.

**¿Por qué es mejor una Vista?** En lugar de importar la tabla Paciente completa, si solo necesitas el IdPaciente, Nombre y la Fecha de Nacimiento, puedes crear una Vista en SQL Server (Módulo 6 de SQL) que solo contenga esas tres columnas.

**Proceso:** Al conectar a SQL Server, en lugar de seleccionar la tabla completa, selecciona la Vista previamente creada.

**Beneficio:** Power BI solo importa la información esencial, lo que reduce el tamaño del archivo .PBIX y acelera la actualización de datos.


## 4. Ventaja SQL: Ejecutar Procedimientos Almacenados para Datos Dinámicos (Conexión con Módulo 6 de SQL)
Si necesitas que tu fuente de datos sea dinámica (por ejemplo, obtener las ventas del último mes o datos basados en un cálculo complejo que solo SQL puede hacer rápido), puedes ejecutar un Procedimiento Almacenado.

**Método:** Cuando te conectas a la Base de Datos SQL, en la ventana de navegación, puedes seleccionar la opción "Opciones avanzadas" e ingresar una consulta SQL personalizada.

**Sintaxis en Power BI:**


```sql
-- Ejecución de un Procedimiento Almacenado
EXEC [NombreEsquema].[NombreProcedimiento] @Parametro1 = Valor1, @Parametro2 = Valor2; 

-- Ejemplo usando tu Proyecto SQL
EXEC dbo.usp_ObtenerReporteVentas @FechaInicio = '2024-01-01';
Importante: Cuando se usa EXEC o una consulta SQL directa, Power BI ignora la navegación a las tablas y solo trae el conjunto de resultados (el result set).
```


## 5. Ejercicio Práctico: Conectar y Comparar

**Objetivo:** Conectar Power BI a la base de datos ProyectoDB (o la que uses para tu proyecto final de SQL) y experimentar la diferencia entre cargar una tabla completa y una consulta filtrada.

**Conexión Inicial:** Conéctate a tu SQL Server con el modo Importar. Navega y selecciona la tabla Paciente y haz clic en "Cargar". Observa el número de filas cargadas.

**Conexión Estratégica:**
- Vuelve a "Obtener datos" → "Base de datos de SQL Server".
- Ingresa los parámetros y selecciona "Opciones avanzadas".
- En el cuadro de comando SQL, escribe una consulta simple que filtre tu tabla, por ejemplo:

```sql
SELECT * FROM Paciente WHERE FechaNacimiento >= '1990-01-01';
Haz clic en "Cargar".
```

**Comparación:** Ve a la Vista de Datos de Power BI. Verás dos tablas (Paciente y Consulta Avanzada). Observa cómo la segunda tabla tiene menos filas, ya que tu filtro se aplicó directamente en SQL Server, antes de que Power BI importara los datos.


## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ Tipos de Conexión: La diferencia fundamental entre Importar (rendimiento máximo) y DirectQuery (datos en tiempo real).
- ✅ Conexión Directa: Cómo configurar los parámetros de conexión y las credenciales para SQL Server.
- ✅ Estrategias de Optimización: Cómo usar los conocimientos de Vistas y Procedimientos Almacenados de SQL para preparar y optimizar la fuente de datos antes de que llegue a Power BI.


## 🎯 Ejercicios de Práctica

**Ejercicio 1: Elección del Modo de Conexión**

- Si tu jefe te pide crear un informe sobre las ventas de Amazon que tiene 50 millones de filas y necesita que los datos se vean actualizados cada 10 minutos, ¿qué modo de conexión elegirías y por qué?

**Ejercicio 2: Preparación de Datos con SQL para BI**

- Suponiendo que tienes la tabla Cita_Consulta y la tabla Doctor de tu proyecto SQL.
- En SSMS, crea una Vista llamada vw_Citas_BI que solo contenga el IdCita, la Fecha, y el Nombre completo del Doctor (usando un JOIN y concatenación).
- En Power BI, conéctate y carga solo la vista vw_Citas_BI (no las tablas originales).
- **Reflexiona:** ¿Cómo esta técnica previene que tengas que crear una columna calculada para el Nombre Completo del Doctor en Power BI?

📖 **[Ir al Módulo 03: Transformación de Datos con Power Query (El ETL)](/modulo-03-Power-Query-ETL/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*
# 💻 Módulo 3: Transformación de Datos con Power Query (El ETL)
¡Bienvenido a la cocina de los datos! Una vez que los datos han sido extraídos de SQL Server, rara vez están listos para el análisis. Este módulo te enseñará a limpiar, transformar y preparar tus datos utilizando el Editor de Power Query, que es la herramienta ETL (Extracción, Transformación, Carga) dentro de Power BI.

## 1. Introducción al Editor de Power Query
El Editor de Power Query es una ventana separada dentro de Power BI Desktop. Es tu entorno de back-end donde manipulas los datos sin afectar el informe final.

**Acceso:** Se accede haciendo clic en "Transformar datos" en la pestaña Inicio de Power BI Desktop.

**Filosofía:** Es una herramienta no destructiva. Cada paso de transformación que realizas se registra en el panel de Pasos Aplicados a la derecha, y puedes deshacer o editar cualquier paso en cualquier momento.


## 2. Concepto de ETL: Extract, Transform, Load
Power Query opera bajo el concepto de ETL. Ya has completado la fase de Extracción al conectar Power BI a SQL Server. Ahora nos enfocaremos en la Transformación.

| **Fase**                | **Descripción**                                                                                      | **Herramienta/Módulo**                                  |
|--------------------------|------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| Extract (Extraer)        | Conectar a la fuente de datos (SQL Server, Excel, CSV, etc.).                                       | Módulo 2 de Power BI (Conexión)                         |
| Transform (Transformar)  | Limpiar, reformatear, corregir errores, agregar columnas calculadas.                                | Power Query Editor                                      |
| Load (Cargar)            | Mover los datos transformados desde Power Query al Modelo de Datos de Power BI.                     | Clic en "Cerrar y aplicar"                              |


## 3. Limpieza de Datos Crucial
La limpieza es el primer paso y el más importante para garantizar análisis precisos.

**Manejo de Nulos:** Los valores NULL (nulos) vistos en SQL Server se manifiestan en Power Query. Puedes usar la opción "Reemplazar Valores" (Ej: reemplazar nulos en la columna Costo por 0) o "Eliminar Filas" si la fila está irrecuperable.

**Valores Duplicados:** Usa "Quitar Duplicados" para asegurar que tus claves primarias (vistas en Módulo 3 de SQL) sean únicas antes de la carga.

**Errores:** Power Query identifica errores (Ej: texto en una columna numérica). Es vital corregirlos o eliminarlos, ya que los errores rompen las medidas de DAX.


## 4. Transformaciones Clave (Refuerzo SQL)
Power Query ofrece transformaciones avanzadas que complementan tu conocimiento de SQL.

**Cambio de Tipos de Datos:** Asegúrate de que los tipos de datos de origen (INT, VARCHAR, DATE) se mapeen correctamente a los tipos de Power BI (Número entero, Texto, Fecha). Un error de tipo de dato es un problema común.

**Reestructuración (Pivot/Unpivot):**

**Unpivot (Desdinamizar):** Fundamental. Transforma filas anchas (Ej: Venta_Enero, Venta_Febrero) en filas largas (Ej: Mes, Valor). Esta es la forma ideal de preparar datos para un modelo relacional y es el opuesto de las funciones PIVOT vistas en SQL Server (Módulo 13 de SQL).

**Pivot (Dinamizar):** Lo contrario, transforma filas largas en filas anchas.

**Combinar y Anexar Consultas:**

**Combinar (Merge):** Es el equivalente a hacer un JOIN en SQL. Se utiliza para unir columnas de dos tablas relacionadas.

**Anexar (Append):** Es el equivalente a UNION ALL en SQL. Se utiliza para apilar filas de dos tablas con la misma estructura (Ej: unir la tabla Ventas_2023 con Ventas_2024).


## 5. Creación de Columnas: Condicionales y Personalizadas
Puedes crear nuevas columnas de datos en Power Query (ideal para limpieza y preparaciones previas).

**Columna Condicional:** Similar a una sentencia CASE en SQL Server. Se usa para crear una clasificación basada en reglas (Ej: si Precio > 100, entonces Clase = "Premium", sino "Estándar").

**Columna Personalizada:** Permite escribir lógica de transformación usando el lenguaje M (Power Query Formula Language).


## 6. El Lenguaje M y Sus Pasos Aplicados
Detrás de cada clic en Power Query, se está escribiendo código en el lenguaje M.

**Pasos Aplicados:** El panel de la derecha es clave. Cada acción se registra como un paso M.

**Ventaja:** Si necesitas una transformación muy específica que no está en la interfaz, puedes editar el código M directamente en la Barra de Fórmulas o haciendo clic derecho en el paso aplicado y seleccionando "Editor Avanzado".

**Fragmento de código**

```m
// Ejemplo de un paso M: Cambiando el tipo de datos de una columna
#"Tipo Cambiado" = Table.TransformColumnTypes(Source, {{"IdProducto", Int64.Type}, {"NombreProducto", type text}}),
```


## 7. Ejercicio Práctico: Limpieza y Desnormalización

**Objetivo:** Practicar la limpieza y una reestructuración de datos (Unpivot) en Power Query.

- Carga un archivo de Excel (o simula) que contenga datos de ventas de esta manera (datos anchos):

| **IdProducto** | **Producto** | **Enero** | **Febrero** | **Marzo** |
|----------------|--------------|------------|--------------|------------|
| 101            | Laptop       | 1500       | 1600         | 1700       |
| 102            | Monitor      | 500        | 550          | 600        |


- En Power Query Editor, selecciona las columnas Enero, Febrero y Marzo.

- Ve a la pestaña "Transformar" y selecciona "Anular dinamización de columnas" (Unpivot Columns).

- Observa cómo ahora tienes una columna Atributo (con los nombres de los meses) y una columna Valor (con los montos de venta).

- Renombra la columna Atributo a Mes y Valor a Venta Total.

- **Aplica la transformación:** ve a la pestaña Inicio de Power Query y haz clic en "Cerrar y aplicar".


## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ Power Query Editor: El entorno clave para transformar tus datos.
- ✅ Flujo ETL: La fase de Transformación y su importancia.
- ✅ Limpieza: Manejar Nulos, Duplicados y Errores para garantizar la calidad de los datos.
- ✅ Transformaciones Avanzadas: Usar Anular dinamización (Unpivot), Combinar (Merge) y Anexar (Append) para dar forma a los datos.
- ✅ Lógica de Transformación: Crear columnas Condicionales y Personalizadas (Lenguaje M).


## 🎯 Ejercicios de Práctica

**Ejercicio 1: Limpieza de Claves Foráneas**

- En tu tabla de Cita_Consulta de SQL, supongamos que la columna IdDoctor tiene 5 valores NULL por un error de inserción.
- Carga la tabla en Power Query.
- Usa la opción "Reemplazar Valores" para cambiar esos 5 valores NULL a un valor específico, por ejemplo, 999 (representando un doctor sin asignar).
- Inspecciona el panel "Pasos Aplicados": ¿Cómo se llama el paso que registra esta acción?

**Ejercicio 2: Creación de Clasificación con Columna Condicional**

- En tu tabla de productos, usa la herramienta "Columna Condicional".
- Crea una nueva columna llamada Margen.
- Aplica la siguiente regla: Si la columna Costo es menor que 200, entonces el Margen es "Bajo". En caso contrario, el Margen es "Alto".
- Aplica la transformación y verifica los resultados en la tabla.

📖 **[Ir al Módulo 04: Modelado de Datos y Normalización en Power BI (El ETL)](/modulo-04-Modelado-Normalizacion-BI/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*
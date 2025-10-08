# 💻 Módulo 4: Modelado de Datos y Normalización en Power BI
Si el Módulo 3 fue la preparación de los ingredientes (limpieza y transformación), este módulo es la arquitectura. Un modelo de datos eficiente es el cimiento de un buen informe. Aquí aplicaremos los principios de la Normalización que aprendiste en SQL Server, pero desde la perspectiva del análisis de datos en Power BI.

## 1. Conceptos de Tablas de Hechos y Tablas de Dimensión
Power BI modela los datos utilizando la arquitectura Estrella (Star Schema), que es una simplificación de la Normalización (Módulo 3 de SQL) optimizada para la velocidad de las consultas de BI (DAX).

| **Tipo de Tabla**                 | **Descripción**                                                                                      | **Propósito**                                                                                                      | **Ejemplo (Sistema de Ventas)**                     |
|----------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| Tabla de Hechos (Facts)          | Contienen los eventos o transacciones que quieres medir. Son largas (muchas filas) y delgadas (pocas columnas). | Almacenan las **MÉTRICAS** y las claves foráneas (FKs) para conectarse a las dimensiones.                         | Venta, Detalle_Tratamiento, MovimientoInventario.   |
| Tabla de Dimensión (Dimensions)  | Contienen los atributos (el "quién, qué, dónde, cuándo"). Son cortas (pocas filas) y anchas (muchas columnas).   | Almacenan los **FILTROS** y las características para segmentar las métricas.                                      | Producto, Doctor, Paciente, Sede.                  |



## 2. Esquema Estrella y Copo de Nieve (Refuerzo de Normalización)

**Esquema Estrella (Star Schema):** La forma ideal en BI. Una única tabla de Hechos está rodeada por tablas de Dimensión. Es rápido y fácil de entender. Es una forma de desnormalización controlada para el análisis.

**Esquema Copo de Nieve (Snowflake Schema):** Es un modelo más normalizado, donde las dimensiones se conectan a otras dimensiones (similar a tu modelo ER de SQL). Aunque más eficiente en espacio en disco, es más lento en Power BI porque requiere más joins (saltos entre tablas).

**Recomendación BI:** Siempre apunta al Esquema Estrella para maximizar el rendimiento en Power BI, aunque hayas normalizado en SQL Server.


## 3. Gestión de Relaciones
Las relaciones son las líneas que dibujas en la Vista de Modelo de Power BI, uniendo una columna clave de una tabla con la clave foránea de otra.

**Claves Primarias y Foráneas:** La clave primaria (la columna Id de una Dimensión) debe ser única. La clave foránea (la columna Id en la tabla de Hechos) puede tener duplicados.

**Cardinalidad:**

**Uno a Muchos (1:N):** La relación más común. El lado "Uno" es la Dimensión (clave única); el lado "Muchos" es la Hecho (clave repetida).

**Uno a Uno (1:1) y Muchos a Muchos (N:N):** Se usan con precaución. Los Muchos a Muchos a menudo requieren una tabla puente para resolverlos (similar al Módulo 3 de SQL).

**Dirección del Filtro:** Indica cómo se propaga el filtro. En un esquema estrella, el filtro siempre debe ir desde la Dimensión hacia la Tabla de Hechos (generalmente, la dirección es única).


## 4. Creación de una Tabla Calendario (Dimension Time/Date)
Una Dimensión de Tiempo es fundamental en BI. Nunca debes confiar únicamente en las fechas de tu tabla de Hechos para análisis complejos de tiempo (YTD, Mes Anterior, etc.).

**Función:** Proporciona atributos de tiempo (Año, Mes, Día de la Semana, Nombre del Mes, Trimestre) que permiten filtrar y agrupar los datos de manera flexible.

**Método:** Se puede crear fácilmente una tabla calendario en Power Query (usando la función `$Date.ToTable$`) o usando una función DAX especializada (tema del Módulo 5).

**Relación:** La columna de Fecha Única de la Tabla Calendario se relaciona 1:N con la columna de Fecha en la Tabla de Hechos.


## 5. Ejercicio Práctico: Diseñar el Modelo Estrella

**Objetivo:** Tomar las tablas cargadas de tu base de datos SQL y estructurarlas en un Esquema Estrella simple.

**Carga/Verificación:** Asegúrate de tener al menos las siguientes tablas cargadas desde tu proyecto SQL (ya sea como tablas o como Vistas optimizadas):

- HechosVenta (Contiene IdProducto, IdDoctor, Monto).

- DimProducto (Contiene IdProducto, Nombre, Categoría).

- DimDoctor (Contiene IdDoctor, NombreDoctor, Especialidad).

**Vista de Modelo:** Navega a la Vista de Modelo de Power BI.

**Relaciones:**

Arrastra el campo `IdProducto` desde la tabla `DimProducto` hacia el campo `IdProducto` en la tabla `HechosVenta`. Power BI debería crear automáticamente una relación 1:N.

Repite el paso para el campo `IdDoctor` entre `DimDoctor` y `HechosVenta`.

**Inspección:** Haz doble clic en una de las líneas de relación. Verifica que la Cardinalidad sea Uno:Muchos y que el Filtro Cruzado esté en dirección Única.


## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ Conceptos Clave: La distinción entre Tablas de Hechos (lo que mides) y Tablas de Dimensión (cómo filtras).
- ✅ Diseño BI: La importancia de apuntar al Esquema Estrella sobre el Esquema Copo de Nieve para el rendimiento.
- ✅ Relaciones: Cómo crear la cardinalidad 1:N en Power BI.
- ✅ Dimensión de Tiempo: La necesidad de una Tabla Calendario para análisis complejos de fechas.


## 🎯 Ejercicios de Práctica

**Ejercicio 1: Identificación de Tablas (Conexión SQL)**

- Basándote en tu sistema de ventas o clínica de SQL Server, clasifica los siguientes objetos para un modelo Power BI:

| **Objeto SQL**       | **¿Hecho o Dimensión?** | **Justificación** |
|-----------------------|--------------------------|--------------------|
| `Procedimiento`         |                          |                    |
| `Cita_Consulta`         |                          |                    |
| `Paciente`              |                          |                    |
| `Detalle_Tratamiento`   |                          |                    |


**Ejercicio 2: Creación de Relación y Error Común**

- En tu modelo, duplica la tabla DimProducto y llámala ProductosAlternos.

- Intenta crear una segunda relación entre ProductosAlternos[IdProducto] y HechosVenta[IdProducto].

- **Observación:** Power BI te permitirá crear la relación, pero la marcará como Inactiva (línea punteada). ¿Por qué Power BI no permite que haya dos relaciones activas entre las mismas dos tablas? (Pista: Piensa en la ambigüedad del filtro).


📖 **[Ir al Módulo 05: Fundamentos de DAX - Lenguaje de Análisis](/modulo-05-Fundamento-DAX/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*


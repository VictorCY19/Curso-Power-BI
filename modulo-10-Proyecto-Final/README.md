# 💻 Módulo 10: Proyecto Final de Análisis de Negocio
¡Felicidades! Has llegado al módulo final. Este es el momento de aplicar todo lo que aprendiste, desde la consulta optimizada con SQL hasta la seguridad con DAX. El Proyecto Final es la culminación de ambos cursos (SQL Server y Power BI) y el resultado que puedes mostrar con orgullo en tu portafolio.

El objetivo es integrar la Base de Datos del Proyecto Final de SQL Server (tu sistema clínico o de ventas) en un informe completo y profesional de Power BI.


## 🎯 Objetivo del Proyecto Integrador
Construir un informe de Power BI robusto y funcional que responda a las preguntas clave del negocio (ventas, desempeño, citas) utilizando el modelo de datos de tu proyecto SQL.


## 🛠️ Estructura del Proyecto Final: Pasos Clave
Este proyecto se divide en cinco fases que replican un flujo de trabajo profesional de Business Intelligence.

## **Fase 1: Optimización y Extracción de Datos (Módulos 2 y 3)**
Aquí conectarás Power BI con tu base de datos SQL, asegurando que solo traes la información necesaria y bien limpia.

**Revisión SQL (Vista/SP):** Antes de conectar, revisa tu proyecto de SQL Server. ¿Qué vistas o procedimientos almacenados (Módulo 6 de SQL) ya creaste para generar reportes? Si no tienes uno, crea una Vista SQL optimizada que consolide la información clave de tu hecho principal (Ej: vw_DatosCita con ID, Fecha, Doctor y Monto).

**Pista:** Usa una vista para evitar traer columnas que sabes que no usarás en el análisis.

**Conexión Estratégica:** Conecta Power BI a SQL Server utilizando la opción de comando SQL Avanzado (Módulo 2) para llamar a tu Vista o Procedimiento Almacenado.

**Limpieza con Power Query:** Lleva tus tablas al Editor de Power Query. Asegúrate de:

**Tipos de Datos Correctos:** Que las fechas sean fechas, los números sean números (Módulo 3).

**Eliminar Duplicados:** En tus claves de dimensión (IdPaciente, IdDoctor).


## **Fase 2: Modelado de Datos (Módulo 4)**
El rendimiento de tu informe depende de un modelo de datos limpio y eficiente.

**Diseño Estrella:** Identifica tu Tabla de Hechos Principal (Ej: Citas/Ventas) y tus Tablas de Dimensión (Ej: Paciente, Doctor, Producto).

**Pista:** Una tabla de Hechos es la que tiene la mayoría de las claves foráneas; las Dimensiones contienen los nombres y atributos.

**Tabla Calendario:** Crea una Tabla Calendario (Módulo 4) y asegúrate de que esté relacionada 1:N con la columna de Fecha en tu Tabla de Hechos.

**Relaciones:** Dibuja las relaciones 1:N entre las claves primarias de tus Dimensiones y las claves foráneas de tus Hechos. Verifica la dirección del filtro.


## **Fase 3: Creación de Métricas DAX (Módulos 5 y 6)**
Convierte los datos sin procesar en inteligencia de negocio.

**Métricas Base (Módulo 5):** Crea las medidas fundamentales (SUM, COUNTROWS) para Ingresos Totales, Número de Citas/Ventas, etc.

**Métricas Avanzadas (Módulo 6):** Aquí está la clave del proyecto. Utiliza CALCULATE para crear al menos tres métricas de tiempo o comparación:

**Crecimiento:** Ingresos vs. Mismo Periodo del Año Anterior.

**Acumulado:** Total de Servicios/Ventas Año a la Fecha (YTD).

**Comparación:** Porcentaje de Ingresos que provienen de la Categoría "Premium" (o similar, usando un filtro duro en CALCULATE).

**Uso de Variables:** Utiliza variables (VAR) en tu métrica más compleja para demostrar buenas prácticas de código.


## **Fase 4: Diseño y Narrativa (Módulos 7 y 8)**
Transforma los números en una historia visual convincente para el negocio.

**Estructura de Informe:** Diseña un informe de tres páginas con un flujo lógico:

- **Página 1: Resumen Ejecutivo/KPIs:** Solo Tarjetas (KPIs), tendencias clave (Gráfico de Líneas) y un Slicer principal (Ej: Rango de Fecha).

- **Página 2: Análisis de Desempeño:** Gráficos que responden a preguntas de desempeño (Ej: ¿Qué doctor/producto tiene el mayor ingreso? - Gráficos de Barras).

- **Página 3: Detalle y Distribución:** Uso de Matrices y la funcionalidad de Drill-Through (Módulo 7) para permitir al usuario ver el detalle de las transacciones (similar a un reporte de SELECT *).

**Funcionalidad Avanzada:** Incluye al menos una de las siguientes características avanzadas (Módulo 8):

- **Parámetro de Campo:** Para que el usuario elija dinámicamente si ve el gráfico por [Total Ingresos] o [Ganancia].

- **Tooltip de Página:** Para mostrar la tendencia de un elemento (Doctor/Producto) al pasar el ratón.


## **Fase 5: Implementación de Seguridad (Módulo 9)**
Demuestra que tu informe es apto para un entorno de producción.

**Definición de Roles:** Crea al menos dos Roles RLS (Módulo 9) en Power BI Desktop:

- **Rol 1 (Especialista):** Un rol que utiliza la función USERNAME() para filtrar los datos y asegurar que el usuario (Ej: un Doctor) solo vea sus propias citas o ventas.

- **Rol 2 (Gerente):** Un rol estático que filtra por una región o sede específica (Ej: 'DimSede'[Region] = "Sur").

- **Prueba Local:** Utiliza la opción "Ver como" en el Desktop para simular a los usuarios y verificar que los filtros de seguridad funcionen correctamente.

## 📝 Documentación del Proyecto
Junto al archivo .PBIX final, incluye un archivo de texto con lo siguiente:

- La Consulta SQL (o el EXEC del SP) que utilizaste para la conexión inicial.

- El código DAX de tu métrica más compleja (la que usa CALCULATE y VAR).

- Los nombres de los Roles RLS y la regla DAX utilizada para cada uno.


## ✅ Resumen del capítulo

**Ahora dominas:**

- ✅ Integración de Stack: La unión eficiente de la capa de datos (SQL Server) y la capa de análisis (Power BI).
- ✅ Ciclo de Vida BI: El flujo de trabajo completo: desde la Extracción y Transformación (ETL) hasta el Modelado y la Publicación Segura (RLS).
- ✅ Lenguaje de Análisis: La capacidad de traducir requisitos de negocio en métricas avanzadas usando el motor DAX (CALCULATE).
- ✅ Narrativa de Datos: La creación de reportes profesionales, interactivos y visualmente efectivos que impulsan la toma de decisiones.

👉 **¡Buena suerte! Este proyecto es tu portafolio, Al completarlo, habrás dominado todo el flujo de trabajo de un analista de BI moderno.**

📖 Puedes enviarme el link de portafolio o tu proyecto comprimido a mi [**Correo**](mailto:al_victor99@hotmail.com?subject=Proyecto_Modulo10_Curso_Power_BI) tratare de responderte lo antes posible, muchas gracias por leer este segundo curso, no olviden compartir este material con personas que crean que les puede ayudar bastante.

¡Hasta el proximo curso! 🦘

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*

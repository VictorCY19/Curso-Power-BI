# 📊 Curso: Análisis y Visualización con Power BI - De Principiante a Avanzado

## 🤔 ¿Qué es este proyecto?
Este curso es la continuación lógica de tu camino de aprendizaje en bases de datos. Si ya sabes construir y consultar datos en SQL Server, este repositorio te enseñará a transformar esos datos en historias de negocio interactivas y visuales usando Power BI Desktop, la herramienta de Business Intelligence más demandada del mercado.

**Mi filosofía:** Transformar los datos complejos que extraes con SQL en decisiones de negocio claras.

---

## 🎯 Objetivo de esta guía
Al finalizar esta guía, serás capaz de:

- Conectar Power BI con diversas fuentes de datos, incluyendo SQL Server.

- Limpiar, transformar y modelar datos complejos (incluyendo la normalización vista en SQL) usando Power Query (M).

- Escribir cálculos avanzados y métricas de negocio con el lenguaje DAX.

- Diseñar reportes interactivos y paneles (Dashboards) que comuniquen información de manera efectiva.

- Publicar y compartir tus análisis en el servicio de Power BI.

- Integrar directamente tus conocimientos de Vistas y Procedimientos Almacenados de SQL para crear informes eficientes.

---

## 📚 Estructura del Curso

### **Módulo 1: Introducción a Power BI y Preparación del Entorno**

- ¿Qué es Power BI? Componentes (Desktop, Service, Mobile).
- El rol del Analista de Datos y la importancia del BI.
- Instalación de Power BI Desktop.
- Navegación por la interfaz: Paneles, Vistas (Informe, Datos, Modelo).
- Conexión inicial: Cargar datos desde archivos planos (CSV, Excel).
- Ejercicio: Cargar datos de prueba e inspeccionar las tablas.

### **Módulo 2: Conexión Estratégica con SQL Server**

- Tipos de conexión: Importar (almacenar en memoria) vs. DirectQuery (consultar en vivo).
- Conexión a SQL Server: Usando las credenciales de tu proyecto.
- Ventaja SQL: Usar Vistas de SQL para importar solo los datos necesarios (Conexión con Módulo 6 de SQL).
- Ventaja SQL: Ejecutar Procedimientos Almacenados para obtener resultados dinámicos (Conexión con Módulo 6 de SQL).
- Ejercicio: Conectar Power BI a la base de datos CursoDB de tu proyecto SQL.

### **Módulo 3: Transformación de Datos con Power Query (El ETL)**

- Introducción al Editor de Power Query.
- Concepto de ETL: Extract (Extraer), Transform (Transformar), Load (Cargar).
- Limpieza de datos: Manejo de nulos, valores duplicados.
- Transformaciones clave: Cambio de tipos de datos, reestructuración (Pivot/Unpivot - Conexión con Módulo 13 de SQL).
- Creación de columnas condicionales y personalizadas.
- El lenguaje M (detrás de Power Query) y sus pasos.
- Ejercicio: Limpiar, estandarizar formatos y corregir errores en las tablas cargadas.

### **Módulo 4: Modelado de Datos y Normalización en Power BI**

- Conceptos de Tablas de Hechos (Facts) y Tablas de Dimensión (Dimensions).
- Esquema Estrella y Copo de Nieve (Refuerzo de Normalización de Módulo 3 de SQL).
- Gestión de Relaciones: Tipos (Uno a Uno, Uno a Muchos, Muchos a Muchos).
- Dirección del Filtro y Activación/Desactivación de Relaciones.
- Creación de una Tabla Calendario (Dimension Time/Date).
- Ejercicio: Modelar los datos de tu sistema de ventas SQL en un Esquema Estrella.

### **Módulo 5: Fundamentos de DAX - Lenguaje de Análisis**

- ¿Qué es DAX (Data Analysis eXpressions)? Contexto de Fila vs. Contexto de Filtro.
- Creación de Columnas Calculadas (usos limitados).
- Creación de Medidas (el corazón del análisis).
- Funciones de agregación básicas: SUM, AVERAGE, COUNTROWS
- Funciones de iteración: SUMX, AVERAGEX.
- Ejercicio: Calcular la ganancia total, el promedio de ventas y el conteo de pedidos.

### **Módulo 6: DAX Intermedio - El Poder de CALCULATE**

- La función CALCULATE: El motor principal de DAX.
- Modificadores de Filtro: ALL, ALLEXCEPT, ALLSELECTED.
- Funciones de Inteligencia de Tiempo: DATESYTD, DATEADD.
- Creación de métricas complejas: Ventas del Mes Anterior, % de Crecimiento.
- Uso de Variables en DAX para optimización y lectura.
- Ejercicio: Crear métricas de Comparación de Año-a-Fecha (YTD) y Crecimiento Mensual.

### **Módulo 7: Diseño y Visualización de Reportes**

- Principios de Visualización de Datos: ¿Qué gráfico usar y por qué?
- Tipos de visualizaciones: Columnas, Barras, Líneas, Mapas, Indicadores (KPIs).
- Uso efectivo de Filtros, Segmentaciones de Datos (Slicers) y Paneles de Filtro.
- Interacción y Drill-Through (Profundización).
- Mejores prácticas de diseño: Uso del color, tipografía, y narrativa.
- Ejercicio: Crear el primer Dashboard interactivo con los datos del sistema de ventas.

### **Módulo 8: Analítica Avanzada en Power BI**

- Agrupación y Binning.
- Uso de Parámetros de Campo.
- Visualizaciones Avanzadas (R, Python, o Custom Visuals).
- Implementación de Tooltips (Información sobre herramientas) de página.
- Funcionalidades de IA: Análisis de Influenciadores Clave.
- Ejercicio: Crear un análisis de distribución de productos por precio y cantidad.

### **Módulo 9: Seguridad y Publicación**

- El servicio de Power BI Service (la nube).
- Publicar el informe desde Power BI Desktop.
- Configuración de la actualización de datos (Gateways para SQL Server).
- Seguridad a Nivel de Fila (RLS): Implementación de roles y filtros dinámicos.
- Compartir informes y colaborar en Espacios de Trabajo.
- Ejercicio: Publicar tu informe, configurarlo para actualización y aplicar un rol RLS.

### **Módulo 10: Proyecto Final de Análisis de Negocio**

- Proyecto Integrador: Usar la base de datos del Proyecto Final de SQL Server.

  **Requerimientos:**

- Conexión optimizada a la BD (Vista o Procedimiento).
- Modelo de datos robusto (Esquema Estrella).
- Al menos 5 métricas avanzadas en DAX (CALCULATE, Inteligencia de Tiempo).
- Diseño de un Dashboard de 3 páginas (Resumen Ejecutivo, Detalle de Ventas, Análisis de Clientes/Productos).
- Implementación de Seguridad a Nivel de Fila (RLS) para simular roles de gerente/vendedor.

---

## 🚀 Características clave (Manteniendo la Filosofía)

✅ **Enfoque Práctico:** Cada módulo usa los datos de tu proyecto SQL anterior.

✅ **Conexión Directa:** Se enfatiza cómo usar Vistas y Procedimientos Almacenados de SQL (Módulos 6 y 13 del curso de SQL) para optimizar la carga de datos en Power BI.

✅ **Aprendizaje Progresivo:** De la carga de datos al Modelado, a DAX, y finalmente a la Visualización y Publicación.

---

## ⚠️ Aspectos importantes a considerar

### **Lo que ESTÁ incluido:**
- Guía estructurada paso a paso
- Ejemplos prácticos y ejercicios
- Proyectos realistas
- Recursos complementarios

### **Lo que NO ESTÁ incluido:**
- **No es una fuente exhaustiva**: Cubro lo esencial, pero siempre recomiendo complementar con documentación oficial
- **No soy un instructor certificado**: Soy un estudiante autodidacta compartiendo mi camino
- **Puede haber errores**: Si encuentras alguno, ¡ayúdame a corregirlo!

## 🛠️ Cómo usar esta guía

1. **Sigue el orden secuencial** de los módulos
2. **Haz todos los ejercicios** - la práctica es fundamental
3. **Experimenta con el código** - modifica los ejemplos y prueba variaciones
4. **Complementa con otros recursos** - nunca dependas de una sola fuente

---

## 🤝 ¿Encontraste un error o tienes sugerencias?

**¡Tu feedback es invaluable!** Como este es mi primer curso, aprecio cualquier comentario:

- **¿Encontraste un error?** → Abre un [Issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new)
- **¿Tienes una mejora?** → Envía un [Pull Request](https://github.com/VictorCY19/Curso-Power-BI/pulls)
- **¿Tienes una duda?** → Revisa los [issues existentes](https://github.com/VictorCY19/Curso-Power-BI/issues) o crea uno nuevo

---

## 📝 Mi compromiso contigo

Como creador y estudiante al mismo tiempo, me comprometo a:
- Mantener el contenido actualizado y relevante
- Corregir errores tan pronto como los identifique
- Mejorar la guía basado en mi aprendizaje continuo
- Responder a issues y pull requests en la medida de lo posible

---

## 🎓 Proyecto Final

El curso culmina con un **proyecto integrador** donde aplicarás todo lo aprendido para construir un sistema completo de base de datos. Es la mejor manera de consolidar tus conocimientos.

---

## ⚡ Empezar ahora

**¿Listo para comenzar?** Ve al [Módulo 1: Introducción a Power BI y Preparación del Entorno](./modulo-01-Introduccion/README.md)

---

> **Nota del autor**: Si estás empezando como yo en este mundo, te animo a que sigas esta guía pero también explores por tu cuenta. El aprendizaje autodidacta es sobre curiosidad y experimentación. ¡Vamos a aprender juntos!

**¿Te unes a mi viaje de aprendizaje?** ⭐ Dale una estrella al repositorio para seguir el progreso.
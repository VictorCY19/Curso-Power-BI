# 💻 Módulo 9: Seguridad y Publicación
Hasta ahora, todo tu trabajo ha estado contenido en tu máquina, dentro del archivo de desarrollo de Power BI Desktop (.PBIX). Este módulo te enseña cómo llevar tus análisis al mundo real: publicar, compartir con tu equipo y, crucialmente, asegurar que cada usuario solo vea los datos que le corresponden, utilizando la Seguridad a Nivel de Fila (RLS).

## 1. El Servicio de Power BI (Power BI Service)
El Power BI Service es el entorno en la nube de Microsoft (SaaS - Software as a Service) donde se gestionan y consumen los informes.

**Función:** Es el centro para la colaboración, la actualización de datos, la seguridad y la creación de Paneles (Dashboards) que consolidan visualizaciones de múltiples informes.

**Espacios de Trabajo (Workspaces):** Son carpetas virtuales donde se agrupan los informes, modelos de datos y paneles para un equipo o proyecto específico (Ej: "Análisis Clínico", "Ventas Nacionales").


## 2. Publicar el Informe y Configurar el Gateway
Publicar es el paso que mueve tu trabajo desde tu PC al Power BI Service.

**Publicación:** Desde Power BI Desktop, haz clic en "Publicar" en la pestaña Inicio. Elige el Workspace de destino.

**El Gateway (Puerta de Enlace):** Dado que tu origen de datos (SQL Server) está probablemente detrás del firewall de tu organización (o en tu máquina local), el Servicio de Power BI (en la nube) no puede acceder directamente a él para actualizar los datos.

**Función del Gateway:** Actúa como un puente seguro que recibe las credenciales y las peticiones de actualización del Servicio de Power BI y las pasa a SQL Server.

**Configuración de Actualización:** Una vez publicado, debes ir al Service, encontrar el Dataset (Modelo de Datos) y configurar la Actualización Programada especificando qué Gateway debe usar y con qué credenciales debe acceder a SQL Server.


## 3. Seguridad a Nivel de Fila (RLS)
La Seguridad a Nivel de Fila (Row-Level Security o RLS) es una característica crítica para entornos empresariales. Permite definir filtros para los datos que restringen el acceso a nivel de fila, asegurando que un usuario solo vea la información relevante para él (Ej: El Doctor "Pérez" solo ve las citas asignadas a él).

**Concepto:** Se basa en crear Roles y definir reglas DAX que se aplican al modelo de datos.

### **a) Creación de Roles**

- En Power BI Desktop, ve a la pestaña Modelado y haz clic en "Administrar roles".
- Crea un nuevo rol (Ej: GerenteRegional, Doctor).
- Asigna una Regla DAX a una tabla del modelo.

### **b) Definición de la Regla DAX**
La regla DAX actúa como un filtro invisible aplicado a la tabla.

**Ejemplo de Regla Estática:**

Fragmento de código
```m
// Regla para el rol 'GerenteRegional'
'DimSede'[Region] = "Norte"
```
Cualquier usuario asignado a este rol solo verá las filas donde la Región sea "Norte".

**Ejemplo de Regla Dinámica (Basada en el Usuario):** Esta es la más común. Utiliza la función USERNAME() de DAX para identificar quién está viendo el informe.

Fragmento de código
```m
// Regla para el rol 'Doctor'
'DimDoctor'[Email] = USERNAME() 
```

Aquí, el email del doctor en la tabla DimDoctor debe coincidir con el email de inicio de sesión del usuario de Power BI.

### **c) Probar los Roles**

- En Power BI Desktop, en la pestaña Modelado, haz clic en "Ver como".
- Selecciona el rol que creaste (Ej: Doctor) y prueba si las visualizaciones se filtran correctamente.


## 4. Asignar Roles y Compartir Informes
Una vez que el informe está publicado y los roles RLS están creados, el paso final se hace en el Power BI Service.

**Asignación de Usuarios a Roles:**

- En el Service, ve al Dataset (Modelo de Datos) asociado a tu informe.
- Haz clic en "Seguridad".
- Asigna los usuarios o grupos de seguridad de tu organización (Ej: perez.a@clinica.com) al rol que creaste (Ej: Doctor).

**Compartir: Para que los usuarios puedan acceder:**

- **Compartir Directo:** Compartes el informe con usuarios específicos (útil para informes puntuales).
- **Espacios de Trabajo (Workspaces):** La forma más limpia. Añades a los usuarios al Workspace con los permisos adecuados (Visor, Colaborador, Miembro).


## 5. Ejercicio Práctico: Implementación de Seguridad Dinámica

**Objetivo:** Simular y probar la seguridad a nivel de fila para un doctor de tu clínica.

**Paso 1: Preparación del Modelo (Desktop)**

Asegúrate de que tu tabla DimDoctor tenga una columna de Email para fines de prueba (incluso si la llenas con tu propio email temporalmente).

**Paso 2: Creación del Rol RLS**

- En Desktop, ve a Modelado → Administrar roles.
- Crea un rol llamado MiDoctor.
- En la tabla DimDoctor, aplica la siguiente regla DAX:

Fragmento de código
```m
'DimDoctor'[Email] = USERNAME()
```

**Paso 3: Prueba Local**

- Ve a Modelado → Ver como.
- Selecciona el rol MiDoctor.
- En el cuadro de texto que aparece, ingresa el Email de prueba que pusiste en la tabla DimDoctor.
- **Observa tu informe:** solo deberías ver los datos asociados al doctor cuyo email ingresaste.


## ✅ Resumen del Capítulo

**Ahora dominas:**

- ✅ Publicación: Mover el trabajo de Desktop al Power BI Service.
- ✅ Actualización: El rol del Gateway para mantener la conexión segura con SQL Server.
- ✅ Seguridad (RLS): El concepto clave de la Seguridad a Nivel de Fila.
- ✅ DAX para RLS: Usar las funciones USERNAME() para crear reglas de seguridad dinámicas y el proceso de Administrar Roles.


## 🎯 Ejercicios de Práctica

**Ejercicio 1: Despliegue de Seguridad Estática**

- Crea un rol RLS llamado GerenteJunior.
- Aplica la siguiente regla a tu tabla de Dimensiones de Productos o Servicios:

Fragmento de código
```m
'DimProducto'[Categoría] <> "Servicios de Bajo Margen" 
(o un filtro similar que restrinja datos no esenciales).
```

- Usa "Ver como" en Desktop, selecciona este rol y verifica que todos los gráficos y tablas del informe ya no muestren datos de la categoría "Servicios de Bajo Margen".

**Ejercicio 2: Flujo de Trabajo y Componentes**

- Describe el flujo de trabajo completo, nombrando los tres componentes (Desktop, Service, Gateway/SQL) y los pasos (1-5) para que un informe de Power BI publicado en la nube pueda mostrar datos actualizados de SQL Server a un usuario final.


📖 **[Ir al Módulo 10: Proyecto Final de Análisis de Negocio](/modulo-10-Proyecto-Final/README.md)**

---

*Si encuentras algún error o tienes sugerencias para mejorar este módulo, por favor [abre un issue](https://github.com/VictorCY19/Curso-Power-BI/issues/new) en el repositorio.*

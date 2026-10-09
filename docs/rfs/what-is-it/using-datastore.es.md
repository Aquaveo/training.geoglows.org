# El Almacén de Datos

El [Almacén de Datos de RFS](https://apps.geoglows.org/previews/rfs-data-store) es el lugar para encontrar y descargar los datos de RFS. Enumera todos los conjuntos de datos que publica el modelo, describe el contenido de cada uno y le permite descargar solo los ríos y las fechas que necesita.

## 1. Elija una versión del modelo

La página de inicio enumera cada versión de RFS. Seleccione **RFS v3**, la versión actual, para ver sus conjuntos de datos. RFS v2 y v1 son archivos históricos que puede explorar, pero sus datos no se pueden descargar a través de esta aplicación.

![La página de inicio del Almacén de Datos de RFS, con la lista de cada versión del modelo](../../static/images/datastore-versions.jpg)

## 2. Busque un conjunto de datos

La lista de conjuntos de datos muestra todo lo disponible para esa versión, como hidrografía, caudal retrospectivo, pronósticos y mapas de inundación.

- Use la **barra de búsqueda** para buscar un conjunto de datos por nombre.
- Use los **filtros** de la izquierda para reducir la lista por categoría, formato de archivo o resolución temporal (por ejemplo, datos horarios o diarios).
- Use **Sort by** (Ordenar por) para ordenar la lista por título o por la fecha de su última actualización.

Seleccione un conjunto de datos para abrir su página.

## 3. Conozca el conjunto de datos

Cada página de conjunto de datos tiene tres pestañas:

- **Overview** (Resumen): una descripción del conjunto de datos y sus metadatos (ver más abajo).
- **Download** (Descarga): herramientas para descargar los datos (ver más abajo).
- **Documentation** (Documentación): información técnica más detallada.

![Una página de conjunto de datos con sus pestañas Overview, Download y Documentation](../../static/images/datastore-dataset-page.jpg)

### Metadatos e información del conjunto de datos

La pestaña **Overview** es un buen punto de partida antes de descargar cualquier cosa. Describe qué contiene el conjunto de datos y cómo está organizado, incluyendo:

- **Descripción**: qué son los datos y cómo se produjeron.
- **Cobertura y resolución**: el periodo de tiempo, el paso de tiempo (por ejemplo, horario o diario), la cobertura espacial y la resolución espacial de los datos.
- **Variables**: el nombre, las unidades y las dimensiones de cada variable en los archivos, como `Q`, el caudal en metros cúbicos por segundo.
- **Detalles del conjunto de datos**: el formato de archivo, el sistema de referencia de coordenadas, la versión del modelo, el proveedor, la frecuencia de actualización y las fechas de creación y última actualización del conjunto de datos.
- **Licencia y cita**: los términos bajo los cuales se comparten los datos y cómo citarlos en su trabajo.
- **Almacenamiento**: dónde se almacenan los datos en el bucket público de RFS.
- **Registro de cambios**: un historial de las actualizaciones del conjunto de datos.
- **Conjuntos de datos relacionados**: enlaces a otros conjuntos de datos que suelen usarse juntos, como el caudal horario, diario y mensual.

![Metadatos y variables del conjunto de datos en la pestaña Overview](../../static/images/datastore-metadata.jpg)

## 4. Descargue los datos

En la pestaña **Download**, siga los pasos numerados:

1. **Área de interés**: elija qué descargar y luego selecciónelo en el mapa. Puede elegir una cuenca, los ríos entre dos puntos, ríos individuales, una o más regiones, o todo el mundo.
2. **Rango de tiempo**: elija las fechas de inicio y fin, o use un atajo como los últimos 30 días o el registro completo.
3. **Formato**: elija el formato de archivo a descargar.
4. **Términos de uso**: lea el acuerdo de uso de datos y marque ambas casillas para aceptarlo junto con la licencia del conjunto de datos.
5. **Solicitud**: inicie sesión, revise el resumen de su solicitud (incluido su tamaño estimado) y seleccione **Download**.

![Selección de un área de interés en la pestaña Download](../../static/images/datastore-area-of-interest.jpg)

### Descargarlo usted mismo

Si prefiere descargar los datos con sus propias herramientas, la sección **Download it yourself** (Descárguelo usted mismo), al final de la pestaña Download, ofrece comandos listos para usar con s5cmd, la AWS CLI, Python y JavaScript. Los datos se almacenan en un bucket público, por lo que estos comandos no requieren una cuenta.

![Comandos de descarga listos para usar en la sección Download it yourself](../../static/images/datastore-download-yourself.jpg)

La página **Packages** (Paquetes) del Almacén de Datos también enlaza a las dos bibliotecas de código mantenidas para leer datos de RFS: **geoglows** para Python y **riverforecastsystem** para JavaScript.

## Resumen

Existen 4 tipos principales de conjuntos de datos fluviales proporcionados por el Sistema de Pronóstico de Ríos (River Forecast System). Todos estos datos están disponibles de forma gratuita.

1. **Hidrografía**: Datos SIG sobre la ubicación de ríos, cuencas y lagos en todo el mundo.
2. **Simulación retrospectiva**: Datos horarios de caudal desde enero de 1940.
3. **Pronósticos**: Pronósticos de caudal a 15 días generados cada día a la medianoche.
4. **Mapas de Inundación**: Extensiones y profundidades de inundación cartografiadas a partir de los pronósticos y de los caudales de los periodos de retorno.

[The GEOGLOWS River Forecast System V3](https://www.geoglows.org){:target="_blank"} © [Dr. Riley Hales](https://hales.app) 2025 tiene licencia
bajo [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/){:target="_blank"}

## Tabla de conjuntos de datos

La forma más sencilla de encontrar y descargar los datos de RFS V3 es el [Almacén de Datos de RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"},
que describe cada conjunto de datos y le permite descargar solo los ríos y las fechas que necesita. Consulte [El Almacén de Datos](../../what-is-it/using-datastore.md) para obtener
instrucciones.

Todos los conjuntos de datos de RFS V3 se almacenan en un único bucket público de AWS S3, `river-forecast-system-v3`, en la región `us-west-2`. **No necesita** una cuenta
de AWS, tarjeta de crédito, ni un nombre de usuario y contraseña para descargar datos de él. Puede explorar el bucket en un navegador web en
[https://v3.s3.riverforecastsystem.com](https://v3.s3.riverforecastsystem.com){:target="_blank"}.

Al consultar datos en AWS, es posible que deba especificar que está accediendo de forma anónima si no tiene una cuenta de AWS o si prefiere no proporcionar credenciales.

| Conjunto de Datos                                                                                                                                | Formato(s) de Archivo | URI y Ruta del Bucket                                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|-----------------------------------------------------------------------------|
| [Pronóstico por Ensamble de 15 Días](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/forecast-15day){:target="_blank"}             | Zarr                  | `s3://river-forecast-system-v3/forecasts15/`                                |
| [Líneas Centrales de Ríos](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/streams){:target="_blank"}                              | GeoParquet            | `s3://river-forecast-system-v3/hydrography/`                                |
| [Límites de Cuencas](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/catchments){:target="_blank"}                                 | GeoParquet            | `s3://river-forecast-system-v3/hydrography/`                                |
| [Puntos de Confluencia](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/confluences){:target="_blank"}                             | GeoParquet            | `s3://river-forecast-system-v3/hydrography/`                                |
| [Lagos](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/lakes){:target="_blank"}                                                   | GeoParquet            | `s3://river-forecast-system-v3/hydrography/`                                |
| [Retrospectivo - Caudal Horario](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-hourly){:target="_blank"}           | Zarr                  | `s3://river-forecast-system-v3/retrospective/hourly.zarr`                   |
| [Retrospectivo - Caudal Diario](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-daily){:target="_blank"}             | Zarr                  | `s3://river-forecast-system-v3/retrospective/daily.zarr`                    |
| [Retrospectivo - Caudal Mensual](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-monthly){:target="_blank"}          | Zarr                  | `s3://river-forecast-system-v3/retrospective/monthly.zarr`                  |
| [Retrospectivo - Caudal Anual](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/retrospective-yearly){:target="_blank"}             | Zarr                  | `s3://river-forecast-system-v3/retrospective/yearly.zarr`                   |
| [Retrospectivo - Máximos Anuales](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/annual-maximums-daily){:target="_blank"}         | Zarr                  | `s3://river-forecast-system-v3/retrospective/maximums.zarr`                 |
| [Retrospectivo - Periodos de Retorno](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/return-periods){:target="_blank"}            | Zarr                  | `s3://river-forecast-system-v3/retrospective/return-periods.zarr`           |
| [Retrospectivo - Curvas de Duración de Caudal](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/flow-duration-curves){:target="_blank"} | Zarr              | `s3://river-forecast-system-v3/retrospective/fdc.zarr`                      |
| [Mapas de Inundación de Pronóstico](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/forecast-flood-maps){:target="_blank"}         | GeoParquet, GeoTIFF   | `s3://river-forecast-system-v3/forecasts15/year=YYYY/month=MM/day=DD/`      |
| [Mapas de Inundación por Periodo de Retorno](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/return-period-flood-maps){:target="_blank"} | GeoTIFF         | `s3://river-forecast-system-v3/flood-maps/lat=YYY/lon=XXX/return-periods/`  |
| [Bibliotecas FLDPLN](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3/fldpln-libraries){:target="_blank"}                           | Zarr, PMTiles         | `s3://river-forecast-system-v3/flood-maps/lat=YYY/lon=XXX/fldpln.zarr/`     |

## Código y Referencias Técnicas

- Scripts para el cálculo de pronósticos: [https://github.com/geoglows/geoglows_ecflow](https://github.com/geoglows/geoglows_ecflow){:target="_blank"}
- Scripts de actualización semanal de la simulación retrospectiva: [https://github.com/geoglows/retrospective-update](https://github.com/geoglows/retrospective-update){:target="_blank"}

## Descarga de datos desde la línea de comandos (recomendado)

La forma más rápida de descargar datos de RFS es utilizando la Interfaz de Línea de Comandos (CLI) de AWS. Si no está familiarizado con la programación o las herramientas de línea de comandos,
pase a la siguiente sección sobre cómo descargar datos con un navegador web.

Usar la CLI permite descargar datos más rápidamente que a través del navegador y se recomienda para descargar grandes volúmenes de datos. Consulte las instrucciones de AWS
para descargar datos desde S3. Es posible que deba agregar el parámetro `--no-sign-request` en sus comandos de copia o sincronización. La pestaña
**Download** de cada conjunto de datos en el [Almacén de Datos de RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"} también ofrece comandos
listos para usar con s5cmd y la AWS CLI.

## Descarga de datos con un navegador web

La forma más simple de explorar los conjuntos de datos de RFS V3 es mediante el [Almacén de Datos de RFS](https://apps.geoglows.org/previews/rfs-data-store/datasets/v3){:target="_blank"}
o el [explorador del bucket](https://v3.s3.riverforecastsystem.com){:target="_blank"}. Esta no es la forma más rápida de descargar grandes volúmenes de datos.
Para un mejor rendimiento al descargar datos, se recomienda usar las instrucciones de la línea de comandos.

RFS permite a los usuarios descargar datos de caudal global directamente desde AWS. Esto proporciona acceso tanto a los datos de la simulación retrospectiva como a los pronósticos
de caudal a 15 días. Estos conjuntos de datos se alojan en buckets de S3, optimizados para el análisis de series temporales y las descargas masivas.

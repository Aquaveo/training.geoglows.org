!!! danger "La descarga masiva generalmente no es necesaria"
    La mayoría de los usuarios no necesitan este tutorial. Todos los productos de pronóstico y de simulación retrospectiva están disponibles para consultas, descargas masivas
    y a través del servicio de datos. Sin embargo, las instrucciones para consultar datos son la forma más rápida y conveniente (y la más económica para GEOGLOWS) para la mayoría de los usos.
    Siga el tutorial sobre [cómo consultar datos de ríos](code-and-apis.es.md) antes de continuar con esta sección.

## Referencias
La mayoría de los usuarios no necesitan descargar el resultado completo de la simulación para todo el mundo. A menudo, basta con una consulta/descarga más grande. Si
decide continuar, debe estar familiarizado con awscli o con algún equivalente similar. Una regla general útil para estimar el espacio en disco necesario es:

- 1 día de pronósticos ocupa aproximadamente 150GB
- El zarr de la simulación retrospectiva horaria ocupa aproximadamente 6TB
- El zarr de la simulación retrospectiva diaria ocupa aproximadamente 500GB
- El zarr de la simulación retrospectiva mensual ocupa aproximadamente 20GB
- El zarr de la simulación retrospectiva anual ocupa aproximadamente 2GB

## awscli

La mejor manera de descargar datos de forma masiva desde los buckets de S3 es utilizar una herramienta de línea de comandos diseñada para este propósito. Estas herramientas permiten descargar varios conjuntos de datos
simultáneamente y a velocidades más altas que las posibles mediante el navegador web. La herramienta básica para esto es awscli.
Use los [tutoriales de AWS S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/download-objects.html){:target="_blank"} para comenzar.

!!! tip "Use `--no-sign-request`"
    Use el parámetro `--no-sign-request` para evitar errores, especialmente si no tiene credenciales de AWS en su computadora.

Todos los datos de RFS V3 se almacenan en un solo bucket. Al descargar datos, los pronósticos se encuentran en `s3://river-forecast-system-v3/forecasts15/` y la simulación
retrospectiva en `s3://river-forecast-system-v3/retrospective/`. El pronóstico de cada día se almacena en su propia carpeta por año, mes y día.

El patrón general del comando CLI para los conjuntos de datos de pronóstico es:

```shell
aws s3 cp s3://river-forecast-system-v3/forecasts15/year=<YYYY>/month=<MM>/day=<DD>/discharge.zarr </local/save/path> --recursive --no-sign-request
```
El patrón general del comando CLI para los conjuntos de datos retrospectivos es:

```shell
aws s3 cp s3://river-forecast-system-v3/retrospective/daily.zarr </local/save/path> --recursive --no-sign-request
```

## s5cmd

`s5cmd` es una alternativa de mayor rendimiento a `awscli`. Consulte la [documentación de s5cmd](https://github.com/peak/s5cmd){:target="_blank"}.
El patrón general del comando CLI para los conjuntos de datos de pronóstico es:

```shell
s5cmd --no-sign-request cp "s3://river-forecast-system-v3/forecasts15/year=<YYYY>/month=<MM>/day=<DD>/discharge.zarr/*" </local/save/path.zarr/>
```

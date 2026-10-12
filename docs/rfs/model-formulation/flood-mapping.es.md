# Mapeo de Inundaciones

!!! warning "Advertencia"
    El propósito de esta sección sobre la formulación del modelo es proporcionar una visión general del RFS, incluyendo sus entradas y resultados. Si le interesa principalmente usar los datos, puede omitir esta sección y pasar a la sección [Datos](../data/available-data.md) de nuestro sitio.

Los mapas de inundación de RFS se crean con [NenCarta](https://nencarta.readthedocs.io/en/latest/configuration.html), una herramienta que automatiza el mapeo de inundaciones fluviales.
NenCarta utiliza la herramienta [Automated Rating Curve (ARC)](https://automated-rating-curve.readthedocs.io/en/latest/) para estimar cómo cambia el nivel del agua en cada río según el caudal,
y el método FLDPLN para convertir un caudal en un mapa del área inundada y su profundidad.

- **¿Por qué FLDPLN?** FLDPLN es una versión mejorada del método HAND (Height Above Nearest Drainage), de uso común. Sus resultados se
  almacenan en tablas, lo que hace que los mapas de inundación sean más rápidos y fáciles de acceder y utilizar.
- **Solo inundaciones fluviales.** Los mapas muestran las inundaciones causadas por ríos que crecen y se desbordan. No muestran las
  inundaciones causadas directamente por lluvias intensas, como el agua que se acumula en zonas bajas o en las calles de las ciudades.
- **Se actualizan con el tiempo.** Los mapas de inundación pueden actualizarse y mejorarse a medida que haya nuevos datos y métodos disponibles.

Esta página no cubre la teoría detrás de estos métodos. Para obtener más información, consulte la [documentación de NenCarta](https://nencarta.readthedocs.io/en/latest/configuration.html) y la
[documentación de ARC](https://automated-rating-curve.readthedocs.io/en/latest/). Para ver los mapas de inundación, utilice las herramientas de mapeo de inundaciones del [Hydroviewer](../web-apps/hydroviewer.md).

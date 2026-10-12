# Flood Mapping

!!! warning "Warning"
    The purpose of this section on model formulation is to provide an overview of the RFS, including its inputs and outputs. If you're primarily interested in using the data, feel free to skip this and move to the [Data](../data/available-data.md) section of our page.

RFS flood maps are created with [NenCarta](https://nencarta.readthedocs.io/en/latest/configuration.html), a tool that automates riverine flood mapping. NenCarta uses the
[Automated Rating Curve (ARC)](https://automated-rating-curve.readthedocs.io/en/latest/) tool to estimate how the water level in each river changes with streamflow, and the FLDPLN
method to turn a streamflow into a map of the flooded area and its depth.

- **Why FLDPLN?** FLDPLN is an improved version of the commonly used HAND (Height Above Nearest Drainage) method. Its results are stored
  as tables, which makes the flood maps faster and easier to access and use.
- **Riverine flooding only.** The flood maps show flooding from rivers rising and overflowing their banks. They do not show flooding caused
  directly by heavy rainfall, such as water ponding in low areas or on city streets.
- **Updated over time.** The flood maps can be updated and improved as new data and methods become available.

This page does not cover the theory behind these methods. To learn more, read the [NenCarta documentation](https://nencarta.readthedocs.io/en/latest/configuration.html) and the
[ARC documentation](https://automated-rating-curve.readthedocs.io/en/latest/). To see the flood maps, use the flood mapping tools in the [Hydroviewer](../web-apps/hydroviewer.md).

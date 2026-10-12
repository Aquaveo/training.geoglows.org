# River Routing

!!! warning "Warning"
    The purpose of this section on model formulation is to provide an overview of the RFS, including its inputs and outputs. If you're primarily interested in using the data, feel free to skip this and move to the [Data](../data/available-data.md) section of our page.

Routing is the step where RFS moves water through the river network. Once the runoff from each river's catchment has been calculated
(see the [Overview](model-formulation.md)), routing carries that water downstream, river by river, to create a hydrograph for every river.
RFS uses [river-route](https://river-route.code.hales.app/){:target="_blank"}, a Python package developed by Dr. Riley Hales to route water through very large river
networks quickly. The code is available on [GitHub](https://github.com/rileyhales/river-route){:target="_blank"}.

## How Water Moves Through the Network

At each time step, the runoff from a river's catchment is added to that river, along with all the water flowing in from the rivers
directly upstream of it. Because a river's flow depends on everything upstream, the rivers are calculated in order from upstream to
downstream: headwater streams first, and the outlet last. This is the order stored in the `riverIndex` attribute of the RFS hydrography.

![Rivers are routed in order from upstream to downstream](../../static/images/river-routing-network.png)

## Muskingum Routing

RFS uses the Muskingum method to calculate how water moves through each river. It estimates the water leaving a river at the next time
step (\(Q_{t+1}\)) from the water entering it at the next time step (\(I_{t+1}\)), the water entering it now (\(I_t\)), and the
water leaving it now (\(Q_t\)):

$$
Q_{t+1} = c_1 I_{t+1} + c_2 I_t + c_3 Q_t
$$

The coefficients \(c_1\), \(c_2\), and \(c_3\) add up to 1, so no water is gained or lost. They are calculated from the length of the
time step and two parameters that are set for each river:

- **k**: the time it takes a flood wave to travel the length of the river. Longer, slower rivers have larger values of k.
- **x**: how much the flood wave spreads out and flattens as it travels, from 0 (the most flattening) to 0.5 (none).

Together, these delay the flood wave and spread it out as it moves downstream. The values for each river are included in the RFS
hydrography as the `musk_k` and `musk_x` attributes.

![Muskingum routing delays a flood wave and flattens its peak](../../static/images/river-routing-muskingum.png)

## Time Steps

river-route routes the water at a time step that is equal to or shorter than the time step of the runoff data, so every runoff value is
routed at least once. The routed flows are then averaged into the time steps of the RFS outputs:

- **Retrospective simulation**: hourly average flows, which are then combined into daily, monthly, and yearly averages.
- **Forecasts**: 3-hour average flows for each of the 15 days of the forecast.

## Learn More

To see routing in action, try the interactive demonstration on the [Model Overview](../background/model-overview.md) page. For the full
details of the method, including the math, read the [river-route documentation](https://river-route.code.hales.app/){:target="_blank"} and its
[math derivations](https://river-route.code.hales.app/references/math/){:target="_blank"}.

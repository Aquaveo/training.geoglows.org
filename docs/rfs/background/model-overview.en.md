# Overview

The river forecast system is designed to predict how much water is in rivers globally. This is calculated using a basic equation that says that all water on the Earth must be conserved. In other words, water that falls as precipitation must then either go into the ground (infiltration), evaporate back into the atmosphere, or it will continue to run off along the ground.

This idea is commonly known as the water cycle. Water cycles through the earth falling as precipitation, then evaporating into the air, then condensing and then falling again.

![The water cycle](../../static/images/Water-Cycle-Art2A_medium.png)

*Image credit: [NASA Global Precipitation Measurement](https://gpm.nasa.gov/education/water-cycle)*

To learn more about the water cycle, see NASA's [Water Cycle](https://gpm.nasa.gov/education/water-cycle) page.

The surface runoff is the water that stays on the surface without evaporating or soaking into the ground. This is like the water you may see after a storm running down the street or sidewalks.

This water will eventually accumulate in certain places creating streams and lakes. The water will then continue to flow downhill as a river until it either reaches the ocean or a lake with no outlets.

Therefore to predict the water in the streams we need to know a couple of things

1. **The elevation data.** With this information, we can assume where streams will begin to accumulate. We know that water flows downhill, so with the elevation of the earth’s surface we know where water will go as it rains.
2. **The quantity of water becoming surface runoff.** There are meteorological models that predict how much it will rain in the future and they can say how much it rained in the past. These are what we use when we check the weather to know if it will rain tomorrow. That same information can be used to know what the streamflow will be tomorrow. Knowing this information allows us to estimate how much water is going to be runoff and therefore flow into the streams.
3. **How much water is upstream of me.** We know that water once it is in a stream continues to flow until it hits a lake with no outlets or an ocean. This means that the water in the stream in my backyard is influenced by how much it rained in my yard, but also by how much water was in it upstream and flowed down to my yard. We can figure this out by continuously moving the water downstream.
4. **How the water moves.** We need to know how water moves into streams and then how the water moves downstream once it is in the river. For example, we need to know the speed that this happens so we know how much time it takes a rain that enters the Mississippi river in the northern part of the United States to reach the Atlantic Ocean.

In the river forecast system, these are the pieces needed to create the hydrologic model. River forecast system uses elevation data from TDX-Hydro which is built from satellite data and uses it to estimate where streams are globally. The quantity of water we get from ECMWF, a European institution that runs meteorological models. They model how much precipitation there was in the past and predict how much there will be in the future. They also predict how much of the precipitation will turn into surface runoff to enter the streams. This is how the quantity of water entering streams can be predicted.

The second two components - how much water is upstream and how water moves are related components. These are calculated using a process called routing. This is where we calculate water moving between little stream segments. If we have it running continuously, then we always see how much water is upstream and we can move it downstream while more water gets added to the river from local rainfall. This is the process that our model performs. There are several different methods to perform this calculation. We do a process called Muskingum routing, which is the name of the equations we use to calculate how the water moved through each little stream segment into the downstream piece.

We have created this web application to better demonstrate how this process works.

[https://cdn.apps.geoglows.org/webroute/live.html](https://cdn.apps.geoglows.org/webroute/live.html#map=1.6/21.3/-14.8)

While there are lots of ways to look at it, a simple way for the demonstration is to select “pulse” as your brush.

<video controls muted playsinline width="100%">
  <source src="/static/videos/webroute-pulse-demo.mp4" type="video/mp4">
</video>

This is choosing to enter water in a specific location. Click somewhere on the stream network map. As the streams change color, you are watching the water move through your river using the routing algorithm that RFS uses. The difference is that instead of randomly selecting locations like in this demonstration, we use the global predictions to put water into all the rivers every time it rains.

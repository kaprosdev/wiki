# FEZSKY format

## TODO

- When creating or adjusting a [Sky](#sky), all textures used for the sky must be placed in an adjacent folder with the same name as the sky.
- If a sky has a `Stars` texture, it is night in-game, and the level is not rainy nor named `TELESCOPE` or `TREE`, there is a roughly 0.005% chance (1 in 20,000) every tick for a shooting star to appear in the sky.
- If `VerticalTiling` is false, the top and bottom pixel rows of `Background` are stretched to fill the sky above and below.
- High values for `InterLayerVerticalDistance` cause sky layers at the back to rise faster as the camera ascends in the level.
- High values for `InterLayerHorizontalDistance` cause sky layers in the _front_ to scroll faster as the camera moves left or right.
- Setting `HorizontalDistance` or `VerticalDistance` to 0 causes sky layers to never scroll in the respective dimension, aside from parallax effects set by the `InterLayer` properties.
  - Setting them to 1 causes the layers to always stay in the same position relative to the "center" of their respective dimension in the level.
  - Setting them to a value greater than 1 causes layers to scroll _against_ the camera's movement direction in that dimension.

## Property definitions

### Sky
|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the sky used internally by the game.|
|Background|String|Name of the background texture used by the sky.|
|WindSpeed|Float|Determines speed of clouds, as well as background layers affected by wind.|
|Density|Float|Determines quantity and density of clouds. (Unused? - set to 1 in every sky)|
|FogDensity|Float|(Changes fog effect - somehow)|
|Layers|[SkyLayer](#skylayer)[]|A list of parallax layers to use in the sky.|
|Clouds|String[]|List of names of cloud textures.|
|Shadows|String|Name of shadow texture to project onto the level (and sky layers, if `FoliageShadows` is enabled).|
|Stars|String|Name of stars texture - blended with other sky layers (need more research)|
|CloudTint|String|Name of file to use as a reference(? what kind) for cloud colors|
|VerticalTiling|Boolean|Determines whether the sky loops vertically (including `Layers`).|
|HorizontalScrolling|Boolean|Determines whether (non-cloud) background layers move based on `WindSpeed`, `WindDistance`, and `WindParallax`.|
|LayerBaseHeight|Float|How high (0.0-1.0) the layer textures are placed in the sky.|
|InterLayerVerticalDistance|Float|Vertical parallax factor between layers.|
|InterLayerHorizontalDistance|Float|Horizontal parallax factor between layers.|
|HorizontalDistance|Float|Horizontal scroll speed of all sky layers (before parallax).|
|VerticalDistance|Float|Vertical scroll speed of all sky layers (before parallax).|
|LayerBaseSpacing|Float||
|WindParallax|Float||
|WindDistance|Float||
|CloudsParallax|Float||
|ShadowOpacity|Float|Determines opacity of `Shadows` over the level.|
|FoliageShadows|Boolean|Causes sky shadows to be drawn over sky layers as well as the level.|
|NoPerFaceLayerXOffset|Boolean|If enabled, layers will not be offset differently on different sides of the level.|
|LayerBaseXOffset|Float|Starting horizontal offset for sky layers. (usually used to prevent grid skies from aligning too well from the level origin?)|

### SkyLayer
|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the texture used by this layer.|
|InFront|Boolean|Presumably determines whether this layer is always rendered over other layers (including non-sky background layers).|
|Opacity|Float|Opacity of the layer.|
|FogTint|Float|How much (0.0 to 1.0) this layer is tinted by the fog color.|

# FEZSKY format

## TODO

- When creating or adjusting a [Sky](#sky), all textures used for the sky must be placed in an adjacent folder with the same name as the sky.
- If Stars is set for a sky, and the level is not rainy nor named `TELESCOPE` or `TREE`, shooting stars will rarely appear in the sky at night

### Sky
|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the sky used internally by the game.|
|Background|String|Name of the background texture used by the sky.|
|WindSpeed|Float|Determines speed of clouds, as well as background layers affected by wind.|
|Density|Float|Determines quantity and density of clouds. (Unused? - set to 1 in every sky)|
|FogDensity|Float|(Changes fog effect - exact behavior unknown)|
|Layers|[SkyLayer](#skyLayer)[]|A list of parallax layers to use in the sky.|
|Clouds|String[]|List of names of cloud textures.|
|Shadows|String|Name of shadow texture to project onto the level (and sky layers, if `FoliageShadows` is enabled).|
|Stars|String|Name of stars texture - blended with other sky layers (need more research)|
|CloudTint|String|Name of file to use as a reference for cloud colors?|
|VerticalTiling|Boolean||
|HorizontalScrolling|Boolean||
|LayerBaseHeight|Float||
|InterLayerVerticalDistance|Float||
|InterLayerHorizontalDistance|Float||
|HorizontalDistance|Float||
|VerticalDistance|Float||
|LayerBaseSpacing|Float||
|WindParallax|Float||
|WindDistance|Float||
|CloudsParallax|Float||
|ShadowOpacity|Float||
|FoliageShadows|Boolean|Causes sky shadows to be drawn over sky layers as well as the level.|
|NoPerFaceLayerXOffset|Boolean||
|LayerBaseXOffset|Float||

### SkyLayer
|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the texture used by this layer.|
|InFront|Boolean|Presumably determines whether this layer is always rendered over other layers (including non-sky background layers).|
|Opacity|Float|Opacity of the layer.|
|FogTint|Float|How much (0.0 to 1.0) this layer is tinted by the fog color.|

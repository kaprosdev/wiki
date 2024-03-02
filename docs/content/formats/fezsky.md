# FEZSKY format

## TODO

- When creating or adjusting a [Sky](#sky), all textures used for the sky must be placed in an adjacent folder with the same name as the sky.
- The `Background` texture is not drawn in full to the sky - over the course of the day, the sky's color is interpolated over the width of the texture.
- `Stars` are only visible:
  - if the level is rainy;
  - if the sky is `PYRAMID_SKY` or `ABOVE`;
  - or if it is night (opacity determined by how far into/out of night it currently is).
    - For `OBS_SKY` specifically, the stars opacity is 0.25 at minimum but otherwise scales linearly to 1 over the night.
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
|Background|String|Name of a background texture used for the sky color. (Game interpolates each pixel column as evenly-spaced keyframes between midnights?)|
|WindSpeed|Float|Determines speed of clouds.|
|Density|Float|Determines quantity and density of clouds. (Unused? - set to 1 in every sky)|
|FogDensity|Float|Determines how much the current day/night|
|Layers|[SkyLayer](#skylayer)[]|A list of parallax layers to use in the sky.|
|Clouds|String[]|List of names of individual cloud textures.|
|Shadows|String|Name of shadow texture to project onto the level.|
|Stars|String|Name of stars texture.|
|CloudTint|String|Name of file to use as a reference(? what kind) for cloud colors|
|VerticalTiling|Boolean|If true, the sky loops vertically (including layers).|
|HorizontalScrolling|Boolean|If true, non-cloud layers move based on `WindSpeed`, `WindDistance`, and `WindParallax`.|
|LayerBaseHeight|Float|How high (0.0-1.0) the bottom of the first layer is placed in the sky.|
|InterLayerVerticalDistance|Float|Vertical parallax factor between layers.|
|InterLayerHorizontalDistance|Float|Horizontal parallax factor between layers.|
|HorizontalDistance|Float|Horizontal scroll speed of all sky layers (before parallax).|
|VerticalDistance|Float|Vertical scroll speed of all sky layers (before parallax).|
|LayerBaseSpacing|Float|How much vertical distance to place between sky layers. Can be negative.|
|WindParallax|Float|Wind parallax factor between layers (only if `HorizontalScrolling` is enabled and `WindSpeed` is not 0).|
|WindDistance|Float|Wind speed multiplier for all sky layers (only if `HorizontalScrolling` is enabled and `WindSpeed` is not 0).|
|CloudsParallax|Float|(Parallax factor for clouds? Can't nail this one down)|
|ShadowOpacity|Float|Determines opacity of `Shadows` over the level.|
|FoliageShadows|Boolean|If true, `Shadows` will be layered multiple times with differing offsets in multiple directions. (See the level `TREE`)|
|NoPerFaceLayerXOffset|Boolean|If enabled, layers will not be offset differently on different sides of the level.|
|LayerBaseXOffset|Float|Starting horizontal offset for sky layers. (usually used to prevent grid skies from aligning too well from the level origin?)|

### SkyLayer
|Property name|Type|Description|
|-|-|-|
|Name|String|Name of a texture used by this layer.|
|InFront|Boolean|If true, this layer is rendered over everything else (including the level).|
|Opacity|Float|Opacity of this layer.|
|FogTint|Float|Influence that fog color has on the color of this layer.|

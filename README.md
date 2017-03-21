# Real Landscape Synthesis for UE4
Landscape synthesis from landcover maps generated by the [LCC.net](https://github.com/bneukom/LCC.net) tool and heightmodels. To automatically synthesise real landscape we use use low resultion globally and freely available satellite imagery and heightmodels combined with machine learning. <b>Note</b> that "Download ZIP" does not work for this project as the sample scene is stored using GIT LFS. 

# Sample Scene
The project contains a sample scene (<i>Sentinel_32TLS_20160823</i>) with generated landcover maps from the Swiss Alps. Following a screenshot of this scene:

![valley2](http://i.imgur.com/o2mMmSl.jpg)

More screenshots are at the bottom of this readme. By using the generated landcover maps we can drastically improve the visualization as with only using the low resolution satellite imagery as shown in the following screenshot:

![comp](http://i.imgur.com/V7X0LfG.jpg)

# Landscape Material
The landscape material supports tree and grass placement using the landcover maps. Different models for the trees or grass can be added if desired. The models used for the sample scene are from the Unreal Kite demo. The landcover types use geotypical textures which are blended together and can optionally also be blended partially with the satellite imagery to achieve higher fidelity. The blending parameters can be changed in the material instance.

# Workflow
To generate new scenes the steps described in the LCC.net [readme](https://github.com/bneukom/LCC.net) must be followed first. After following these steps we should have landcover maps for earch desired landcover type as well as a heightmap. First we import the heightmap into the Unreal Engine and set the material to an instance of <i>MAT_Landscape</i>. Note that the landscape has to be scaled according to the resoltution of the heightmap. GDEM v2 has a spatial resolution of 30 meters and therfore our landscape should have scale factor of 3000 for the x and y coordinates. The z scale must be calculated using the difference of the minimum altitude and maximum altitude of the heightmap divided by 512 as described [here](https://wiki.unrealengine.com/World_Machine_to_Unreal_Engine_4_-_In_Depth_Guide).

The default material supports grass, rock, gravel, snow, water, tree, agriculture and builtup land cover types. If other landcover maps were generated using the [LCC.net](https://github.com/bneukom/LCC.net) tool, the material has to be adapted accordingly. The landcovermaps can then be imported using the "Landscape Paint Tool" using the "Import from File" menu.

<p align="center">
   <img src="http://i.imgur.com/ZXjcerH.png" alt="landscape import" height="400"/>
   <img src="http://i.imgur.com/Zyu5MFL.jpg" alt="landscape import heightmap" height="400"/>
</p>

# Landscape Grass Bug
Due to the large scale factor of the landscape, the grass tool seems to spawn grass at wrong locations (UE4.14). I have posted a simple fix to the LandscapeGrass.cpp class (the Engine needs to be cloned and rebuilt as described on the UnrealEngine Github page) in an official forum [thread](https://answers.unrealengine.com/questions/535737/grass-tool-spawns-below-landscape.html).

# Future Work
* Add support for 3D building models using the [StreetMap Plugin](https://github.com/ue4plugins/StreetMap)
* Add the classification algorithms from LCC.net directly into UE4 as a plugin
* Add more grass nodes for clutter such as rocks and gravel

# Sample Scene Screenshots
Note that the scene was not modified by hand, everything is generated automatically.

![lake](http://i.imgur.com/NfWtd7T.jpg)

![valley](http://i.imgur.com/me6KWro.jpg)

![field](http://i.imgur.com/WYsyBrb.jpg)

![snow](http://i.imgur.com/rVHfkxn.jpg)

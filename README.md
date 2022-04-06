## Foot Traffic Analysis Tool


![FootTrafficSmallest](https://user-images.githubusercontent.com/69476462/161852711-5b2ed707-fe72-4132-a269-1d479ab4b3da.gif)


###### Animation showing the generated analysis meshes of a procedurally generated urban model.


### Description

This tool analyzes the most common routes from local residences to user designated destinations (i.e. metro stations, key institutions, shopping centers, etc.) within a given analysis area.  The tool quantifies how many times each stretch of road is used to reach each given destination and displays these results on screen.  An optional functionality within the tool allows the user to allocate additional built stock alongside the streets that have the most traffic.  This generative approach is designed to facilitate efficiently placed commercial zoning development where pedestrian activity is the highest (and thus most lucrative.)

### How To Use 
#### Inputs

1. **Crv: Analysis Area** > Input from one referenced closed polygon curve that encloses the analysis area
2. **Crv: Street Center Lines** > Input from referenced open curve(s) that show the center line of street(s) that cross through the analysis area.
3. **Srf: Streets** > Input directly from 'Streets' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script).
4. **Num: Center Road Offset** > Input the width of streets within the analysis area.  You may directly connect the values from the 'Street Size' panel (in the provided class grasshopper script) or connect a slider.
5. **Srf: Blocks** > Input directly from 'Blocks' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script). 
6. **Brep: Residential Buildings** > Input directly from 'Buildings' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script).  
7. **Pt: Destination 1** > Right click the connected pt node and choose a point in rhino to reference.
8. **Pt: Destination 2** (optional) > Right click the connected pt node and choose a point in rhino to reference.  You may choose to leave this node unreferenced.  Adding multiple destination points after the first will increase computation time.
9. **Pt: Destination 3** (optional) > Right click the connected pt node and choose a point in rhino to reference.  You may choose to leave this node unreferenced.  Adding multiple destination points after the first will increase computation time.
10.  **Num: Population** > Set one value on the attached slider.  The recommended default value is 1000 for an analysis area consisting of 50-200 buildings. The script uses this value to distribute origin points throughout the analysis area which are used in conjunction with the user defined destination points and street network in the analysis area to generate a shortest walk analysis. Input 6: Residential Buildings is used to allocate a proportionate amount of the population .  It is recommended that you raise this value if you anticipate the total amount of buildings in the analysis to be above 200.  Conversely, you may lower the value to substantially decrease computation time if the 
11. **Num: Population Threshold for 'High Traffic'** > Set one value on the attached slider.  This value determines when a street that which X amount of foot traffic en route to a user defined destination may considered 'Highly Trafficked'.  This threshold is transfered to the generative commercial building portion of the script to determine where to build.  In other words, a LOWER threshold will yield MORE commercial generation, and vice versa.  This value also is used to calculate the percentage of street lengths within the analysis area that see 'High Traffic', which is output for use in Scout.  Please note: adding destination points after the first means the same street network within the analysis area are analyzed multiple times.  The number of uses on a given road from each simulation after the first are overlaid on top of each other
12. **Num: Analysis Color Sensitivity Upper Bound**
13. **Num: New Commercial Building Offset Divisor**
14. **Num: New Commercial Building Height Divisor**
15. Right click on "Context" -> Select Multiple and select building obstructions.
16. Right click on "Ground" -> Select Multiple and select ground.
17. Right click on "Ground" -> Select Multiple and select the massing(s) you want to test.
18. Adjust Threshold X,Y,Z
19. Review visual and metric outputs. Does it look correct? Does something look wrong? Common issues below.

![description](../images/grasshopper_tree.jpg)


#### Troubleshooting

Make sure to properly load the context as it is crucial for to test visibility quality

If you don't already have the Visibility Quality Tool, please add to your library for easy usage.

<!--add a list your downloadable links below with "link " appended to the beginning. You should have sample rhino + grasshopper files and a legend-->


#### Required Files

[Rhino File](https://github.com/XIM-GSAPP/XIM-GSAPP-Fa20/raw/main/src/files/Analysis%20Tool%20Example.3dm)

[Grasshopper File](https://github.com/XIM-GSAPP/XIM-GSAPP-Fa20/raw/main/src/files/Analysis%20Tool%20Example.gh)


![description](../images/tool_example_4.jpg)


<br />

<!-- ![description of image](/XIM-GSAPP-Fa20/images/tool_example_4_.jpg) -->

### Modeling Standards
<!--Revise for specific modeling requirements for you analysis to run properly. If useful, add an image of properly vs improperly model geometry-->
<b>Please follow the following Rhino standards to ensure the proper functionality of the tool: </b>


<input type="checkbox"> <b>My test massing is a single, simplified, CLOSED polysurface.</b>

  <li>Try "SelClosedSrf" to make sure it is closed.</li>

<input type="checkbox"> <b>My model is oriented to True North.</b>

  <li>Re-orient if it was rotated off of North at the start of the project.</li>

<input type="checkbox"> <b>Any groups or blocks in the model have been ungrouped/exploded.</b>

  <li>Try "SelBlockInstance" and "SelGroup" to make sure.</li>

<input type="checkbox"> <b>My model is set to either Meters or Feet (not mm or in).</b><br>

<input type="checkbox"> <b>My model is free of overlapping, coplanar, or intersecting geometry.</b><br>

<input type="checkbox"> <b>Any obstructions around the space have been modeled (trees, topography, buildings).</b><br>

<input type="checkbox"> <b>Any curved surfaces in the model have been simplified to individual flat planes.</b><br>

<input type="checkbox"> <b>Any surrounding context has been made into a single, joined mesh.</b>

### Sources, Calculations + Metrics
<!--add text and/or images for any sources for you metrics, calculations & equations, assumptions and specific metric output-->

<p>This tool uses this method of calculating X from this source. The metric is derived in this manner. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>


### Limitations & Context
<!--add text and/or images that expose potential for bias by stating limitations (ie what does this tool not do,) and the context in which it was created.-->

This tool does X it does not do Z and Y. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

### Examples
<!--add images and text to describe a use case below-->

Here is how we used this tool on a project! Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.



Some more text here perhaps.

<b> More project examples here: </b>

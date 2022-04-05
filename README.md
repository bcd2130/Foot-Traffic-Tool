## Foot Traffic Analysis Tool


![FootTrafficSmallest](https://user-images.githubusercontent.com/69476462/161852711-5b2ed707-fe72-4132-a269-1d479ab4b3da.gif)


###### Animation showing the generated analysis meshes of a procedurally generated urban model.


### Description

This tool analyzes the most common routes from local residences to user designated destinations (i.e. metro stations, key institutions, shopping centers, etc.)  The tool quantifies how many times each stretch of road is used to reach each given destination and displays these results on screen.  An optional functionality within the tool allows the user to allocate additional built stock alongside the streets that have the most traffic.  This generative approach is designed to facilitate efficiently placed commercial zoning development where pedestrian activity is the highest (and thus most lucrative.)

### How To Use 
#### Inputs

1. Crv: Analysis Area > Select the closed polygon that encloses the analysis area
2. Crv: Street Center Lines > Select open curves in Rhino that are the center of streets within analysis area
3. Srf: Streets > Input directly from 'Streets' output in 'Blocks and Parcels' cluster 
4. Num: Center Road Offset > Input the width of streets within the analysis area
5. Srf: Blocks
6. Brep: Residential Buildings
7. Pt: Destination 1
8. Pt: Destination 2 (optional)
9. Pt: Destination 3 (optional)
10. Num: Population Threshold for 'High Traffic'
11. Num: Analysis Color Sensitivity Upper Bound
12. Num: New Commercial Building Offset Divisor
13. Num: New Commercial Building Height Divisor
14. Right click on "Context" -> Select Multiple and select building obstructions.
15. Right click on "Ground" -> Select Multiple and select ground.
16. Right click on "Ground" -> Select Multiple and select the massing(s) you want to test.
17. Adjust Threshold X,Y,Z
18. Review visual and metric outputs. Does it look correct? Does something look wrong? Common issues below.

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

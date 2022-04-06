# Foot Traffic Analysis Tool


![FootTrafficSmallest](https://user-images.githubusercontent.com/69476462/161852711-5b2ed707-fe72-4132-a269-1d479ab4b3da.gif)


###### Animation showing the generated analysis meshes of a procedurally generated urban model.


## 1. Description

This tool analyzes the most common, shortest routes from local residences to user designated destinations (i.e. metro stations, key institutions, etc.) within a given analysis area.  The tool quantifies how many times each stretch of road is used to reach each given destination and displays these results on screen.  An added functionality within the tool allows the user to allocate additional built stock alongside streets that see the most foot traffic.  This generative approach is designed to facilitate efficiently allocated commercial zoning and development where the highest projected pedestrian activity exists.

## 2. How To Use 
### Inputs: Basic Design Space

1. **Crv: Analysis Area** > Input from one referenced closed polygon curve.
2. **Crv: Street Center Lines** > Input from referenced open curve(s) that show the center line of street(s) that cross through the analysis area.
3. **Srf: Streets** > Input directly from 'Streets' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script).
4. **Num: Center Road Offset** > Input the width of streets within the analysis area.  You may directly connect the values from the 'Street Size' panel (in the provided class grasshopper script).
5. **Srf: Blocks** > Input directly from 'Blocks' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script). 
6. **Brep: Residential Buildings** > Input directly from 'Buildings' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script).

### Inputs: Cluster Controls

7. **Pt: Destination 1** > Right click the connected pt node and choose a point in rhino to reference.
8. **Pt: Destination 2** (optional) > Right click the connected pt node and choose a point in rhino to reference.  You may choose to leave this node unreferenced.
9. **Pt: Destination 3** (optional) > Right click the connected pt node and choose a point in rhino to reference.  You may choose to leave this node unreferenced.
10.  **Num: Population** > Set one value on the attached slider.
11. **Num: Threshold** > Set one value on the attached slider.
12. **Num: Color Sensitivity** > Set one value on the attached slider.
13. **Num: Offset Divisor** > Set one value on the attached slider.
14. **Num: Height Divisor** > Set one value on the attached slider.

![description](../images/grasshopper_tree.jpg)


## 3. Troubleshooting

1. Destination points may be placed anywhere on the world XY plane, inside or outside the analysis area.  However, if do not place a destination point on an existing street (Input 2), the script will connect automatically connect it to your street network with the shortest straight line possible.  Ensure that that line ends at an existing street end point.
2. All input numbers must be positive.  See


## 4. Required Files

[Rhino File](https://github.com/XIM-GSAPP/XIM-GSAPP-Fa20/raw/main/src/files/Analysis%20Tool%20Example.3dm)

[Grasshopper File](https://github.com/XIM-GSAPP/XIM-GSAPP-Fa20/raw/main/src/files/Analysis%20Tool%20Example.gh)


![description](../images/tool_example_4.jpg)


<br />

<!-- ![description of image](/XIM-GSAPP-Fa20/images/tool_example_4_.jpg) -->

## 5. Modeling Standards and *Detailed Explanation of What is Happening Under the Hood*

1. **Crv: Analysis Area** > Curve must be closed.  Curve must encloses the analysis area (street curves do not exist outside it).  
- *Used as a pathway for shortest walk simulations.*
2. **Crv: Street Center Lines** > Curve(s) must be open.  
- *Used as pathways for shortest walk simulations.*
3. **Srf: Streets** > Surfaces (not closed), trimmed or not.  
- *Used to refine generated commercial building geometry that extends beyond blocks into the street.*
4. **Num: Center Road Offset** > You must input exactly one positive number.  All numbers less than or equal to 0 are ignored. 
- *Used to keep shortest walk simulations in the center of roads.*
5. **Srf: Blocks** > Surfaces (not closed), trimmed or not. 
- *Used to find where commercial structures can be added.*
6. **Brep: Residential Buildings** > Closed breps only. One brep per parcel only - you must solid union breps together before connecting to this input.
- *Used for population allocation in shortest walk simulations.*
7. **Pt: Destination 1** > One referenced point only. 
- *Used as an origin point for the shortest walk simulation*
8. **Pt: Destination 2** (optional) > One referenced point only.  You may choose to leave this node unreferenced.  Adding multiple destination points after the first will increase computation time.
- *Used as an origin point for the shortest walk simulation*
9. **Pt: Destination 3** (optional) > One referenced point only.  You may choose to leave this node unreferenced.  Adding multiple destination points after the first will increase computation time.
- *Used as an origin point for the shortest walk simulation*
10.  **Num: Population** One number only.
- *The recommended default value is 1000 for an analysis area consisting of 50-200 buildings (see: Input 6 - Brep: Residential Buildings). The script uses this value to distribute origin points throughout the analysis area which are connected to the user defined destination points to compute the shortest walk analysis.  Residential building inputs are categorized by size and attributed a proportionate amount of the population based on their size.  If the total amount of buildings in the analysis area is high (over 200) the population may not be easily divisible among residential buildings because the population per building is always rounded up to the closest integer (to keep at least one resident per residential building).  This will negatively impact the fidelity of the analysis as smaller buildings 'steal' population from larger buildings.  In this case it is wise to increase population.  Conversely, you may lower the population value if the total number of buildings is low (less than 50).  This will reduce overall computation time.
11. **Num: Threshold** > One number only.
- *This value determines when a street that sees X amount of foot traffic en route to a user defined destination may considered 'highly trafficked'.  This threshold is transfered to the generative portion of the script to determine where to place commerical buildings:  a LOWER threshold will yield MORE commercial generation, and vice versa.  This value also is used to calculate the percentage of streets within the analysis area that see 'high traffic', which can be used as a metric in Scout (see: Outputs).  Please note: adding destination points after the first means the same streets network within the analysis area are analyzed multiple times.  The results of these simulations are combined, meaning this threshold should be raised if Input 10 increases or Input 8 and/or Input 9 are used.*
12. **Num: Color Sensitivity** > One number only.
- *This value determines the upper bound of the analysis display.  You may set this value to be identical to Input 11 - Num: Threshold by default.  The ability to set this value seperately to Input 11 - Num: Threshold has been added to this script to allow users to retain creative agency of the color display for the analysis in Grasshopper/Scout while choosing a seperate value that determines the threshold whereby added commercial building generation takes place.*
13. **Num: Offset Divisor** > One number only.
- *Each street segment that passes the 'highly trafficked' threshold (Input 12) is attributed a value equal to the number of people that use that street segment in the shortest walk simulation.  Commercial buildings alongside those street segments are generated automatically and their horizontal footprint (offset from the street) can be controlled using this slider.  A higher value will reduce the building footprint, and vice versa.*
14. **Num: Height Divisor** > One number only.
- *Each street segment that passes the 'highly trafficked' threshold (Input 12) is attributed a value equal to the number of people that use that street segment in the shortest walk simulation.  Commercial buildings alongside those street segments are generated automatically and their vertical footprint can be controlled using this slider.  A higher value will reduce the building height, and vice versa.*

**General Notes**
A. For inputs 1-6, use the provided design space geometry clusters.
B. Curve and surface inputs must be planar and projected (paralell to the XY plane).
C. All input geometry must be and located on world XY plane.  3D geometry bases must be placed on the world XY plane (no geometry floating in the air).
D. Recommended model unit: feet.


## 6. Sources, Calculations + Metrics
<!--add text and/or images for any sources for you metrics, calculations & equations, assumptions and specific metric output-->

<p>This tool uses this method of calculating X from this source. The metric is derived in this manner. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>


## 7. Limitations & Context
<!--add text and/or images that expose potential for bias by stating limitations (ie what does this tool not do,) and the context in which it was created.-->

This tool does X it does not do Z and Y. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

## 8. Examples
<!--add images and text to describe a use case below-->

Here is how we used this tool on a project! Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.



Some more text here perhaps.

<b> More project examples here: </b>

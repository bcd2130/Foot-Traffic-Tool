# Foot Traffic Analysis Tool


![FootTrafficSmallest](https://user-images.githubusercontent.com/69476462/161852711-5b2ed707-fe72-4132-a269-1d479ab4b3da.gif)


###### Animation showing an analysis of a procedurally generated urban model.


## 1. Description

This tool analyzes the most common, shortest routes from local residences to user designated destinations (i.e. metro stations, key institutions, etc.) within a given analysis area.  The tool quantifies how many times each stretch of road is used to reach each given destination and displays these results on screen.  An added functionality within the tool allows the user to allocate additional built stock alongside streets that see the most foot traffic.  This generative approach is designed to facilitate efficiently allocated commercial zoning and development where the highest projected pedestrian activity exists.

![Combined 1](https://user-images.githubusercontent.com/69476462/162016904-a0773f33-ed0d-4725-8bb8-179fadc876a9.png)
###### Left: The tool performing an analysis of a residential buildings (white) within an urban context by color coding the most commonly used nearby streets in red and least in blue.
###### Right: Procedurally generated commercial buildings (blue-grey) can be automatically added to the urban model alongside the most used streets where pedestrian audiences are most likely to be found using the Foot Traffic Analysis Tool.

## 2. How To Use 
### Inputs

1. **Crv: Analysis Area** > Input from one referenced closed polygon curve.
2. **Crv: Street Center Lines** > Input from referenced open curve(s) that show the centerline of street(s) that cross through the analysis area.
3. **Srf: Streets** > Input directly from 'Streets' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script).
4. **Num: Center Road Offset** > Input the width of streets within the analysis area.  You may directly connect the values from the 'Street Size' panel (in the provided class grasshopper script).
5. **Srf: Blocks** > Input directly from 'Blocks' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script). 
6. **Brep: Residential Buildings** > Input directly from 'Buildings' output in *'Blocks and Parcels'* cluster (in the provided class grasshopper script).
7. **Pt: Destination 1** > Right click the connected pt node and choose a point in rhino to reference.
8. **Pt: Destination 2** (optional) > Right click the connected pt node and choose a point in rhino to reference.  You may choose to leave this node unreferenced.
9. **Pt: Destination 3** (optional) > Right click the connected pt node and choose a point in rhino to reference.  You may choose to leave this node unreferenced.
10.  **Num: Population** > Set one value on the attached slider.
11. **Num: Threshold** > Set one value on the attached slider.
12. **Num: Color Sensitivity** > Set one value on the attached slider.
13. **Num: Offset Divisor** > Set one value on the attached slider.
14. **Num: Height Divisor** > Set one value on the attached slider.

### Outputs

1. **Num: PPSS Above Threshold Only** > Displays the number of 'People per Street Segment' above the user defined threshold (Input 11) for the **Rhino** visualization.
2. **Col: Analysis Color** > Display colors of the overlaid analysis mesh for the **Rhino** visualization.  (Defined by Input 12.)
3. **Pt: Text Display Point** > Provides a location to add a text readout for the **Rhino** visualization.  Displays values above the upper bounds analysis only (Input 12).
4. **Brep: Analysis Extrusions (Scout)** > Analysis overlay geometry for **Scout** and/or **Rhino**.  Connect to the corresponding 'Analysis Geometry" group in Part 11 of the **Scout** pipeline.
5. **Num: PPSS** > 'People per Street Segment', from the analysis of shortest walk(s) from origin points to destination(s).  Connect to the corresponding 'Analysis Geometry" group in Part 11 of the **Scout** pipeline. 
6. **Num: % Above Threshold (Scout)** > Displays the proportion of all streets that exceed the threshold (Input 11).  These street segments are categorized as having 'high traffic' and used in scout as a metric to understand how concentrated or dispersed movement is within the analysis area.  Connect to the corresponding node in 'Outputs for Data.csv' in Part 3 of the **Scout** Pipeline.
7. **Brep: New Commercial Buildings** > Generates geometry based on the Foot Traffic Analysis results.  Read 10, 11, 13 and 14 in Section 5 for more information.  You may add this procedurally generated geometry to your residential buildings for further analysis (of the combined result) in **Rhino**.  Connect these massings to the "Blank Geometry' group in Part 13 of the **Scout** Pipeline.

![Canvas](https://user-images.githubusercontent.com/69476462/162018597-6dcce408-c84e-4a55-afeb-e02c651c3e5d.png)
###### An entire working example of the tool in action is provided below (Section 4).  Pictured here from left to right: group 1: residential urban context generator, group 2: The Foot Traffic Analysis Tool and its controls, group 3: visualizations.

![Canvaszoom](https://user-images.githubusercontent.com/69476462/162019466-4e7cdbf2-03c9-4abb-870a-ff65e8b17183.png)
###### A zoomed in view of the inputs and output of the Foot Traffic Analysis Tool as discussed in depth in this section.

## 3. Troubleshooting

1. Destination points may be placed anywhere on the world XY plane, inside or outside the analysis area.  However, if you do not place a destination point on an existing street (Input 2), the script will automatically connect it to your street network with the shortest straight line possible.  Ensure that that line ends at an existing street end point.
2. All input numbers must be positive.  See Section 5 for details.


## 4. Required Files

[Rhino File (Google Drive)](https://drive.google.com/file/d/1Dl6bLP5LsK59_b2Z96hwKzbD1wWGi-fn/view?usp=sharing)

[Grasshopper File (Github)](https://github.com/bcd2130/Foot-Traffic-Tool/blob/main/Foot%20Traffic%20Analysis%20Tool.gh)


## 5. Modeling Standards and *Detailed Explanation of What is Happening Under the Hood*

1. **Crv: Analysis Area** > Curve must be closed.  Curve must enclose the analysis area (street curves do not exist outside it).  
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
- *The recommended default value is 1000 for an analysis area consisting of 50-200 buildings (see: Input 6 - Brep: Residential Buildings). The script uses this value to distribute origin points throughout the analysis area which are connected to the user defined destination points to compute the shortest walk analysis.  Residential building inputs are categorized by size and attributed a proportionate amount of the population based on their size.  If the total number of buildings in the analysis area is high (over 200) the population may not be easily divisible among residential buildings because the population per building is always rounded up to the closest integer (to keep at least one resident per residential building).  This will negatively impact the fidelity of the analysis as smaller buildings 'steal' population from larger buildings.  In this case it is wise to increase population.  Conversely, you may lower the population value if the total number of buildings is low (less than 50).  This will reduce overall computation time.*
11. **Num: Threshold** > One number only.
- *This value determines when a street that sees X amount of foot traffic en route to a user defined destination may be considered 'highly trafficked'.  This threshold is transferred to the generative portion of the script to determine where to place commercial buildings:  a LOWER threshold will yield MORE commercial generation, and vice versa.  This value also is used to calculate the percentage of streets within the analysis area that see 'high traffic', which can be used as a metric in Scout (see: Outputs).  Please note: adding destination points after the first means the same streets network within the analysis area are analyzed multiple times.  The results of these simulations are combined, meaning this threshold should be raised if Input 10 increases or Input 8 and/or Input 9 are used.*
12. **Num: Color Sensitivity** > One number only.
- *This value determines the upper bound of the analysis display.  You may set this value to be identical to Input 11 - Num: Threshold by default.  The ability to set this value separately to Input 11 - Num: Threshold has been added to this script to allow users to retain creative agency of the color display for the analysis in Grasshopper/Scout while choosing a seperate value that determines the threshold whereby added commercial building generation takes place.*
13. **Num: Offset Divisor** > One number only.
- *Each street segment that passes the 'highly trafficked' threshold (Input 12) is assigned a value equal to the number of people that use that street segment in the shortest walk simulation.  Commercial buildings alongside those street segments are generated automatically and their horizontal footprint (offset from the street) can be controlled using this slider.  A higher value will reduce the building footprint, and vice versa.*
14. **Num: Height Divisor** > One number only.
- *Each street segment that passes the 'highly trafficked' threshold (Input 12) is assigned a value equal to the number of people that use that street segment in the shortest walk simulation.  Commercial buildings alongside those street segments are generated automatically and their vertical footprint can be controlled using this slider.  A higher value will reduce the building height, and vice versa.*

![Threshold-Animation](https://user-images.githubusercontent.com/69476462/162023744-144ad04a-ff12-489e-b24f-450532128b30.gif)
###### An animation showing how raising the threshold value (Input 11) limits where commercial building generation occurs.

**General Notes**

A. For inputs 1-6, it is recommended that you use the provided design space geometry clusters.

B. Curve and surface inputs must be planar and projected (parallel to the XY plane).

C. All input geometry must be located on the world XY plane.  3D geometry bases must be placed on the world XY plane (no geometry floating in the air).

D. Recommended model units: feet.


## 6. Metrics
The Foot Traffic Analysis Tool counts the total number of times a segment of street is used to arrive at a user selected destination and displays these data as colored extrusions for use in scout.  The user may define a threshold (Input 11) for the total number of times a segment of street is used, above which, segments of street are defined as having 'high traffic'.  These segments are measured in linear feet and divided by the total length of all segments of street within the analysis area.  The resulting number is represented as a percentage.  This Percentage of Streets with High Traffic gives users insight as to how concentrated or dispersed movement is to streets within the analysis area.  If the percentage is low, this indicates highly congested pathways.  A higher value indicates that more streets within the analysis area are useful movement axes.  Either option could be desirable depending on the intention of the designer.  High concentration yields more effective, targeted intervention areas and allows less building density which in turn makes parcels available for other uses, such as greenspace.  However this outcome means high congestion in certain spots within the analysis area.  Conversely, a high percentage means more streets have population routing that exceeds the threshold, which in turn requires more land to be used to capture commercial activity but also less overall congestion.


## 7. Limitations & Context
This tool is intended to be used in conjunction with outputs made by other grasshopper clusters that together generate urban design iterations [see: X Information Modeling Spring 2022 (XIM S2022)].  You may alter or replace these expected geometry generators as you see fit, however, you should make sure the geometry types and data structures they make are replicated.  Some functionalities have been added to the geometry generators from XIM S2022 (see *'Air Rights Modification'* cluster) and some functionalities have been stripped from it (multiple street options are no longer included).  Reintroducing multiple street options (or adding design space options) into the iteration pool may require the user to change some aspects of the Foot Traffic Tool.  To help in this regard relevant design space generators from XIM S2022 are included with the analysis tool so that the user can more easily alter the design space with a working geometry generator for reference first.

## 8. Examples

![ezgif-4-dc6d0e5414](https://user-images.githubusercontent.com/69476462/162081474-c07ef663-2876-4ad7-95c3-0d956c21f782.gif)
###### An animation showing a range of residential geometry options complimented by the Foot Traffic Analysis Tool's procedurally generated commercial building allocations.

![ViewCapture20220406_124512](https://user-images.githubusercontent.com/69476462/162025744-14db4e71-03d8-4b12-b059-90b0fb39298c.png)
###### Alternative visualization option shows the most used streets as colored pipes rather than extruded surfaces.





# Foot-Traffic-Tool

Visibility Quality Tool
description

Description
This is a basic description of the tool that is simple enough that for anyone to understand what the tool does and why someone would use it. Keep it to 3 sentences or less.

How To Use
Step by Step Instructions:

Link to epw file
Link to epw file`
Right click on "Context" -> Select Multiple and select building obstructions.
Right click on "Ground" -> Select Multiple and select ground.
Right click on "Ground" -> Select Multiple and select the massing(s) you want to test.
Adjust Threshold X,Y,Z
Review visual and metric outputs. Does it look correct? Does something look wrong? Common issues below.
description

Troubleshooting
Make sure to properly load the context as it is crucial for to test visibility quality

If you don't already have the Visibility Quality Tool, please add to your library for easy usage.

Required Files
Rhino File

Grasshopper File

description


Modeling Standards
Please follow the following Rhino standards to ensure the proper functionality of the tool:

My test massing is a single, simplified, CLOSED polysurface.

Try "SelClosedSrf" to make sure it is closed.
My model is oriented to True North.

Re-orient if it was rotated off of North at the start of the project.
Any groups or blocks in the model have been ungrouped/exploded.

Try "SelBlockInstance" and "SelGroup" to make sure.
My model is set to either Meters or Feet (not mm or in).

My model is free of overlapping, coplanar, or intersecting geometry.

Any obstructions around the space have been modeled (trees, topography, buildings).

Any curved surfaces in the model have been simplified to individual flat planes.

Any surrounding context has been made into a single, joined mesh.

Sources, Calculations + Metrics
This tool uses this method of calculating X from this source. The metric is derived in this manner. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

Limitations & Context
This tool does X it does not do Z and Y. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

Examples
Here is how we used this tool on a project! Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

Some more text here perhaps.

More project examples here:

---
layout: page
title: Frequently Asked Questions
permalink: /faq/
---




How do I install WindNinja?
---------------------------
***


**Windows**: Download the installer from [firelab.org](http://www.firelab.org/windninja) and save it to your computer.  Then, double-click on the installer in this saved location.  Follow the installation instructions in the window that opens.  Once installed, use the Start menu to start WindNinja.

**Linux**: Follow the instructions on [building from source](https://github.com/firelab/windninja/wiki/Building-WindNinja-on-Linux).




<br>
<br>
<br>





Where can documentation about running WindNinja be found?
---------------------------------------------------------
***


[Tutorials can be found online here.](http://firelab.github.io/windninja/main/2016/07/26/tutorial.html)

Much of the available documentation is included in the WindNinja installation.  To find this, first install WindNinja.  Next, go to Start->Programs->WindNinja-x.x.x.  Here you will find links to the included documentation, which includes tutorials, elevation file download instructions, wind vector viewing instructions, and example elevation files.


Another place to find WindNinja documentation is on WindNinja's distribution web site:  http://www.firelab.org/windninja


<br>
<br>
<br>


What is the difference between WindNinja and WindWizard?
--------------------------------------------------------
***

[WindWizard](http://www.firelab.org/project/windwizard) is no longer available. There is now an optional conservation of mass and momentum solver in WindNinja which replaces the functionality of WindWizard.

The physics in the WindWizard solver were based on proprietary software that required users to purchase a license. Because this severely hampered usability, WindWizard is no longer available. Instead, WindNinja has been upgraded to include the advanced physics previously included in WindWizard, but without the licensing fees. As of version 3.0, WindNinja includes an optional momentum solver that replaces the functionality of WindWizard. There are now two options for the solver (the number-crunching part of WindNinja): 1) conservation of mass and 2) conservation of mass and momentum. The conservation of mass option is the native, fast-running solver used in previous versions of WindNinja. The conservation of mass and momentum option is a new solver based on the OpenFOAM toolkit. OpenFOAM is free, open-source software for computational fluid dynamics (CFD) from the OpenFOAM Foundation: http://openfoam.org.

The major differences, from a user’s perspective, between the two solvers are:

<br>

* The conservation of mass solver runs much faster than the conservation of mass and momentum solver (less than a minute for conservation of mass compared to about 1 hour for conservation of mass and momentum).

* The conservation of mass solver's approximation of the momentum equation is simpler and, at times, less accurate than that of the conservation of mass and momentum solver. This is mainly why the conservation of mass solver runs so much faster than the conservation of mass and momentum.

* The conservation of mass simulations are normally less accurate during stronger winds on the lee sides of ridges and mountains where re-circulation eddies can occur.

* The conservation of mass solver incorporates some non-neutral atmospheric stability effects, while the conservation of mass and momentum is only valid under near-neutral stability.

* WindNinja has a feature that allows users to enter measured wind information at several locations to drive the flow. WindNinja will produce a wind field that matches the winds as these locations. This feature is not currently available for the conservation of mass and momentum solver.

* WindNinja has a feature that automatically fetches and uses coarser U.S. National Weather Service forecast model outputs to drive the flow. This feature is not currently available for the conservation of mass and momentum solver.



<br>
<br>
<br>


Is WindNinja faster than WindWizard? How much?
----------------------------------------------
***
[WindWizard](http://www.firelab.org/project/windwizard) is no longer available. There is now an optional conservation of mass and momentum solver in WindNinja which replaces the functionality of WindWizard. The conservation of mass solver (the native WindNinja solver) runs much faster than the conservation of mass and momentum solver (less than a minute for conservation of mass compared to about 1 hour for conservation of mass and momentum).

<br>
<br>
<br>



How do I view WindNinja outputs?
--------------------------------
***
There are several ways to view WindNinja outputs.  Probably the most convenient is to use Google Earth and WindNinja's KMZ output file (.kmz).  As of version 3.0, WindNinja can generate a GeoPDF output file (.pdf). GeoPDFs can be viewed in any PDF reader, but can also be viewed in GIS programs including the Avenza PDF Maps mobile application. Another way, if you have a FARSITE landscape file (.lcp), is to use FlamMap with WindNinja's fire behavior output files (.asc).  Last, you could use a GIS such as ArcView or ArcMap with WindNinja's shape file output files (.shp, .shx, .dbf).  Instructions for plotting wind vectors using ArcView and ArcMap can be found within the help menu of WindNinja.


<br>
<br>
<br>



What elevation file formats does WindNinja accept?
--------------------------------------------------
***

Starting with WindNinja 2.0.0, several common file formats can be used.  They are:
* Arc/Info ASCII Raster (*.asc)
* FARSITE landscape file (*.lcp)
* GeoTiff (*.tif)
* ERDAS IMAGINE (*.img)

WindNinja can now (as of 2.3.x) download dem files for you, and properly project the file.


<br>
<br>
<br>



How do I obtain an elevation file?
----------------------------------
***

There are many different ways to obtain elevation files for WindNinja. WindNinja can now download a file for you with the best-fit UTM projection.

If you already have an elevation file, it can be used in WindNinja so long as it meets WindNinja's requirements.  See the FAQ question about elevation file requirements.


<br>
<br>
<br>




What happens if I don't have GIS projection information with my elevation file?
-------------------------------------------------------------------------------
***

### Pre-2.3.0:

Without projection information, you can still use WindNinja but some options will not be available.  Specifically, you won't be able to make Google Earth output files (.kmz).  Also, if you want to do a diurnal simulation, you will have to manually enter a latitude and longitude for your area (with projection information WindNinja can automatically find the latitude and longitude for you).

### 2.3.0 and after

WindNinja *requires* projection information with your DEM.


<br>
<br>
<br>



What are the requirements for elevation files?
----------------------------------------------
***

First, the elevation file must be one of the allowable file formats (Arc/Info ASCII Raster (.asc), FARSITE landscape file (.lcp), GeoTiff (.tif), ERDAS IMAGINE (.img)).  Second, the elevation file must not have any areas without data (NO_DATA values).  See WindNinja Tutorial 1 in the help menu for more information about common reasons for having NO_DATA values and ways to fix these problems.  Third, elevation files must not be too large in extent.  We generally recommend that elevation files should be less than 50x50 km (about 30x30 miles).  Fourth, elevation files must be in units of meters.  This means both the horizontal and vertical units.  Last, if WindNinja 2.3.0 or newer is used, it must be georeferenced in a projected coordinate system.


<br>
<br>
<br>



If I use a coarse (say 90m) DEM, can I simulate a larger area?
--------------------------------------------------------------
***

The DEM resolution is really not so much the issue, it is the computational resolution of the wind simulation.   WindNinja resamples the DEM to build the internal computational resolution, which is the resolution of the actual wind simulation.  This computational resolution is the limiting factor in simulations when it comes to computational time and computational memory (running out of computer RAM).  The choice of computational resolution should be such that the terrain is adequately resolved for the wind simulation, meaning that the scale of terrain that you want to resolve is resolved.  For example, if you want to resolve all terrain features of a certain size, say hills of horizontal size of around 100 meters, then the computational resolution should probably be at least 10 to 30 meters so that there are several cells on the 100 meter hills.  And so the computational resolution choice is probably really a function of the terrain.  "Smoother" terrains with large average distances between hills/ridges could use larger cell sizes than "rougher" terrain.

Through experience, we've found that 100 to 300 meter computational (mesh) resolutions are usually adequate for most terrains.  This can be obtained by choosing "fine" for mesh resolution and keeping the DEM extent to less than 40-50 km on a side.  The user can choose "custom" for resolution and manually enter a computational cell size in meters.  You could play around with a larger DEM (say 100 km by 100 km) and manually set the computational (mesh) resolution.  The limiting factor will be computer RAM, at some point you'll run out.


<br>
<br>
<br>



Have you compared results with different grid resolutions to know if it markedly changes wind behavior?
-------------------------------------------------------------------------------------------------------
***

We have.  For an example and discussion, you could look at the images on pages 30-31 of [Jason Forthofer's master's thesis](http://www.firelab.org/document/forthofer-thesis).  Note that this terrain is fairly gentle though.  The appropriate grid resolution is dependent on the specific terrain and what winds you want to resolve. Probably one of the best things to do is to experiment with different computational (mesh) resolutions for your terrain to see how much difference there is (sensitivity).


<br>
<br>
<br>



Is WindNinja accurate along the borders of the modeling domain?
---------------------------------------------------------------
***

As with most numerical models of this type, winds along the border of the modeling domain may have some error.  This is because, in reality, terrain features outside the modeling domain may affect the wind flow inside the domain.  But since these terrain features are not modeled, the simulation results do not reflect them.  There is a simple solution to deal with this problem.  Use an elevation file that is slightly larger than the area you want to model so there is a buffer around your desired area.  We recommend a 10-20% buffer size.


<br>
<br>
<br>



Are there any issues about using the model at fine scales?
----------------------------------------------------------
***

*Say I'd like to use it to model the wind over an area of about 100 hectares which has a fairly complex topography - is WindNinja ok to use with (say) 10 m grid DEMs?*

There shouldn't be any issues, although WindNinja hasn't been tested much at this scale.


<br>
<br>
<br>



Any insights on how well WindNinja captures flow eddies?
--------------------------------------------------------
***

Because of how the conservation of mass solver (the native solver) simulates momentum, it cannot capture eddies (reversed flow) at all.  Instead you will just see very low wind speeds in these areas, but not reversed direction. The conservation of mass and momentum solver (available since version 3.0) will capture eddies in the flow field. We are in the process of evaluating the conservation of mass and momentum solver, including its ability to resolve lee-side eddies, against field observations in complex terrain.


<br>
<br>
<br>



How should I cite the model in a publication?
---------------------------------------------
***

The best peer-reviewed reference is:

Forthofer, J.M., Butler, B.W., Wagenbrenner, N.S., 2014. [A comparison of three approaches for simulating fine-scale surface winds in support of wildland fire management. Part I. Model formulation and comparison against measurements] (http://www.fs.fed.us/rm/pubs_other/rmrs_2014_forthofer_j001.pdf). Int. J. Wildland Fire. 23:969-981.

_Note: In this publication WindNinja is referred to as the "mass-conserving" model._


<br>
<br>
<br>



Additional publications:
---------------------------------------------
***
See the page below


<div class="col col-4">
  <div class="block green">
      <div class="block-body height-1">
          <span class="post-meta white-text"></span>

          <h2>
            <a class="post-link white-text" href="http://firelab.github.io/windninja/main/2016/07/01/select.html">Select Publications & Products</a>
          </h2>

      </div>
  </div>
</div>
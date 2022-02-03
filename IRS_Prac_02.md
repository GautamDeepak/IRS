# Introductory Remote Sensing (ENV202/502)
Prac 1 - Image visualisation (single- and multi-band)


### Acknowledgments 
- [Earth Engine Beginning Curriculum](https://docs.google.com/document/d/1ZxRKMie8dfTvBmUNOO0TFMkd7ELGWf3WjX0JvESZdOE/edit#!)
- [Google Earth Engine guide](https://developers.google.com/earth-engine/guides)

### Objective

The objective of this Prac is to get you started with satellite images. By the end of this exercise, you will be learn the visualisation skills of the satellite images. We will work on visualisation of single-band image (using SRTM) and multi-band image (using Sentinel-2).
---------------------------------------------------
## 1. Getting started with image

1. Open up the Google Earth Engine environment by going to this address in the **Chrome browser**: [https://code.earthengine.google.com](https://code.earthengine.google.com).

2. Lets navigate to Darwin area where we will be working today. Use you mouse left click + drag on the mapping area to navigate to Darwin. You can use the mouse wheel to zoom in or out. 

![Figure 2. Zoom to Darwin](Prac1/navigate2darwin.png)


2. If the script area is not clear, clear the script workspace by selecting "Clear script" from the Reset button dropdown menu.

![Figure 3. Clear script](Prac1/clearscript.png)

3. Search for "elevation" or "SRTM" and click on the "NASA SRTM Digital Elevation 30m" result to show the dataset description.

![Figure 4. Search for elevation data](Prac1/searchelevation.png)

4. View the information on the dataset - look under "description" and "bands". Once you are happy, click on "Import", which moves the variable to the Imports section at the top of your script.

![Figure 4. View elevation datasource and import](Prac1/viewinfo.png)

Question: How many bands do this data have and whats the spatial resolution?

5. Rename the default variable name "image" to anything you like. Here we will rename it to "theSRTM".

![Figure 5. Rename image](Prac1/rename.png)

6. Print/add the image object to the console by copying the script below into the code editor, and click "run" :

```JavaScript
print(theSRTM);
```
![Figure 6. Print SRTM](Prac1/printrun.png)


7. Browse through the information that was printed to the console window. Open the “bands” section to show the one band named “elevation”. Note that all this same information is automatically available for all variables in the Imports section.

![Figure 7. SRTM in console](Prac1/browseprint.png)


## 2. Introduction to the GEE environemnt

**Question:** *Modify the above script to print your name in the console.*

## 3. Introduction to JavaScript

## 4. Finding the avaialble datasets in the GEE

## 5. Finding information about the datasets


## 11. The complete script used in this Prac

![Figure 18. polygon](Prac01/polygon.png)
```JavaScript
// Apply spatial reducer to compute mean elevation over the roi
var meanElevation = theSRTM.reduceRegion({
        reducer: 'mean',
        geometry: roi,
        scale: 90
});
// print the mean elevation
print('Mean elevation', meanElevation.get('elevation'));
```
-------
### Thank you

I hope you found this prac useful. A recorded video of this prac can be found on your learnline.
Coming up next week: Next week visualisation and computation

#### Kind regards, Deepak Gautam
------
### The end
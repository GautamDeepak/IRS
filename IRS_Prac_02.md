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

2. Lets navigate to Darwin area where we will be working today. Use you mouse left click and drag on the mapping area to pan to Darwin. You can use the mouse wheel or + - button to zoom in or out. The navigation in the mapping pane is very much google maps like.

![Figure 2. Zoom to Darwin](Prac1/navigate2darwin.png)

3. Now lets search for an elevation dataset. In the search bar, type in "elevation" or "SRTM" and click on the "NASA SRTM Digital Elevation 30m" result to show the dataset description. To learn more about this dataset, check out the blurb and associated resources in the learnline.

![Figure 4. Search for elevation data](Prac1/searchelevation.png)

4. View the information on the dataset - read under "description" and "bands". Once you are happy, click on "Import", which imports the image to the Imports section at the top of your script.

![Figure 4. View elevation datasource and import](Prac1/viewinfo.png)

**Question:** *How many bands did this data have and what are their spatial resolution?*

5. Rename the default variable name "image" to anything you like. Naming convention is that the name should short but descriptive enough for you to understand when you revisit this script later in the future. Here we will rename the image "theSRTM".

![Figure 5. Rename image](Prac1/rename.png)

6. We used print command in last prac. Here lets use the print command to print the image object to the console by copying the script below into the code editor, and click "run" :

```JavaScript
print(theSRTM);
```
![Figure 6. Print SRTM](Prac1/printrun.png)


7. The print command just prints the textual information not the image. Browse through the information that was printed to the console window. Open the “bands” section to show the band named “elevation”. Note that all this same information is automatically available for all variables in the Imports section.

![Figure 7. SRTM in console](Prac1/browseprint.png)

8. Always know that you can look into the image description, or printed information, or within the import section to look into more detail about the image. 

9. Similarly lets import a multi-band image from Sentinel-2. Here I have provided the image ID so the image can be directly imported by copying the below command to your code editor. 
```JavaScript

```

**Task: Note we now have two images imported. First one is the SRTM image and the second one is the sentinel-2 image. The images are single and multi-band respectively. Now, like we printed and looked into the band information of the SRTM image, please print and look the band information of the sentinel-2 image.**

## 2. Visualising the single band image

1. Note that we are currently working with the single band image. 

## 3. Visualising the multi-band image

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
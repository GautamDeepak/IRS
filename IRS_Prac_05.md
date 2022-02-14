# Introductory Remote Sensing (ENV202/502)
Prac 5 - Introduction to Google Earth Engine and basic JavaScript


### Acknowledgments 
- [Earth Engine Beginning Curriculum](https://docs.google.com/document/d/1ZxRKMie8dfTvBmUNOO0TFMkd7ELGWf3WjX0JvESZdOE/edit#!)
- [Google Earth Engine guide](https://developers.google.com/earth-engine/guides)

### Objective

The objective of this Prac is to get you started with satellite images. By the end of this exercise, you will learn the visualisation skills of the satellite images. We will work on visualisation of single-band image (using NASA SRTM as an example) and multi-band image (using Sentinel-2 as an example). Using these skills, you will be able to visualise any other optical images in the Google Earth Engine.

---------------------------------------------------

## 2. Introduction to the GEE environemnt


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
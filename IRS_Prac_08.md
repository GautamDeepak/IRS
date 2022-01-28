# Introductory Remote Sensing (ENV202/502)
Prac 1 - Introduction to Google Earth Engine and basic JavaScript


### Acknowledgments 
- [Earth Engine Beginning Curriculum](https://docs.google.com/document/d/1ZxRKMie8dfTvBmUNOO0TFMkd7ELGWf3WjX0JvESZdOE/edit#!)
- [Google Earth Engine guide](https://developers.google.com/earth-engine/guides)


### Prerequisites


Completion of this Prac exercise requires the use of the Google Chrome browser and a Google Earth Engine account. If you have not yet signed up - please do so now in a new tab: [Earth Engine account registration](https://signup.earthengine.google.com/)

Once registered you can access the Earth Engine environment [here:](https://code.earthengine.google.com)

Google Earth Engine uses the JavaScript programming language. We will cover the very basics of this language during this course. If you would like more detail you can read through the introduction provided here: [JavaScript background](https://developers.google.com/earth-engine/tutorials/tutorial_js_01)


### Objective

The objective of this Prac is to give you an introduction to the Google Earth Engine processing environment and basic JavaScript. By the end of this exercise, you will be able to navigate the Google Earth Engine environment, search for, find, and visualise a broad range of remotely sensed datasets. 
---------------------------------------------------
## 1. Signup for the GEE environemnt

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
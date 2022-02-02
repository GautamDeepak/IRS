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

The objective of this Prac is to give you an introduction to the Google Earth Engine processing environment and basic JavaScript. By the end of this exercise, you will be able to navigate the Google Earth Engine environment, search for and find a broad range of remotely sensed datasets. 
---------------------------------------------------
## 1. Signup for the GEE environemnt
1. If you have not done so already, sign up [here](https://code.earthengine.google.com/signup/)
2. Follow the signup and activation process.
3. For help look into the "Frequently asked questions" file in your learnline.

## 3. Navigate through the GEE environment interface.
1. Open up the Google Earth Engine environment by going to this address in the **Chrome browser**: [https://code.earthengine.google.com](https://code.earthengine.google.com). You should see the GEE landing page as below. This suggests that your signup and activation of the Earth Engine account went through well. 

![Figure 1. The Google Earth Engine environment](Figures/Prac01_LandingPage)

2. Notice GEE environment is divided up into four panels: 
- The top-left panel has tabs for Scripts, Documentation and Assets  
- The editor (top-centre) panel is for writing and running JavaScript commands  
- The top-right panel has tabs for the console, inspector and tasks  
- The bottom panel is Map interface with geometry features and a google map like feel. 

3. Navigate through the four panels and try to understand what each panel does. I recommend you take the feature tour.

![Figure 1. The Google Earth Engine environment](Prac01/FeatureTour.PNG)   

4. Check out all the buttons that are available to you and try to understand them. 



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
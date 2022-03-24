# Introductory Remote Sensing (ENV202/502)
Prac 3 - Working through image collection to find the right image and understanding band combination

### Acknowledgments
- [Earth Engine Beginning Curriculum](https://docs.google.com/document/d/1ZxRKMie8dfTvBmUNOO0TFMkd7ELGWf3WjX0JvESZdOE/edit#!)
- [Google Earth Engine guide](https://developers.google.com/earth-engine/guides)

### Objective

So far you have worked with single- and multi-band optical images. However, we have not worked with the image collection. A single image of the earth observation satellite covers only a small portion of the earth surface. Through time more acquisition leads to global coverage and that is repeated over and over to create a historical spatiotemporal archive of images. As a remote sensing scientist, you need to have the skills to look for and work with images acquired at a certain time and on a certain location - which is quite easy in Google Earth Engine. The objective of this Prac is to gain experience in working through an image collection, finding a suitable image, and understanding the band combination.

------------------------------------------------------------------------

## 1. Working with image collection 

1. Just above the Coding panel in the search bar. Search for ‘Darwin’ in this GEE search bar, and click the result to pan and zoom the map to Darwin. Note the results populated under the "places" refers to the actual location on earth.


![Figure 1. Navigating to the area of interest in Google Earth Engine](Figures/Prac03_SearchDarwin.png)


2. Now let's make use of the geometry tool available to us in GEE. There is marker geometry (to define a point), line geometry (to define a line), shape geometry (to define a polygon with any number of sides) and rectangle geometry (to define a rectangle). Let's use the marker geometry to create a point on the Casuarina campus of Charles Darwin University (located in the suburb of Brinkin, north of Rapid Creek). You need to click on the marker geometry and then click on where you want to create the point. Once you create the point, you will see the point geometry being added to your Coding panel as a variable (var) under the Imports heading.


![Figure 2. Creating a geometry point](Figures/Prac03_DrawPoint.png)

3. Rename the default name of the point ‘geometry’ to any name you want. Let's call it ‘campus’. Rename by clicking the import name ‘geometry’.

![Figure 3. Renaming a geometry point](Figures/Prac03_RenameCampus.png)


4. Search for ‘Sentinel-2’ in the search bar. In the results section, you will see ‘Sentinel-2: Multi-spectral Instrument (MSI), Level-1C’ - click on it and then click the ‘Import’ button. Here, from previous pracs, you know that the detailed information of the image is available to you in the description window. 

![Figure 4. Importing Sentinel-2 data](Figures/Prac03_Import_Sentinel.png)


5. After clicking import, Sentinel-2 will be added to our Imports in the Coding panel as a variable. It will be listed below our campus geometry point with the default name "imageCollection". Let's rename this "imageCollection" to “sent2” by clicking on it and typing "sent2". Note that you can rename it to any name you want. 

![Figure 5. Importing Sentinel-2 data](Figures/Prac03_RenameSent2.png)

6. It is important to understand that we have now added access to the full Sentinel-2 image collection (i.e. every image that has been collected to date) to our script. For this exercise we don't want to load all these images - we want a single cloud-free image over Charles Darwin University. As such, we can now filter the image collection with a few criteria, such as time of acquisition, spatial location and cloud cover.

## 2. Filtering the image collection

1. To achieve this filtering we need to use a bit of coding. In the JavaScript programming language, two backslashes (//) indicate comment lines and are ignored in actual processing steps. We use // to write notes to ourselves in our code, so that we (and others who might want to use our code) can understand why we have done certain things. 

```JavaScript
// Before using any new variable you need to define the variable using command "var" as below
    var anImage = sent2

    // sent2 is an image collection so lets filter the collection by the the date range we are interested in
    .filterDate("2015-07-01", Date.now())

    // Next we include a geographic filter to narrow the search to images at the location of our point
    .filterBounds(campus)

    // Next we will also sort the collection by a metadata property, in our case cloud cover is a very useful one
    .sort("CLOUD_COVERAGE_ASSESSMENT")
	
    // Now lets select the first image out of this collection - i.e. the most cloud free image in the date range and over the campus
    .first();  //Note that upto here was one line of script, hence, no use colon

// And let's print the image to the console.
print("A Sentinel-2 scene:", anImage);
```

2. You need to copy the entire piece of code above and paste it into the GEE code editor. Then click the "Run" button and watch Google do its magic...... This piece of code will search the full Sentinel-2 archive (2015 to present), look for images that are acquired over the Casuarina campus, sort them according to percentage cloud cover, and then return the least cloudy image for us. Information relating to this image will be printed to the Console, where it is listed as "A Sentinel-2 scene" with some details about that scene(COPERNICUS/S2/20160410T013712_20160410T013707_T52LGM). We know from the Image id that it was collected on the 10th of April 2016. (Note you may end up with a different cloud-free image)

![Figure 6. Filtering the collection](Figures/Prac03_Filtering.png)


3. **Take a moment** to play with and understand the above filtering script. Use the figure below as a guide
![Figure 16. NDVI map](Figures/Prac03_FilteringExample.png)

4. **Self-assessment questions:** Try modifying the above script to answer the questions. Discuss in the discussion board with your classmates if you are stuck. 
- *What do the numbers within the filterDate() represent?* 
- *Think about what would happen if you removed or commented out the filterDate command?*
- *Modify the above script to get an image from last - month. Can you do that?*
- *What does filterBounds represent?*
- *What will happen if you remove or comment out the filterBounds() command.*
- *Where did we get the keyword "CLOUD_COVERAGE_ASSESSMENT" to sort the images.*
- *What will happen if you remove the ".first()" command?*


5. Now we have refined the entire image collection to a single image called "anImage". To view this image, we need to add it to our mapping layer. Before doing that, however, let's define how we want to display the image. Let’s start with a true colour representation by adding the following lines of script and clicking "Run".

```JavaScript
// Define visualization parameters in a JavaScript dictionary for true colour rendering. Bands 4,3 and 2 needed for RGB.
var trueViz = {
  bands: ["B4", "B3", "B2"],
  min: 0,
  max: 3000
  };

// Add the image to the map, using the visualization parameters.
Map.addLayer(anImage, trueViz, "true-colour image");
```

**Note:** *The above script could have also been written as: -Map.addLayer(anImage, {bands: ["B4", "B3", "B2"], min: 0, max: 3000 }, "true-colour image");  ... However, we have defined a variable called trueViz and plugged in that variable in the Map.addLayer command*

6. Above script specifies that for a true colour image, bands 4,3 and 2 should be used in the RGB composite. After the image appears on the map, you can zoom in and explore Darwin. We see great detail in the Sentinel-2 image, which is at 10m resolution for the selected bands. The (+) and (-) symbols in the upper left corner of the map can be used for zooming in and out (also possible with the mouse scroll wheel/trackpad). A left-click with the mouse brings up the "hand" for panning to move around the image. Moving your mouse over the "Layers" button in the top right-hand corner of the map panel shows you the available layers, and lets you adjust the opacity of different layers.

![Figure 7. Adding a true colour image to the map](Figures/Prac03_TrueColor.png)

7. Try moving your marker geometry to a different location (e.g. to Melbourne), run the script and see what happens... You should get a cloud-free image from Melbourne. So, you now have the skills to look for images from anywhere in the globe (by moving your geometry) and from the desired time range (by adjusting the start and end date in the filtering script). Please practice and once you are happy with the filtering and displaying of images, move the marker back to the Casuarina campus for the following steps.

## 3. Band combination
1. Different landcover types on the earth surface such as water, forest, grassland, desert, bare land etc interact differently with electromagnetic energy. As a result, the spectral information recorded by the satellite for those landcover types varies. For example, the spectral value in the near-infrared region for vegetation is quite high while for the water is quite low. To find out more about how different landcover interact with the electromagnetic energy, you can use the Inspector tool which is located in the Console Panel - left hand tab. Click on the Inspector tab and then click on the image in the map view. The satellite recorded band values for the pixel you clicked will be displayed in the Inspector window. Click over some different landcover types (sports fields, tennis courts, mangroves, ocean, beach, houses etc) to see how different landcover have a different spectral profile.

![Figure 8. Band values](Figures/Prac03_BandValues.png)

2. In the above example, I clicked on the sports field. The band values represent the spectral characteristics of photosynthetically active vegetation. For example, I can see absorption in the blue (B2) and red (B4) bands, the green band (B3) is a bit more reflective while the NIR band (B8) is highly reflective. Now, it is your turn to inspect different landcover types. Try to figure out which landcover types look similar (in the band value) and which are distinct.  

3. Now let's learn how to create false-colour composites. The Sentinel-2 has 13 spectral bands. However, our true colour display only utilises three bands (Red Green and Blue). So, in a sense, we are not using the full potential of the Sentinel-2 capabilities. Similar to how we displayed true colour composite, we can display the false colour composite. We displayed true colour composite by displaying the Red band in red colour, the green band in green colour and the blue band in blue colour. To create a false-colour composite, we play with the band combination and plug in different bands. For example, in the below false-colour infrared composite, the NIR band is displayed in red colour, the red band is displayed in green colour and the green band is displayed in blue colour. Paste the following lines and click "Run".

```JavaScript
//Define false-colour visualization parameters.
var falseViz = {
  bands: ["B8", "B4", "B3"],
  min: 0,
  max: 3000
  };

// Add the image to the map, using the visualization parameters.
Map.addLayer(anImage, falseViz, "false-color composite");
```

![Figure 9. Adding a false colour composite to the map](Figures/Prac03_FalseColor
.png)

**Question*** We know that vegetation looks green. In the above false-colour infrared composite, the green band is displayed as blue colour. That means green vegetation should have appeared as blue colour. Why instead vegetation appears as red colour?*

4. The above false-colour infrared composites place the near infra-red band in the red channel. Chlorophyll content in green leaves has a strong response in the NIR band. Vegetation that appears dark green in true colour thus appears bright red in the false colour. Note the variations in red that can be seen in the vegetation bordering Rapid Creek. False-colour composites help us to contrast between different landcover types or highlight some landcover types. Sometimes those contrast may not appear clearly on the true colour composite. The false-colour infrared composite helps us clearly distinguish the photosynthetically active vegetation. 

5. Let's do one more false colour composite and you can practice the rest. I am going to do the land/water false-colour composite. This composite uses the following bands: NIR (B8), SWIR(B11), and Red(B4).  

```JavaScript
//Define land/water false-colour visualization parameters.
var falseLandWaterViz= {
  bands: ["B8", "B11", "B4"],
  min: 0,
  max: 3000,
  };

// Add the image to the map, using the visualization parameters.
Map.addLayer(anImage, falseLandWaterViz, "false-color Land/Water");
```

![Figure 9. Adding a false colour composite to the map](Figures/Prac03_FalseLandWater.png)

## 4. Exercise for you

1. Filter the Sentinel-2 image collection to get two cloud-free images from the Darwin region during the dry season of 2016 and the dry season of 2021.
*Hint: You need to do the filtering two times. First filtering to get the 2016 image and the second filtering to get the 2021 image. Store the two images in two variables e.g. var dry2016Image = ..., and var dry2021Image = ...*

2. Display the two images in true colour composite and examine what has changed in the landscape between 2016 and 2021. 

3. Display the two images in false colour infrared composite and examine how vegetation cover and condition has changed in the six years.  

4. So far we have only explored two visualisation options (true-colour and false-colour infrared), but there are many more possible combinations:
    - True colour: 4 3 2
    - False-colour infrared: 8 4 3
    - False-colour urban: 12 11 4
    - Agriculture: 11 8 2
    - Healthy vegetation: 8 11 2
    - Land/Water: 8 11 4
    - Shortwave infrared: 12 8 4
    - Vegetation analysis: 11 8 4
    - you can also make your unique combination

5. Experiment with the combinations listed above and think about why we might want to use them.

## 5. Complete script 
```JavaScript
var campus = /* color: #d63000 */ee.Geometry.Point([130.86795149296128, -12.370376579036192]);
var sent2 = ee.ImageCollection("COPERNICUS/S2");

var anImage = sent2
  // sent2 is an image collection so lets filter the collection by the the date range we are interested in
  .filterDate("2020-01-01", Date.now())

  // Next we include a geographic filter to narrow the search to images at the location of our point
  .filterBounds(campus)

  // Next we will also sort the collection by a metadata property, in our case cloud cover is a very useful one
  .sort("CLOUD_COVERAGE_ASSESSMENT")
	
  // Now lets select the first image out of this collection - i.e. the most cloud-free image in the date range and over the campus
  .first();  //Note that upto here was one line of script, hence, no use colon

  // And let's print the image to the console.
  print("A Sentinel-2 scene:", anImage);
    
// Define visualization parameters in a JavaScript dictionary for true colour rendering. Bands 4,3 and 2 needed for RGB.
var trueViz = {
  bands: ["B4", "B3", "B2"],
  min: 0,
  max: 3000
  };

// Add the image to the map, using the visualization parameters.
Map.addLayer(anImage, trueViz, "true-colour image");
  
//Define false-colour visualization parameters.
var falseViz = {
  bands: ["B8", "B4", "B3"],
  min: 0,
  max: 3000
  };

// Add the image to the map, using the visualization parameters.
Map.addLayer(anImage, falseViz, "false-color composite");

//Define land/water false-colour visualization parameters.
var falseLandWaterViz= {
  bands: ["B8", "B11", "B4"],
  min: 0,
  max: 3000,
  };

// Add the image to the map, using the visualization parameters.
Map.addLayer(anImage, falseLandWaterViz, "false-color Land/Water");
```

-------
### Thank you

I hope you found this prac useful. A recorded video of this prac can be found on your learnline.
Coming up next week: Analysis of spectral reflectance curve.

#### Kind regards, Deepak Gautam
------
### The end



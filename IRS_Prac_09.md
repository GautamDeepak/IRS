# Introductory Remote Sensing (ENV202/502)
Prac 9 - Working with Terrestrial Laser Scanning (TLS) data in CloudCompare


### Acknowledgments 
- 

### Prerequisites

Completion of this Prac exercise requires use of the CloudCompare software package. CloudCompare is a powerful package for visualising and processing point-clouds, and best of all is open-access. You can download the version to match your operating system. [Download here](https://www.danielgm.net/cc/)

### Objective
The objective of this Prac is to familiarise yourself with 3D point cloud data. We will use data that we collected last week on campus in the Boab court. 
---------------------------------------------------

## 1. Downloading the data.
1. We collected multiple scans with a Leica BLK360 laser scanner, and we will work with two of these scans today.

![Figure 1. Leica BLK360 scanning](Prac8/leica.png)

2. Scan data can be downloaded in .las format below (please note that each file is ~ 200 MB):

- [Scan 1](https://charlesdarwinuni-my.sharepoint.com/:u:/g/personal/deepak_gautam_cdu_edu_au/EQLh_JE920JLp_blNIwjTKsBiGV8vVQzt1FMhq6hNhOvAw?e=6X6zBP) | [Scan 2](https://charlesdarwinuni-my.sharepoint.com/:u:/g/personal/deepak_gautam_cdu_edu_au/ERJnGoCYMHVAi85v6DKOWMIB5e4ydWOG5zyEwNVHqeTEFQ?e=4q7Ar5)

## 2. Getting to know CloudCompare

1. Launch the CloudCompare application.

![Figure 2. CloudCompare](Prac8/cloudcompare.png)

2. Note that your interface might look a bit different depending on if you are in Windows or Machintos machine - but don't worry the tools and menus are consistent across platforms.

3. Open up the first scan by clicking File>Open, navigate to where you downloaded/saved the data, and click on Boab_1.las

![Figure 3. CloudCompare](Prac8/cc_open.png)

4. A window will appear asking if you would like to apply default settings - click Apply

![Figure 4. CloudCompare](Prac8/cc_apply.png)

5. Another window will appear asking you about coordinate transformations - click Yes

![Figure 5. CloudCompare](Prac8/cc_yes.png)

6. A progress bar should appear showing you how many points are being ingested (28 million in this case) and then the point cloud should render in the main viewing window as shown below.

![Figure 6. CloudCompare](Prac8/cc_boab1.png)

7. The top-left panel houses the file structure. Click on Baob_1.las and you will see some information appear in the panel below it, and the spatial extent of the file will be highlighted in the main window. In the properties panel (lower left) we can see that the current display options are set to RGB (the Leica BLK360 captures true-colour images in addition to laser data) and that there are 28,846,128 points in this cloud. 

![Figure 7. CloudCompare](Prac8/cc_gui.png)

8. Let's zoom in a bit closer to see more detail. Hold your mouse over the main viewing window and use the scroll wheel to zoom in and out.

![Figure 8. CloudCompare](Prac8/cc_zoom.png)

9. As you can see, we are looking down on our scan from above - a bird's eye perspective. The green lawn is clearly visible, and the black dot in the location where the scanner was placed (the scanner does not scan directly beneath itself). See what other features you can identify - the boab trees, building, sun-shades etc.

10. Although this aerial view is interesting, we currently have a 2D view. The reason we use LiDAR is for a 3D perspective - so use your LEFT mouse button to click and tilt the scene. Your RIGHT mouse button will pan the image (up, down, left, right) and the SCROLL WHEEL is for zooming in and out.

![Figure 9. CloudCompare](Prac8/cc_3d.png)

11. The 3D navigation takes a while to get used to. Play around a bit to get the hang of it - and try navigate to the view shown below. You can see your fellow students waiting in the shade on the steps of the Mal Nairn Auditorium.

![Figure 9. CloudCompare](Prac8/cc_mal.png)

12. If at some stage you get lost in the scene, you can use the 1:1 button to return to an aerial view of the full spatial extent.

![Figure 10. CloudCompare](Prac8/cc_lost.png)

13. So far we have been visualising the TLS data in RGB - that is the reflectance values recored by the camera are being given to each point. We see some issue with this in the tips of tree branches whereby the blue colour of the sky is given to the thin branches of the boab trees. This is partly due to the camera resolution being coarser than the laser resolution.

14. Since the TLS is recording distance to objects in x,y and z coordinates, we can also visualise the cloud in terms of elevation. With the file selected in the top-left panel, click Edit>Colours>Height ramp from the main menu.

![Figure 11. CloudCompare](Prac8/cc_heightramp.png)

15. A new window will appear where you can apply a colour scale to the elevation data. Use the default options and click OK

![Figure 12. CloudCompare](Prac8/cc_heightramp2.png)

16. The point cloud will now be rendered with a default colour scale showing lower elevation points in blue and taller points in green.

![Figure 13. CloudCompare](Prac8/cc_heightramp3.png)

17. Zoom in a bit to see the effect in 3D.

![Figure 14. CloudCompare](Prac8/cc_heightramp4.png)

18. To create a more 3D textured look we can use a light shader. Using the main menu navigate to
Display>Shaders & filters and turn on the E.D.L shader.

![Figure 15. CloudCompare](Prac8/cc_shader.png)

19. This results in a visualisation with more depth/texture.

![Figure 15. CloudCompare](Prac8/cc_shader2.png)

## 3.  Merging multiple point clouds
2. Navigate to where the scan data are stored and select Boab_1.las and Boab_2.las before clicking "Open". If you cannot see your files or they are greyed out, make sure you have the file type set to ".las" or "All".


![Figure 2. Opening two files](Prac9/cc_open2.png)

3. Click "Apply to all" and "Yes to all" when the two dialogue boxes pop up.

4. Once the two files have loaded, you will see that they are not correctly aligned.

![Figure 3. Opening two files](Prac9/cc_overlap.png)

5. In fact, if you zoom in closer (using the mouse wheel), you will see that they are positioned exactly on top of each other (even though they were collected ~ 10m apart).

![Figure 4. Opening two files](Prac9/cc_overlap_zoom.png)

6. This issues occurs because the scans are in the scanners own coordinated system (SOC) and not in a geographic coordinate system (the BLK360 lacks a GPS). The origin of both scans is 0,0,0 (x,y,z) - every point is relative to the scanner itself.

7. We will align these two scans using a combination of manual translation (rough positioning) and an automated computer algorithm called Iterative Closest Point (ICP) for fine tuning.

8. Before starting with this, let us map both clouds according to an elevation colour scale (height ramp) - using the default scale for blue to green. Be sure to select both clouds before applying the colour ramp.

![Figure 5. Two file colour ramp](Prac9/cc_dual_hr.png)

![Figure 6. Two file colour ramp](Prac9/cc_dual_hr2.png)


9. Next select only the Boab_3.las file, and choose the "Translate" tool from either the main Menu or from the icon in the toolbar.

![Figure 7. Translate](Prac9/cc_translate.png)


10. You will see a new toolbar appear in the top-right corner of the main window, and small white text in the top-centre of the main window will remind you that the tool is active.

![Figure 8. Translate](Prac9/cc_translate2.png)

11. Before going any further we will change the rotation axis from xyz to z only in the translation dialogue window. This will ensure that the point cloud can only be moved (left/right, up/down) or rotated around the z x-axis, preventing any unwanted tilting.

![Figure 9. Translate](Prac9/cc_translate3.png)

12. Now we can use the right-mouse click to drag the selected cloud (Boab_3) in any direction we like - in the screenshot below you will see I have shifted it over to the right.

![Figure 10. Translate](Prac9/cc_translate4.png)

13. Now we can see the two scans clearly, and we can see that Boab_3 needs to be rotated clockwise to align better with Boab_1. Using the left mouse button click and drag the Boab_3 cloud to rotate it by about 30 degrees in teh clockwise direction.

![Figure 11. Translate](Prac9/cc_translate5.png)

14. Now that the rotation looks better, we can use the right-mouse button to pull the whole cloud over to the left again and position it in better alignment with Boab_1.

15. That looks much better, so now we can click the green tick to accept these changes to the orientation matrix of Boab_3.

16. If we zoom in, we can now see the two separate scan locations, they are no longer on top of each other but are very nearly in the correct position.

![Figure 11. Translate](Prac9/cc_translated2.png)

17. However if we examine some straight lines for example, it is still clear that some minor offset is present.

![Figure 12. Translate](Prac9/cc_translated.png)

18. We will correct this in Part 3 using the ICP algorithm

-------
### Thank you

I hope you found this prac useful. A recorded video of this prac can be found on your learnline. After this prac, you are ready to complete Assignment#2.  Coming up next week: image classification and accuracy assessment.

#### Kind regards, Shaun R Levick (edit Deepak Gautam)
------
### The end
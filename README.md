# Ru3esium
Interactive cesiumJS and THREEjs Example

This software is an interactive 4D Transactional Reporting System based upon location, time and data. Utilizing CesiumJS to show location and handle time. Utilizing THREEjs to display details of your data Summarizing your data the over the entire time period. Interactive: Clicking an item in one system will make changes in the other system.

<img src="http://mib.alltovr.com/images/Ru3esium.jpg" alt="AllToVr.com">

This project started with Cesium-threejs-experiment by Wilson Mukar. Please read the original posts here: https://cesium.com/blog/2017/10/23/integrating-cesium-with-threejs/

There are two versions of this software: This version has no ability to communicate with the server. For the version that has communication with the server via Socket.io; Visit: https://mib.alltovr.com/apps/itc/Ru3esium-ioAutoLoad.html

Location: 
We are dealing with every legal address worldwide; so your data is sorted by: Countries, States and zip codes.

A primary goal of this project was to have EVERYTHING loadable from a “local” CZML file. This version can ONLY load local files! How you build your file is up to you.

First order of business was to have cesium and threejs data in the same CZML file (3ZML). This required me to parse the file myself. I pull out the cesium data packets and separate them by countries, states, zip codes, transactions and then everything else. Each one has its own czmlDataSource. There maybe 100+ 3ZML files to load…. All THREEjs data packets create the THREEjs scene on the fly…

Another challenge was real-time rendering. With so many 3ZML files; the system is always building the scene and never returns to the renderer. So I build a timer to delay making the next 3ZML file long enough to allow the renders to do their job. One day I will find a better way…

Picking: The key to making CesiumJS and THREEjs interactive is knowing the ID of the other system. Both systems use a 6 part ID separated by a “-“; “system-subType-category-subcategory-vsubcategory-transaction”. System is “cml” or “three” (I am also interactive with AltSpaceVR). SubType is “Lbl”,”cat”,”sub”,”vsub” and ”trans”. When you choose an entity in CesiumJS; I simply reposition the THREEjs camera in front of that THREEjs object. When you click a THREEjs object; I have CesiumJS FlyTo the location. Zip codes and states FlyTo a different Altitude. Transactions have an extra line to show the transaction details. In the THREEjs scene; the plane on the graph representing that transaction is highlighted.

Layout Manager: The order in which information is received cannot be guaranteed; Placing the information into the THREEjs scene needed to be coordinated. Specifically; the layout of category, subcategory and vsubCategory. Also having the layout based upon a users preference is a good thing, but not fully implemented. One user may want to see things front to back, left to right and then top to bottom while another user want things a different way.

Performance side note: I found that if the rendering loop starts before the cesium viewer is fully loaded, the cesium viewer can take 30 seconds to load. So the rendering is loop delayed by 3 seconds.

The data files: In the “chartResults” directory are all the 3ZML files for this demonstration. There is a file for each country, state and zipcode. Click on “Load Local Files” button. You can load all of them or just select the ones you want to display.


Installation:

Location of script files:  This will be the location of the files on your server. Search and replace “YourSite” with the name of your site.

Here are the basic operating instructions of the HTML screen:

Click on “Load Local Files” button. You can load all of them or just select the ones you want to display.

Globe:

Bottom right of the globe is the “Full Screen” button. This system is best viewed in this mode.

Bottom left of the globe is your time controls. You can change the time line anyway you like. Transactions will appear on the globe (blue balloon) based upon the date and time.

Click on the ? for instruction on mouse controls.

Clicking on a label will zoom to that chart.

Clicking on a transaction (blue balloon) will zoom to that chart and highlight the transaction details.

Clicking on the little camera in the top left corner of the transaction details; will zoom to the address.
While the transaction details are open; the camera will always “LookAT” that address when you pan around. Close the transaction details to return to movement of the globe.

The Chart Area:

Clicking on a chart will zoom the globe the corresponding item.
Clicking on a transaction (small box) will zoom the globe and display the transaction details.

Chart Controls:

Left click + drag = rotate

Right click + drag = left, right, up, down

Scroll wheel = zoom in/out

Conclusion:
This project will drastically improve the quality of “Data Presentation” by bringing together the best of both 3D worlds used in today’s technology.

I look forward to the day when all of this functionality is incorporated into CesiumJS and THREEjs masters.




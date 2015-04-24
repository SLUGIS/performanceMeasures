#How to Update Performance Measures Map
#####This map was produced using the annual incident data from Bill Winter and filtered by Greg Alex.  It also relies on a layer called 'atoms_dt' that categorizes areas as either *Urban*, *Suburban*, *Rural*, *Remote* or *Undeveloped* based on total population and population density.  This layer is subject to change as time goes on.  

###Steps  
1.  Recieve incident spreadsheet from Bill Winter and Greg Alex.  

2.  Filter out First O Scene and Balance of Alarm using this code:  
`=IF(A2<>A1,"FIRST",IF(F1="FIRST","SECOND",IF(F1="second","THIRD",IF(F1="third","FOURTH","N/A"))))`  

3.  Save this file out as a CSV.  

4.  Open the CSV in QGIS and plot it using the LAT(y) and LON(x) columns.  

5.  Save out shapefiles of both the First On Scene and Balancae of Alarm Calls.   

6.  Using Join by Location in QGIS join each of the two new layers with 'atoms_dt'.  This will merge the category field wit the incidents.  

7.  Following Joe's example determine the pass/fail percentage for each category.  

8.  Archive former FOS and BOA incident data.  

9.  Strip out all of the fields from your shapefiles except: DATE, TIME, INCIDENT, TYPE, DSP_TO_ONS, UNIT.  Make sure they appear in the attribut table in this format too.  USe the Table Manager plugin in QGIS to rename and reorder them.  

10.  Style the new incident data    
`FOS = black circle w/white outline, size=5.0, outline width=0.4`   
`BOA = white circle w/black outline; size=5.0, outline width=0.4`  

11.  Using qgis2leaf export the map to the desktop.  The transparency will not render for the polygon layers and it will not look exactly like the live map.  This is because qgis2leaf still can't handle some styling options.  Don't worry about this as you only need to replace the current FOS and BOA layers with your new ones that are in the `/data` folder within your newly exported folder on the desktop.  

####¡¡¡Test it on a local copy first to ensure it is working before you commit it to the gh-pages branch!!!  
Simply copy and replace the `exp_FOS.js` and `exp_BOA.js` into the matching folder of your local copy of the GitHub repo to be sure it is working.  Then replace the existing `exp_FOS.js` and `exp_BOA.js` layers in the gh-pags branch of the **performanceMeasures** repo.

https://slugis.github.io/performanceMeasures

#How to Update Performance Measures Map
#####This map was produced using the annual incident data from Bill Winter and filtered by Greg Alex.  It also relies on subsets of a layer called 'ServiceLevelAreas' that categorizes areas as either *Urban*, *Suburban*, *Rural*, *Remote* or *Undeveloped* in accordance with the [Strategic Plan specifications](http://www.calfireslo.org/Documents/Plans/FINALstratPlan%28reduced%29.pdf#page=165 "Service Level Decision Model").  This layer is subject to change as time goes on and can be found in the ServiceLevelAreas.gdb.  

###Steps  
1.  Recieve monthly incident summary spreadsheet from Bill Winter and Greg Alex.  

2.  In Excel filter out First On Scene and Balance of Alarm incidents using this code in a new column:  
`=IF(A2<>A1,"FIRST",IF(F1="FIRST","SECOND",IF(F1="second","THIRD",IF(F1="third","FOURTH","N/A"))))`  

3.  Save this file as a CSV.  

4.  Open the CSV in QGIS and plot it using the YCOORD(latitude) and XCOORD(longitude) columns.  

5.  Save shapefiles of both the First On Scene and Balance of Alarm incidents.   

6.  Using Join Attributes by Location in QGIS (Vector->Data Management Tools->Join Attributes by Location) join each of the two new layers with 'ServiceLevelAreas'.  This will merge the category field with the incidents.  

7.  Following [Joe's example](https://gist.github.com/oeon/c3e67e745f78da4b2a11 "Strategic Plan GIS Notes") determine the pass/fail percentage for each category.  

8.  Archive former FOS and BOA incident data in `/archivedIncidents`.  

9.  Strip out all of the fields from your FOS and BOA shapefiles except: DATE, TIME, INCIDENT, TYPE, DSP_TO_ONS, UNIT.  Make sure they appear in the attribute table in this order too.  Use the [Table Manager plugin](https://plugins.qgis.org/plugins/tablemanager/ "Table Manager plugin") in QGIS to rename and reorder them.  

10.  Style the new incident data in QGIS:      
`FOS = black circle w/white outline, size=5.0, outline width=0.4`   
`BOA = white circle w/black outline; size=5.0, outline width=0.4`  

11.  Use [qgis2leaf](https://plugins.qgis.org/plugins/qgis2leaf/ "qgis2leaf") (Web->qgis2leaf) to export the map to the desktop.  If you open the `index.html` the transparency will not render for the polygon layers and it will not look exactly like the live map.  This is because qgis2leaf still can't handle some styling options.  Don't worry about this as you only need to replace the live FOS and BOA layers in the `\data` folder of the **performanceMeasures** repo.  

12.  Clone this **performanceMeasures** repo to your desktop.  Copy and paste your newly exported FOS and BOA layers into the `\data` folder in this repo.

##BEFORE COMMITTING CHANGES  

####¡¡¡Test it by opening the index.html in a browser  first to ensure it is working before you commit it to the gh-pages branch!!!    
--------------------------------------------------------------------------------------------------------------------------

###Statistics Graph  
The statistics graph is made using [Plotly](https://plot.ly/ "Plotly") under a `slugis` account with standard email and password credentials.  The graph is a stacked bar chart.  Follow these steps to create the chart:  

1.  Create a new grid under the Workspace tab in Plotly.  

2.   Set it up like this table:  

|First On Scene|Name|Balance of Alarm|Name2|Standards
|----------|-------|-------------|-----|-----------
|  % |   Urban Pass   |   %   |  Urban Pass    |  90     
|  % |   Suburban Pass|   %   |  Suburban Pass |  90    
|  % |   Rural Pass   |   %   |  Rural Pass    |  85 
|  % |   Remote Pass  |   %   |  Remote Pass   |  80   

*  You will need to fill in the percentages for FOS and BOA from your previous calculations (*Step 7*).

4.  Select First On Scene(*y*) and Name(*x*) as blue columns.  

5.  Select Balance of Alarm(*y*) and Name2(*x*) as green columns.  

6.  Select Statistics(*y*) as any color column.  

7.  Make sure both colors are being represented as bar charts and then create the bar chart.  

8.  Now you can tweak the layout and add *%* as a suffix for the axes.  

9.  Save the graph and click the Share button to get the link.  Replace the existing links in the `index.html` for `function showGraph` at line 598.

You can use the map widget as a black box, stand-alone piece of native JavaScript along with your own JavaScript.  You can also use the use the code as part of a GWT project as a pre-built library.  And finally you can grab the Java source, add it to your own GWT project and hack it up for your own use.


# Using the widget with your own JavaScript code. #

You'll need the olmapwidget.1.1.tar.gz file and a copy of the [OpenLayers](http://openlayers.org) JavaScript code (we use OL 2.10).  To install:
  1. Extract the tar file somewhere in the document root of your Web server, ($TOMCAT\_HOME/webapps/ROOT works just fine as a place to experiment).
  1. Add OpenLayers to the JavaScript/frameworks/OpenLayers directory the stub of which appears after your extract the tar file.  For example, to install in you Tomcat root:
    1. tar -xvzf OpenLayers-2.10.tar.gz
    1. cd OpenLayers-2.9.1
    1. cp OpenLayers.js $TOMCAT\_HOME/webapps/ROOT/JavaScript/frameworks/OpenLayers/.
    1. cp -R img/ $TOMCAT\_HOME/webapps/ROOT/JavaScript/frameworks/OpenLayers/.
    1. cp -R theme/ $TOMCAT\_HOME/webapps/ROOT/JavaScript/frameworks/OpenLayers/.
    1. Load your page.  For example: http://olmapwidget.appspot.com/OLMapWidget/mapwidget.html
    1. Using mapwidget.html as an example use the widget for your own purposes.

# Using the widget in your own GWT project. #

You'll need the olmapwidget.1.1.jar, olmapwidget\_css\_images.1.1.tar.gz and the gwt-openlayers-client-0.5.jar. The jar file has the map widget you can add to your own GWT widgets.  I'm going to assume you have or will create a GWT project using the Eclipse plug-in. If not, your on your own.  Sorry.  To get going with GWT:
  1. Go to an existing GWT project or start a new one.
  1. Add olmapwidget.1.1.jar and gwt-openlayers-client-0.5.jar to your build path.
  1. Put the JavaScript, css and images you need somewhere in your document hierarchy.  (You'll need to refer to the JavaScript in the HTML page that loads you map widget as described in step 6).
```
cd $TOMCAT_HOME/webapps/ROOT
tar -xzvf olmapwidget_css_images.1.1.tar.gz
```
  1. Inherit the OLMapWidget and GWT-OpenLayers modules in your module definition.
```
  <inherits name="com.weathertopconsulting.olmapwidget.OLMapWidget"/>
  <inherits name='org.gwtopenmaps.openlayers.OpenLayers'/>
```
  1. In the EntryPoint class or in some widget create a map and initialize the data extent and set the tool:
```
import com.weathertopconsulting.olmapwidget.client.map.OLMapWidget;
public class MapExample implements EntryPoint {
    OLMapWidget mapWidget = new OLMapWidget();
    	public void onModuleLoad() {

		mapWidget.setDataExtent(-90, 90, -180, 180, 1);
		mapWidget.setTool("xy");
                RootPanel.get().add(mapWidget);
        }
}
```
  1. Reference all the underlying JavaScript and css in the HTML page that loads your entry point class.
```
    <script type="text/javascript" language="javascript" src="JavaScript/frameworks/OpenLayers/OpenLayers.js"></script>
    <script type="text/javascript" language="javascript" src="JavaScript/frameworks/OpenLayersExtensions/DrawSingleFeature.js"></script>
    <script type="text/javascript" language="javascript" src="JavaScript/frameworks/OpenLayersExtensions/HorizontalPath.js"></script>
    <script type="text/javascript" language="javascript" src="JavaScript/frameworks/OpenLayersExtensions/VerticalPath.js"></script>
```
  1. Either debug in hosted mode or compile and deploy your GWT code with the map widget included.  A GWT version of the widget is here: http://olmapwidget.appspot.com/MapExample.html.  (Note: there are no event listeners for the moves and features being added like in the native JavaScript version.  I didn't need them in my GWT project.  I might add them later.)

# Build the map widget from source and modify it for fun and profit. #

The source code for my part of the map widget (not the GWT-OpenLayers integration) is hosted in the Google code project.  The process to get going is essentially the same as what is described above for using the binary distribution, but instead of including the olmapwidget.1.1.jar in your build path, you'll have the source you pulled from this site.
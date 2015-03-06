# Storytelling from Space: Tools/Resources

This list of resources is all about acquring and processing aerial imagery. It's generally broken up in three ways: how to go about this in Photoshop/GIMP, using command-line tools, or in GIS software, depending what's most comfortable to you. Often these tools can be used in conjunction with each other.

## Acquiring Landsat & MODIS

### Web Interface
* USGS Earth Explorer - Browser and data access (create a login)  
  <http://earthexplorer.usgs.gov/>
  - Landsat archive
  - Many other products, like aerial/orthophotography
    
 * GLOVIS (Java/Firefox required)  
 <http://glovis.usgs.gov/?popout=TRUE>
 	- Similar data different interface
 	
 * NASA WorldView - Browser and data access  
 <https://earthdata.nasa.gov/labs/worldview/> 
 
 * NASA GIBS - MODIS tileserver
 <https://wiki.earthdata.nasa.gov/display/GIBS/Global+Imagery+Browse+Services+%28GIBS%29+Home>

 * NASA Near-Real Time satellite data links
 <https://earthdata.nasa.gov/data/near-real-time-data/rapid-response>

 * Google Earth Engine
 <https://earthengine.google.org/>

 * Landsat 8 Acquisition Calendar 
 <https://landsat.usgs.gov/tools_L8_acquisition_calendar.php>

### Scripting
* Landsatutil (Development Seed)  
<http://www.developmentseed.org/blog/2014/08/29/landsat-util/>
<https://github.com/developmentseed/landsat-util>

* Fetch from Google Earth Engine   
<https://gist.github.com/briantjacobs/ab695cc15775df9570ed>

 * Landsat 8 data on AWS
 <http://aws.amazon.com/public-data-sets/landsat/>

 * Landsat data on Google Storage 
 <https://console.developers.google.com/storage/browser/earthengine-public/landsat/>

## Processing Landsat

### Background 
* Landsat 7/8 bands and combinations  
<http://blogs.esri.com/esri/arcgis/2013/07/24/band-combinations-for-landsat-8/>


### Photoshop

* How To Make a True-Color Landsat 8 Image (Rob Simmon, NASA)
<http://earthobservatory.nasa.gov/blogs/elegantfigures/2013/10/22/how-to-make-a-true-color-landsat-8-image/>

* Processing Landsat 8 (Tom Patterson, National Park Service)  
<http://www.shadedrelief.com/landsat8/introduction.html>

* Avenza Geographic Imager - Expensive but excellent plugin. Allows you to much of what GDAL does (plus things it can't) and preserve geographic metadata.
<http://www.avenza.com/geographic-imager>

* Without Geographic Imager, you need GDAL tools if you want to  preserve geographic metadata:  
	
	Dump metadata from a file before messing with it in Photoshop
	```
listgeo -no_norm original.tif > original.geo
	```
	Add the metadata back after saving back out
	```
geotifcp -g original.geo modified.tif modified_geotiff.tif
	```

### GIMP
	
* Merging bands into RGB in GIMP  
<http://edwardmjohnson.wordpress.com/using-landsat-imagery-in-gimp/>
* Pansharpening in GIMP (translate from Portuguese!)  
<http://www.processamentodigital.com.br/2013/11/17/gimp-2-8-fusao-de-imagens-landsat-8-em-pseudo-cores-naturais/>

	


### Scripting

##### GDAL - Geospatial Data Abstraction Library & ImageMagick (command-line photoshop)

*  GDAL: ogr2ogr (for vector) and GDAL (for raster)

	```
brew install gdal --enable-unsupported --with-postgres
	```
	*note: "--enable-unsupported" allows you to install third party drivers, necessary for proprietary formats like MrSID and FileGDB. See this <http://briantjacobs.com/mrsid-gdal-homebrew/>*
		
*  ImageMagick, aka `convert`
	
	```
brew install imagemagick
	```
	
* **GDAL cheatsheet - Derek Watkins (NYTimes)** ← *see "Raster Operations"* 
<https://github.com/dwtkns/gdal-cheat-sheet>
	
* **Processing Satellite Imagery (Mapbox)** ← *extra helpful* 
  <https://www.mapbox.com/foundations/processing-satellite-imagery/>
  
* Dan's GDAL scripts  
<https://github.com/gina-alaska/dans-gdal-scripts>
* Pansharpening Landsat 7 with Dan's scripts
<http://blog.remotesensing.io/2013/04/pansharpening-using-a-handy-gdal-tool/>	
  
* Convert Landsat 8 GeoTIFF images into RGB pan-sharpened JPEGs.  
<https://gist.github.com/briantjacobs/48320e59954ee7ec5cd1>

* Charlie Lloyd's (Mapbox) Rake Task
<https://gist.github.com/briantjacobs/0d3f9a62fc7ca115ee5b>

	
	
##### Orfeo - More advanced. Do things like atmospheric correction and NDVI.

* Pansharpening with Orfeo 
* <https://www.mapbox.com/blog/pansharpening-satellite-imagery-openstreetmap/>
 

### GIS

##### QGIS - Open Source alternative to ArcGIS
	
* Install  	

	```
brew tap homebrew/science	
brew install qgis24 --with-grass7 --with-orfeo	
# May need: <https://xquartz.macosforge.org/landing
# May also need:	
sudo pip install psycop2	
echo 'export PYTHONPATH=$PYTHONPATH:/usr/local/lib/python2.7/site-packages' >> ~/.bash_profile
	```		
	
* QGIS 2.0: Composition Color RGB for Landsat-8 (translate from Portuguese) 
<http://www.processamentodigital.com.br/2013/11/23/qgis-2-0-composicao-colorida-rgb-para-imagens-landsat-8/>
		

## Creating Web Imagery

* GDAL2Tiles  
<http://www.gdal.org/gdal2tiles.html>

* MapTiler
<http://www.maptiler.org/>

* TileMill  
<https://www.mapbox.com/tilemill/>

* SimpleTiles / SimplerTiles (Ruby)
<http://propublica.github.io/simple-tiles/>
<http://propublica.github.io/simpler-tiles/>


## Storytelling Tools

* JuxtaposeJS - Compare two images  
<http://juxtapose.knightlab.com/>

* Leaflet (see tileLayer or imageOverlay)  
<http://leafletjs.com/>
 
* Leaflet.Sync   
<https://github.com/turban/Leaflet.Sync>
 
* Google Earth   
<https://www.google.com/earth/>

* Google Earth Tutorial for GeoTiff  
<http://www.google.com/earth/outreach/tutorials/importgis.html>


## Storytelling from Space, In the wild
* Losing Ground (ProPublica / The Lens)  
<http://projects.propublica.org/louisiana>

* Disappering Mississppi Delta (SkyTruth)  
<http://blog.skytruth.org/2014/09/disappearing-mississippi-delta-1972-2014.html>

* Long Swath  
<http://earthobservatory.nasa.gov/Features/LDCMLongSwath/>  
* Long Swath Gigapan:   
<http://gigapan.com/gigapans/9741ab68dda60a8b05b9c1bfce147500>

* NYTimes: A Rogue State Along Two Rivers  
	<http://www.nytimes.com/interactive/2014/07/03/world/middleeast/syria-iraq-isis-rogue-state-along-two-rivers.html>
* NYTimes: Assessing the Damage and Destruction in Gaza
	<http://www.nytimes.com/interactive/2014/08/03/world/middleeast/assessing-the-damage-and-destruction-in-gaza.html>
	
* NYTimes: ISIS in Maps and Photos 
	<http://www.nytimes.com/interactive/2014/06/12/world/middleeast/the-iraq-isis-conflict-in-maps-photos-and-video.html>
	
* Monitoring Oil Reserves from Space  
<https://www.mapbox.com/blog/Monitoring-oil-reserves-from-space/>

* Animated Gifs of Earth over time (Google Earth Engine)
<https://plus.google.com/b/106191537604091348855/photos/+GoogleEarth/albums/5875822979804092129>

* Hurricaine Sandy before/after  
<http://oceanservice.noaa.gov/news/weeklynews/nov12/ngs-sandy-imagery.html>

* The Continuing Crisis in Northern Iraq
<http://blog.amnestyusa.org/middle-east/moving-on-from-the-mountain-the-continuing-crisis-in-northern-iraq/>

* Counting Whales from Space
<http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0088655>

* Using Repeat Satellite Imagery to Track Tank Movements
<http://sciience.tumblr.com/post/111780500452/using-repeat-satellite-imagery-to-track-tank>

* Gaza: X-ray of a disaster
<http://www.letemps.ch/interactive/2014/gaza-radiographie/>

* Google Earth Engine   
<https://earthengine.google.org/#intro>

## Misc Geospatial Tools

* Web interface for CS2CS, quickly convert coordinates  
<http://cs2cs.mygeodata.eu/>

* Find the EPSG from WKT from gdalinfo  
<http://www.prj2epsg.org/search>

* Geojson.io - Draw geographic things, get info and export  
<http://geojson.io/>

* Noah Veltman's geotools - Easily get bounding boxes and such
<http://dev.noahveltman.com/geotools/>

## Bonus

* USGS land cover classification data
 - 1992-2011: <http://www.mrlc.gov/finddata.php>
 - 70's: <http://pubs.usgs.gov/ds/2006/240/>

* Installing Open Source geographic software  
<https://github.com/nvkelso/geo-how-to/wiki/Installing-Open-Source-Geo-Software:-Mac-Edition>
	
* Creating the Blue Marble  
<http://earthobservatory.nasa.gov/blogs/elegantfigures/2011/10/06/crafting-the-blue-marble/>

* Rainbow planes  
<http://booktwo.org/notebook/rainbow-plane/>
<https://www.flickr.com/photos/stml/sets/72157637938061015/>

* Global Forest Change from Lndsat and MODIS
<http://www.globalforestwatch.org/>
<http://earthenginepartners.appspot.com/science-2013-global-forest/download_v1.1.html>

* Carlton Complex Wildfire, Washington  
<http://earthobservatory.nasa.gov/NaturalHazards/view.php?id=84169>
<http://www.dailymail.co.uk/news/article-2705138/Aerial-photos-true-scale-devastation-Washington-states-largest-wildfire-burned-nearly-400-square-miles-destroyed-150-homes.html>
	
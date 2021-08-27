gdalinfo 2018_Ortho_3857_nodata_255_jpg_60.tif -stats --config GDAL_PAM_ENABLED TRUE

https://support.esri.com/en/technical-article/000019013

Description
A map tile package (.tpk) created using the Create Map Tile Package tool contains a set of tiles (images) from a map or raster dataset. In some instances, when opening a map tile package and zooming to certain levels in ArcGIS Pro, some map tiles are not displayed.

Cause
This is a known issue. The Create Map Tile Package tool returns incomplete tiles when the input raster does not have pyramids and statistics.

Solution or Workaround
Use the Build Pyramids And Statistics tool to build pyramids and calculate statistics for the raster dataset before using it to create a map tile package.

https://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html

https://cran.r-project.org/web/packages/slippymath/slippymath.pdf

http://www.liedman.net/tiled-maps/

started at 11:15 100% cpu 1.15 TB tif

JPG compression is about 1/3 the size of LZW compression

Cloud Optimized GeoTiff output from Copy Raster

gdalwarp -t_srs EPSG:3857 -s_srs "+proj=lcc +lat_0=38 +lon_0=-82.5 +lat_1=40.0333333333333 +lat_2=38.7333333333333 +x_0=600000 +y_0=0 +ellps=GRS80 +towgs84=-0.9956,1.9013,0.5215,0.025915,0.009246,0.011599,-0.00062 +units=us-ft +no_defs" -r average -multi -srcnodata 255 -of VRT g:\data\imagery\_testing\gas_dept_3in.tif g:\data\imagery\_testing\gas_dept_3in_3857.tif.vrt

https://www.cogeo.org/developers-guide.html

gdal_translate gas_dept_3in_3857.tif.vrt gas_dept_3in_3857_cogt.tif -of COG -co COMPRESS=JPG

http://cog-validate.radiant.earth/html

1. Download Rasters

Load Raster data into Desktop GIS and check the accuracy with GPS points.

2. Build Mosaic

gdalbuildvrt FAI_2018_3IN_MOSAIC.vrt \\192.168.168.22\2018_Orthos\TIFFS\TIFFS\*.tif

3. Create the Cloud Optimized GeoTIFF

gdal_translate FAI_2018_3IN_MOSAIC.tif FAI_2018_3IN_COG.tif -a_srs EPSG:3735 -of COG -co COMPRESS=JPEG -co BIGTIFF=YES -co OVERVIEWS=IGNORE_EXISTING -co QUALITY=85

This is the file that our desktop users will load onto their machines.
The COG format is purpose built for use over low bandwidth connections, so it is perfect for using over a city-wide file-share network. In testing it is faster than loading a mosaic in our enterprise SQL database.

This will create a COG approximately 10% the size of the raw TIFFs.

4. Create the Virtual Raster in WebMercator

This VRT will be used as the input for the raster tiles. 
Note that the best outcomes came from exporting a TIFF from Arc* in 3857, but the difference is negligible.

Load the raster_3857.vrt into desktop GIS. Examine the visual quality. Check the accuracy vs data exported into WebMercator from ArcPro using the default transformation (WGS 1984 ITRF00 <> NAD 1983)

Use one of the tiling methods to create the raster tiles. First we will use gdal2tiles then we will use Generate XYZ Tiles (mbtiles).

"...the horizontal discrepancy between the NAD 83 (CORS93) and NAD 83
(HARN) positions for a control point is almost always less than 10 cm, and the horizontal
discrepancy between any two NAD 83 (CORSxx) positions for a control point is almost
always less than 2 cm." ~ https://www.fs.fed.us/GRAIP/downloads/GPS/Understanding%20the%20Evolution%20of%20WGS%201984%20and%20NAD%201983%20(Rev2).pdf

https://desktop.arcgis.com/en/arcmap/latest/map/projections/pdf/geographic_transformations.pdf

getting errors with imagery shifted in weird ways when the webmercator vrt is created, but not when the COG is exported from arcmap




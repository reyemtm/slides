gdalinfo 2018_Ortho_3857_nodata_255_jpg_60.tif -stats --config GDAL_PAM_ENABLED TRUE

https://support.esri.com/en/technical-article/000019013

Description
A map tile package (.tpk) created using the Create Map Tile Package tool contains a set of tiles (images) from a map or raster dataset. In some instances, when opening a map tile package and zooming to certain levels in ArcGIS Pro, some map tiles are not displayed.

Cause
This is a known issue. The Create Map Tile Package tool returns incomplete tiles when the input raster does not have pyramids and statistics.

Solution or Workaround
Use the Build Pyramids And Statistics tool to build pyramids and calculate statistics for the raster dataset before using it to create a map tile package.
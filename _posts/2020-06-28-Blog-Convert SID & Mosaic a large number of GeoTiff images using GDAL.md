---
layout: post
title: Underconstruction
excerpt: Sample bash script using GDAL
created: 06/29/2020, 00:00:24
tags: [GDAL, Mosaic, SID, Bash script, Geotiff]
comments: false
category: blog
---

Sometimes raw raster data coming with raw format which does not include any projection infomation in metadata. Using such raw data is difficult for further processing; therfore, it could be very useful to convert them to the format such as Geotiff which is usable for different purposes. On the other hand, due to large valume of the high resolution raster dataset, they are distributed in the tiles so that each tile covers only special zone. Making a mosaic out of several tiles to further analysis is compulsary.One of the Geospatial Data Abstraction Library is a computer software library for reading and writing raster and vector geospatial data formats, and is released under the permissive X/MIT style free software license by the Open Source Geospatial Foundation is [GDAL](https://gdal.org/). This library includes tools for both raster (gdal_translate, gdal_warp etc.) & vector (ogr2ogr, ogrmerge etc.). However, it is well-known for its tools for dealing raster datasets. In this sample code, this powerful library was used to firstly, convert the [SID (MrSID – Multi-resolution Seamless Image Database)](https://gdal.org/drivers/raster/mrsid.html) to [GeoTiff](https://gdal.org/drivers/raster/gtiff.html) & creation of mosaic out the converted raster tiles. In the end, general overview was created frrom mosaic rasters.

![One tile](./master/images/tile_lt.JPG")

# Conversion of SID to GeoTiff

in the first step, it is required to use loop in bash to read and conver each SID tile to GeoTiff one.
```BASH
#! /bin/bash
 for filename in *.sid 
do
gdal_translate -a_srs EPSG:3346 -of GTiff -co COMPRESS=DEFLATE -co ZLEVEL=9 $filename $(pwd)/tiff/${filename%.*}.tif
done
```
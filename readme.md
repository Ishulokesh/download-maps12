Download Mexican maps- One stop solution for every map in Mexico
=====================

You'll need to have __wget__, __gdal__, and __R__ installed to download and create the maps. Then just run

 ```
$ make
 ```

If something went wrong with the downloading, use:

 ```
$ make clean
 ```

You can also use a docker image to run the program

```
docker pull diegovalle/download-maps12
# shared directory to store the output
mkdir -p /tmp/download-ine2010 
docker run -v /tmp/download-ine2010:/download-maps12/map-out -i -t diegovalle/download-maps12
```

and run make within the container

Since the scripts download a whole bunch of maps it may take a while to finish

### Output

In the map-out directory you'll find

* distritos: Shapefile of the electoral distritos (districts)
* secciones-inegi: Shapefile of electoral secciones (precincts) __with both the ife and inegi codes for the municipalities each seccion belongs to__
* estados: Shapefile of the Mexican states
* localidades: Shapefiles of the rural localities and the polygons of the urban ones
* municipios: Shapefile of the counties of Mexico
* rdata-secciones: serialized secciones (precincts) map as an R object
* otros: All the new shapefiles the INEGI added in 2017 (localidades, colonias, escuela, etc)

Since the IFE uses a different coding standard for the municipalities of Mexico than the INEGI, I've recoded the municipality codes so that they match the ones the INEGI uses. 

 ```
Ecatepec, México according to the INEGI is 15 033, while according to the IFE it's 15 034
Guadalajara, Jalisco according to the INEGI is 14 039, while according to the IFE it's 14 041
```

These codes are only available for the secciones electorales (precincts) shapefile and they are contained in the variables:

* MUN_INEGI: The inegi municipio codes
* MUN_IFE: The original ife municipio codes that came with the file

The codebook for the the census data that comes with the shapefiles is in the FD_SECC_IFE.pdf file and the ife and inegi codes are in the ife.to.inegi.csv file

Author:

[Diego Valle-Jones](http://www.diegovalle.net)

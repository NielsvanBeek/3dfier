When preparing the BGT GML files as input for 3dfier, the BGT_conversion.bat batch script can be used. 
The script requires GDAL >2.0 to perform the filtering and conversion.
OGR is used to only select polygonal geometries and stroke CurvePolygons, it also filters the history of objects by selecting those of which the 'eindregistratie' is not set.

Usage:
- Extract the BGT GML files in a folder
- Copy all GFS files from "BGT gfs files" into the same folder
- Make sure all GFS files are newer then the GML files (assure this by editing all GFS files, add/remove a character, save, restore character, save)
- Run BGT_conversion.bat (or the commands within if on Linux/Mac)
- Use generated sqlite files as input to 3dfier

Usage Windows:
- Extract the BGT GML files in a folder
- Copy all GFS files from "BGT gfs files" into the same folder
- Run BGT_conversion_full.bat (this script is a combination of BGT_fix_srs_win.bat, BGT_fix_gfs_date_win.bat and BGT_conversion.bat)
- Use generated sqlite files as input to 3dfier

Known issues:
* ogr2ogr fails with message on 'eindregistratie no such attribute'; remove the 'eindregistratie == NULL' from the command. This happens when the GML file does not contain any historical objects with an 'eindregistratie' attribute.
* ogr2ogr fails with 'ERROR 1: Did not get at least 3 values or invalid number of set of coordinates'; in bgt_begroeidterreindeel.gml and bgt_onbegroeidterreindeel.gml replace all '<gml:posList>' strings with '<gml:posList srsDimension="2">'. Not all 'kruinlijn' geometries are writting with the srsDimension argument which ogr does not accept.
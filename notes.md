### Processing Steps  

1. simplfy geometry to 0.25 tolerance  
2. select & export buildings greater than 500sqft  
3. re-project data to epsg:4326; wgs 84  
4. count points in polygon (addr in bldg)[qgis]  
5. count points in polygon (poi in bldg)[qgis]
6. join attributes by location (poi > bldg)
7. remove poi attributes where poi point count != "1"
8. delete poi attribute columns except "name", "type"
9. join attributes by location (addr > bldg)
10. remove address numbers attributes where addr point count != "1" (leave street names)
11. delete unnecessary columns
12. calculate building [ptype2] codes to text -> new [ptype] column (readme)
13. calculate address [type] codes to text -> new [ptype] column (readme)
14. calculate street prefix abbr to long-from
15. calculate road type abbr to long-form (usps suffixes)
16. concatenate street names
17. calculate city = york county
18. calcualte state = virginia
19. spatial join with zipcodes
20. join ```osm_schema.shp``` fields & calculate
21. final column clean-up

###Building Footprints  
Buildings will be simplified to ```0.25``` using common geometry simplification tools. Attributes from the ```PTYPE2``` column will be mapped to OSM tags:  

| Code  | Type | Count |  Note |
| ------------- | ------------- |------------- |------------- |
| 1  | Residential  | 19299  | House  |
| 2  | Garage/Outbuilding/Shed  | 12973  | Only Map Over 300sqft?  |
| 3  | Business/Commercial  | 1454  | Commercial  |
| 4  | Public (School, Fire Station, Church, Pump Station)  | 363  | Will Split By Name If Possible  |
| 5  | Federal  | 1006  | Will Split By Name If Possible  |
| 6  | Timeshare/Hotel/Campground  | 293  | Will Split By Name If Possible  |
| 7  | Marine Structure (boat houses – incomplete)  | 22   | Will Not Map   |
| 0  | Outside County Boundary  | 3  | Will Not Map   |

###Addresses 
Single points within building footprint will be spatially joined to building footprints and mapped to common address tags. Additional guidance from county GIS department:  
```"... The RECORD_ADDR field signifies if the point represents the parcel; points with a value of 0 mean they are additional addresses, like stores in a strip mall or individual apartment units.  I’ve also included our Common Places layer which is similar to a Points of Interest layer.."```  
Attributes from the ```ADDRTYPE``` column will be mapped to OSM tags:  

| Code  | Type | Count |  Note |  
| ------------- | ------------- |------------- |------------- |
| 1  | Residential  | 25809  | Single Pt Spatial Join  |
| 2  | Commercial  | 1952  | Single Pt Spatial Join  |
| 3  | Utility  | 200  | Will Not Map  |
| 4  | Vacant/Not Needed  | 3974  | Will Not Map  |
| 5  | Other  | 258  | Will Not Map  |
| 6  | Public/Semi-Public  | 158  | Single Pt Spatial Join  |
| 7  | Timeshare/Hotel/Campground  | 1628  | Single Pt Spatial Join   |
| 8  | Common Area  | 676  | Will Not Map  |

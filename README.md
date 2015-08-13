# yorkcounty_OSM_imports
Repository for getting York County GIS layers imported to OpenStreetMap  

![](https://raw.githubusercontent.com/jonahadkins/yorkcounty-OSM-imports/master/york.jpg)

York County, Virginia GIS department has provided building footprints, address points, and points of interest for importing into OpenStreetMap after a request via email. The data was graciously provided as is, license free, and at no cost by the GIS department with the note:  
```"..York County’s FOIA policy still allows our department to charge for GIS data, however we have decided to provide some GIS data to not for profit organizations.."```  

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


# GmE 221 - Laboratory Exercise 1

## Overview
This laboratory sets up a spatial analysis environment using Python and PostGIS and performs a parcel-landuse overlay analysis.

## Environment Setup
- Python 3.x
- PostgreSQL with PostGIS
- GeoPandas, SQLAlchemy, psycopg2

## How to Run
1. Activate the virtual environment
2. Run 'main.py' to test the database connection
3. Run 'overlay.py' to compute landuse percentages

## Outputs
- PostGIS table: 'parcel_landuse_percentage'
- Visualization in QGIS

## Reflections
### D.4 Reflection: Interpreting the Database Connection
- The create_engine function from the sqlalchemy library, in combination with the gpd.read_postgis function of GeoPandas, is a powerful way to establish a connection between the code and the repository of the data. With this, it already eliminates the need of manual uploading of static files and the hassle of finding the directory or folder of needed data. In a computational perspective, the engine serves as the bridge from the database to the computational environment.

### E.7 Reflection: Overlay Analysis Milestone
- The sql_overlay query allows the implementation of multiple geoprocessing steps in one go. Instead of manually doing it in a GIS software wherein you click a button, generate an output, then use that secondary output to generate another output, before even reaching to your desired data is very tedious. Unlike using the geoprocessing algorithms available in PostGIS, wherein you just load the required data, establish the query, save your desired results to the database, all in one go.
- This is a very efficient and powerful way of answering spatial questions.

### F.3 Reflection: Interpreting Algorithm Output
- The algorithm aims to determine which land use does a parcel belong to. Most of the small parcels had 100% of their total area belonging in one land use category, while other parcels, such as the case for the parcel with a parcel_pin of 193-01-0016-001-01 wherein the entire lot was divided into four different categories: Buffer Zone (81.44%), Commercial Industrial Zone (30.67%), Residential Zone - Low Density (68.95%), and Residential Zone - Medium Density (0.87%). 
- There were parcels that had extremely low area percentages. This just means that there is a very tiny portion of their parcel that belongs to a different category other than the dominant one.
- The CRS choice affects the area computations and accuracy of the position of layers. In computing land area, it is required that the coordinate reference system is in a projected one so the units are linear (sqm, ha, acres, etc.) The geometry quality contributes to the quality of the resulting output. As they say, "garbage in, garbage out". In terms of scaling, If the number of parcels significantly increased, there might be a decrease in performance when executing the query, depending on the total number of resulting features.
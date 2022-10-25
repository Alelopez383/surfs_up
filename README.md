# Surfs Up
We are creating an analysis on the weather in Hawaii for a new shop Surf n´shake in the OAHU island. For that, we are using Pyhton, VS Code, SQLite and Flask.

## Precipitation Data

Analyzing precipitation levels and showing the cold, hard, data that backs up Oahu as the perfect place to surf. 

![image](https://user-images.githubusercontent.com/43974872/197577848-24525e63-36fd-4cd7-a65a-b910fb1df9d9.png)

 Oahu is a great location for the new surf shop. 
 
 ## Flask app
 We start our application with a test for the rooutes.
 
 ```

import datetime as dt
import numpy as np
import pandas as pd

import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine, func

from flask import Flask, jsonify

engine = create_engine("sqlite:///hawaii.sqlite")
Base = automap_base()
Base.prepare(engine, reflect=True)

Measurement = Base.classes.measurement
Station = Base.classes.station

session = Session(engine)
app = Flask(__name__)
@app.route("/")
def welcome():
    return(
    '''
    Welcome to the Climate Analysis API!
    Available Routes:
    /api/v1.0/precipitation
    /api/v1.0/stations
    /api/v1.0/tobs
    /api/v1.0/temp/start/end
    ''')

@app.route("/api/v1.0/precipitation")
def precipitation():
   prev_year = dt.date(2017, 8, 23) - dt.timedelta(days=365)
   precipitation = session.query(Measurement.date, Measurement.prcp).\
    filter(Measurement.date >= prev_year).all()
   precip = {date: prcp for date, prcp in precipitation}
   return jsonify(precip)
   
```
 
 
 ![image](https://user-images.githubusercontent.com/43974872/197831761-1f4fbf6b-735d-4a98-9383-529498b52839.png)
 
 ### Route: Precipitation
 
 ![image](https://user-images.githubusercontent.com/43974872/197834906-1f244de9-5930-4f91-93c2-44743595011c.png)

### Route: Stations

![image](https://user-images.githubusercontent.com/43974872/197838173-7d216616-638e-4e0e-9919-76495d7a7c72.png)

### Route: Monthly Temperature

![image](https://user-images.githubusercontent.com/43974872/197849391-9b017f4d-7580-4f41-9954-74369984b8de.png)

### Route: Statistics

The next route report on the minimum, average, and maximum temperatures. In this case, during the month of june in 2017, the minimum temperature was 71° degrees; the maximun was 83° degrees and the monthly average temperature was 77.2° degrees.

![image](https://user-images.githubusercontent.com/43974872/197850774-5f548eb2-4a68-4cd4-949f-6c3efd49f5a3.png)

# Temperature trends for the Surf n' Icream Shop
We are doing an analysis temperature data for the months of June and December in Oahu, in order to determine if the surf and ice cream shop business is sustainable year-round.

## Summary Statistics for June

Doing the analysis temperature data for the month of June in Oahu, we found that minimum temperature is 64° degrees; the maximun is 85° degrees and the monthly average temperature is 75° degrees.

![image](https://user-images.githubusercontent.com/43974872/197855782-fc06acf0-8337-425a-a5c1-4e89836a255a.png)

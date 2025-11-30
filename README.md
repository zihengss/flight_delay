# Airline Delay Analysis Database

`airline_delay_analysis.db` is a SQLite database that integrates airline operation data, airport metadata, weather conditions, fuel prices, and stock performance to support comprehensive analysis of flight delays in the United States.

It contains the following tables:

1. `Airline` – core flight-level data
2. `Airports` – airport metadata
3. `Carriers` – airline company information
4. `Weather` – daily weather per city
5. `FuelPrice` – daily jet fuel price
6. `FuelIndex` – normalized fuel price index
7. `StockPrice` – airline-related stock data

---

# 1. Airline Table

Primary table containing one row per scheduled or operated flight.

## Location and Identification Columns

| Column              | Description                            |
| ------------------- | -------------------------------------- |
| `airline_id`        | Internal unique row ID.                |
| `FL_DATE`           | Flight date.                           |
| `OP_UNIQUE_CARRIER` | Airline carrier code (e.g., AA, DL).   |
| `OP_CARRIER_FL_NUM` | Flight number assigned by the carrier. |
| `ORIGIN_AIRPORT_ID` | Numeric ID for origin airport.         |
| `ORIGIN`            | Origin airport IATA code.              |
| `ORIGIN_CITY_NAME`  | Origin city name.                      |
| `ORIGIN_STATE_ABR`  | State abbreviation.                    |
| `ORIGIN_STATE_FIPS` | FIPS state code.                       |
| `ORIGIN_STATE_NM`   | Full state name.                       |
| `ORIGIN_WAC`        | World Area Code for origin.            |
| `DEST_AIRPORT_ID`   | Destination airport ID.                |
| `DEST`              | Destination airport IATA code.         |
| `DEST_CITY_NAME`    | Destination city name.                 |
| `DEST_STATE_ABR`    | Destination state abbreviation.        |
| `DEST_STATE_FIPS`   | Destination state FIPS code.           |
| `DEST_STATE_NM`     | Destination state name.                |
| `DEST_WAC`          | World Area Code for destination.       |
| `CRS_DEP_TIME`    | Scheduled departure time (HHMM).                      |
| `DEP_TIME`        | Actual departure time (HHMM).                         |
| `DEP_DELAY`       | Actual departure delay in minutes.                    |
| `DEP_DELAY_NEW`   | Departure delay with negative values clipped to zero. |
| `DEP_DEL15`       | 1 if departure delay is 15 minutes or more.           |
| `DEP_DELAY_GROUP` | Delay group category (15-minute bins).                |
| `DEP_TIME_BLK`    | Scheduled departure time block (e.g., "0600-0659").   |
| `CRS_ARR_TIME`    | Scheduled arrival time.                               |
| `ARR_TIME`        | Actual arrival time.                                  |
| `ARR_DELAY`       | Actual arrival delay in minutes.                      |
| `ARR_DEL15`       | 1 if arrival delay is 15 minutes or more.             |
| `ARR_DELAY_GROUP` | Arrival delay group category.                         |
| `ARR_TIME_BLK`    | Scheduled arrival time block.                         |
| `CANCELLED`           | 1 if the flight was canceled.                          |
| `CANCELLATION_CODE`   | Reason code (A=Carrier, B=Weather, C=NAS, D=Security). |
| `DIVERTED`            | 1 if the flight diverted to another airport.           |
| `CRS_ELAPSED_TIME`    | Scheduled elapsed time in minutes.                     |
| `ACTUAL_ELAPSED_TIME` | Actual elapsed time in minutes.                        |
| `AIR_TIME`            | Time spent in the air.                                 |
| `FLIGHTS`             | Number of flights (usually 1).                         |
| `DISTANCE`            | Flight distance in miles.                              |
| `DISTANCE_GROUP`      | Distance category (50-mile bins).                      |
| `CARRIER_DELAY`       | Delay caused by airline operations.              |
| `WEATHER_DELAY`       | Delay caused by weather conditions.              |
| `NAS_DELAY`           | Delay caused by the National Airspace System.    |
| `SECURITY_DELAY`      | Delay caused by security issues.                 |
| `LATE_AIRCRAFT_DELAY` | Delay caused by previous aircraft arriving late. |
| `DEP_DELAY_OVER15` | 1 if departure delay ≥ 15 minutes.   |
| `ARR_DELAY_OVER15` | 1 if arrival delay ≥ 15 minutes.     |
| `TOTAL_DELAY`      | Combined total delay.                |
| `ANY_DELAY`        | 1 if any delay condition is present. |

---

# 2. Airports Table

| Column         | Description          |
| -------------- | -------------------- |
| `airport_id`   | Unique airport ID.   |
| `airport_code` | Airport IATA code.   |
| `city_name`    | City of the airport. |
| `state_abbr`   | State abbreviation.  |
| `state_name`   | Full state name.     |

---

# 3. Carriers Table

| Column         | Description            |
| -------------- | ---------------------- |
| `iata_code`    | Airline code.          |
| `carrier_name` | Official airline name. |

---

# 4. Weather Table

| Column       | Description                       |
| ------------ | --------------------------------- |
| `date`       | Date of weather record.           |
| `t2m`        | Temperature at 2 meters (Kelvin). |
| `v10`        | Wind speed at 10 meters.          |
| `snc`        | Snow cover percentage.            |
| `sde`        | Snow depth equivalent.            |
| `city_name`  | City name.                        |
| `state_abbr` | State abbreviation.               |
| `state_name` | Full state name.                  |
| `lat`        | Latitude.                         |
| `lng`        | Longitude.                        |
| `t2m_C`      | Temperature in Celsius.           |

---

# 5. FuelPrice Table

| Column           | Description            |
| ---------------- | ---------------------- |
| `date`           | Date of record.        |
| `jet_fuel_price` | Jet fuel price in USD. |

---

# 6. FuelIndex Table

| Column           | Description                  |
| ---------------- | ---------------------------- |
| `date`           | Date of index.               |
| `jet_fuel_index` | Normalized fuel index value. |

---

# 7. StockPrice Table

| Column              | Description                            |
| ------------------- | -------------------------------------- |
| `stock_price_id`    | Unique row ID.                         |
| `date`              | Trading date.                          |
| `price`             | Closing price.                         |
| `open_price`        | Opening price.                         |
| `high_price`        | Highest trading price.                 |
| `low_price`         | Lowest trading price.                  |
| `volume`            | Number of shares traded.               |
| `change_percentage` | Percentage change from previous close. |
| `company_name`      | Company or ETF name.                   |
| `iata_code`         | Airline code (if applicable).          |

---


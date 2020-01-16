# Some basic stuff for collecting and analysing data from the TIER scooters 🛴

It stores the geopositions, battery level, state and some other information of every [TIER](https://tier.app) scooter inside Paderborn (the region can be [configured](https://github.com/myxor/TierScooterAnalysis/blob/master/config.example.ini#L2)) into a local SQLite database.
It currently provides a basic nodejs RESTful API and two HTML pages to visualize the stored data.

## Screenshots

Here are some screenshots so you can see how it looks right now.

### Heatmap of all geopositions

![Heatmap of all geopositions](./screenshots/heatmap.png "Heatmap of all geopositions")


### Current positions of all vehicles and track of one vehicle

![Current positions of all vehicles and track of one vehicle](./screenshots/current_positions_and_track.png "Current positions of all vehicles and track of one vehicle")


## RESTful API

The node RESTful API currenctly provides three endpoints to request the stored data:

### get list of vehicles

#### get list of all vehicles

    GET http://localhost:3000/vehicles
    
#### get single vehicle filtered by internal id
    
    GET http://localhost:3000/vehicles?vehicle_id=34
    
#### get single vehicle filtered by id from TIER

    GET http://localhost:3000/vehicles?id=9cd68586-a1e9-48f6-8eb5-a39a25f59769

### get current positions

#### get list of all current positions

    GET http://localhost:3000/current
    
#### get current position of single vehicle filtered by internal id

    GET http://localhost:3000/current?vehicle_id=34
    
#### get current position of single vehicle filtered by id from TIER

    GET http://localhost:3000/current?id=9cd68586-a1e9-48f6-8eb5-a39a25f59769


### get the log

    GET http://localhost:3000/log
    
#### get the log of single vehicle filtered by internal id

    GET http://localhost:3000/log?vehicle_id=34



## Pre-requisites 🛠
* [Node](https://nodejs.org/en/download/)
* [Python3](https://www.python.org/downloads/)
* A modern browser

## Quick start 🍕

1. Clone this repository
2. Run the following command from the root directory of the repo in your favourite terminal.

  ```npm install```

3. Start API with

  ```node api.js```

4. Copy config.example.ini to config.ini and adapt settings if you want

5. Run the data aggregator with

  ```python3 log.py```

6. Boom! Open index_current_positions.html or index_heatmap.html in your browser.



## Periodic aggregation of the data

You can run the logger on your server by crontab:

The following example will log vehicle information every minute:

  ```*/1 * * * * /usr/bin/python3 ~/TierScooterAnalysis/log.py```

By default the script will log every position that is different from the last one logged for this vehicle or if the last logged position is atleast 30 minutes old.


## Technology stack
* Python3 for backend data aggregator
* Node for the RESTful API
* jQuery, CSS, HTML for the frontend
* SQLite for the database

## Help wanted

Any participation and help from others on this is very welcome.

-----------

## Note

I don't work for TIER Mobility GmbH or have any relationship with it.

If this project violates the general terms and conditions of TIER Mobility GmbH in any way, please let me know and the project will be stopped.

I am not responsible for any damage or costs incurred in connection with this project.

This project is considered just for fun.

## Thanks

Based on the great work of [/ubahnverleih/WoBike](https://github.com/ubahnverleih/WoBike#tier-scooter-europe-uae).

## Earthquakes App

Deployed: http://earthquakes-jmmerritt.now.sh

This Single Page Application was developed as part of a weekend homework at CodeClan.

The aim was to practice fetching data from external APIs, and using VueJS to display the returned data.

I chose the USGS (US Geological Survey) API, which has an extensive collection of data available. I used data on earthquakes.

There were 2 strands that I focused on for the homework, and I'd love to explore more in the future.

1. Fetching Large Earthquakes

I have one view which fetches data since USGS records began for earthquakes over 8.0 magnitude. I display this data in both a table and on a map - using "Leaflet".

2. Custom Criteria

A user can also enter in a date range and minimum magnitude to return a table of earthquakes that match their criteria.

Running instructions:

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

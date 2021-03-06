# oepnv-nuremberg  
 A wrapper for multiple datapoints from VAG and VGN  
  
## Where is the data comming from?  
 Departures and stops are comming from the official VAG API endpoint  
 URL: https://opendata.vag.de/  
 License: Creative Commons Attribution 4.0 Int.  
  
 Stops based on an adress come from an undocumented endpoint of the VGN  
 URL: HPSSuggest.php  
 License: Unknown  
  
 Connections between stops come from a web scraper directly from VGN.de.  
 URL: https://www.vgn.de/verbindungen/  
 License: Unknown  

## Functions and todo list

- [ ] Departures based on Ids (Not supported by API, will use Cache)
- [X] Departures based on names
- [X] Departures based on GPS
- [ ] Stops based on IDs (Not supported by API, will use Cache)
- [X] Stops based on names
- [X] Stops based on GPS
- [ ] Cacheing of Stops
- [ ] Turn (part of)adress into list of near stops
- [ ] Get routes from and to stops
- [ ] Get routes to anything. IDs, Stopnames, Adresses, GPS
- [ ] Get current elevator malfunctions
- [ ] Get current timetable changes
  
## Usage
 > A working example is [Test.js](https://github.com/BolverBlitz/oepnv-nuremberg/blob/main/test.js)

 Usage:
 ```js
 const vgn = require('oepnv-nuremberg');

 var Name = 'Opern';
 vgn.getstops(Name).then(
   function(message) {
     console.log(message);
 }).catch(error => console.log(error));
 ```

## Methods

### getStops
limit: Limit the listed stops to this amount  
 ```js
getStops('Plärrer', {limit: 1});
 ```

### getStopsbygps
limit: Limit the listed stops to this amount  
distance: Limit to stops in a radius in meters arround your GPS position (default: 500m)  
sort: Sort your stops by distance or alphabetically (default: 'distance')  
 ```js
getStopsbygps('49.45015694', '11.083455', {limit: 3, distance: 200, sort: 'distance'});
 ```

### getDepartures
Product: Bus/Ubahn or Tram  
TimeSpan: In minutes  
TimeDelay: Look for future departures in minutes  
LimitCount: Limit the listed departures to this amount   
```js
getDepartures('704', {Product: "ubahn", TimeSpan: 10, TimeDelay: 445, LimitCount: 10})
```

### getDeparturesbygps
limit: Limit the listed stops to this amount  
distance: Limit to stops in a radius in meters arround your GPS position (default: 500m)  
sort: Sort your stops by distance or alphabetically (default: 'distance') 
Product: Bus/Ubahn or Tram  
TimeSpan: In minutes  
TimeDelay: Look for future departures in minutes  
LimitCount: Limit the listed departures to this amount  
```js
getDeparturesbygps('49.4480881582118', '11.0647882822154', {Product: "ubahn", TimeSpan: 10, TimeDelay: 45, LimitCount: 2, limit: 5, distance: 200, sort: 'Distance'})
```

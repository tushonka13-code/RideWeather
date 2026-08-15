RideWeather Prototype 1.6

Mobile reliability fixes:
- Routing uses POST and identifies the app to the public Valhalla demo service.
- Routing requests have an 18-second timeout.
- If one alternate-route request fails, successful candidates are still used.
- Weather has a 12-second timeout and no longer blocks the route from becoming usable.
- The Calculate Ride button is re-enabled as soon as the route is ready.


Prototype 1.7: improved rural-address geocoding with multiple fallback geocoders and ZIP normalization.


Prototype 1.8: stronger rural-address geocoding using ArcGIS and U.S. Census fallbacks, with more tolerant OpenStreetMap matching.

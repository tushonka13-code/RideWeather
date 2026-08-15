RideWeather Prototype 1.6

Mobile reliability fixes:
- Routing uses POST and identifies the app to the public Valhalla demo service.
- Routing requests have an 18-second timeout.
- If one alternate-route request fails, successful candidates are still used.
- Weather has a 12-second timeout and no longer blocks the route from becoming usable.
- The Calculate Ride button is re-enabled as soon as the route is ready.


Prototype 1.7: improved rural-address geocoding with multiple fallback geocoders and ZIP normalization.


Prototype 1.8: stronger rural-address geocoding using ArcGIS and U.S. Census fallbacks, with more tolerant OpenStreetMap matching.


Prototype 1.9: adds route-filtered live NCDOT TIMS accident/police incident alerts, alert-radius control, map markers, and spoken alerts during navigation. Waze user reports are not directly accessed.


Prototype 2.0: replaced the unreliable direct NCDOT browser feed with the current public NCDOT TIMS ArcGIS feature service, with the original NCDOT feed retained as fallback.


Prototype 2.1: expanded live traffic/safety alert coverage beyond NC with a provider architecture and direct TDOT SmartWay incident feed for Tennessee routes. Coverage is automatically selected from the route geometry.


Prototype 2.2: nationwide traffic-event architecture.
- Keeps direct North Carolina and Tennessee state feeds.
- Adds optional Road511 normalized event coverage for routes anywhere in the U.S./Canada.
- Road511 API key is entered by the user and stored only in browser localStorage.
- Alerts remain filtered to the calculated route corridor and deduplicated when feeds overlap.
- Road511 currently offers a 14-day no-card trial; its free trial is limited to two jurisdictions, while paid plans provide all U.S./Canadian jurisdictions.


Prototype 2.3: live weather radar overlay.
- Adds RainViewer radar tiles directly over the Leaflet map.
- Radar toggle, opacity control, timeline scrubber, and playback.
- Loads past radar frames plus available nowcast frames.
- Radar remains visually above the base map while the existing route stays visible.
- RainViewer attribution is displayed in the radar control.
- Public RainViewer API is used under its personal/educational/small-scale community terms.


Prototype 2.4: radar display fix.
- Radar control is overlaid directly on the map.
- Fixes the critical Leaflet zoom issue: radar tiles have maxNativeZoom 7 while remaining visible at normal map zoom levels.
- Route and alternate route layers are brought above the radar.
- Adds a manual radar refresh button and loading status.


Prototype 2.5: radar control UI fix.
- Overrides the app-wide 100%-width white-button styling so radar controls display their labels correctly.
- Radar buttons now have explicit readable text and compact widths.
- Adds a clear live-radar status line.


Prototype 2.6: traffic/nationwide UI cleanup.
- Fixes the Road511 Save button inheriting global button styling and appearing as a blank oversized field.
- Shows clearly which traffic feeds are active without a Road511 key.
- Shows when nationwide Road511 coverage is enabled.


Prototype 2.7: motorcycle highway-avoidance and radar timeline fix.
- Avoid highways is strengthened as a hard routing preference: motorway/trunk/interstate use is disabled/penalized in Valhalla costing options where supported.
- Radar timeline now shows a small recent-history segment followed by NOW and then RainViewer nowcast/future frames.
- Slider defaults to NOW; future precipitation is to the right.
- Radar playback starts at NOW and plays forward into the forecast instead of replaying history.
- Frame labels explicitly identify Past, NOW, and Future.


Prototype 2.8: stricter Interstate avoidance.
- Uses Valhalla's documented motorcycle `use_highway` option at 0 for every candidate when Avoid highways is ON.
- Rejects candidate routes whose Valhalla response contains Interstate/I-## references.
- Scores any unavoidable Interstate route with a very large penalty.
- If the road network makes strict avoidance impossible, the app falls back to the best available route and explicitly warns the rider instead of silently claiming the route avoided highways.
- Preserves the 2.7 radar timeline: recent history -> NOW -> future/nowcast.


Prototype 2.9: highway-use modes.
- Avoid highways: strict avoidance.
- Use sparingly: strongly discourages highways but allows them when they materially improve the route.
- Normal: no highway preference.
- The existing future-oriented radar timeline is retained.


Prototype 3.0: fixed highway-mode migration bug.
- Removed unsafe direct access to the deleted `#highways` checkbox.
- All routing and summary logic now safely uses the new AVOID / SPARING / NORMAL radio group.
- Keeps backward compatibility if the legacy checkbox exists.
- Prevents the `can't access property "checked", $(...) is null` error.


Prototype 3.1: real backroad routing for strict highway avoidance.
- Fixed the route calculation call so SPARING is no longer accidentally treated as NORMAL.
- In AVOID mode, RideWeather now detects Interstate segments returned by Valhalla, extracts their route coordinates, and reroutes with those segments excluded.
- Multiple exclusion/reroute passes are attempted before falling back.
- A highway fallback is only used when no clean alternative can be produced.
- SPARING mode continues to discourage highways without requiring a completely highway-free route.

# Privacy

rapp·go has no application backend, account system, analytics, advertising, or telemetry.

## Location

The browser provides an exact location only after the player grants permission. That point is used locally for map position, distance checks, and spawn placement. Network requests use the center of a coarse geohash cell rather than the exact point:

- weather: geohash precision 5 (a several-kilometer area)
- nearby places: geohash precision 6 (a neighborhood-scale area)

CARTO receives ordinary map-tile coordinates for the map currently in view. Open-Meteo supplies weather, and OpenStreetMap Overpass supplies public place data. Their own privacy policies apply to those requests.

## Local data

The journal is stored in IndexedDB. Theme, satchel, cooldown, coarse cached weather/place data, and the last map position are stored locally in the browser. Clearing site data removes them.

## Sharing

A creature link contains its public procedural genome and content id. It does not contain an account, device identifier, exact GPS coordinate, or the player's location history. Recipients verify the content id locally before they can keep it.

IVAO FlightBoard
A lightweight real-time IVAO airport traffic board for websites, OBS overlays, ATIS displays, and live streams.

The project provides:

Live airport traffic from the IVAO Whazzup feed
Arrivals and departures with movement status
ATIS information with selectable controllers
ATC coverage indicators
Live airport ranking based on current IVAO traffic
Transparent OBS-ready overlays
Dark navy / cyan aviation-board visual style
Responsive desktop and mobile layouts
Project Files
File	Purpose
index.html	Main IVAO FlightBoard website
developer.html	Developer profile page
ivao-live-stream-obs.html	Compact split arrivals/departures overlay
ivao-atis-overlay.html	ATIS airport-board overlay
ivao-traffic-overlay.html	Compact live traffic summary overlay
Quick Start
The project is static HTML and does not require a build step.

Run locally
From the project folder:

python -m http.server 5500
Then open:

http://127.0.0.1:5500/
Use a local web server instead of opening the files directly with file://. This makes the behavior closer to a Vercel deployment and works better with OBS Browser Source.

Deploy to Vercel
Create a new GitHub repository.
Upload all project files to the repository.
Open Vercel.
Select Add New Project.
Import the GitHub repository.
Use the default settings and click Deploy.
The homepage is index.html, so the main website will be available at:

https://YOUR-PROJECT.vercel.app/
Website URLs
Main website
https://YOUR-PROJECT.vercel.app/
Live Stream with airport controls
This version shows the ICAO input and Load button. It is useful when selecting airports in a normal browser.

https://YOUR-PROJECT.vercel.app/ivao-live-stream-obs.html?icao=VTBB&live=1&traffic=1&controls=1
ATIS with airport and controller controls
https://YOUR-PROJECT.vercel.app/ivao-atis-overlay.html?icao=VTBB&atis=VTBB_APP&live=1&controls=1
Traffic summary
https://YOUR-PROJECT.vercel.app/ivao-traffic-overlay.html?icao=VTBB&live=1
Airport Selection
The overlays accept any four-letter ICAO airport code.

Examples:

VTBB  # Thailand regional airspace
VTBD  # Don Mueang International Airport
VTBS  # Suvarnabhumi Airport
KJFK  # John F. Kennedy International Airport
EGLL  # London Heathrow Airport
RJTT  # Tokyo Haneda Airport
OMDB  # Dubai International Airport
URL parameters
Parameter	Description	Example
icao	Airport or airspace ICAO code	icao=VTBB
atis	ATIS controller callsign	atis=VTBB_APP
live	Enables live IVAO data mode	live=1
controls	Shows airport/controller controls	controls=1
v	Optional cache-busting value	v=4
For a clean OBS overlay, omit controls=1.

OBS Setup
Add each overlay as an OBS Browser Source.

Do not use Window Capture for the overlays because it can scale and blur the text.

Live Stream Overlay
URL:

https://YOUR-PROJECT.vercel.app/ivao-live-stream-obs.html?icao=VTBB&live=1&traffic=1
Recommended Browser Source settings:

Width: 1920
Height: 230
FPS: 60
This overlay displays two equal lanes:

Left: Arrivals
Right: Departures
ATIS Overlay
URL:

https://YOUR-PROJECT.vercel.app/ivao-atis-overlay.html?icao=VTBB&atis=VTBB_APP&live=1
Recommended settings:

Width: 1920
Height: 140
FPS: 60
Traffic Summary Overlay
URL:

https://YOUR-PROJECT.vercel.app/ivao-traffic-overlay.html?icao=VTBB&live=1
Recommended settings:

Width: 1920
Height: 140
FPS: 60
The overlays use transparent backgrounds. Place them over a stream scene, simulator capture, map, or camera source.

Live Data
The website reads current traffic from the IVAO Whazzup feed:

https://api.ivao.aero/v2/tracker/whazzup
The main website refreshes approximately every 30 seconds. The Live Stream overlay refreshes approximately every 5 minutes to avoid blinking and unnecessary card resets.

The Popular Airports section ranks airports by the number of current departure and arrival flight-plan movements found in the live feed.

Troubleshooting
The overlay does not update
Confirm that the URL uses https://YOUR-PROJECT.vercel.app/.
Confirm that live=1 is included.
In OBS, right-click the Browser Source and select Refresh cache of current page.
If necessary, add a cache-busting parameter such as &v=4.
The overlay is blurry
Use Browser Source, not Window Capture.
Set the Browser Source width and height directly to the recommended values.
Do not stretch the source with Transform.
Keep the OBS canvas and output at the same resolution, preferably 1920×1080.
Use Lanczos as the OBS downscale filter when downscaling is required.
No ATIS is shown
ATIS is available only when the selected controller is online and is publishing an ATIS in the IVAO feed. Check the controller callsign, for example:

VTBB_APP
VTBD_TWR
KJFK_APP
EGLL_ATIS
Developer
Narongrit Sittisuonjit
IVAO VID 684960
Thailand Event Coordinator
Thailand Division Trainer

Contact: narongrit.sittisuonit@ivao.aero

Credits
Built for the IVAO virtual aviation community by Narongrit Sittisuonjit.

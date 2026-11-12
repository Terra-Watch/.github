<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/terra-watch/dashboard/main/frontend/public/brand/logo-on-dark.svg">
  <img src="https://raw.githubusercontent.com/terra-watch/dashboard/main/frontend/public/brand/logo.svg" alt="TerraWatch" height="72">
</picture>

**Early warning and response for forest fires in India.**

A web application and a network of lookout stations for forest rangers and control-room staff. It forecasts where a fire is likely tomorrow, sorts satellite detections into real fires and false ones, follows the fires that are burning, and puts the next action in front of a person.

English · हिन्दी · ଓଡ଼ିଆ

[Website](https://terra-watch-tawny.vercel.app) · [Dataset](https://zenodo.org/records/23647151)

</div>

---

## Our approach

Software suggests and people decide. A model never verifies, assigns, dispatches or announces. Anything that becomes an action goes through a person into an ordinary check, and a check moves up a ladder that only people move.

| Rung | Meaning | Moved here by |
|---|---|---|
| **Signal** | A satellite, station or report points to a place. No person has looked. | Automatic ingestion |
| **Report** | A person says there is a fire. Not checked. | A citizen, or staff logging a call |
| **Verified** | Staff checked the evidence and agree it is real. | Control Room |
| **Responding** | An officer is on the way or on site. | Control Room, with the officer's acceptance |
| **Contained** | Under control. | Control Room |
| **Closed** | Finished and kept for the record, with a reason. | Control Room |

Each rung has its own shape, colour and word, so meaning never depends on colour alone.

## Who uses it

| Role | What they do |
|---|---|
| **Ranger** | See tomorrow's forecast for their area and the fires near them, accept an assignment, record what they find (confirmed, not confirmed, inconclusive), also offline. |
| **Control Room** | Read the forecast board and map, work the satellite and active-fire boards, send a crew, verify and close checks, publish approved notices. |
| **Admin** | Manage accounts, access by state and stations. |
| **Citizen** | A secondary input: send a report (place, time, photos), read notices and the community. |

Each person sees only the states or communities they are granted.

## What it does

### Fire forecast
The chance that a satellite will detect a fire in each 55 km forest area tomorrow, shown as a level (None, Moderate 10%, High 30%, Extreme 60%), with the places to look, what is usual for the week, suggested actions and yesterday's record. A gradient-boosted model scores 7,148 forest cells in 17 states and the scores are calibrated. On the held-out year 2025 it reaches an average precision of 0.519 per cell and 0.795 per area, against 0.292 for climatology; areas rated Extreme had a detected fire on 81% of area-days.

### Satellite detections
Every VIIRS detection is kept and sorted into likely fire, unconfirmed, known heat source (mines, kilns, power plants) or outside forest, with the reason in words. A classifier of the chance that a burn scar follows within 1 km scores each one. Nothing is hidden; each group can be switched on.

### Active fires
Detections within 1 km and 36 hours are one fire, with its size, growth, the side it grew toward and the nearest named villages. A board orders fires by who needs attention. A control-room user can send a crew (a check in the queue), warn villages, or mark a fire handled, out or not a forest fire.

### Past fires: the spread outlook
A gated U-Net trained on 2,930 past fires ranks the forest cells within 8 km of a burning fire, in three bands, for the next one to two days. On the 2025 test fires its top band covers a median 75% of the cells that burned, against 50% for nearest-first. It is a ranking, not an arrival time. The page shows archived fires checked against what burned.

### Lookout stations
Fixed ESP32-S3 stations read fine particles, temperature and humidity, and a microphone and a sound classifier listen for chainsaws and blasts. Each reading is judged against that station's own normal and its neighbours, and the control room sees one sentence per station. Stations form a LoRa mesh that relays through each other. In simulation 95 to 98% of reports arrive after the busiest relay fails. A station never confirms a fire; only a ranger on the ground does.

### Field work and notices
A check is verified, assigned and closed with a reason. Rangers accept, visit and record what they find; a retry after a lost connection is stored once. Official notices are written by one person and approved by a second.

### Citizen reports and community
Citizens may send a report with place, time and photos, and read notices and the community. Stored photos have their location data removed and faces in public copies are blurred.

### Demo
The demonstration uses archived days of 2025 replayed from the final model, shown with the fires that were actually detected, one state and one day at a time.

## Safety and privacy

- Access is limited by state and community on the server, and every state change is written to an audit log.
- Official notices are written by one person and approved by a second.
- Emergency numbers, thresholds and retention periods come from configuration, never from built-in defaults.
- Secrets are never printed or committed.
- A missing dot on a map is never evidence that there is no fire, and the views say so.

## Repositories

| Repository | Content |
|---|---|
| [dashboard](https://github.com/Terra-Watch/dashboard) | The web application: backend, frontend, tests |
| [wildfire-ignition-forecasting](https://github.com/Terra-Watch/wildfire-ignition-forecasting) | The next-day forecast: data build, models, calibration |
| [acoustic-ml](https://github.com/Terra-Watch/acoustic-ml) | The sound classifier for the stations |
| [node-firmware](https://github.com/Terra-Watch/node-firmware) | Station firmware: sensors, routing, packets |
| [gateway-firmware](https://github.com/Terra-Watch/gateway-firmware) | Gateway firmware and the bridge to the server |

## Data sources

| Source | Use |
|---|---|
| NASA FIRMS (VIIRS) | Satellite fire detections |
| ERA5-Land, Open-Meteo, NOAA GFS | Weather and the weather forecast |
| MODIS burned area, Sentinel-2 | What burned, for the spread outlook |
| OpenStreetMap contributors | Basemap and named places |
| Rangers' field observations | Evidence and verification |

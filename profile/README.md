<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/terra-watch/dashboard/main/frontend/public/brand/logo-on-dark.svg">
  <img src="https://raw.githubusercontent.com/terra-watch/dashboard/main/frontend/public/brand/logo.svg" alt="TerraWatch" height="72">
</picture>

**Forecast, outlook and monitoring of forest fires in India.**

TerraWatch forecasts where a fire is likely tomorrow, shows where a burning fire is likely to spread in the next one to two days, and monitors the forest with satellite detections and lookout stations. A web application puts all three in front of forest rangers and control-room staff.

English · हिन्दी · ଓଡ଼ିଆ

[Website](https://terra-watch-tawny.vercel.app) · [Dataset](https://zenodo.org/records/23647151)

</div>

---

## Three parts

| Part | Question | What TerraWatch gives |
|---|---|---|
| **Forecast** | Where is a fire likely tomorrow? | A level for each 55 km forest area, with the places to look |
| **Outlook** | Where will a burning fire spread next? | The forest cells within 8 km ranked in three bands for the next one to two days |
| **Monitoring** | What is burning or happening now? | Satellite detections sorted into real and false, active fires with size and growth, and readings from lookout stations |

Software suggests and people decide. A model never verifies, assigns, dispatches or announces; a ranger or a control-room user acts on what it shows, and the record sets the forecast against what was found.

## Who uses it

| Role | What they do |
|---|---|
| **Ranger** | See tomorrow's forecast for their area and the fires near them, accept an assignment, record what they find (confirmed, not confirmed, inconclusive), also offline. |
| **Control Room** | Read the forecast board and map, work the satellite and active-fire boards, send a crew, verify and close checks, publish approved notices. |
| **Admin** | Manage accounts, access by state and stations. |
| **Citizen** | A secondary input: send a report (place, time, photos), read notices and the community. |

Each person sees only the states or communities they are granted.

## Forecast

The chance that a satellite will detect a fire in each 55 km forest area tomorrow, shown as a level (None, Moderate 10%, High 30%, Extreme 60%), with the places to look, what is usual for the week, suggested actions and yesterday's record. A gradient-boosted model scores 7,148 forest cells in 17 states and the scores are calibrated. On the held-out year 2025 it reaches an average precision of 0.519 per cell and 0.795 per area, against 0.292 for climatology; areas rated Extreme had a detected fire on 81% of area-days.

## Outlook

A gated U-Net trained on 2,930 past fires ranks the forest cells within 8 km of a burning fire, in three bands, for the next one to two days. On the 2025 test fires its top band covers a median 75% of the cells that burned, against 50% for nearest-first. It is a ranking, not an arrival time. The page shows archived fires checked against what burned.

## Monitoring

### Satellite detections
Every VIIRS detection is kept and sorted into likely fire, unconfirmed, known heat source (mines, kilns, power plants) or outside forest, with the reason in words. A classifier of the chance that a burn scar follows within 1 km scores each one. Nothing is hidden; each group can be switched on.

### Active fires
Detections within 1 km and 36 hours are one fire, with its size, growth, the side it grew toward and the nearest named villages. A board orders fires by who needs attention. A control-room user can send a crew (a check in the queue), warn villages, or mark a fire handled, out or not a forest fire.

### Lookout stations
Fixed ESP32-S3 stations read fine particles, temperature and humidity, and a microphone and a sound classifier listen for chainsaws and blasts. Each reading is judged against that station's own normal and its neighbours, and the control room sees one sentence per station. Stations form a LoRa mesh that relays through each other. In simulation 95 to 98% of reports arrive after the busiest relay fails. A station never confirms a fire; only a ranger on the ground does.

## Response and records

Around the three parts, a control-room user sends a crew as a check, a ranger accepts, visits and records what they find (also offline, and a retry after a lost connection is stored once), and official notices are written by one person and approved by a second. Citizens may send a report with place, time and photos and read notices; stored photos have location data removed and faces in public copies are blurred. The demonstration replays archived days of 2025 from the final model beside the fires that were actually detected, one state and one day at a time.

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
| [fire-spread-model](https://github.com/Terra-Watch/fire-spread-model) | The spread outlook: cases, models, notebooks |
| [acoustic-ml](https://github.com/Terra-Watch/acoustic-ml) | The sound classifier for the stations |
| [node-firmware](https://github.com/Terra-Watch/node-firmware) | Station firmware: sensors, routing, packets |
| [relay-firmware](https://github.com/Terra-Watch/relay-firmware) | Relay firmware for the LoRa mesh |
| [gateway-firmware](https://github.com/Terra-Watch/gateway-firmware) | Gateway firmware and the bridge to the server |
| [terrawatch-datasets](https://github.com/Terra-Watch/terrawatch-datasets) | Data catalog and bucket paths for all datasets |

## Data sources

| Source | Use |
|---|---|
| NASA FIRMS (VIIRS) | Satellite fire detections |
| ERA5-Land, Open-Meteo, NOAA GFS | Weather and the weather forecast |
| MODIS burned area, Sentinel-2 | What burned, for the spread outlook |
| OpenStreetMap contributors | Basemap and named places |
| Rangers' field observations | Evidence and verification |

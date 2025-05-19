# Garmin Grafana Advanced Dashboard
This repository provides and advanced dashboard for the [Garmin-Grafana](https://github.com/arpanghosh8453/garmin-grafana) project.

## Table of contents

- [Advanced data](#advanced-data)
- [Installation](#installation)
- [Data fetch configuration](#data-fetch-configuration)
- [Full dashboard Example](#full-dashboard-example)

## Advanced data
This dashboards adds panels for the following metrics:

* **Hydration panel**: daily fluid intake, fluid consumption during activities and hydration goal
![Hydration](https://github.com/brunothesatellite/grafana-dashboard/blob/main/Hydration.png?raw=true)

* **Lactate Threshold**: lactate threshold heart rate, pace and speed for endurance analysis. Provide last values and also trend of time.
![Lactate Threshold](https://github.com/brunothesatellite/grafana-dashboard/blob/main/Lactate-Threshold.png?raw=true)

* **Hill Score**: running efficiency on hills, including hill strength, hill endurance and global hill score
* **Race Prediction**: single panel for race prediction with inverted Y-axis
![Hill Score](https://github.com/brunothesatellite/grafana-dashboard/blob/main/Performance.png?raw=true)

* **Training Status - Load**: overall training load, fitness trends, and recovery. Includes Min-Max load threshold, chronic load and training load.
* **Endurance Score**: overall stamina and endurance capacity.
![Training Status and Endurance Score](https://github.com/brunothesatellite/grafana-dashboard/blob/main/Trainingstatus-endurancescore.png?raw=true)

* **Training Status - Ratio, Status, Intensity**
   * Status: same colors as Garmin Connect, indicates global status over time (maintaining, Productive, Non Productive, etc.)
   * Workload ratio: last value and over time. Indicates if you training condition improves (or not)
   * Training intensity: an advanced panel combining training load, chronic load, endurance score and activities intensity (aerobic / anaerobic) for deep analysis (ChatGPT can help you analysing this graph)
![Training Status Complete](https://github.com/brunothesatellite/grafana-dashboard/blob/main/Trainingstatus-fusion.png?raw=true)



## Installation
To use the my advanced Grafana dashboard, use manual import. I quote the installation chapter from Garmin-Grafana project, step 9 from [Manual Installation](https://github.com/arpanghosh8453/garmin-grafana#manual-install-with-docker-recommended-if-you-understand-linux-concepts)
For manual import, please use the [JSON file](https://github.com/brunothesatellite/grafana-dashboard/blob/main/Advanced-Garmin-Stats.json)  In the Grafana dashboard, the heatmap panels require an additional plugin that you must install. This can be done by using the `GF_PLUGINS_PREINSTALL=marcusolsson-hourly-heatmap-panel` environment variable like in the [compose-example.yml](https://github.com/arpanghosh8453/garmin-grafana/blob/main/compose-example.yml) file, or after the creation of the container very easily with docker commands. Just run `docker exec -it grafana grafana cli plugins install marcusolsson-hourly-heatmap-panel` and then run `docker restart grafana` to apply that plugin update. Now, you should be able to see the Heatmap panels on the dashboard loading successfully.

## Data fetch configuration
To fetch these advanced metrics, I recommend to updated the FETCH_SELECTION line of you compose file with these values (please refer to the [documentation](https://github.com/arpanghosh8453/garmin-grafana/discussions/119) for the complete list of options):

**General Health Metrics**

* `hydration` → Monitors daily fluid intake to maintain hydration levels.

**Sleep & Recovery**

* `training_readiness` → Analyzes sleep, recovery, and training load to determine readiness for exertion.

**Daily Movement & Performance**

* `activity` → Logs exercise sessions and general activity data.

**Advanced Athletic Metrics**

* `lactate_threshold` → Identifies lactate threshold heart rate and speed for endurance analysis.
* `vo2` → Calculates VO2 max, a key indicator of aerobic fitness.
* `race_prediction` → Estimates potential race completion times based on fitness trends.
* `training_status` → Analyzes overall training load, fitness trends, and recovery.

**Endurance & Strength Scores**

* `hill_score` → Assesses running efficiency on hills, factoring in elevation gain.
* `endurance_score` → Evaluates overall stamina and endurance capacity.

## Full dashboard Example

![Dashboard](https://github.com/brunothesatellite/grafana-dashboard/blob/main/Advanced-dashboard.png?raw=true)



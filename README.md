# 🇲🇩 Moldova: Primării Puternice Dashboard

An interactive, data-driven dashboard tracking the voluntary territorial amalgamation (mergers) of local public authorities (LPAs) in the Republic of Moldova. This platform bridges municipal GIS layers with real-time pipeline data to monitor funding stimulus, population consolidation, spatial expansion, and the local political landscape.

---

## 🚀 Live Demo

The dashboard is optimized for web deployment and can be viewed live via GitHub Pages:
👉 **[View Live Dashboard](https://frank0051.github.io/Moldova-Primarii-Puternice-Dashboard/)**

---

## ✨ Key Features

* **🗺️ Interactive Territorial Mergers Map:** A responsive Leaflet-powered map (exported via QGIS) showcasing the active borders of validated voluntary clusters. This map is dyanmic based on the raion drop-down filter being used (zoom-in) or the cluster card being clicked (zoom-in and dim surrounding areas). 
* **📈 Dynamic Top-Level KPIs:** Real-time summary metrics parsing global counts for:
* Total strong clusters formed.
* Number of individual local governments joining the initiative.
* Consolidated citizens supported by the reform.
* Total financial stimulus packages invested by the central government.

* **🌍 Integrated Map Area Tracker:** A dedicated map-side metric displaying the total territorial scope covered ($\text{km}^2$), computed directly from structural spatial features.
* **🏛️ Political Landscape Profiler:** Minimalist card integration displaying the political affiliations of both the sitting **Mayors** and **Council majorities** involved in each cluster without interface clutter.
* **🎯 Dynamic Raion Filtering:** Automatically extracts unique entries from the data stream to generate an alphabetical, diacritic-safe filter menu—eliminating hardcoded lists.
* **🔗 Source Verification:** Direct anchor links embedded within cluster showcase cards routing users straight to government announcements and local council press releases.

---

## 📊 Data Pipeline Architecture

The application is built on a decoupled, frontend-first data consumption model that loads configuration assets at runtime:

### 1. `Pipeline.csv`

The core business logic, KPIs, and text showcases are powered by this flat CSV file. PapaParse converts rows on the fly using the following verified schema:

| Column Header | Data Type | Description |
| --- | --- | --- |
| `Cluster_ID` | String (`YYYY-MM`) | Chronological identifier for tracking rollout tracking. |
| `Cluster_Name` | String | Unique identifier assigned to the merger cluster. |
| `Region_Raion` | String | Administrative district name used for dynamic dropdown filtering. |
| `Designated_Center` | String | The main administrative locality chosen as the cluster center. |
| `Combined_Population` | Integer | Aggregated population count of all participating communities. |
| `Financial_Stimulus_MDL` | Float | Central government investment allocations (in Millions MDL). |
| `km2` | Float | Geographic land mass area of the combined entities. |
| `Participating_Communities` | String | Semicolon-separated (`;`) list of all villages/communes involved. |
| `Mayor_Party` | String | Affiliation(s) of the local community mayors (e.g., `PAS; Ind.`). |
| `Major_Council_Party` | String | Predominant party representation within the local councils. |
| `Source` | String (URL) | Clickable URL link validating the amalgamation decision. |

### 2. QGIS GeoJSON Layer (`uat3_post2025mergers_1.js`)

Handles spatial polygon attributes and coordinate parsing. The dashboard dynamically matches features by joining the CSV's `Cluster_Name` with the map's structural `Sheet1_Cluster_ID`.

---

## 🛠️ Tech Stack

* **Structure & Layout:** HTML5, Tailwind CSS (via CDN)
* **Mapping Engine:** Leaflet.js, Autolinker.js (QGIS2Web build)
* **Data Parsing:** PapaParse (Remote asynchronous CSV fetching)
* **Hosting:** GitHub Pages

---

## 🔧 Local Development & Deployment

Because this project relies exclusively on client-side JavaScript modules, there are no heavy environments or build steps required.

1. Clone the repository locally:
```bash
git clone https://github.com/frank0051/Moldova-Primarii-Puternice-Dashboard.git

```


2. Navigate into the directory:
```bash
cd Moldova-Primarii-Puternice-Dashboard

```


3. Run a local development server (to bypass CORS restrictions during asynchronous JSON/CSV execution):
```bash
# If you have Python installed
python -m http.server 8000

# If you prefer Node.js
npx serve .

```


4. Open your browser and navigate to `http://localhost:8000`.

---

## 📝 Updating Data Entries

To add or modify validated clusters:

1. Open **`Pipeline.csv`** in any text editor or spreadsheet manager.
2. Append a new row or update existing columns ensuring strict compliance with the column header schemas (separating participating communities with a `;`).
3. Commit and push the changes directly to the `main` branch. The live GitHub Pages dashboard will update automatically within minutes.

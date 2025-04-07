<<<<<<< HEAD


# 🔥 Wildfire Prediction

A POC to **predict potential wildfire-prone areas** using satellite images taken *before* fire outbreaks.

## 🌍 Inspiration

As an aspiring contributor to GSoC 2025, I explored the Science and Medicine category and found the Alaska organization, which deeply resonated with my passion for sustainable energy and environmental resilience. Alaska faces unique wildfire challenges, with large-scale fires occurring annually in its boreal forests, tundra, and remote wilderness. Predicting fire-prone areas in such regions is vital for disaster mitigation and efficient resource allocation. While vegetation acts as fuel, key fire triggers include weather conditions (humidity, wind speed, temperature) and ignition sources (like lightning or human activity). Traditional wildfire prediction methods often rely on historical data and human observation, which can be delayed or inaccurate in remote terrains. This project aims to develop a hybrid deep learning model that leverages optical, thermal, and SAR (Synthetic Aperture Radar) satellite imagery, combined with ground-based weather data, to deliver timely and accurate wildfire risk predictions. Satellite data provides real-time insights into vegetation health, thermal anomalies, fuel dryness, and burn severity—even in cloud-covered or inaccessible regions—making it a powerful alternative to conventional approaches.

---

## 📊 Step 1: Data Collection

- **MODIS FIRMS**: Fire locations dataset (300-500m resolution)  
  📥 ![Download Dataset](./assets/Dataset.png)

- **Sentinel-2 Satellite**: High-resolution imagery (10m resolution, updated every 5 days)  
  🌐 [Access via AWS Open Data](https://registry.opendata.aws/sentinel-2/)
  ![sentinel](./assets/sentinel.png)

---

## 🧹 Step 2: Data Preparation
![dp](./assets/interactive-map-in-jupyter.png)

1. **Explore data** using an interactive map with:
   - Date filters
   - Layer selection
   - Popups for metadata

2. **Download & crop satellite images** taken *before* each fire event.
   - Automated processing at scale.

3. **Overlay fire locations** on corresponding satellite images.
![generating_data_before_fires](./assets/generating-dataset-before-fires.png)

4. **Convert images to grayscale** for simplified model input.

5. **Label data**:
   - “Future fire” (images prior to known fire)
   - “Non-fireable” (images from safe regions)
   ![fnf](./assets/fire-vs-nofire.png)
   ![fnf](./assets/fire-vs-nofire-gray.png)

---

## 🧠 Step 3: Train the Model

- **Model**: Visual Transformer (ViT)
- **Task**: Binary classification  
  ➤ “Potential place for future fire” vs “No future fire”

---

## 📈 Step 4: Evaluation & Prediction

Three prediction interfaces:
1. 🌐 **URL Input** – Paste a link to a satellite image.
2. 📂 **Image Upload** – Upload your own image file.
![upp](./assets/upload-file-and-predict.png)
3. 🗺️ **Map Click** – Choose a point using Latitude/Longitude.
![prelatlon](./assets/predict-from-lat-lon-for-now.png)

![mlm](./assets/map-fullscreen+popup+burnedzone-red.png)


---

## 🚀 Usage

Coming soon: Web app or CLI interface for real-time wildfire risk prediction.

---

Here's the **Future Work** section with bullet points converted into **checkbox format**, matching your README style:

---

### Future Work

While this project currently detects wildfire burn scars using a U-Net model, several enhancements are planned to shift toward predictive capabilities—especially for fire-prone regions like Alaska:

- [ ] **Integrate multimodal satellite data** (optical, thermal, SAR) to improve prediction accuracy in various weather and visibility conditions.  
- [ ] **Fuse ground-based environmental data** such as temperature, humidity, wind speed, and lightning activity to enrich the fire risk model.  
- [ ] **Develop temporal prediction models** that use pre-fire satellite imagery to anticipate high-risk ignition zones.  
- [ ] **Create high-resolution risk maps** using Sentinel-2 and similar datasets to support local firefighting and resource planning.  
- [ ] **Contribute to GSoC 2025** by collaborating with organizations like Alaska to build sustainable, AI-driven wildfire forecasting tools.  


---


## 🙌 Credits

Made with ❤️ by [@Prajak](https://github.com/prajak002)

---

## 📌 License

This project is open-source under the [MIT License](LICENSE).

---

Let me know if you want me to generate the file for download or add badges, environment setup, or usage examples.
=======
# Alaska Wildfire Prediction Using Satellite Imagery

**Mentors:** Yali Wang (ywang35 -at- alaska.edu) and Arghya Kusum Das (akdas -at- alaska.edu)

**Overview:** Given Alaska’s unique wildfire patterns, where large-scale fires occur annually in boreal forests, tundra, and remote wilderness, predicting fire-prone areas can help mitigate disasters and optimize resource allocation. The presence of vegetation (fuel) is necessary for a fire, but the determining factors are weather conditions (humidity, wind speed, temperature) and an ignition source (lightning, human activity, etc.). 
This project aims to develop a hybrid deep learning model to predict wildfire risk in Alaska by integrating optical, thermal, and synthetic aperture radar (SAR) satellite imagery with ground-based weather data.
Traditional wildfire prediction relies on weather data, historical fire records, and human observations, which can be delayed or inaccurate in remote areas like Alaska. In contrast, satellite imagery provides real-time, high-resolution insights into vegetation health, thermal anomalies, burn severity mapping, soil moisture, fuel dryness, and even cloud-penetrating fire detection.

Satellite choices:

| Satellite | Resolution | Revisit Frequency | Why Use It? |
| ------ | ------ | ------ | ------ |
| Landsat 8 & 9 (NASA/USGS) | 30m (multispectral), 100m (thermal) | 16 days | Tracks pre/post-fire vegetation and burn severity with great detail.|
| Sentinel-2 (ESA) | 10m (RGB, NIR), 20m (SWIR) | 5 days | High-resolution images for fire risk classification and early warnings. |
| MODIS (Terra/Aqua, NASA) | 250m (fire detection), 1km (thermal) | Daily | Provides historical fire perimeters and active fire locations. |
| VIIRS (Suomi NPP & NOAA-20) | 375m (fire detection), 750m (thermal) | Daily | Real-time fire monitoring, capturing active hotspots. |
| Sentinel-1 (ESA) | 5m - 20m | 6-12 days | SAR imaging for vegetation moisture & burned area mapping. |
| ALOS-2 (JAXA) | 10m - 100m | 14 days | L-band SAR for detecting dry fuel and terrain changes. |

Additional ground data sources:

1). ERA5 Climate Reanalysis (ECMWF): Provides historical & real-time temperature, wind, and humidity data.

2). NOAA NWS Weather Data: Near real-time humidity, wind, and temperature.

3). Alaska Fire Service (AFS) Wildfire Data: Historical ignition source data (lightning, human activity).

**Current Status:** This project is currently in the research stage.

**Expected Outcomes:** 
This project aims to develop a deep-learning model that predicts wildfire risk in Alaska using a combination of satellite and ground-based weather data. The expected outcome of this project would involve both the dataset preprocessing pipeline and the performance of the developed model. Especially, the dataset preprocessing would include how to process the pre-fire and post-fire images efficiently and integrate the ground-based data with satellite imagery. Expected outcomes include:

Minimum viable product (MVP): 

Fire risk classification: Given pre-fire satellite images, the model predicts the probability of a fire occurring within a defined time frame like 1 month, 3 months, or 6 months. The classifications should be "High Fire Risk," "Moderate Risk," or "No Risk."

1). Data pipeline development:

Preprocessing satellite images: Band selection, geospatial cropping, cloud removal (For this step, we are mostly interested in analyzing [Sentinel-2 data](https://dataspace.copernicus.eu/explore-data/data-collections/sentinel-data/sentinel-2));

Synthetic Aperture Radar (SAR) analysis: Extracting fuel moisture & terrain features (For this step, we are mostly interested in extracting information like vegetation density and soil moisture from [Sentinel-1 SAR data](https://dataspace.copernicus.eu/explore-data/data-collections/sentinel-data/sentinel-1));

Time-series weather data integration: Incorporating temperature, wind, and humidity. We have access to past decades of weather data for almost the past 30 years for multiple different places in Alaska.

2). Model training and prediction:

A hybrid model such as CNN-LSTM that analyzes satellite data and time-series weather trends (CNN-LSTM is just an example. We are open to multiple different types of analysis methodology);

A web-based GIS dashboard to visualize fire-prone regions in Alaska;

A report on model performance and fire risk metrics.

**Required Skills:** Python. Experience with deep learning and machine learning.

**Code Challenge:** Experience with multi-band satellite imagery, geospatial data processing (like ArcGIS Pro), and remote sensing.

**Source Code:** [https://github.com/YaliWang2019/AK-Satellite-Imagery-Wildfire-Prediction](https://github.com/YaliWang2019/AK-Satellite-Imagery-Wildfire-Prediction) (New Project)

**Discussion Forum:** [https://github.com/YaliWang2019/AK-Satellite-Imagery-Wildfire-Prediction/discussions](https://github.com/YaliWang2019/AK-Satellite-Imagery-Wildfire-Prediction/discussions)

**Effort:** 350 Hours

**Difficulty Level:** Medium/Hard
>>>>>>> e4b11974065c998ade129f5ab046c8d37bcb6863

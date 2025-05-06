# **Heat Risk Prediction in Philadelphia**

This project was developed as the final assignment for *MUSA-6950: AI for Urban Sustainability*. It aims to explore spatial patterns of heat risk in Philadelphia and apply machine learning models to predict risk levels using remotely sensed data.

[See Code Here](https://colab.research.google.com/drive/1k6kQBDay5nuWGCT8cvm53MDGf8EaSxPx#scrollTo=XbSYjVc4R5KC)

[See Slides Here](https://docs.google.com/presentation/d/1hz_kNX-35LVLT7ZOXFNPFMF3bPcrYzSqFJT2yprs1Ss/edit?slide=id.g34e0695fc43_0_293#slide=id.g34e0695fc43_0_293)

---

## **Introduction**

With the increasing frequency and intensity of heatwaves, urban heat risk poses a growing threat to human health—especially in densely built environments. The Urban Heat Island (UHI) effect further amplifies local temperatures due to surface features like impervious surfaces, vegetation loss, and limited water bodies. Identifying and predicting spatial heat risk is critical for effective urban planning and mitigation strategies.

---

## **Data Preparation**

This study utilizes two main datasets: the **Philadelphia Administrative Boundary** and **Landsat 8 satellite imagery**.

* **Philadelphia Administrative Boundary**
  Downloaded from the TIGER (Topologically Integrated Geographic Encoding and Referencing) dataset published by the U.S. Census Bureau.

* **Landsat 8 Imagery**
  Acquired via the Google Earth Engine (GEE) API. Since the focus is on heat risk, the study targets the summer months (June to August) from 2020 to 2024. A total of seven cloud-free (cloud cover < 20%) images were selected. The median composite of these images was calculated to minimize the impact of clouds and outliers. The final raster dataset was clipped to the Philadelphia boundary.

* **Features (Independent Variables)**

  * Bands 2, 3, 4 (RGB), Band 5 (Near Infrared)
  * Remote sensing indices: NDVI, NDBI, MNDWI, and SAVI

* **Target Variable (Dependent Variable)**
  Heat risk level, derived from Band 10 (Thermal Infrared, 100m resolution) by converting brightness temperature to **Land Surface Temperature (LST)**. The LST was resampled to **30m resolution** and categorized into **three heat risk levels**:

  * **Low**: ≤ 35°C
  * **Medium**: 35–45°C
  * **High**: ≥ 45°C

---

## **Model Training**

A stratified random sampling approach was used to extract 5,000 samples evenly across the three heat risk levels because of the unbalanced distribution of each risk level. The data was split into training and testing sets using a 7:3 ratio.

Two models were trained for comparison:

* **Convolutional Neural Network (CNN)**
  Model structure adapted from Fu et al. (2024).
![image](https://github.com/user-attachments/assets/8a9f85e3-3c16-40b4-9233-f0f70f511bc6)

* **Random Forest (RF)**
  A traditional machine learning classifier well-suited for tabular data.

---

## **Results**

* **CNN Accuracy**: 0.78
* **Random Forest Accuracy**: 0.77

The CNN slightly outperformed the RF model. However, since the input samples were pixel-based and lacked spatial context, CNN did not fully leverage its advantage in spatial feature extraction.

Feature importance analysis from the RF model identified the top three predictors:

1. Band 4 (Red)
2. NDBI
3. Band 2 (Blue)

---

## **Future Work**

* Evaluate model generalizability across different time periods and geographic areas
* Optimize feature selection based on importance rankings
* Use **air temperature** instead of LST for a more accurate assessment of heat risk. 

## Reference
Fu, S., Wang, L., Khalil, U., Cheema, A. H., Ullah, I., Aslam, B., Tariq, A., Aslam, M., & Alarifi, S. S. (2024). Prediction of surface urban heat island based on predicted consequences of urban sprawl using deep learning: A way forward for a sustainable environment. Physics and Chemistry of the Earth, Parts A/B/C, 135, 103682. 

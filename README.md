# EO-SAR-Change-Detection

1. Datasets Used
a. Sentinel-2 (Optical) - Source: Copernicus Open Access Hub (via Google Earth Engine) - Product: Sentinel-2 Level-2A (Surface Reflectance) - Spatial Resolution: 10 m (bands B2, B3, B4, B8) - Derived Indices: NDVI, NDWI, NDBI Two temporal composites were generated using the median reducer: Pre-event: 2018 Post-event: 2024 Cloud masking was implemented using the Scene Classification Layer (SCL).
b. Sentinel-1 (SAR) - Source: Copernicus Open Access Hub (via GEE) - Product: Sentinel-1 GRD - Bands: VV, VH.
c. Bangalore metropolitan shapefile as Region of Interest (ROI).
2. Methodology

a. Pre-Processing - Images were reprojected, resampled, and coregistered to a common 10m grid (EPSG:4326).
b. Change Detection Approach - A bi-temporal differencing method was applied: NDVI = (NIR − RED) / (NIR + RED) NDWI = (GREEN − NIR) / (GREEN + NIR) NDBI = (SWIR − NIR) / (SWIR + NIR) Change maps were generated as: ΔIndex = Post − Pre
c. Thresholding and Classification - Vegetation Loss: ΔNDVI < −0.2 Urban Expansion: ΔNDBI > 0.2 Water Body Change: ΔNDWI > 0.2 A hierarchical mask and confidence filtering minimized class overlap.
d. Confidence Map Computation - Confidence = |ΔIndex| / Max(|ΔIndex|) Values range from 0 (uncertain) to 1 (highly confident). Separate confidence maps were generated for vegetation, urban, and water.

3. Results and Interpretation
a. Vegetation Change Map: Identifies deforestation or agricultural loss. Urban Change Map: Highlights infrastructure or built-up growth. Water Body Change Map: Detects new or expanded water areas.
Vegetation mapped as NDVI_diff:-
Gain threshold > +0.20 , Loss Threshold < −0.20, Stable −0.20 to +0.20
Urban mapped as NDBI_diff :-
Gain threshold > +0.10, Loss threshold < −0.10, Stable −0.10 to +0.10
Water mapped as NDWI_diff:-
Gain threshold > +0.15, Loss threshold < −0.15, Stable −0.15 to +0.15.
Gain threshold values per pixel is denoted as 1, Loss threshold as 2 and Stable threshold as 3.
b. High-confidence (>0.7): Strong, spatially coherent changes. Medium-confidence (0.4–0.7): Transitional zones. Low-confidence (<0.4): Nise or seasonal variation.

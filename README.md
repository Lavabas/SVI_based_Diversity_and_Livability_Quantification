# Quantifying Streetscape Diversity and Livability Using Street-View Images
## Overview
This project leverages street-view images (SVI) from Mapillary to quantify urban streetscape characteristics and assess livability in Trincomalee, Sri Lanka. Using deep learning-based semantic segmentation, each street panorama is analyzed for its proportion of greenery, buildings, roads, and sky. The analysis computes:
1. Streetscape Entropy – a measure of diversity or mixed-use in the visual environment.
2. Livability Index – a simple metric combining greenery, sky openness, and road accessibility, penalizing congested or built-up areas.

The resulting maps visualize spatial patterns of urban quality, helping identify mixed-use streets, green/open areas, and potentially low-livability streets. This approach demonstrates a novel integration of SVI and computational urban morphology.

## Objective
- Showcase the potential of street-level imagery for urban analysis in smaller or under-represented cities like Trincomalee.
- Quantify streetscape diversity and livability at a high spatial resolution.
- Provide a visual and quantitative basis for urban planning, pedestrian experience, and environmental quality assessment.

<img width="1920" height="1080" alt="Screenshot (399)" src="https://github.com/user-attachments/assets/ce4655a4-fe08-45e2-a6f8-772d2218705f" />
<img width="1920" height="1080" alt="Screenshot (398)" src="https://github.com/user-attachments/assets/390e7bde-03ad-4b07-b538-d39ae099fc14" />


### Data
1. Street-Level Imagery (SVI): Downloaded from Mapillary for Trincomalee town.
2. Metadata CSV: Includes id, filepath, latitude, longitude for each SVI image.
3. Optional Comparison: Sentinel-2 NDVI imagery from Google Earth Engine for greenery validation.

### Methodology
1. Data Acquisition
- Query Mapillary API for Trincomalee bounding box.
- Download images and save metadata (svi_trinco.csv).

2. Semantic Segmentation
- Pretrained DeepLabV3 (ResNet50) model used to classify pixels into building, road, vegetation, sky.
- Preprocessing: resize images to 512×512, normalize, feed into model.

3. Index Computation
- Entropy: Shannon entropy of pixel class proportions → higher values indicate diverse/mixed streetscape.
- Livability Index: Weighted sum: 0.5*greenery + 0.3*sky + 0.2*road - 0.2*building.

4. Visualization
- Folium map displays:
    Marker color = entropy (blue → yellow).
    Marker size = livability.
    Legends: color legend for entropy, circle-size legend for livability.
- Optional overlay of Sentinel-2 NDVI for greenery comparison.

5. Interpretation of Results
   <img width="2376" height="980" alt="image" src="https://github.com/user-attachments/assets/c0b6e22e-c788-47f9-ae5f-39ccfa2d94fb" />
Here’s an overall interpretation of the Trincomalee Entropy–Livability analysis.

## Tools & Libraries
- Python Libraries:
folium, matplotlib, branca, numpy, pandas, torch, torchvision, segmentation-models-pytorch, cv2

- Data Sources:
Mapillary SVI for street-level images

- Optional Sentinel-2 NDVI via Google Earth Engine

- Environment: Google Colab (CPU/GPU)


## Key Findings
#### Streetscape Entropy (diversity of visual elements)
- Mean entropy: ~0.61 (on a 0–1 scale).
- Spread: Most streets fall between 0.52 and 0.69, indicating moderate diversity.
- Low values (~0.1–0.3): Streets dominated by a single element (likely roads or buildings).
- High values (~0.9–1.0): Streets with a balanced mix of greenery, sky, roads, and buildings.
- Interpretation: Trincomalee’s streets are neither monotonous nor hyper-diverse, but some hotspots of mixed-use and greenery exist.

#### Livability Index
- Mean livability: ~ -0.10 (negative on average, because the building penalty dominates).
- Range:
Lowest: -0.19 → highly congested or built-up streets.
Highest: +0.09 → greener, more open streets with better visual quality.
- Distribution: Skewed slightly toward negative values → majority of streets are built-up or congested, with fewer high-livability areas.

#### Entropy–Livability Relationship
- Correlation: +0.98 (very strong positive).
- Interpretation: Streets that are visually diverse (balanced mix of greenery, sky, and built space) are also rated more livable.
- This validates the conceptual design: entropy and livability move together in Trincomalee.

#### Overall Spatial Insight (Conceptual)
- High entropy + high livability: Likely green/mixed-use boulevards, waterfront roads, or peri-urban streets where openness and greenery remain.
- Low entropy + low livability: Likely dense inner streets, highly built-up, congested, and less pedestrian-friendly.
- Middle ranges: Typical urban residential/commercial streets with moderate diversity but little openness.

### Implications for Trincomalee
1. Urban Quality Gap: Trincomalee shows limited high-livability streets → need for greening interventions and streetscape improvements.
2. Entropy as Proxy for Livability: The almost perfect correlation suggests entropy alone could be a strong indicator of environmental quality.

### Planning Opportunities:
1. Target low-entropy, low-livability streets for tree planting, open space creation, or facade improvements.
2. Preserve and enhance high-entropy streets as models of sustainable and livable urban form.

## Potential Novelty & Contribution
1. First SVI-based urban livability assessment in Trincomalee, demonstrating the transferability of methods from large cities to smaller urban contexts.
2. Integration of streetscape entropy with a simple, interpretable livability index for visual and quantitative urban analysis.


🌴 Coconut Tree Detection from High-Resolution Imagery Using YOLO in Python

📄 Overview:
This project demonstrates a deep learning–based pipeline for detecting individual coconut trees in very high-resolution aerial imagery using a dual-branch YOLO (You Only Look Once) object detection model. Leveraging 3-band aerial imagery (~9 cm spatial resolution) and manually digitized training samples, the model was trained to achieve accurate crown-level detections. The end-to-end workflow includes dataset preparation, YOLO formatting, training, evaluation, and export of results in both raster and vector formats for GIS analysis.

📊 Project Specifications:
| Attribute                | Details                                                               |
| ------------------------ | --------------------------------------------------------------------- |
| **Title**                | Coconut Tree Detection from High-Resolution Imagery Using YOLO        |
| **Imagery Source**       | Aerial imagery                                                        |
| **Platform**             | Airborne                                                              |
| **Spatial Resolution**   | \~9 cm                                                                |
| **Sample Type**          | Bounding boxes digitized in QGIS                                      |
| **Detection Model**      | YOLOv11 Dual-Branch (Ultralytics)                                     |
| **Programming Language** | Python                                                                |
| **Output Formats**       | GeoTIFF (prediction raster), Shapefile (tree polygons), PNG (visuals) |
| **Validation Metrics**   | Precision, Recall, F1-Score, mAP                                      |

⚙️ Dependencies:
Install required packages: pip install ultralytics geopandas rasterio shapely matplotlib numpy
| Library         | Purpose                                           |
| --------------- | ------------------------------------------------- |
| **ultralytics** | Training and inference with YOLOv11               |
| **geopandas**   | Shapefile handling (labels, outputs)              |
| **rasterio**    | Reading/writing georeferenced raster imagery      |
| **numpy**       | Numerical operations                              |
| **matplotlib**  | Visualization of detections and metrics           |
| **shapely**     | Geometry manipulation (bounding boxes → polygons) |
| **os / glob**   | File management and dataset organization          |

🚀 Workflow:
A[🎯 Define Objective] --> B[🛰️ Load High-Resolution Imagery]
B --> C[🧭 Digitize Training Labels (Bounding Boxes in QGIS)]
C --> D[💾 Convert Labels to YOLO Format (.txt)]
D --> E[📂 Split Dataset into Train / Val / Test]
E --> F[🧠 Train YOLO Model]
F --> G[🗺️ Run Inference on Full Scene]
G --> H[🧹 Post-process: NMS + GIS Conversion]
H --> I[📤 Export Outputs (GeoTIFF + Shapefile)]
I --> J[📊 Evaluate Results with Metrics]

📌 Model Parameters:
| Parameter       | Value  | Description            |
| --------------- | ------ | ---------------------- |
| **epochs**      | 2000   | Training iterations    |
| **batch\_size** | 32     | Batch size             |
| **img\_size**   | 256    | Input patch size       |
| **lr0**         | 0.0001 | Initial learning rate  |
| **optimizer**   | AdamW  | Optimization algorithm |

📈 Evaluation Metrics:
| Metric                | Value | Description                                                 |
| --------------------- | ----- | ----------------------------------------------------------- |
| **Precision (B)**     | 0.886 | 88.6% of predicted trees are correct (few false positives). |
| **Recall (B)**        | 0.802 | 80.2% of actual trees were detected (some missed).          |
| **mAP\@0.5 (B)**      | 0.850 | Strong object localization accuracy at IoU = 0.5.           |
| **mAP\@0.5–0.95 (B)** | 0.507 | Moderate robustness across stricter IoU thresholds.         |
| **Fitness Score**     | 0.541 | Combined optimization score from YOLO metrics.              |

⚡ Speed Profile (per image):
| Stage       | Time (ms) | Notes                                  |
| ----------- | --------- | -------------------------------------- |
| Preprocess  | 0.60 ms   | Resizing and normalization             |
| Inference   | 8.08 ms   | Forward pass through YOLOv11           |
| Loss        | 0.013 ms  | Training loss computation              |
| Postprocess | 2.56 ms   | Non-Max Suppression (NMS) + formatting |

➡️ Total Inference Time ≈ 11.2 ms per image (~90 FPS).

🏆 Interpretation:
      High Precision (0.886) → Most detections are correct with minimal false positives.
	    Good Recall (0.802) → Majority of trees detected, with some missed.
	    Strong mAP@0.5 (0.850) → Bounding boxes align well with ground truth.
	    Moderate mAP@0.5–0.95 (0.507) → Box alignment varies under stricter thresholds.
	    Fast Inference (~90 FPS) → Suitable for large-scale, real-time mapping.

📦 Final Outputs:
| Output Type           | Format    | Description                                    |
| --------------------- | --------- | ---------------------------------------------- |
| **Detection Raster**  | GeoTIFF   | Scene-wide raster with detected bounding boxes |
| **Vector Footprints** | Shapefile | Polygonized coconut tree detections            |
| **Visualization**     | PNG/JPG   | Annotated imagery with predictions             |
| **Trained Model**     | .pt       | YOLO weights for reuse or deployment           |

❓ Why YOLO for Coconut Tree Detection?
  🌈 High-Resolution Data
	      Distinctive coconut crowns visible in ~9 cm imagery enable precise object detection.
       
  ⚡ YOLO (You Only Look Once)
	      State-of-the-art object detector
	      High accuracy with fast inference
	      Supports transfer learning from pretrained weights
       
  🧠 Dual-Branch Architecture
	      Combines spectral and spatial features for robust detection
	      Handles variability in crown size, lighting, and background clutter

📌 Conclusion:
    This project demonstrates the potential of YOLOv11 dual-branch for high-precision coconut tree detection in ultra high-resolution aerial imagery. By integrating:
	    ✅ Digitized training labels (bounding boxes)
	    ✅ High-resolution imagery (~9 cm GSD)
	    ✅ A robust YOLOv11 architecture
	    ✅ GIS-based post-processing

we achieved strong performance with Precision = 0.886, Recall = 0.802, and mAP@0.5 = 0.850.
The final deliverables—a classified GeoTIFF, a shapefile of detected trees, and a trained YOLO model—support applications in plantation management, crop inventory, and ecological monitoring.

✍️ **Author:** Subham Roy ✨🌟 

#Assessing RGB-only UAV Semantic Segmentation for Coastal Land-Cover Mapping: Limits of Mangrove Discrimination in Kuala Selangor, Malaysia
## Overview
# Assessing RGB-only UAV Semantic Segmentation for Coastal Land-Cover Mapping: Limits of Mangrove Discrimination in Kuala Selangor, Malaysia
This repository contains the supporting materials for the study.
The study presents a deep learning framework for pixel-level coastal land-cover mapping using high-resolution UAV imagery. A U-Net semantic segmentation model with a ResNet34 encoder was developed using the ArcGIS Pro Deep Learning Framework to classify mangrove and surrounding land-cover categories.

The workflow includes:
- Drone image preprocessing
- Training sample preparation
- Manual polygon annotation
- Deep learning model training
- Pixel-based classification
- Accuracy assessment

# Study Area
The study was conducted at Kuala Selangor Nature Park, Selangor, Malaysia.
High-resolution drone imagery was used to map mangrove vegetation and surrounding land-cover classes.
# Dataset Information
The input dataset consists of a high-resolution drone orthomosaic raster.
Dataset characteristics:
- File format: GeoTIFF (.tif)
- Raster type: Drone orthomosaic imagery
- Original UAV imagery contained four spectral bands:

- Band 1: Blue
- Band 2: Green
- Band 3: Red
- Band 4: Near Infrared (NIR)
Only RGB bands (Blue, Green, Red) were used as input channels for U-Net–ResNet34 semantic segmentation.
Coordinate Reference System:
- Projected Coordinate System:
- WGS 1984 UTM Zone 47N
- EPSG Code:
- 32647
- Geographic Coordinate System:
- WGS 1984
- Unit:
 - Meter
- Spatial resolution:
- 0.046085 m/pixel
- Area of Interest (AOI):
- Approximately 14.99 ha
The original high-resolution drone orthomosaic dataset is approximately 49.67 GB. Due to its large size, the complete dataset is not publicly uploaded.  
The dataset is available from the corresponding author upon reasonable request.
# Land-Cover Classes
The model classifies six land-cover categories:
| Class ID | Class Name |
|----------|------------|
| 1 | Mangrove |
| 2 | Non-Mangrove |
| 3 | Palm |
| 4 | Water |
| 5 | Grass |
| 6 | Soil |

# Methodology Workflow

The complete workflow consists of:
1. Drone image acquisition and orthomosaic generation
2. Training polygon creation
3. Class label assignment
4. Polygon-to-raster conversion
5. Training data generation
6. U-Net–ResNet34 model training
7. Pixel classification using deep learning
8. Accuracy assessment
Workflow:
Drone Orthomosaic  
→ Training Polygon Annotation  
→ Label Raster Generation  
→ Export Training Data  
→ U-Net–ResNet34 Training  
→ Deep Learning Classification  
→ Accuracy Assessment
# Training Data Preparation
Training samples were generated using the ArcGIS Pro **Export Training Data For Deep Learning** tool.
Parameters:
- Input imagery:
  - RGB drone orthomosaic
- Image format:
  - TIFF
- Tile size:
  - 256 × 256 pixels
- Stride:
  - 128 × 128 pixels
- Training label format:
  - Classified Tiles
- Class attribute field:
  - class_id
The generated image chips and label masks were used for model training.
---
# Label Raster Preparation
Ground-truth labels were created from manually digitized training polygons.
Processing:
Training Polygons  
→ Polygon to Raster  
→ Label Raster

Parameters:
- Input features:
  - Training polygons
- Value field:
  - class_id
- Cell assignment type:
  - Maximum Area
- Output format:
  - TIFF
The generated label raster was aligned with the drone orthomosaic.

# Model Architecture

Deep learning model:

- Architecture:
  - U-Net Semantic Segmentation

- Encoder Backbone:
  - ResNet34

- Input:
  - RGB drone imagery

- Output:
  - Pixel-level land-cover classification map

# Model Configuration

Training parameters:
- Model type:
  - U-Net
- Backbone:
  - ResNet34
- Image chip size:
  - 256 × 256 pixels
- Batch size:
  - 8

- Maximum epochs:
 - 25

- Validation split:
  - 10%
 - Learning rate:
  - 0.001
- Weight initialization:
  - ALL_RANDOM

- Data augmentation:
  - Default

- Loss Function:
  - Dice Loss

- Monitoring metric:
  - Validation Loss
# Deep Learning Environment
The model was developed using the ArcGIS Pro Python deep learning environment.
Software:
- ArcGIS Pro 3.6.0
- ArcGIS Pro Deep Learning Framework
- Image Analyst Extension
Python environment:
- Python 3.9.18
- PyTorch
- TorchVision
- TorchAudio
- CUDA Toolkit 11.8

GPU-enabled deep learning libraries were used for model training and inference.
# Model Inference and Classification

The trained model was applied using the ArcGIS Pro **Classify Pixels Using Deep Learning** tool.
Inference parameters:
- Input raster:
  - Drone orthomosaic RGB imagery
- Model definition:
  - U-Net–ResNet34 Deep Learning Package (.dlpk)
- Processing mode:
  - Process as mosaicked image
- Tile size:
  - 256 × 256 pixels
- Padding:
  - 32 pixels
 - Batch size:
  - 4
The output was a georeferenced semantic segmentation raster containing six land-cover classes.

# Accuracy Assessment
Model performance was evaluated using independent validation points generated in ArcGIS Pro.
Parameters:
- Input classification raster:
  - MangroveU-Net_Classification_v1.tif
- Number of random points:
  - 500
  - # Accuracy Assessment

Model performance was evaluated using independent validation points generated in ArcGIS Pro.

Parameters:
- Input classification raster:
- MangroveU-Net_Classification_v1.tif
- Initial validation points:
- 500
- Valid validation points used:
- 409
- Sampling strategy:
- Equalized stratified random sampling
- Target field:
- CLASSIFIED
Evaluation Metrics:
1. Overall Accuracy (OA)
2. Kappa Coefficient
3. Precision
4. Recall
5. F1-score (Harmonic Mean of Precision and Recall)
6. Macro-F1 (Arithmetic Mean of the F1-scores)
7. Intersection over Union (IoU)
8. Mean Intersection over Union (mIoU)
# Results
The trained U-Net–ResNet34 model achieved:
- Overall Accuracy:
- 90.46%
- Kappa Coefficient:
- 0.8834
- Macro-F1:
- 85.92%
- Mean Intersection over Union (mIoU):
- 77.94%
The model successfully generated pixel-level classification maps for mangrove and surrounding land-cover classes.
# Repository Structure
## Software
- ArcGIS Pro Deep Learning
- Python
- Deep learning libraries
## Usage
1. Prepare image-mask pairs
2. Train U-Net model
3. Perform inference
4. Evaluate classification accuracy using the confusion matrix and performance metrics including Overall Accuracy (OA), Kappa Coefficient, Precision, Recall, F1-score, and Intersection over Union (IoU).

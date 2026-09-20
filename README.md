#Assessing RGB-only UAV Semantic Segmentation for Coastal Land-Cover Mapping: Limits of Mangrove Discrimination in Kuala Selangor, Malaysia
Drone-based mangrove mapping using U-Net with ResNet34 encoder for semantic segmentation
# Drone-Based Mangrove Mapping Using U-Net–ResNet34
A deep learning framework for high-resolution drone-based mangrove mapping using U-Net with a ResNet34 encoder for semantic segmentation and land-cover classification.
## Overview
This repository contains the supporting materials for the study:

**"Mangrove forest mapping and classification using drone imagery and U-Net deep learning model"**
The study presents a deep learning approach for pixel-level classification of mangrove ecosystems using high-resolution drone imagery. A U-Net semantic segmentation model with a ResNet34 encoder was developed using the ArcGIS Pro Deep Learning Framework.

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
- Spectral bands:
  - Band 1: Blue
  - Band 2: Green
  - Band 3: Red
  - Band 4: Near Infrared (NIR)
Coordinate Reference System:
- Projected Coordinate System:
  - WGS 1984 UTM Zone 47N
- EPSG Code:
  - 32647
- Geographic Coordinate System:
  - WGS 1984
- Unit:
  - Meter

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
  - 20

- Validation split:
  - 10%
- Weight initialization:
  - Random initialization
- Data augmentation:
  - Default
- Loss function:
  - Dice Loss
- Monitoring metric:
  - Validation Loss
# Deep Learning Environment
The model was developed using the ArcGIS Pro Python deep learning environment.
Software:
- ArcGIS Pro 3.5.0
- ArcGIS Pro Deep Learning Framework
- Image Analyst Extension
Python environment:
- Python 3.9
- PyTorch
- TorchVision
- TorchAudio
- CUDA Toolkit 11.8
GPU-enabled deep learning libraries were used for model training and inference.
---=
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
- - Batch size:
  - 4
The output was a georeferenced semantic segmentation raster containing six land-cover classes.

# Accuracy Assessment
Model performance was evaluated using independent validation points generated in ArcGIS Pro.
Parameters:
- Input classification raster:
  - MangroveU-Net_Classification_v1.tif
- Number of random points:
  - 500
- Sampling strategy:
  - Equalized stratified random sampling
- Target field:
  - CLASSIFIED
Evaluation metrics:
- Overall Accuracy (OA)
- Kappa Coefficient
- Precision
- Recall
- F1-score
- Intersection over Union (IoU)

# Results

The trained U-Net–ResNet34 model achieved:

- Overall Accuracy:
  - 90.46%

- Kappa Coefficient:
  - 0.8834

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
4. Evaluate accuracy using confusion matrix, OA, Kappa, Precision, Recall, F1-score, and IoU

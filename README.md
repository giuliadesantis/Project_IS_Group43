# Group 43 - Project Image Segmentation
Members:
- Alessia Serra (s359693)
- Letizia Brizzi (s354966)
- Giulia De Santis (s360859)
- Arianna Miori (s353777)

# Mask Architecture for Road Scenes
This is the starting repository for two projects:
- Mask Architecture Anomaly Segmentation for Road Scenes  [[Project Description](https://drive.google.com/file/d/1Vz08DHsP_mojpCTAQTR6NHVq-2rEqAZM/view?usp=sharing)]
- Comprehensive Road Scene Understanding for Autonomous Driving  [[Project Description](https://drive.google.com/file/d/1tq5F_j_8O2vlGWbkU1ayPjYvCml1VEwr/view?usp=sharing)]

The support folder with datasets, checkpoints, bin used for our project [[Project Folder](https://drive.google.com/drive/folders/1anujPehiSRqow-CwUA580wxEa24htbA1?usp=sharing)].

This repository consists of the code base for training/testing ERFNet on the Cityscapes dataset and perform anomaly segmentation. It also contains some code referring to EoMT. Some of this code may be unnecessary for your project.

## Folders
For instructions, please refer to the README in each folder:

* [eval](eval) contains tools for evaluating/visualizing an ERFNet model's output and performing anomaly segmentation.
* [trained_models](trained_models) Contains the ERFNet trained models for the baseline eval. 
* [eomt](eomt) It is almost the original folder of the EoMT project. Inside it you will find code to train and pretrained checkpoints for EoMT.

## Project's Notebooks

### Comprehensive Road Scene Understanding for Autonomous Driving
In STEP 4 we compared two different trained versions of the EoMT model (one pre-trained on Cityscapes for semantic segmentation and one on COCO for panoptic segmentation) to analyze the differences in their class spaces and target tasks.
- **STEP4.ipynb** visualizes and qualitatively analyzes the predictions of both models on sample images from the Cityscapes validation set, comparing the semantic output on Cityscapes (19 classes) against the one on COCO (133 categories split into things and stuff), defining a consistent evaluation strategy to handle the mismatch between the class spaces ('coco_to_cityscapes_map' does the mapping between the classes in the two datasets). Also, it quantitatively evaluates the semantic segmentation performance of both model versions across the entire Cityscapes validation set. It computes per-pixel class scores by combining mask and class logits, ensuring an identical and fair evaluation pipeline for both models. Additionally, it visualizes the panoptic output for the COCO-trained model, using a picture from COCO dataset.

  
- STEP5.ipynb performs semantic inference on Cityscapes validation images using the fine-tuned model weights. It evaluates the overall semantic segmentation alignment and quantifies the global performance across classes (such as road, sidewalk, person, car, train, etc.), reporting final mean IoU global.

- STEP5_semanticPlotCocoFT.ipynb plots a qualitative comparison showing the source image, the model's predicted color map, matching the colors of the target image, and the ground-truth target mask.

In STEP 7 we evaluate the anomaly detection performance of the pre-trained ERFNet model on 5 distinct anomaly benchmarks, establishing the classic baseline for our study. Specifically, we extract pixel-level anomaly scores using three different scoring functions (MSP, Max Logit, and Max Entropy), and evaluate the results using AuPRC and FPR@TPR95 metrics.
- **STEP7.ipynb** computes the anomaly maps and evaluates the baseline performance across 5 anomaly datasets. Additionally, it computes the mIoU score on the standard Cityscapes validation set to ensure that the pre-trained ERFNet model maintains high performance on In-Distribution semantic segmentation.

  
In STEP 8 we compared four different baseline methods (MSP, Max Logit, Max Entropy and RbA) to extract anomaly scores from the model's predictions over 5 distinct anomaly benchmarks. To further improve the anomaly segmentation results, we performed Temperature Scaling calibration where we compute an empirical grid search over a set of temperatures. For each method and temperature, the notebooks **STEP8_Cityscapes_Coco.ipynb** and  **STEP8_CocoFineTuned.ipynb** compute anomaly detection metrics: AuPRC and FPR@TPR95. In particular:
- **STEP8_Cityscapes_Coco.ipynb** evaluates the pre-trained EoMT checkpoints (trained on Cityscapes and COCO)
- **STEP8_CocoFineTuned.ipynb** manages the conversion of our custom fine-tuned .ckpt into a .bin format and evaluates the fine-tuned EoMT model.

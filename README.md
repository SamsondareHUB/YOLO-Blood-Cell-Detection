# Blood Cell Detection on BCCD with YOLOv8

Object detection of red blood cells (RBC), white blood cells (WBC) and platelets on the BCCD (Blood Cell Count and Detection) dataset, using a YOLOv8s model trained in Google Colab on a T4 GPU.

## Overview

This project fine-tunes a pretrained YOLOv8s model to localise and classify three blood cell types in microscopy images. The notebook downloads the dataset from GitHub, converts the Pascal VOC annotations to YOLO format, trains for 20 epochs, and evaluates on the validation split with detailed logging.

## Dataset

- Source: [Shenggan/BCCD_Dataset](https://github.com/Shenggan/BCCD_Dataset)
- Classes: RBC, WBC, Platelets
- Annotations: Pascal VOC XML, converted to YOLO format in the notebook
- Splits: the train, val and test lists provided by the dataset repository

| Split | Images | Boxes |
|-------|--------|-------|
| Train | 205    | 2804  |
| Val   | 87     | 1137  |
| Test  | 72     | 945   |

## Method

| Metric        | Value |
|---------------|-------|
| Precision     | 0.871 |
| Recall        | 0.855 |
| mAP@50        | 0.922 |
| mAP@50-95     | 0.647 |

| Class     | AP@50 |
|-----------|-------|
| RBC       | 0.882 |
| WBC       | 0.993 |
| Platelets | 0.892 |

## Results

Evaluated on the validation split using the best checkpoint.

Per-class AP@50:

### Confusion matrix

![Confusion matrix](images/confusion_matrix_normalized.png)
Normalized confusion matrix on the validation split at a confidence threshold of 0.25. Columns are the true class and rows the predicted class.

### Training curves

![Training curves](images/results.png)

## Discussion

## Discussion

The model reaches an mAP@50 of 0.922 on the validation split after 20 epochs. White blood cells are detected almost perfectly (AP@50 0.993), which is expected given their large size and distinct appearance. Platelets (0.892) and red blood cells (0.882) score lower.

The normalized confusion matrix (validation split, confidence threshold 0.25) shows that the model makes essentially no errors between cell types. Every white blood cell is detected and correctly labelled, while 11% of red blood cells and 13% of platelets are missed. The remaining errors are false detections, and about 90% of them are predicted as red blood cells, the most frequent class by a wide margin (967 of the 1,137 validation instances). Likely contributors are crowded or overlapping cells and partially visible cells at image borders, where annotations are ambiguous, though this was not verified in detail.

The gap between mAP@50 (0.922) and mAP@50-95 (0.647) indicates that most cells are found but box localisation is less precise at stricter IoU thresholds. This is most pronounced for platelets (mAP@50-95 of 0.451 at a confidence threshold of 0.25), which are small enough that a few pixels of box error lowers IoU substantially.

Limitations: the dataset is small (364 images), the validation split contains only 87 images, class counts are heavily imbalanced, and results come from a single run with one seed, so the numbers should be read as indicative rather than definitive..

## Reproducing the results

1. Open `notebooks/yolov8-bccd-blood-cell-detection.ipynb` in Google Colab.
2. Set the runtime to T4 GPU (Runtime, Change runtime type).
3. Run all cells from top to bottom.

The notebook writes a timestamped log (`experiment.log`) and a `results_summary.json` file alongside the plots.

## Repository structure

```
notebooks/   Colab notebook with saved outputs
images/      Figures used in this README
README.md
```

## Acknowledgements

- BCCD dataset by Shenggan and contributors
- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics)

## Author

Samson Oluwadare, Department of Computer Science, Ekiti State University
[LinkedIn](https://www.linkedin.com/in/samson-oluwadare) | [GitHub](https://github.com/SamsondareHUB)

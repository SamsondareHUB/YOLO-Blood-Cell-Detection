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
| Train | XX     | XX    |
| Val   | XX     | XX    |
| Test  | XX     | XX    |

## Method

| Setting        | Value               |
|----------------|---------------------|
| Model          | YOLOv8s (pretrained)|
| Epochs         | 20                  |
| Image size     | 640                 |
| Batch size     | 16                  |
| Seed           | 42                  |
| Hardware       | Google Colab T4 GPU |
| Training time  | XX minutes          |

## Results

Evaluated on the validation split using the best checkpoint.

| Metric        | Value |
|---------------|-------|
| Precision     | XX.XX |
| Recall        | XX.XX |
| mAP@50        | XX.XX |
| mAP@50-95     | XX.XX |

Per-class AP@50:

| Class     | AP@50 |
|-----------|-------|
| RBC       | XX.XX |
| WBC       | XX.XX |
| Platelets | XX.XX |

### Confusion matrix

![Confusion matrix](images/confusion_matrix_normalized.png)

### Training curves

![Training curves](images/results.png)

## Discussion

Add two or three sentences here on what the confusion matrix shows, for example which classes are confused most often, and any likely reasons (overlapping cells, class imbalance, small platelet size).

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

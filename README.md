<h1 align="center">WSL_CellDino</h1>
<h2 align="center">WEAKLY SUPERVISED CELL SEGMENTATION AND TRACKING WITH TRANSFORMER</h2>

![CellDino](figures/celldino.png)

## Table of Contents

- **[Introduction](#introduction)**
- **[Installation](#installation)**
- **[Prepare Data](#prepare-data)**
- **[Training and Inference on CTC Datasets](#training-and-inference-on-ctc-datasets)**
- **[Acknowledgements](#acknowledgements)**

### Introduction

This repository introduces a **weakly supervised training method for CELL DINO**. The code for the method **WILL BE COMING SOON**.

**Key notes:**
- This weakly supervised approach is designed for all transformer-based end-to-end cell tracking and segmentation frameworks—not limited to CellDINO.
- The method lowers the annotation cost, making large-scale cell segmentation and tracking feasible with minimal supervision.
- The framework leverages transformer architectures to enable effective end-to-end learning for both cell segmentation and tracking tasks.

### Installation

See [installation instructions](INSTALL.md)

### Prepare Data

We trained and evaluated our approach on 2D datasets from the **[Cell Tracking Challenge (CTC)](http://celltrackingchallenge.net)**:

- "DIC-C2DH-HeLa"
- "Fluo-N2DH-GOWT1"
- "Phc-C2DH-U373"
- "Fluo-N2DH-SIM+"
- "Fluo-C2DL-MSC"

To train on the CTC datasets, please download and unzip the datasets from the [CTC website](http://celltrackingchallenge.net/2d-datasets/). Save the training data (without any renaming) in:
```
...\ctc_raw_data\train
```
Your `ctc_raw_data` folder should look like this:
```
ctc_raw_data
└───train
    |───DIC-C2DH-HeLa
        |───01
            └───0000.tif
            ....
        |───01_GT
        |───01_ST
        |───02
            └───0000.tif
            ....
        |───02_GT
        └───02_ST
      ....
```

Run "data_preprocess.py" to convert the raw data into the format required for training, which will be stored in the `datasets` folder:
```
datasets
└───DIC-C2DH-HeLa
    |───train
        |───01
            |───bounding_boxes
            |───images
            |───instance_mask
            └───lineage.txt
        └───02
    |───val
    └───gt	
 ....
```

After preprocessing, generate the COCO-format JSON file:
```bash
python datasets/2COCO.py
```

### Training and Inference on CTC Datasets

- **Training**

To train with CellDINO (or other transformer-based cell tracking/segmentation frameworks), use:
```cmd
python train_net.py --num_gpus 1 --train_file train_json_file_path --val_file val_json_file_path --config-file config_path MODEL.WEIGHTS /path/to/checkpoint_file
```

- **Inference**

To run inference:
```cmd
python train_net.py --nums_gpus 1 --test --submit  --config-file config_file --input_dir /path/to/input_dir --submit_dir /path/to/submit_dir MODEL.WEIGHTS /path/to/checkpoint_file
```

### Acknowledgements

Many thanks to these excellent opensource projects:

- [MaskDino](https://github.com/IDEA-Research/MaskDINO/)
- [EmbedTrack](https://github.com/kaloeffler/EmbedTrack/)

---

**Modification Explanation**  
- The README now clearly states this is a weakly supervised training method for CELL DINO and similar transformer-based cell segmentation/tracking frameworks.  
- Added a note that the code will be released soon.  
- Clarified the generality of the method for all transformer-based frameworks, not just CellDINO.  
- Highlighted the advantages of weak supervision (lower annotation cost, scalability).  
- Refined the introduction and section headings to emphasize the new method.  

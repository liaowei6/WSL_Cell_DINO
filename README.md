<h1 align="center">wSL_CellDino</h1>
<h2 align="center">WEAKLY SUPERVISED CELL SEGMENTATION AND TRACKING WITH TRANSFORMER</h2>

![CellDino](figures/celldino.png)

## Table of Contents

- **[Introduction](#introduction)**
- **[Installation](#dependencies)**
- **[Prepare Data](#prepare-data)**
- **[Training and Inference on CTC Datasets](#training-and-inference-on-ctc-datasets)**
- **[Acknowledgements](#acknowledgements)**

### Introduction

This repository provides a version of CellDino on segmentation. CellDino is a transformer-based end-to-end cell segmentation and tracking model. The tracking version will be updated soon!

**Weakly-supervised training for CELL DINO will be coming soon.**

### Installation

See [installation instructions](INSTALL.md)

### Prepare Data

We trained and evaluated our approach on 2D datasets from the **[Cell Tracking Challenge (CTC)](http://celltrackingchallenge.net)**:

"DIC-C2DH-HeLa",

"Fluo-N2DH-GOWT1",

"Phc-C2DH-U373",

"Fluo-N2DH-SIM+",

"Fluo-C2DL-MSC".

To train on the CTC datasets please download and unzip the aforementioned datasets from the CTC from [here](http://celltrackingchallenge.net/2d-datasets/). Save the training data (without any renaming[...]
```
...\ctc_raw_data\train
```
After that you should have a structure in the `ctc_raw_data` folder as follows:

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

Then run the script "data_preprocess.py" to converts the raw data into the data required for training and the converted data is stored in the `datasets` folder with the following structure:

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

After completing the data processing, run the following command to generate the JSON file in the COCO format:

```bash
python datasets/2COCO.py
```

### Training and Inference on CTC Datasets

- **Training**

To train CellDion, you can use the following command:

```cmd
python train_net.py --num_gpus 1 --train_file train_json_file_path --val_file val_json_file_path --config-file config_path MODEL.WEIGHTS /path/to/checkpoint_file
```

- **Inference**

You can using the following command to inference.

```cmd
python train_net.py --nums_gpus 1 --test --submit  --config-file config_file --input_dir /path/to/input_dir --submit_dir /path/to/submit_dir MODEL.WEIGHTS /path/to/checkpoint_file
```

### Acknowledgements

Many thanks to these excellent opensource projects:

- [MaskDino](https://github.com/IDEA-Research/MaskDINO/)
- [EmbedTrack](https://github.com/kaloeffler/EmbedTrack/)

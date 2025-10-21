# Demo testing PerSAM

See details on PerSAM [here](https://github.com/ZrrSkywalker/Personalize-SAM)

## Requirements
### Installation

`Python==3.8.20`

Install requirements from `requirements.txt`

Download default SAM weights [here](https://dl.fbaipublicfiles.com/segment_anything/sam_vit_h_4b8939.pth). Or go find sam_vit_h_4b8939.pth yourself. Models should be placed in the root directory.

## Getting Started

The input data directory should be organized as follows:
```
datadir/
|–– Annotations/
|   |–– Object1/
|       |–– 00.png
|       |–– 01.png
|–– Images/
    |–– Object1/
        |–– 00.jpg
        |–– 01.jpg
        |–– 02.jpg
        |–– ...
```
Note that only one reference image WITH annotations needs to be provided (image index `00`) to be used as the training example. Output will include inference on all images in `Images/`. In the above example directory, `00` and `01` can be used for training, but `02` is only for testing.

`cellulartestdata` has been provided as a sample.

### Usage

For our use case identifying structures in whole slide images, we use the multi-object segmentation script.

```bash
python persam_f_multi_obj.py --data "./cellulartestdata" --max_objects 50 --training_size 2 --outdir "celldata"
```
#### Args:
```bash
--data, <path to input data directory>
--outdir <outputs filename>
--ckpt <model path> # if you want to use a non-default model, mod the code too
--sam_type <model name>
--max_objects <max number of objects to segment>
--iou_threshold <threshold for detecting if a segmentation is a duplicate>
--training_size <number of training examples>
```

*iou_threshold is worth playing with. IoU = intersection area / union area. The algorithm computes this value between a new mask and all old masks, throwing out new masks when the value is over threshold FINISH ME *

*Note that `training_size` is a custom parameter, not part of the original PerSAM. Only works for `persam_f_multi_obj`. Default is 1, if you change this value you must provide the according number of reference image+annotation examples or else unexpected behavior. (for now)*

After running, the output masks and visualizations will be stored at `outputs/<output filename>`. 

## Acknowledgement
Credits to PerSAM and all of their creditors.
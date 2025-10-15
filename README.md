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
|–– Images/
    |–– Object1/
        |–– 00.jpg
        |–– 01.jpg
        |–– ...
```
Note that only one reference image with annotations needs to be provided (image index 00). Output will include inference on all images in `Images/`.

`cellulartestdata` has been provided as a sample.

### Usage

For our use case identifying structures in whole slide images, we use the multi-object segmentation script.

```bash
python persam_f_multi_obj.py --data "./cellulartestdata" --max_objects 50 --outdir "celldata"
```
#### Args:
```bash
--data, <path to input data directory>
--outdir <outputs filename>
--ckpt <model path> # if you want to use a non-default model, mod the code too
--sam_type <model name>
--max_objects <max number of objects to segment>
--iou_threshold <threshold for detecting if a segmentation is a duplicate>
```

After running, the output masks and visualizations will be stored at `outputs/<output filename>`. 

## Acknowledgement
Credits to PerSAM and all of their creditors.
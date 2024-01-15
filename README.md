# GARField: Group Anything with Radiance Fields

This is the official implementation for [GARField](https://www.garfield.studio).

<div align='center'>
<img src="https://www.garfield.studio/data/garfield_training.jpg" height="230px">
</div>

### TODO
- [ ] Update GARField use section, with videos of example usage

## Installation
1. Install nerfstudio from source. This project requires the latest version of nerfstudio
(more specifically, the new viewer based on viser).
```
git clone git@github.com:nerfstudio-project/nerfstudio.git
cd nerfstudio
pip install -e .
```

2. To use GARField with Gaussian Splatting, `cuml` is required (for global clustering).
The best way to install it is through conda: `conda install -c rapidsai -c conda-forge -c nvidia cuml`

3. Install GARField!
```
git clone git@github.com:chungmin99/garfield.git
pip install -e .
```

This installs both `garfield` (NeRF geometry), and `garfield-gauss` (Gaussian geometry).
Note that `garfield-gauss` requires reference to a fully trained `garfield` checkpoint,
as it relies on the affinity field from `garfield`. See the main paper for more details.

## Running GARField
You can use it like any other third-party nerfstudio project.
```
ns-train garfield --data /your/data/here
```
Note that GARField will pause to generate groups using Segment-Anything at around 2000 steps
(set by default, this can be set in GarfieldPipeline).
Afterwards, you can start interacting with the affinity field. Here we're using
[`donuts`](https://drive.google.com/file/d/1CK-gZ-GuxESWkbmPc3VtlEgdjd2Ijkii/view?usp=drive_link) scene from LERF.
1. PCA visualization of affinity field: select `instance` as the output type,
   and change the value of `scale` slider.
2. Affinity visualization between 3D point and scene: use "Click" button to
   select the point, and select `instance_interact` as the output type. 
   You might need to drag the viewer window slightly to see this output type.
   Again, interact with the `scale` slider!
   
⚙️...example video coming soon

Also, note: the results can change a lot between 2k to 30k steps. 

Once the model is trained to completion, you can use the outputted config file for `garfield-gauss`.

## Running GARField with Gaussian Splatting geometry!
Although GARField's affinity field is optimized using NeRF geometry, it can be
used to group and cluster gaussians in 3D!
```
ns-train garfield-gauss --data /your/data/here --pipeline.garfield-ckpt outputs/your/data/garfield/.../config.yml
```
1. Interactive selection
2. Global clustering
   
⚙️...example video coming soon

## Citation
If you use this work or find it helpful, please consider citing: (bibtex)

```
@inproceedings{garfield2024,
 author = {Kim, Chung Min and Wu, Mingxuan and Kerr, Justin and Tancik, Matthew and Goldberg, Ken and Kanazawa, Angjoo},
 title = {GARField: Group Anything with Radiance Fields},
 booktitle = {arXiv},
 year = {2024},
}
```

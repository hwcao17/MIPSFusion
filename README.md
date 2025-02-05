# MIPSFusion
This project is based on our SIGGRAPH Asia 2023 paper, [MIPS-Fusion: Multi-Implicit-Submaps for Scalable and Robust Online Neural RGB-D Reconstruction](https://arxiv.org/pdf/2308.08741.pdf)


## Introduction
MIPSFusion is a neural RGB-D SLAM method based on multi-implicit submap representation, which enables scalable online tracking and mapping for large indoor scenes. Based on divide-and-conquer mapping scheme, each submap is assigned to learn a sub-area of the scene, as shown by the colored bounding box, and a new submap will be created when scanning a new area. This incremental strategy ensures our method has the potential to reconstruct large scenes. Besides, our method can handle fast camera motion.
<img src="fig/1.png" alt="drawing" width="700"/>


## Installation
We recommend to creat an annacoda environment from [environment.yaml](environment.yaml)
```
conda env create -f environment.yaml
conda activate MIPSFusion
```
If [pypose](https://github.com/pypose/pypose) or [tiny-cuda-nn](https://github.com/NVlabs/tiny-cuda-nn) is not installed successfully, please try to follow their official installing instructions.

Build other external dependencies
```
cd external/NumpyMarchingCubes
python setup.py install
```


## Run
```
python main.py --config {config_file}
```
For example:
```
python main.py --config configs/FastCaMo-synth/apartment_2.yaml
```
&#x1F6A8; Beforing running, please make sure that `data/datadir` in `{config_file}`(the directory storing the data of this sequence) is set correctly.

&#x27A1; The result will be saved to `{result_path}=output/{dataset_name}/{sequence_name}/0` by default. For example: `output/FastCaMo-synth/apartment_2/0`.


## Visualization and save estimated poses
You can run
```
python render_mesh.py --config {config_file} --seq_result {result_path} --ckpt {ckpt_id} --LC
```
Here `ckpt_id` is the ID corresponding to a selected checkpoint (checkpoints are periodically saved when code running), such as `100`, `500`, `final`. 

By this way, You can choose to either render the final mesh or reconstructed mesh until `100-th` (or `500-th`) frame.

For example:
```
python render_mesh.py --config configs/FastCaMo-large/floor1.yaml --seq_result output/FastCaMo-large/floor1/0 --ckpt final --LC
```
&#x27A1; The reconstructed mesh can be found at `{result_path}/result`. For example: `output/FastCaMo-large/floor1/0/result`.

&#x27A1; The estimated poses can be found at `{result_path}/poses_LC`. For example: `output/FastCaMo-large/floor1/0/poses_LC`.

&#x27A1; To get the poses estimated without loop closure, remove the `--LC` flag and the poses can be found at `{result_path}/poses_GO`

## Dataset
FastCaMo-synth dataset (proposed in [ROSEFusion](https://github.com/jzhzhang/ROSEFusion)) can be found [here](https://1drv.ms/u/c/b190b6248ff4b487/EYDML_iplvpCht3XPdxoolYBRznXPXOWnigS-B6SxKKc3g?e=eLk9HZ)(with GT poses), and our FastCaMo-large dataset can be found [here](https://drive.google.com/drive/folders/186viK0tSAFVDO_6YJbC3MGXOXzcBQT_z?usp=drive_link).


## Acknowledgement
Some codes are modified from [Neural RGB-D Surface Reconstruction](https://dazinovic.github.io/neural-rgbd-surface-reconstruction/), [NICE-SLAM](https://github.com/cvg/nice-slam), [Co-SLAM](https://github.com/HengyiWang/Co-SLAM/tree/main), [pypose](https://github.com/pypose/pypose), and [tiny-cuda-nn](https://github.com/NVlabs/tiny-cuda-nn). Thanks to all of the above.


## Citation
If you find our code or paper useful, please cite
```
@article{tang2023mips,
  title={MIPS-Fusion: Multi-Implicit-Submaps for Scalable and Robust Online Neural RGB-D Reconstruction},
  author={Tang, Yijie and Zhang, Jiazhao and Yu, Zhinan and Wang, He and Xu, Kai},
  journal={arXiv preprint arXiv:2308.08741},
  year={2023}
}
```

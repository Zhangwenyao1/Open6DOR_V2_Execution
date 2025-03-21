# SoFar Execution Benchmark (Open6DOR V2)

To assess our system, we introduce Open6DOR V2, a largescale robot manipulation benchmark designed for 6-DoF object
rearrangement in simulation. This benchmark demands robust positional and orientational reasoning in open-world settings
and supports both open-loop and closed-loop robotic control.

[Zekun Qi](https://qizekun.github.io/) *, [Wenyao Zhang]() *, [Yufei Ding](https://selina2023.github.io/) *, [Runpei Dong](https://runpeidong.web.illinois.edu/), [Xinqiang Yu](), [Jingwen Li](), [Lingyun Xu](), [Baoyu Li](https://baoyuli.github.io/), [Xialin He](https://xialin-he.github.io/), [Guofan Fan](https://github.com/Asterisci/), [Jiazhao Zhang](https://jzhzhang.github.io/), [Jiawei He](https://jiaweihe.com/), [Jiayuan Gu](https://jiayuan-gu.github.io/), [Xin Jin](http://home.ustc.edu.cn/~jinxustc/), [Kaisheng Ma](http://group.iiis.tsinghua.edu.cn/~maks/leader.html), [Zhizheng Zhang](https://scholar.google.com/citations?user=X7M0I8kAAAAJ&hl=en), [He Wang](https://hughw19.github.io/) and [Li Yi](https://ericyi.github.io/).

[![Project Page](https://img.shields.io/badge/Project-Page-Green.svg)](https://qizekun.github.io/sofar/)
[![Paper PDF](https://img.shields.io/badge/Paper-PDF-orange.svg)](https://arxiv.org/abs/2502.13143)
[![Hugging Face](https://img.shields.io/badge/🤗-Hugging_Face-yellow.svg)](https://huggingface.co/collections/qizekun/sofar-67b511129d3146d28cea9920)
[![Code License](https://img.shields.io/badge/Code%20License-Apache_2.0-green.svg)](https://github.com/tatsu-lab/stanford_alpaca/blob/main/LICENSE)
[![Data License](https://img.shields.io/badge/Data%20License-CC%20By%20NC%204.0-red.svg)](https://github.com/tatsu-lab/stanford_alpaca/blob/main/DATA_LICENSE)

<div style="text-align: center;">
    <img src="assets/teaser.jpg" width=100% >
</div>

## Installation

**Create an anaconda environment:**

```
conda create -n sofar_execution python=3.10 (any version above 3.10 should be fine)
conda activate sofar_execution
```

**Clone this repo:**

```
git clone https://github.com/Zhangwenyao1/Open6DOR_V2_Execution 
```

This repository's code is based in the [LIBERO](https://github.com/Lifelong-Robot-Learning/LIBERO.git).

**Install LIBERO:**

see [LIBERO](https://github.com/Lifelong-Robot-Learning/LIBERO.git) for installation instructions.

**Install GSNET:**

see [`GSNET/READNE.md`]

This code is based on [graspnet-baseline](https://github.com/graspnet/graspnet-baseline), you can use the code to predict the grasp.

**Install Motion Planning Moduel:**

see [`./plan/README.md`]

You need modify the checkpoint or config  path  in following files in plan:

> plan/src/utils/constants.py

The motion planning module code is based in the [ompl](https://github.com/lyfkyle/pybullet_ompl).

**Install SoFar:**

see [SoFar](https://github.com/qizekun/SoFar) for installation instructions.

**Notion:**

You have to install GroundingDINO and Florence for the evaluation.

You need modify the checkpoint or config  path  in following files in SoFar:

> SoFar/depth/metric3dv2.py
>
> SoFar/segmentation/grounding_dino.py
>
> SoFar/segmentation/sam.py
>
> SoFar/serve/pointso.py
> sofar_execution_libero.py (the output folder)

## Download Asset and Task Json

Download the [Open6dorV2 assets](https://drive.google.com/file/d/1BPfAFqq7KBbZS1WMZI054Ee5KJurW8ZG/view?usp=sharing) and extract it to `./datasets/open6dor_v2/`. The overall directory structure should be:

```
│Open6DOR_V2_Execution/datasets/objects/
├── objaverse_rescale/
│   ├── 0a51815f3c0941ae8312fc6917173ed6
│   └── ...
├── ycb_16k_backup/
│   └── 0_banana
│   └── ...
```

## Execution

**For SoFar:**

You can run the evaluation in the script folder for different track:

for the position track:

> python sofar_execution/script_open6dor_exec_motion_planning.py  sofar --grasp_track_name task_refine_rot  --root_dir you_path --output_file your_path --output_root your_path --list_file_path your_path

for the rotation track:

> python sofar_execution/script_open6dor_exec_motion_planning_rotonly.py sofar --grasp_track_name task_refine_rotonly  --root_dir you_path --output_file your_path --output_root your_path --list_file_path your_path

for the 6 dof track:

> python sofar_execution/script_open6dor_exec_motion_planning_rot.py sofar --grasp_track_name task_refine_rot  --root_dir you_path --output_file your_path --output_root your_path --list_file_path your_path

# Evaluation

> python evaluation/evaluation_sofar.py

## Acknowledgement

We would like to express our deepest gratitude to [haoran liu](https://github.com/lhrrhl0419) for the planning module and experiments !!!

## Citation

If you find our ideas / environments helpful, please cite our work at

```
@article{qi2025sofar,
  author = {Qi, Zekun and Zhang, Wenyao and Ding, Yufei and Dong, Runpei and Yu, Xinqiang and Li, Jingwen and Xu, Lingyun and Li, Baoyu and He, Xialin and Fan, Guofan and Zhang, Jiazhao and He, Jiawei and Gu, Jiayuan and Jin, Xin and Ma, Kaisheng and Zhang, Zhizheng and Wang, He and Yi, Li},
  title = {SoFar: Language-Grounded Orientation Bridges Spatial Reasoning and Object Manipulation},
  journal = {arXiv preprint arXiv:2502.13143},
  year = {2025}
}
```

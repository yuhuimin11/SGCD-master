# SGCD-master

**This is the code for our paper** `Semantic-enhanced Graph Contrastive Learning with Adaptive Denoising for Drug Repositioning`.

## Prerequisites

* `cuda version < 11.0`
* `pytorch>=1.7.1 & <=1.9`
  * Note: Pytorch version greater than 1.9 has OOM bugs. See <https://github.com/pytorch/pytorch/issues/67680>.


Example installation using [`conda`](https://conda.io):

```bash
# Use the cuda version that matches your nvidia driver and pytorch
conda install pytorch=1.8.1 cudatoolkit=10.1 pyg -c pyg -c pytorch -y
```

## Reproduction

The parameters in the paper is preloaded in [`./properties/SGCD.yaml`](properties/SGCD.yaml).
```
## Documentation
src
  │  main.py
  │  radm.py
  │  sgcd.py
  │  trainer.py
properties
  │  SGCD.yaml
  │  overall.ymal
```
### Model

The basic structure of our model an be found in `sgcd.py`.

### Training

Training-related utilities can be found in [`trainer.py`](./trainer.py).

### Config Files
The tasks can be run directly from the command line:

```bash
python main.py <task_name> [<task_name>...]
```

In a specific task, `base` option specifies the task it should inherit from.
`type` option specifies the type of operation of this configuration.
a

## Troubleshooting

<details>

<summary>CUDA Out of Memory</summary>

We run experiments with V100(32GB) GPUs, please reduce the batch size if you don't have enough resources. Be aware that smaller batch size will hurt the performance for contrastive training
If the issue persists after adjusting batch size, downgrade pytorch to as early as possible (e.g. LTS 1.8.1 as of 2021/03).
This is possibly due to memory issues in higher pytorch versions.
See <https://github.com/pytorch/pytorch/issues/67680> for more information.

</details>

<details>

<summary>torch-geometric installation is failed</summary>

Please try downgrading the cuda version. Due to library dependency, torch_cluster, torch_scatter, torch_sparse and torch_spline_conv are required to install torch-geometric installations.

</details>


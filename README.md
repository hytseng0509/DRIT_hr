
# Diverse Image-to-Image Translation via Disentangled Representations (High resolution)

Pytorch implementation for multi-modality I2I on translation tasks with high resolution images. We adopt a multi-scale generator and discriminator architecture to stable the training and enhance the quality of generated images.
The project is an extension to the "Diverse Image-to-Image Translation via Disentangled Representations(https://arxiv.org/abs/1808.00948)", ECCV 2018.

Contact: Hsin-Ying Lee (hlee246@ucmerced.edu) and Hung-Yu Tseng (htseng6@ucmerced.edu)

## Paper
Diverse Image-to-Image Translation via Disentangled Representations<br>
[Hsin-Ying Lee](http://vllab.ucmerced.edu/hylee/)\*, [Hung-Yu Tseng](https://sites.google.com/site/hytseng0509/)\*, [Jia-Bin Huang](https://filebox.ece.vt.edu/~jbhuang/), [Maneesh Kumar Singh](https://scholar.google.com/citations?user=hdQhiFgAAAAJ), and [Ming-Hsuan Yang](http://faculty.ucmerced.edu/mhyang/)<br>
European Conference on Computer Vision (ECCV), 2018 (**oral**) (* equal contribution)

Please cite our paper if you find the code or dataset useful for your research.
```
@inproceedings{DRIT,
  author = {Lee, Hsin-Ying and Tseng, Hung-Yu and Huang, Jia-Bin and Singh, Maneesh Kumar and Yang, Ming-Hsuan},
  booktitle = {European Conference on Computer Vision},
  title = {Diverse Image-to-Image Translation via Disentangled Representations},
  year = {2018}
}
```

## Example Results
<img src='imgs/hd_result.png' width="1000px"/>

## Usage

### Prerequisites
- Python 3.5 or Python 3.6
- Pytorch 0.4/1.0 and torchvision (https://pytorch.org/)
- [TensorboardX](https://github.com/lanpa/tensorboard-pytorch)
- [Tensorflow](https://www.tensorflow.org/) (for tensorboard usage)
- Docker file based on CUDA 9.0, CuDNN 7.1, and Ubuntu 16.04 is provided in the [[DRIT]](https://github.com/HsinYingLee/DRIT) github page.

### Install
- Clone this repo:
```
git clone https://github.com/hytseng0509/DRIT_HR.git
cd DRIT_HR/src
```

## Datasets
- We calidate our model on street scene datasets: [GTA](https://download.visinf.tu-darmstadt.de/data/from_games/) and [Cityscapes](https://www.cityscapes-dataset.com/)
```
cd datasets/gta2cityscapes
```
- Images from two domains should be places in folders "trainA" and "trainB" separately

## Usage
- Training
```
python3 train.py --dataroot ../datasets/gta2cityscapes -name NAME --display_dir DISPLAY_DIR --result_dir RESULT_DIR
tensorboard --logdir DISPLAY_DIR/yosemite
```
Results and saved models can be found at `RESULT_DIR/yosemite`.

- Generate results with randomly sampled attributes
  - Require folder `testA` (for a2b) or `testB` (for b2a) under dataroot
```
python3 test.py --dataroot ../datasets/gta2cityscapes -name NAME --output_dir OUTPUT_DIR --resume MODEL_FILE --num NUM_PER_IMG
```
- Generate results with attributes encoded from given images
  - Require both folders `testA` and `testB` under dataroot
```
python3 test.py --dataroot ../datasets/gta2cityscapes -name NAME --output_dir OUTPUT_DIR --resume MODEL_FILE --num NUM_PER_IMG
```
- Results can be found at `OUTPUT_DIR/NAME`

## Note
- The feature-wise transformation (i.e. `--concat 0`) is not fully tested yet
- We also implement [Mode Seeking](https://github.com/HelenMao/MSGAN) loss, specify `--ms` to apply it in the training
- Due to large number of training images in the GTA dataset, the default training epoch is set to 90. Please refer to the default setting in original [DRIT](https://github.com/HsinYingLee/DRIT) if the number of training image is around 1K.
- Feel free to contact the authors for any potential improvement of the code.

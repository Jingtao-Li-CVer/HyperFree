
<div align="center">

<h1>HyperFree: A Channel-adaptive and Tuning-free Foundation Model for Hyperspectral Remote Sensing Imagery (CVPR2025)</h1>

[Jingtao Li](https://jingtao-li-cver.github.io/home_page/)<sup>∗</sup>, [Yingyi Liu]()<sup>∗</sup>, [Xinyu Wang](https://jszy.whu.edu.cn/WangXinyu/zh_CN/index.htm)<sup>†</sup>, [Yunning Peng](), [Chen Sun](), [Shaoyu Wang](), [Zhendong Sun](), [Tian Ke](), [Xiao Jiang](), [Tangwei Lu](), [Anran Zhao](), [Yanfei Zhong](http://rsidea.whu.edu.cn/zhongyanfei.htm)<sup>†</sup>


<sup>∗</sup> Equal contribution, <sup>†</sup> Corresponding author

</div>

<p align="center">
  <a href="https://rsidea.whu.edu.cn/HyperFree.pdf" target="_blank">Paper</a> |
    <a href="https://github.com/Jingtao-Li-CVer/HyperFree" target="_blank">Code</a> |
    <a href="https://www.wjx.cn/vm/e84nlpp.aspx#" target="_blank">Hyper-Seg Engine</a> |
  <a href="https://rsidea.whu.edu.cn/hyperfree.htm" target="_blank">Website</a> |
  <a href="https://mp.weixin.qq.com/s/nm8VnTcXvvS_aEatX0543A" target="_blank">WeChat</a> 
</p >

<p align="center">
  <a href="#-Update">Update</a> |
  <a href="#-Outline">Outline</a> |
  <a href="#-Hyper-Seg-Data-Engine">Hyper-Seg Data Engine</a> |
  <a href="#-Pretrained-Checkpoint">Pretrained Checkpoint</a> |
  <a href="#-Tuning-free-Usage">Tuning-free Usage</a> |
  <a href="#-Tuning-Usage">Tuning Usage</a> |
  <a href="#-Segment-Any-HSI-Usage">Segment Any HSI Usage</a> |
  <a href="#-Acknowledgement">Acknowledgement</a>
</p >

# 🔥 Update
**2026.10.22**
- We have uploaded a new mask version for HyperSeg with location information in **([Hyper-Seg](https://www.wjx.cn/vm/e84nlpp.aspx#))**.

**2026.7.27**
- We have uploaded HyperImageNet, the largest hyperspectral benchmark with 26,084 airborne hyperspectral image patches, 224 spectral bands, and 138 fine-grained land-cover categories. **([HyperImageNet](https://arxiv.org/abs/2607.21050))**.
  
**2025.04.23**
- Bugs are fixed for tuning-free classification and detection tasks.
  
**2025.04.17**
- The script to tune HyperFree decoder only for different semantic segmentation tasks. `Efficient_decoder_tuning.py`

**2025.04.15**
- UperNet with HyperFree as backbone is uploaded for full tuning comparison. `Full-Tuning-with-UperNet.py` 

**2025.04.06**
- Hyper-Seg has been moved to a new website for faster download! **([Hyper-Seg](https://www.wjx.cn/vm/e84nlpp.aspx#))**
- Some bugs are fixed

**2025.04.05**
- Checkpoints of HyperFree-l and HyperFree-h are released! **([Huggingface](https://huggingface.co/JingtaoLi/HyperFree/tree/main))** 

**2025.02.27**
- HyperFree is accepted by CVPR2025! **([paper](https://rsidea.whu.edu.cn/HyperFree.pdf))** 

# ✨ Outline
1. We propose the first tuning-free hyperspectral foundation model, which can process any hyperspectral image in different tasks with **promptable or zero-shot manner**.
2. A weight dictionary that spans the full spectrum, enabling **dynamic generation of the embedding layer for varied band numbers** according to input wavelengths.
3. We propose to map both prompts and masks into feature space to **identify multiple semantic-aware masks for one prompt**, where different interaction workflows are designed for each downstream tasks.
4. We built the Hyper-Seg data engine to train the HyperFree model and tested it on **11 datasets from 5 tasks in tuning-free manner**, **14 datasets from 8 tasks in tuning manner** as an extensive experiment.

<figure>
<div align="center">
<img src=figs/framework.png width="95%">
</div>

<div align='center'>

Overview of HyperFree.

</div>
<br>

<table>
  <tr>
    <td style="width: 50%; padding-right: 0px;"> 
      <figure>
        <img src="figs/tuning-free-res.png" alt="Image 1" style="width: 100%; height: auto;">
        <figcaption style="text-align: center;">Results in tuning-free manner.</figcaption>
      </figure>
    </td>
    <td style="width: 50%; padding-left: 0px;">
      <figure>
        <img src="figs/tuning-res.png" alt="Image 2" style="width: 100%; height: auto;">
        <figcaption style="text-align: center;">Results in tuning manner.</figcaption>
      </figure>
    </td>
  </tr>
</table>

# 📂 Hyper-Seg Data Engine
1. We built a data engine called Hyper-Seg to generate segmented masks automatically for spectral images and expand the data scale for promptable training. Below is the engine workflow and we finally obtained **41900 high-resolution image pairs with size of 512×512×224**.
2. The dataset is available at [here](https://www.wjx.cn/vm/e84nlpp.aspx#). 

<p align="center">
  <img src="figs/data_engine.png" width="600"> 
</p>

# 🚀 Pretrained Checkpoint
HyperFree is mainly tested with ViT-b version and the corresponding checkpoint is available at [Hugging Face](https://huggingface.co/JingtaoLi/HyperFree/tree/main). Download it and put in the Ckpt folder.
| Method | Backbone | Model Weights |
| :------- | :------: | :------: |
| HyperFree-b | ViT-b | [Hugging Face](https://huggingface.co/JingtaoLi/HyperFree/blob/main/Ckpt/HyperFree-b.pth)| 
| HyperFree-l | ViT-l | [Hugging Face](https://huggingface.co/JingtaoLi/HyperFree/blob/main/Ckpt/HyperFree-l.pth)|
| HyperFree-h | ViT-h | [Hugging Face](https://huggingface.co/JingtaoLi/HyperFree/blob/main/Ckpt/HyperFree-h.pth)| 

# 🔨 Tuning-free Usage 

HyperFree can complete five tasks including multi-class classification, one-class classification, target detection, anomaly detection, and change detection in tuning-free manner. We have provided both sample data ([Data](https://huggingface.co/JingtaoLi/HyperFree/tree/main) folder) and corresponding scripts (Fine-tuning-free-manner Folder).

**Tips**: In practice, we find that preprocessing operations such as selecting discriminative bands and contrast enhancement can significantly improve the processing performance

1. **Hyperspectral multi-class classification**. For each new image, change the below hyper-paramaters for **promptable classification**.
```python
data_path = "./../../Data/hyperspectral_classification/WHU-Hi-LongKou.tif"
wavelengths = [429.410004,  439.230011,  449.059998,......]
GSD = 0.456  # Ground sampling distance (m/pixel)

num_classes = 3  # At least one prompt for each class
few_shots[0][120, 324] = 1
few_shots[1][258, 70] = 1
few_shots[2][159, 18] = 1
```
2. **Hyperspectral one-class classification**. For each new image, change the below hyper-paramaters for **promptable classification**.
```python
    parser.add_argument('-ds', '--data_path', type=str,
                        help='Dataset')
    parser.add_argument('-sl', '--wavelengths', type=str,
                    help='Central wavelength of sensor')
    parser.add_argument('-g', '--GSD', type=float, default='0.043', help='Ground sampling distance (m/pixel)')
    parser.add_argument('-p', '--prompt_point', nargs='+', type=int, default=[600, 90],
                        help='The index of prompt_point')
```
3. **Hyperspectral target detection**. For each new image, change the below hyper-paramaters for **promptable segmentation**.
```python
img_pth = './../../Data/hyperspectral_target_detection/Stone.mat'
wavelengths = [429.410004,  439.230011,  449.059998,......]
GSDS = 0.07 # Ground sampling distance (m/pixel)
target_spectrum = './../../Data/hyperspectral_target_detection/target_spectrum_stone.txt' # Storing the target spectraum
```
4. **Hyperspectral anomaly detection**. For each new image, change the below hyper-paramaters for **zero-shot detection**.
```python
path = './../../Data/hyperspectral_anomaly_detection/abu-beach-2.mat'
wavelengths = [429.410004,  439.230011,  449.059998,......]
GSDS = 7.5 # Ground sampling distance (m/pixel)
area_ratio_threshold = 0.0009 # Decide how small the targets are anomalies
```
5. **Hyperspectral change detection**. For each new image, change the below hyper-paramaters for **zero-shot detection**. (mask_path is optional)
```python
img1_paths = ['./../../Data/hyperspectral_change_detection/Hermiston/val/time1/img1_1.tif', ......] # Images at first time-step
img2_paths = ['./../../Data/hyperspectral_change_detection/Hermiston/val/time2/img2_1.tif', ......] # Images at second time-step

wavelengths = [429.410004,  439.230011,  449.059998,......]
GSD = 30 # Ground sampling distance (m/pixel)
ratio_threshold = 0.76 # a float, pixels with the change score higher than ratio_threshold quantile are considered as changes
```
# 🔨 Tuning Usage 
1. **Full-tuning**. If you want to tune the whole HyperFree, we have provided the `Full-Tuning-with-UperNet.py` to load the model.
2. **Efficient-tuning**. If you want to tune the HyperFree decoder only, we have provided the `Efficient_decoder_tuning.py` to load the model.

# 🔨 Segment Any HSI Usage similar to SAM
1. **Segment Everyting** If you want to use the full-spectrum segmented masks for your own task. Please use the `Seg_Any_HSI.py` script, where the hyper-paramaters below need to be changed.
```python
data_path = "./../../Data/hyperspectral_classification/WHU-Hi-LongKou.tif"
wavelengths = [429.410004,  439.230011,  449.059998,......]
GSD = 0.456  # Ground sampling distance (m/pixel)
pred_iou_thresh = 0.6  # Controling the model's predicted mask quality in range [0, 1].
stability_score_thresh = 0.6  # Controling the stability of the mask in range [0, 1].
```
2. **Segment Cerain Mask** If you only want to segment certain mask given point prompt, please use `Seg_Any_HSI_given_one_prompt.py` script. Each prompt would output three masks.

# ⭐ Citation

```
Li J, Liu Y, Wang X, et al. HyperFree: A Channel-adaptive and Tuning-free Foundation Model
for Hyperspectral Remote Sensing Imagery[J]. arXiv preprint arXiv:2503.21841, 2025.
``` 


# 💖 Acknowledgement
This project is based on [SAM](https://segment-anything.com/). Thank them for bringing prompt engineering from NLP into the visual field!<br>


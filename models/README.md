# JDNet：Joint Self-Attention and Scale-Aggregation for Self-Calibrated Deraining Network

[Cong Wang](https://supercong94.wixsite.com/supercong94)\*, [Yutong Wu](https://github.com/Ohraincu)\*, [Zhixun Su](http://faculty.dlut.edu.cn/ZhixunSu/zh_CN/index/759047/list/index.htm) †, Junyang Chen 

<\* Both authors contributed equally to this research. † Corresponding author.>

This work has been accepted by ACM'MM 2020. [\[Arxiv\]](https://arxiv.org/abs/2008.02763) 

<div align=center>
<img src="https://github.com/Ohraincu/JDNet/blob/master/fig/result.png" width="60%">

Fig1：An example from real-world datasets.
</div>

## Abstract
In this paper, we propose an effective algorithm, called JDNet, to solve the single image deraining problem and conduct the segmentation and detection task for applications. Specifically, considering the important information on multi-scale features, we propose a Scale-Aggregation module to learn the features with different scales. Simultaneously, Self-Attention module is introduced to match or outperform their convolutional counterparts, which allows the feature aggregation to adapt to each channel. Furthermore, to improve the basic convolutional feature transformation process of Convolutional Neural Networks (CNNs), Self-Calibrated convolution is applied to build long-range spatial and inter-channel dependencies around each spatial location that explicitly expand fields-of-view of each convolutional layer through internal communications and hence enriches the output features. By designing the Scale-Aggregation and Self-Attention modules with Self-Calibrated convolution skillfully, the proposed model has better deraining results both on real-world and synthetic datasets. Extensive experiments are con- ducted to demonstrate the superiority of our method compared with state-of-the-art methods.

<div align=center>
<img src="https://github.com/Ohraincu/JDNet/blob/master/fig/overall.png" width="80%" height="80%">

Fig2：The architecture of Joint Network for deraining (JDNet).
</div>

## Requirements
- CUDA 9.0
- Python 3.6 (or later)
- Pytorch 1.1.0
- Torchvision 0.3.0
- OpenCV

## Dataset
Please download the following datasets:

* Rain12  [[dataset](http://yu-li.github.io/paper/li_cvpr16_rain.zip)]
* Rain100L [[dataset](http://www.icst.pku.edu.cn/struct/Projects/joint_rain_removal.html)]
* Rain100H [[dataset](http://www.icst.pku.edu.cn/struct/Projects/joint_rain_removal.html)]
* Real-world images [[dataset](https://pan.baidu.com/s/1gpuB6NUHPnQEtgRn4evr5A)](password:vvuk)

## Setup
Please download this project through 'git' command.
All training and testing experiments are in a folder called [code](https://github.com/Ohraincu/JDNet/tree/master/code):
```
$ git clone https://github.com/Ohraincu/JDNet.git
$ cd code
```  
Next, we can see folders in the following form:

    |--ablation  
        |--r1  
        |--r2

    |--base 
        |--rain100H 
        |--rain100L

    |--diff_loss
        |--mae
        |--mse

The implementation code in our work is in the [base](https://github.com/Ohraincu/JDNet/tree/master/code/base) folder. In the [ablation](https://github.com/Ohraincu/JDNet/tree/master/code/ablation) folder, there are two experimental codes for ablation learning mentioned in the paper. The only difference between the code in the [loss](https://github.com/Ohraincu/JDNet/tree/master/code/loss) folder and the [base](https://github.com/Ohraincu/JDNet/tree/master/code/base) is that different loss functions are used in the training process.

Thanks to [the code by Li et al.](https://xialipku.github.io/RESCAN/), our code is also adapted based on this.

## Training
After you download the above datasets, you can perform the following operations to train:
```
$ cd config
$ python train.py
```  
You can pause or start the training at any time because we can save the pre-trained models (named 'latest_net' or 'net_x_epoch') in due course.

## Testing
After running eval.py, you can get the corresponding numerical results (PSNR and SSIM):
```
$ python eval.py
``` 
If the visual results on datasets need to be observed, the show.py can be run:
```
$ python show.py
``` 
All the pre-trained model in each case is placed in the corresponding 'model' folder, and the 'latest_net' model is directly referenced by default. If you want to generate results for your training intermediate model, you can make the following changes to eval.py or show.py:
```
parser.add_argument('-m', '--model', default='net_x_epoch')
```

## Supplement to settings.py
One thing to note is that, there are two types of input in our training or testing.

One takes a paired image as input, and the other uses a single rainy image, as shown in Fig3 and Fig4 respectively.

<div align=center>
<table>
    <tr>
        <td ><center><img src="https://github.com/Ohraincu/JDNet/blob/master/fig/ex_pair.png" width="600"></center></td>
        <td ><center><img src="https://github.com/Ohraincu/JDNet/blob/master/fig/ex_unpair.png" width="200"></center></td>
    </tr>
    <tr>
        <td >Fig3: Paired image.</td>
        <td >Fig4: Unpaired image.</td>
    </tr>
</table>
</div>

For the different forms of input images, we need to modify some settings in the settings.py:

```
pic_is_pair = True  #input picture is pair or single
data_dir = '/Your_paired_datadir'
if pic_is_pair is False:
    data_dir = '/Your_unpaired_datadir'
```
At this point, if you have the following representation in your train/eval/show.py:

```
dt = sess.get_dataloader('test')
```
The path of the dataset you are about to run is: "/Your_paired_datadir/test"



## Citation
Wait for update！

## Contact

If you are interested in our work or have any questions, please directly contact my github.
Email: ytongwu@mail.dlut.edu.cn / supercong94@gmail.com

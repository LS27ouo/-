1.工具论文简介  
**Data augmentation using learned transformations for one-shot medical image segmentation**  
[Amy Zhao](https://people.csail.mit.edu/xamyzhao), [Guha Balakrishnan](https://people.csail.mit.edu/balakg/), [Fredo Durand](https://people.csail.mit.edu/fredo), [John Guttag](https://people.csail.mit.edu/guttag), [Adrian V. Dalca](adalca.mit.edu)  
CVPR 2019. [eprint arXiv:1902.09383](https://arxiv.org/abs/1902.09383)

2.运行要求  
* Python 3.6+ (Python 2.7 may work but has not been tested)
* CUDA 10.0+
* Tensorflow 1.13+ and Keras 2.2.4+

3.功能模块  
一共有三个模块，分别是数据集模块，源代码模块和实验结果输出模块。  
数据集模块放在`data/`文件夹，数据集类型为`.npz`文件。  
源代码模块放在了`src/`文件夹，`ext/`是代码运行需要的额外包。  
实验结果输出模块放在了`experiments/`文件夹，在这里你可以查看代码运行的具体输出和结果文件。  

4.运行方式  
你需要按照先训练模型数据然后再进行数据扩增。  
具体的操作为：  
你需要先用一个带标签的样本训练spatial和appearance的转换模型，然后再训练无标签的样本集。 
a.训练转换模型：  
训练spatial转换模型时首先前向传播，接着后向传播   
python main.py trans --gpu 0 --data mri-100unlabeled --model flow-fwd  
python main.py trans --gpu 0 --data mri-100unlabeled --model flow-bck  
训练apperance转换模型  
python main.py trans --gpu 0 --data mri-100unlabeled --model color-unet  
b.数据扩增和分割训练：  
python main.py seg --gpu 0 --data mri-100unlabeled  
注：gpu 0 是指gpu的id，你也可以设置别的id，mri-100unlabeled是本项目使用的数据集名称，你也可以使用自己的数据集，只要在这里改变名字。

5.实验结果  
你可以在experiments文件夹中找到扩增的mri图像和训练完的模型
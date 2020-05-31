## 智能垃圾分类系统作业

### 1.代码结构

```
 {repo_root}
  ├── models	//模型文件夹
  ├── utils		//一些函数包
  |   ├── eval.py		// 求精度
  │   ├── misc.py		// 模型保存，参数初始化，优化函数选择
  │   ├── radam.py
  │   └── ...
  ├── args.py		//参数配置文件
  ├── build_net.py		//搭建模型
  ├── dataset.py		//数据批量加载文件
  ├── preprocess.py		//数据预处理文件，生成坐标标签
  ├── train.py		//训练运行文件
  ├── transform.py		//数据增强文件
```

![image-20200531180305710](C:\Users\42543\AppData\Roaming\Typora\typora-user-images\image-20200531180305710.png)

### 2. 环境设置

python版本为3.6，具体的函数包如下（其实只要是最新版本的就好）：

* pytorch>=1.0.1
* torchvision==0.2.2
* matplotlib>=3.1.0
* numpy>=1.16.4
* scikit-image
* pandas
* sklearn

## 3.运行步骤

1. 建立文件夹data，把garbage_classify全部解压缩到data下

2. 运行preprocess.py，生成训练集和测试集运行文

3. 单张显卡的话，修改arg.py 85行 parser.add_argument('--gpu-id', default='0, 1, 2, 3' 为'--gpu-id', default='0'，同时修改 '--train-batch'，'--test-batch'为适当的数字

4. 你还需要注意除了`train_batch`以外还要对`epoch`即训练的总次数设置成一个适当的值。

5. 这里可以给出一个数据：

   > GTX 1070显卡，8G显存，16G电脑内存，单GPU
   >
   > train_batch = 2 ( 若是 > 2 ，会报GPU内存不足的问题 )，基本上1个 epoch 大概 45分钟左右

6. 运行train.py

7. 其中args.py文件存放了读取数据集的路径，以及保存模型结果的路径，在本地运行的时候需要修改自身配置的路径

## 4.遇到的问题及一些注意事项

* （1）首先就是，所有的路径必须是`纯英文`、`纯英文`、`纯英文`，重要的事情说三遍！！！
* （2）在运行 preprocess.py 的时候要注意生成文件的路径。
* （3）如何去查看你电脑有记得GPU呢？访问电脑路径 `C:\Program Files\NVIDIA Corporation\NVSMI` 通过 cmd 进入此路径，然后运行 `nvidia-smi.exe` 之后就会给出你电脑的GPU运行情况，以下给出我电脑的 GPU 运行情况，如果有多个的话，会如橘黄色框框中显示的一样，按照 0-n 的序号向下排列，然后根据自己的情况，操作 **运行步骤-3**。

![image-20200531180654177](C:\Users\42543\AppData\Roaming\Typora\typora-user-images\image-20200531180654177.png)

* （4）在运行train.py的过程中你有可能会遇到一下问题，提示你说你的 GPU 的内存不足。这时候你得尝试将args.py 中的 `train_batch`（即 batch_size） 的值设置的小一点，但这也意味着训练一个 epoch 的时间将会**非常的漫长，并且一旦值设置的还不够小:**
  * **轻则训练第一轮的时候就会提示你 GPU 容量不足并中断程序；**
  * **重则他在训练中途会突然中断并对你进行嘲讽（Buy a new RAM），等于需要再花费更多的时间从新训练！！！！**

![QQ图片20200531182512](C:\Users\42543\Desktop\QQ图片20200531182512.png)

![image-20200531183918910](C:\Users\42543\AppData\Roaming\Typora\typora-user-images\image-20200531183918910.png)

* 这里是 需要这设置的地方

![image-20200531182827524](C:\Users\42543\AppData\Roaming\Typora\typora-user-images\image-20200531182827524.png)

![image-20200531183955287](C:\Users\42543\AppData\Roaming\Typora\typora-user-images\image-20200531183955287.png)

* （5）需要注意生成文件的路径。
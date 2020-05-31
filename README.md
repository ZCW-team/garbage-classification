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

### 2. 环境设置

python版本为3.6，具体的函数包如下：

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
4. 运行train.py
5.其中args.py文件存放了读取数据集的路径，以及保存模型结果的路径，在本地运行的时候需要修改自身配置的路径

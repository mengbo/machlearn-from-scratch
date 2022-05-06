# 极客时间《零基础实战机器学习》课程代码

[《零基础实战机器学习》](https://time.geekbang.org/column/intro/100085501) 是极客时间的一门关于机器学习的入门课，本项目的代码是从黄佳老师的代码 fork 而来，并进行了整理。

## 环境配置

按照 [为学习数学配置软件环境](https://zhuanlan.zhihu.com/p/98674607) 的思路，首先需要安装 Pythone 环境：

```shell
brew install python pipenv jupyterlab
```

通过如下命令来配置环境：

```shell
git clone https://github.com/mengbo/machlearn-from-scratch.git
cd machlearn-from-scratch

pipenv --python 3
pipenv install

# pipenv install ipykernel
pipenv run python3 -m ipykernel install --user --name machlearn

# pipenv install numpy pandas matplotlib
	
# pipenv install plotly nbformat
jupyter labextension install jupyterlab-plotly

# pipenv install seaborn

# pipenv install scikit-learn xgboost

# pipenv install opencv-python

# pipenv install tensorflow keras pydot
brew install graphviz

# pipenv install lifelines

# pipenv install flask
```

通过如下命令运行 JupyterLab，Kernel 选择 machlearn：

```
jupyter lab
```

对于测试数据集 [Flowers Recognition](https://www.kaggle.com/datasets/alxmamaev/flowers-recognition) 已经拷贝到项目目录下的 `input/flowers-recognition` 目录中。


## 细节问题

### matplotlib.pyplot 中文问题

可以通过增加程序代码的方式解决：

```python
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif']=['FangSong']
plt.rcParams['axes.unicode_minus']=False
```

也可以通过修改配置文件解决：

```shell
echo "font.sans-serif: FangSong" > ~/.matplotlib/matplotlibrc
echo "axes.unicode_minus: False" >> ~/.matplotlib/matplotlibrc
```

### TensorFlow 错误提示

由于没有优化编译，会产生一些错误提示，完全可以忽略，也可以通过设置如下环境变量解决：

```shell
export TF_CPP_MIN_LOG_LEVEL=2
```

也可以直接在代码中设置：

```python
import os os.environ['TF_CPP_MIN_LOG_LEVEL']='2'
```


### JupyterLab 下 SVG 图片显示不全

TensorFlow 中的 model_to_dot 产生的 SVG 图片在 JupyterLab 下面显示不全，虽然可以通过调整 CSS 等方法解决，但最简单的办法是修改图片的 DPI 值，例如如下代码：

```python
SVG(model_to_dot(cnn, show_shapes=True, dpi=65).create(prog='dot', format='svg'))
```

### 逻辑回归的 max_iter 参数值

当 `sklearn.linear_model.LogisticRegression` 的  `max_iter` 参数设置的比较小时，损失函数没有收敛，会出现警告。对于模型的训练和预测效果都已经不错的情况，不需要再增加 `max_iter` 值，一切以预测效果为基准。

建议修改参数为：`LogisticRegression(solver='lbfgs', max_iter=1000)`


## 思维导图

![思维导图](https://github.com/mengbo/machlearn-from-scratch/blob/main/machlearn-from-scratch.mm.png?raw=true)


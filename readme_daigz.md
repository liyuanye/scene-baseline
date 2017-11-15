## 环境配置
为了方便管理，conda 新建一个虚拟环境：
```bash
conda create --name pytorch python=3.6
source activate pytorch  # 进入 pytorch 环境
```
安装python3.6、CUDA8.0的pytorch，挂上代理，否则 pytorch 下载很慢：
```bash
conda install pytorch torchvision cuda80 -c soumith
```
在requirements.txt所在目录安装Fire, Visdom, tnt等packages：
```bash
pip install -r requirements.txt
```
**关于 Visdom**:
启用 Visdom 时会以为被墙，加上终端没有走sock5翻墙，会导致 connection timed out。
将react-grid-layout.min.js 和 plotly-plotly.min.js这两个文件下载下来放到 .../visdom/static/js/ 中。通过百度云下载：
链接: https://pan.baidu.com/s/1bo25jrD
密码: 8uct

## 准备数据集
注意新建文件夹、文件路径和名称：
```
train_dir = '/data/image/ai_cha/scene/sl/train/'
test_dir = '/data/image/ai_cha/scene/sl/testa'
val_dir = '/data/image/ai_cha/scene/sl/val'
meta_path = '/data/image/ai_cha/scene/sl/scene.pth'
```

## 改不支持 Python3.6 的代码
utils.py 文件中:
line 15 和 line 63 行的 iteritems() 改为items()

## 启动Visdom
新建一个终端：
```bash
source activate pytorch
python -m visdom.server
```
成功启用 Visdom 的话，打开 localhost:8097 会看到蓝色大背景。

## 训练1
新建 checkpoints 目录用来保存模型。

新建一个终端：
```bash
python main.py train --model='resnet34'
```

## 给测试数据集分类
```bash
python main.py submit --model='resnet34' --load-path='res34_1018_2204_0.938002232143' 
```

## 训练2：
将下载的预训练模型 whole_resnet50_places365.pth.tar 放到 checkpoints。
```bash
python main.py train --model='resnet365'
```

## 修改
by lee
utils.py
line 21	unicode() str()


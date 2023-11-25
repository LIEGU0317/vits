# 如何使用

## Python Version
### Python3.10
```bash
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu116
```
### Python3.7
```bash
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu110
```

## 克隆这个仓库

```sh
git clone https://github.com/CjangCjengh/vits.git
```

## 选择清洗器（cleaners）

- 在 config.json 中填写 "text_cleaners"
- 编辑 text/symbols.py
- 从 text/cleaners.py 中移除不必要的导入项

## 安装依赖

```sh
pip install -r requirements.txt
```

## 创建数据集

### 单一发音人

在 config.json 中 "n_speakers" 应设为0

```
path/to/XXX.wav|转录文字
```

- 示例

```
dataset/001.wav|こんにちは。
```

### 多个发音人

发音人ID应从0开始

```
path/to/XXX.wav|发音人ID|转录文字
```

- 示例

```
dataset/001.wav|0|こんにちは。
```

## 预处理

如果你已经完成这一步，在 [config.json](config_parameters.md) 中将 "cleaned_text" 设置为 true

```sh
# 单一发音人
python preprocess.py --text_index 1 --filelists path/to/filelist_train.txt path/to/filelist_val.txt --text_cleaners chinese_cleaners

# 多个发音人
python preprocess.py --text_index 2 --filelists path/to/filelist_train.txt path/to/filelist_val.txt --text_cleaners chinese_cleaners
```

## 构建单调对齐搜索

```sh
cd monotonic_align
#mkdir "monotonic_align"  # Windows
python setup.py build_ext --inplace
cd ..
```

## 训练

```sh
# 单一发音人
python train.py -c <配置> -m <文件夹>

# 多个发音人
python train_ms.py -c <配置> -m <文件夹>
```

## 推理

### 在线

查看 [inference.ipynb](inference.ipynb)

### 离线

查看 [MoeGoe](https://github.com/CjangCjengh/MoeGoe)

# 在Docker中运行

```sh
docker run -itd --gpus all --name "容器名称" -e NVIDIA_DRIVER_CAPABILITIES=compute,utility -e NVIDIA_VISIBLE_DEVICES=all "镜像名称"
```

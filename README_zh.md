# 如何使用

> 如果你也没有GPU资源，可以尝试使用 Featurize 平台。以下是我的[邀请链接](https://featurize.cn?s=fd01af08da454204adf7aef8e07caa64)。

在 Featurize 平台上，你可以找到以下资源：
- [paimon中文语音数据集-单声道-22050Hz](https://featurize.cn/datasets/paimon_video)
- [paimon中文语音数据集-单声道-48000Hz](https://featurize.cn/datasets/paimon_audio_v2)

**当前使用环境**

- **硬件和软件配置**：
  - Python 3.7
  - CUDA 11.2
  - Telsa V100 GPU
- **安装的库**：
  - PyTorch 1.6.0 (CUDA 10.1 版本)
  - torchaudio 0.6.0
  - torchvision 0.7.0 (CUDA 10.1 版本)
- **基于 Featurize 基础环境**：
  - PyTorch 1 环境（兼容性好）
  - Docker 20.10.10
  - Python v3.7
  - PyTorch v1.10
  - TensorFlow v2.7.0


## Python 版本

### Python 3.7
```bash
pip install torch==1.6.0+cu101 torchvision==0.7.0+cu101 torchaudio==0.6.0 -f https://download.pytorch.org/whl/torch_stable.html
```

### Python 3.10
```bash
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu116
```

## 克隆这个仓库

```sh
git clone https://github.com/LIEGU0317/vits.git
```

## 选择清洗器（Cleaners）

> 仓库已针对中文训练进行了修改，训练中文时可跳过此步骤。

- 在 `config.json` 中填写 `"text_cleaners"`
- 编辑 `text/symbols.py`
- 从 `text/cleaners.py` 中移除不必要的导入项

## 安装依赖

```sh
pip install -r requirements.txt  # 或 requirements_py310.txt
```

## 创建数据集

### 单一发音人

在 `config.json` 中 `"n_speakers"` 应设为 0。

格式：
```
path/to/XXX.wav|转录文字
```

示例：
```
dataset/001.wav|こんにちは。
```

### 多个发音人

发音人 ID 应从 0 开始。

格式：
```
path/to/XXX.wav|发音人ID|转录文字
```

示例：
```
dataset/001.wav|0|こんにちは。
```

## 预处理

如果你已经完成这一步，在 [config.json](config_parameters.md) 中将 `"cleaned_text"` 设置为 true。

```sh
# 单一发音人
python preprocess.py --text_index 1 --filelists path/to/filelist_train.txt path/to/filelist_val.txt --text_cleaners chinese_cleaners

# 多个发音人
python preprocess.py --text_index 2 --filelists path/to/filelist_train.txt path/to/filelist_val.txt --text_cleaners chinese_cleaners
```

## 构建单调对齐搜索

```sh
cd monotonic_align
mkdir "monotonic_align"
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

# 在 Docker 中运行

```sh
docker run -itd --gpus all --name "容器名称" -e NVIDIA_DRIVER_CAPABILITIES=compute,utility -e NVIDIA_VISIBLE_DEVICES=all "镜像名称"
```

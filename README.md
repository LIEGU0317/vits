# How to Use
[【简体中文】](README_zh.md)

> If you're also struggling without a GPU, you might want to try the Featurize platform. Here's my [invitation link](https://featurize.cn?s=fd01af08da454204adf7aef8e07caa64).

## Python Version

### Python 3.10
```bash
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu116
```

### Python 3.7
```bash
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu110
```

## Clone the Repository

```sh
git clone https://github.com/CjangCjengh/vits.git
```

## Choose Cleaners

> The repository has been modified for training in Chinese, so you can skip this step if training in Chinese.

- Fill in `"text_cleaners"` in `config.json`
- Edit `text/symbols.py`
- Remove unnecessary imports from `text/cleaners.py`

## Install Dependencies

```sh
pip install -r requirements_py310.txt  # or requirements.txt
```

## Create Dataset

### Single Speaker

Set `"n_speakers"` to 0 in `config.json`.

Format:
```
path/to/XXX.wav|transcribed text
```

Example:
```
dataset/001.wav|こんにちは。
```

### Multiple Speakers

Speaker IDs should start from 0.

Format:
```
path/to/XXX.wav|speaker ID|transcribed text
```

Example:
```
dataset/001.wav|0|こんにちは。
```

## Preprocessing

If you have already completed this step, set `"cleaned_text"` to true in [config.json](config_parameters.md).

```sh
# Single speaker
python preprocess.py --text_index 1 --filelists path/to/filelist_train.txt path/to/filelist_val.txt --text_cleaners chinese_cleaners

# Multiple speakers
python preprocess.py --text_index 2 --filelists path/to/filelist_train.txt path/to/filelist_val.txt --text_cleaners chinese_cleaners
```

## Build Monotonic Alignment Search

```sh
cd monotonic_align
mkdir "monotonic_align"
python setup.py build_ext --inplace
cd ..
```

## Training

```sh
# Single speaker
python train.py -c <config> -m <folder>

# Multiple speakers
python train_ms.py -c <config> -m <folder>
```

## Inference

### Online

See [inference.ipynb](inference.ipynb)

### Offline

See [MoeGoe](https://github.com/CjangCjengh/MoeGoe)

# Running in Docker

```sh
docker run -itd --gpus all --name "container name" -e NVIDIA_DRIVER_CAPABILITIES=compute,utility -e NVIDIA_VISIBLE_DEVICES=all "image name"
```

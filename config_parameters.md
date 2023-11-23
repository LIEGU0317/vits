> 以`configs/chinese_base.json`为例

# 模型训练参数

## train
- `log_interval`: 训练日志打印间隔，默认为 200。
- `eval_interval`: 评估间隔，默认为 1000。
- `seed`: 随机种子，默认为 1234。
- `epochs`: 训练轮数，默认为 10000。
- `learning_rate`: 学习率，默认为 2e-4。
- `betas`: Adam优化器的beta参数，默认为 [0.8, 0.99]。
- `eps`: Adam优化器的epsilon参数，默认为 1e-9。
- `batch_size`: 批量大小，默认为 32。
- `fp16_run`: 是否使用混合精度训练，默认为 True。
- `lr_decay`: 学习率衰减，默认为 0.999875。
- `segment_size`: 分段大小，默认为 8192。
- `init_lr_ratio`: 初始学习率比率，默认为 1。
- `warmup_epochs`: 学习率热身轮数，默认为 0。
- `c_mel`: 梅尔频谱通道数，默认为 45。
- `c_kl`: KL散度权重，默认为 1.0。

## data
- `training_files`: 训练文件路径，默认为 "filelists/juzi_train_filelist.txt.cleaned"。
- `validation_files`: 验证文件路径，默认为 "filelists/juzi_val_filelist.txt.cleaned"。
- `text_cleaners`: 文本清理器列表，默认为 ["chinese_cleaners"]。
- `max_wav_value`: 最大音频数值，默认为 32768.0。
- `sampling_rate`: 采样率，默认为 22050。
- `filter_length`: 滤波器长度，默认为 1024。
- `hop_length`: 跳跃长度，默认为 256。
- `win_length`: 窗口长度，默认为 1024。
- `n_mel_channels`: 梅尔频道数，默认为 80。
- `mel_fmin`: 最小梅尔频率，默认为 0.0。
- `mel_fmax`: 最大梅尔频率，默认为 null。
- `add_blank`: 是否添加空白，默认为 True。
- `n_speakers`: 说话人数，默认为 8。
- `cleaned_text`: 是否使用已清理的文本，默认为 True。

## model
- `inter_channels`: 中间通道数，默认为 192。
- `hidden_channels`: 隐藏通道数，默认为 192。
- `filter_channels`: 滤波通道数，默认为 768。
- `n_heads`: 多头注意力机制的头数，默认为 2。
- `n_layers`: 网络层数，默认为 6。
- `kernel_size`: 卷积核大小，默认为 3。
- `p_dropout`: 丢失率，默认为 0.1。
- `resblock`: 是否使用残差块，默认为 "1"。
- `resblock_kernel_sizes`: 残差块的卷积核大小列表，默认为 [[3, 7, 11], [3, 7, 11], [3, 7, 11]]。
- `resblock_dilation_sizes`: 残差块的膨胀大小列表，默认为 [[1, 3, 5], [1, 3, 5], [1, 3, 5]]。
- `upsample_rates`: 上采样率列表，默认为 [8, 8, 2, 2]。
- `upsample_initial_channel`: 上采样初始通道数，默认为 512。
- `upsample_kernel_sizes`: 上采样卷积核大小列表，默认为 [16, 16, 4, 4]。
- `n_layers_q`: Q层的层数，默认为 3。
- `use_spectral_norm`: 是否使用谱归一化，默认为 False。
- `gin_channels`: GIN通道数，默认为 256。

## speakers
- 说话人列表，默认为 ["小八", "唐乐吟", "小洇", "花玲", "许老师", "邱琳", "七一", "八四"]。

## symbols
- 符号列表，默认为 ["_", "，", "。", "！", "？", "—", "…", "ㄅ", "ㄆ", ..., " "]

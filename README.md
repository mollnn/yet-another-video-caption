# yet-another-video-caption

## 数据集配置

所有数据位于 `./data` 中。

所有视频（包括 train/val/test） 位于 `./data/video` 中。

所有视频信息（包括 train/val/test）输入到 `./data/input.json`。

程序会在 `./data` 中产生一些中间信息，请勿修改。

## 依赖

```
pip install tqdm pillow pretrainedmodels nltk
```

此外，请确保已当前环境下已经正确配置 CUDA 运行库，CUDNN，Pytorch(GPU)，ffmpeg

## 食用步骤

1. 确保数据集已正确配置

2. 确保依赖已经正确安装

3. 抽取数据，将你希望使用的 train/val/test 划分参数输入 `makedata.py` 中，然后执行该脚本

4. 依次执行（请自行修改 `batch_size` 和 `saved_model` 参数！）
```
python prepro_feats.py --output_dir data/feats/resnet152 --model resnet152
python prepro_vocab.py
python train.py --epochs 3001 --batch_size 1 --checkpoint_path data/save --feats_dir data/feats/resnet152 --model S2VTAttModel --with_c3d 0 --dim_vid 2048
python eval.py --recover_opt data/save/opt_info.json --saved_model data/save/model_10.pth --batch_size 1
```

## 速度测试



## Todo

大小写问题

## References

https://github.com/xiadingZ/video-caption.pytorch

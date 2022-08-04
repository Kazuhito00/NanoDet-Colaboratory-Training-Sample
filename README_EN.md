[[Japanese](https://github.com/Kazuhito00/NanoDet-Colaboratory-Training-Sample)/English] 

> **Warning**<br>
> This repository does not support NanoDet-Plus.

# NanoDet-Colaboratory-Training-Sample
<img src="https://user-images.githubusercontent.com/37477845/133970089-092f3e41-7ef0-4bbd-a1e2-45d10d9e8efa.gif" width="60%"><br>

This is a sample to training [NanoDet](https://github.com/RangiLyu/nanodet) on Google Colaboratory and export a file in ONNX format.<br>
It includes the following contents.<br>
* Data set(Annotation not implemented)
* Data set(Annotated)
* Colaboratory script (environment setting, model training)

# Requirement
* Pytorch 1.7 or later
* pytorch-lightning 1.4.7 or later
* OpenCV 3.4.2 or later ※Only when performing inference samples
* onnxruntime 1.5.2 or later ※Only when performing inference samples

# About annotation
It is assumed that annotation data is annotated using VoTT and output in Pascal VOC format.<br>
However, it is further converted to MS COCO format in the notebook.<br><br>

The notebook sample assumes the following directory structure.<br>
However, since "pascal_label_map.pbtxt" and "ImageSets" are not used in this sample, <Br>
There is no problem even if you do not store it.
```
02.annotation_data
│  pascal_label_map.pbtxt
│  
├─Annotations
│      000001.xml
│       :
│      000050.xml
│      
├─ImageSets
│          
└─JPEGImages
        000001.jpg
         :
        000050.jpg
```

# Usage
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Kazuhito00/NanoDet-Colaboratory-Training-Sample/blob/main/NanoDet_Colaboratory_Training_Sample.ipynb)<br>
Training will be conducted on Google Colaboratory.<br>
Open your notebook from the [Open In Colab] link and run it in the following order:
1. PyTorch Lightningインストール(PyTorch Lightning install)
1. 乱数シード固定(Random seed fixed)
1. データセットダウンロード(Download Dataset)<Br>If you want to use your own dataset, set "use_sample_image = True" to False and specify the path of your own dataset in <br> "dataset_directory".
1. Pascal VOC形式 を MS COCO形式へ変換(Convert Pascal VOC format to MS COCO format)
1. モデル訓練(Training Model)<br>Please store "nanodet-m.yml" in the "nanodet" directory before executing "!python train.py nanodet-m.yml". <br>When using your own data set, change the following items in "nanodet-m.yml".
    1. Number of classes<br>num_classes(model->arch->head->num_classes)
    1. Training data image storage path<br>img_path(data->train->img_path)
    1. Training data annotation storage path<br>ann_path(data->train->ann_path)
    1. Validation data image storage path<br>img_path(data->val->img_path)
    1. Validation data annotation storage path<br>ann_path(data->val->ann_path)
    1. Batch size<br>batchsize_per_gpu(device->batchsize_per_gpu)
    1. Class name list<br>class_names
1. ONNX変換(Convert to ONNX)
1. ONNXファイル情報確認(Check ONNX file information)
1. 学習済ファイルダウンロード(Download Trained Model)

# Author
Kazuhito Takahashi(https://twitter.com/KzhtTkhs)
 
# License 
NanoDet-Colaboratory-Training-Sample is under [Apache-2.0 License](LICENSE).

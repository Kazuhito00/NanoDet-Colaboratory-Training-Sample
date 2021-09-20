[Japanese/[English](https://github.com/Kazuhito00/NanoDet-Colaboratory-Training-Sample/blob/main/README_EN.md)] 

# NanoDet-Colaboratory-Training-Sample
<img src="https://user-images.githubusercontent.com/37477845/133970089-092f3e41-7ef0-4bbd-a1e2-45d10d9e8efa.gif" width="60%"><br>

[NanoDet](https://github.com/RangiLyu/nanodet)をGoogle Colaboratory上で訓練しONNX形式のファイルをエクスポートするサンプルです。<br>
以下の内容を含みます。<br>
* データセット ※アノテーション未実施
* データセット ※アノテーション済み
* Colaboratory用スクリプト(環境設定、モデル訓練)

# Requirement
* Pytorch 1.7 or later
* pytorch-lightning 1.4.7 or later
* OpenCV 3.4.2 or later ※推論サンプルを実施する場合のみ
* onnxruntime 1.5.2 or later ※推論サンプルを実施する場合のみ

# About annotation
[VoTT](https://github.com/microsoft/VoTT)を使用してアノテーションを行い、<br>
Pascal VOC形式で出力したアノテーションデータを前提としています。<br>
ただし、ノートブック内で更にMS COCO形式変換しています。<br><br>

ノートブックのサンプルでは、以下のようなディレクトリ構成を想定しています。<br>
ただし、本サンプルでは「pascal_label_map.pbtxt」と「ImageSets」は利用しないため、<Br>
格納しなくても問題ありません。
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
トレーニングはGoogle Colaboratory上で実施します。<br>
[Open In Colab]リンクからノートブックを開き、以下の順に実行してください。
1. PyTorch Lightningインストール(PyTorch Lightning install)
1. 乱数シード固定(Random seed fixed)
1. データセットダウンロード(Download Dataset)<Br>自前のデータセットを使用したい方は「use_sample_image = True」をFalseに設定し、<br>「dataset_directory」に自前のデータセットのパスを指定してください
1. Pascal VOC形式 を MS COCO形式へ変換
1. モデル訓練(Training Model)<br>「!python train.py nanodet-m.yml」を実施する前に「nanodet」ディレクトリに「nanodet-m.yml」を格納してください。<br>自前のデータセットを使用する場合「nanodet-m.yml」の以下の項目を変更してください。
    1. クラス数<br>num_classes(model->arch->head->num_classes)
    1. 学習データ 画像格納パス<br>img_path(data->train->img_path)
    1. 学習データ アノテーション格納パス<br>ann_path(data->train->ann_path)
    1. 検証データ 画像格納パス<br>img_path(data->val->img_path)
    1. 検証データ アノテーション格納パス<br>ann_path(data->val->ann_path)
    1. バッチサイズ<br>batchsize_per_gpu(device->batchsize_per_gpu)
    1. クラス名リスト<br>class_names
1. ONNX変換(Convert to ONNX)
1. ONNXファイル情報確認(Check ONNX file information)
1. 学習済ファイルダウンロード

# Author
高橋かずひと(https://twitter.com/KzhtTkhs)
 
# License 
TFLite-ModelMaker-EfficientDet-Colab-Hands-On is under [MIT license](https://en.wikipedia.org/wiki/MIT_License).

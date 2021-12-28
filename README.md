# EfficientNetV2-with-TPU

EfficientNetV2 adalah jenis jaringan saraf convolutional yang memiliki kecepatan pelatihan lebih cepat dan efisiensi parameter yang lebih baik dari model sebelumnya . Untuk mengembangkan model ini, penulis menggunakan kombinasi pencarian dan penskalaan arsitektur saraf yang sadar pelatihan , untuk bersama-sama mengoptimalkan kecepatan pelatihan. Model dicari dari ruang pencarian yang diperkaya dengan operasi baru seperti Fused-MBConv .

Secara arsitektur perbedaan utama adalah:
- EfficientNetV2 secara ekstensif menggunakan MBConv dan fusi-MBConv yang baru ditambahkan di lapisan awal.
- EfficientNetV2 lebih memilih rasio ekspansi yang lebih kecil untuk MBConv karena rasio ekspansi yang lebih kecil cenderung memiliki lebih sedikit overhead akses memori.
- EfficientNetV2 lebih menyukai ukuran kernel 3x3 yang lebih kecil, tetapi menambahkan lebih banyak lapisan untuk mengkompensasi bidang reseptif yang berkurang yang dihasilkan dari ukuran kernel yang lebih kecil.
- EfficientNetV2 sepenuhnya menghapus tahap stride-1 terakhir di EfficientNet asli, mungkin karena ukuran parameternya yang besar dan overhead akses memori

## Note 


| Model               | Size  | acc-val| top-5 | acc-test |
  | ----------------- | ----- | -----  | ----- | -----    |
  | EfficientNetV2B0  | 224   | 90.68  | 99.76 | 89.86    | 
  | EfficientNetV2B1  | 240   | 90.76  | 99.78 | 90.07    |
  | EfficientNetV2B2  | 260   | 87.08  | 99.48 | 86.85    | 
  | EfficientNetV2B3  | 300   | 90.38  | 99.80 | 89.29    | 
  | EfficientNetV2T   | 320   | 92.80  | 99.86 | 92.53    | 
  | EfficientNetV2S   | 384   | 89.94  | 99.74 | 89.27    | 
  | EfficientNetV2M   | 480   | 91.86  | 99.70 | 90.53    | 
  | EfficientNetV2L   | 480   | 93.10  | 99.80 | 92.38    | 
  | EfficientNetV2XL  | 512   | 93.24  | 99.72 | 93.41    | 


| model        | input | val-acc | top-5-acc   | Reported|     
  | ---------- | ----- | ------- | ------- | ------- | 
  | EffV2B0    | 224   | 90.68   | 99.76 | 0.94386 |               
  | EffV2B1    | 240   | 90.76   | 99.78 | 0.94936 |  
  | EffV2B2    | 260   | 87.08   | 99.48| 0.95262 |
  | EffV2B3    | 300   | 90.38   | 0.80642 | 0.95262 |                             
  | EffV2T     | 320   | 92.80   | 0.82506 | 0.96228 |  
  | EffV2S     | 384   | 89.94   | 0.8386  | 0.967   |               
  | EffV2M     | 480   | 91.86   | 0.8509  | 0.973   |               
  | EffV2L     | 480   | 93.10   | 0.855   | 0.97324 |        
  | EffV2XL    | 512   | 93.24   | 0.86532 | 0.97866 | 

- Train 90%(45000rb)
- Validation 10%(5000rb) 
- Test(10000rb) 
- Epochs = 25
- WeightDecay = 1e-5
- Batchsize = 16 * 8(strategy.num_replicas_in_sync) 

- optimizers adabelief dengan LearningRateSchduler(Triangular2CyclicalLearningRate) dan Rectified = True(mencegah overshoot)

| V2 Model    | Params | Top1 | Input | ImageNet21K | Imagenet21k-ft1k | Imagenet |
  | ----------- | ------ | ---- | ----- | ----------- | ---------------- | -------- |
  | EffV2B0 | 7.1M  | 78.7 | 224 | [v2b0-21k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k.h5)|[v2b0-21k-ft1k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k-ft1k.h5)|[v2b0-imagenet.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-imagenet.h5)|
  | EffV2B0 | 7.1M  | 78.7 | 224 | [v2b0-21k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k.h5)|[v2b0-21k-ft1k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k-ft1k.h5)|[v2b0-imagenet.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-imagenet.h5)|
  | EffV2B0 | 7.1M  | 78.7 | 224 | [v2b0-21k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k.h5)|[v2b0-21k-ft1k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k-ft1k.h5)|[v2b0-imagenet.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-imagenet.h5)|
  | EffV2B0 | 7.1M  | 78.7 | 224 | [v2b0-21k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k.h5)|[v2b0-21k-ft1k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k-ft1k.h5)|[v2b0-imagenet.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-imagenet.h5)|
  | EffV2B0 | 7.1M  | 78.7 | 224 | [v2b0-21k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k.h5)|[v2b0-21k-ft1k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k-ft1k.h5)|[v2b0-imagenet.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-imagenet.h5)|
  | EffV2B0 | 7.1M  | 78.7 | 224 | [v2b0-21k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k.h5)|[v2b0-21k-ft1k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k-ft1k.h5)|[v2b0-imagenet.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-imagenet.h5)|
  | EffV2B0 | 7.1M  | 78.7 | 224 | [v2b0-21k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k.h5)|[v2b0-21k-ft1k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k-ft1k.h5)|[v2b0-imagenet.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-imagenet.h5)|
  | EffV2B0 | 7.1M  | 78.7 | 224 | [v2b0-21k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k.h5)|[v2b0-21k-ft1k.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-21k-ft1k.h5)|[v2b0-imagenet.h5](https://github.com/leondgarse/keras_efficientnet_v2/releases/download/effnetv2_pretrained/efficientnetv2-b0-imagenet.h5)|


## Referensi

- [Official efficientnetv2](https://github.com/google/automl/tree/master/efficientnetv2)
- [EfficientNetV2: Smaller Models and Faster Training](https://arxiv.org/pdf/2104.00298) 
- [EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks](https://arxiv.org/pdf/1905.11946) 
- [EfficientNet: Improving Accuracy and Efficiency through AutoML and Model Scaling](https://ai.googleblog.com/2019/05/efficientnet-improving-accuracy-and.html?m=1) 

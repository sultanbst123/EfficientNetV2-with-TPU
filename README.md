# EfficientNetV2-with-TPU

<p align="center">
 <img src="https://github.com/sultanbst123/EfficientNetV2-with-TPU/blob/main/images.png"><i> EfficientNet </i>
</p>

EfficientNetV2 adalah jenis jaringan saraf convolutional yang memiliki kecepatan pelatihan lebih cepat dan efisiensi parameter yang lebih baik dari model sebelumnya . Untuk mengembangkan model ini, penulis menggunakan kombinasi pencarian dan penskalaan arsitektur saraf yang sadar pelatihan , untuk bersama-sama mengoptimalkan kecepatan pelatihan. Model dicari dari ruang pencarian yang diperkaya dengan operasi baru seperti Fused-MBConv .

Secara arsitektur perbedaan utama adalah:
- EfficientNetV2 secara ekstensif menggunakan MBConv dan fusi-MBConv yang baru ditambahkan di lapisan awal.
- EfficientNetV2 lebih memilih rasio ekspansi yang lebih kecil untuk MBConv karena rasio ekspansi yang lebih kecil cenderung memiliki lebih sedikit overhead akses memori.
- EfficientNetV2 lebih menyukai ukuran kernel 3x3 yang lebih kecil, tetapi menambahkan lebih banyak lapisan untuk mengkompensasi bidang reseptif yang berkurang yang dihasilkan dari ukuran kernel yang lebih kecil.
- ** 'EfficientNetV2'  sepenuhnya menghapus tahap stride-1 terakhir di  'EfficientNet'  asli, mungkin karena ukuran parameternya yang besar dan overhead akses memori **

## Note 


| Model               | Size  | acc-val| top-5 | acc-test | weight |
  | ----------------- | ----- | -----  | ----- | -----    | -----   |
  | EfficientNetV2B0  | 224   | 90.68  | 99.76 | 89.86    | imagenet |
  | EfficientNetV2B1  | 240   | 90.76  | 99.78 | 90.07    | imagenet |
  | EfficientNetV2B2  | 260   | 87.08  | 99.48 | 86.85    | imagenet |
  | EfficientNetV2B3  | 300   | 90.38  | 99.80 | 89.29    | imagenet |
  | EfficientNetV2T   | 320   | 92.80  | 99.86 | 92.53    | imagenet |
  | EfficientNetV2S   | 384   | 89.94  | 99.74 | 89.27    | imagenet |
  | EfficientNetV2M   | 480   | 91.86  | 99.70 | 90.53    | imagenet |
  | EfficientNetV2L   | 480   | 93.10  | 99.80 | 92.38    | imagenet |
  | EfficientNetV2XL  | 512   | 93.24  | 99.72 | 93.41    | imagenet21K-ft1k |

- Train 90%(45000rb)
- Validation 10%(5000rb) 
- Test(10000rb) 
- Epochs = 25
- WeightDecay = 1e-5
- Batchsize = 16 * 8(strategy.num_replicas_in_sync) 

- optimizers adabelief dengan LearningRateSchduler(Triangular2CyclicalLearningRate) dan Rectified = True(mencegah overshoot)


## Referensi

- [Official efficientnetv2](https://github.com/google/automl/tree/master/efficientnetv2)
- [EfficientNetV2: Smaller Models and Faster Training](https://arxiv.org/pdf/2104.00298) 
- [EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks](https://arxiv.org/pdf/1905.11946) 
- [EfficientNet: Improving Accuracy and Efficiency through AutoML and Model Scaling](https://ai.googleblog.com/2019/05/efficientnet-improving-accuracy-and.html?m=1) 

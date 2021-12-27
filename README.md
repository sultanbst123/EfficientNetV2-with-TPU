# EfficientNetV2-with-TPU

EfficientNetV2 adalah jenis jaringan saraf convolutional yang memiliki kecepatan pelatihan lebih cepat dan efisiensi parameter yang lebih baik dari model sebelumnya . Untuk mengembangkan model ini, penulis menggunakan kombinasi pencarian dan penskalaan arsitektur saraf yang sadar pelatihan , untuk bersama-sama mengoptimalkan kecepatan pelatihan. Model dicari dari ruang pencarian yang diperkaya dengan operasi baru seperti Fused-MBConv .

Secara arsitektur perbedaan utama adalah:
- EfficientNetV2 secara ekstensif menggunakan MBConv dan fusi-MBConv yang baru ditambahkan di lapisan awal.
- EfficientNetV2 lebih memilih rasio ekspansi yang lebih kecil untuk MBConv karena rasio ekspansi yang lebih kecil cenderung memiliki lebih sedikit overhead akses memori.
- EfficientNetV2 lebih menyukai ukuran kernel 3x3 yang lebih kecil, tetapi menambahkan lebih banyak lapisan untuk mengkompensasi bidang reseptif yang berkurang yang dihasilkan dari ukuran kernel yang lebih kecil.
- EfficientNetV2 sepenuhnya menghapus tahap stride-1 terakhir di EfficientNet asli, mungkin karena ukuran parameternya yang besar dan overhead akses memori

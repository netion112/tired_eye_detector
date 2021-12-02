**Ini merupakan hasil fork dari blog di bawah ini**
Saya mencoba untuk memperjelas agar lebih mudah dipahami dari tulisan asli Author pada artikel tersebut.

# [How to train an object detection model easy for free](https://www.dlology.com/blog/how-to-train-an-object-detection-model-easy-for-free/) | DLology Blog

Versi bahasa Indonesia dan modifikasi dapat Anda temui pada blog:
[Auftechnique](https://auftechnnique.com/11-langkah-training-objek-detection-tanpa-highend-komputer-secara-gratis) 

## Cara menjalankannya

Anda dapat download file Notebook untuk Colab pada link ini [File Colab](https://auftechnnique.com/11-langkah-training-objek-detection-tanpa-highend-komputer-secara-gratis) 


Alternatifnya, jika ingin menggunakan gambar yang akan di training dibandingkan dengan apa yang ada pada contoh
Anda dapat fork link github di bawah ini:

Dibutuhkan [Python 3.5+](https://www.python.org/ftp/python/3.6.4/python-3.6.4.exe).
### Fork, lalu clone repository pada komputer Anda.
```
https://github.com/zacky131/object_detection_demo
```
### Install library yang dibutuhkan
`pip3 install -r requirements.txt`


### Langkah 1: Buat anotasi pada gambar yang akan di training
- Simpan beberapa foto, idealnya memiliki ekstensi `jpg` pada folder `./data/raw. (Jika objek yang akan Anda training cukup sederhana, maka 20 gambar sudah cukup)
- Ubah ukuran seluruh foto menjadi (800, 600) dengan cara:
```
python resize_images.py --raw-dir ./data/raw --save-dir ./data/images --ext jpg --target-size "(800, 600)"
```
Gambar yang telah di ubah ukurannya akan masuk ke dalam folder`./data/images/`
- Bagi file tersebut pada folder Train/test (Anda dapat memasukkan 80% jumlah gambar pada training dan 20% pada test), `./data/images/train` and `./data/images/test`

- Anotasikan gambar tersebut dengan menggunakan tools [labelImg](https://tzutalin.github.io/labelImg/), simpan file output berupa `xml` di dalam masing-masing folder `./data/images/train` dan `./data/images/test`. 

*Tips: Anda dapat menggunakan shorcut (`w`: draw box, `d`: next file, `a`: previous file, etc.) untuk mempercepat proses anotasi.*

- Commit dan push gambar yang telah di anotasikan bersama dengan file xml nya  (`./data/images/train` and `./data/images/test`) pada repository Anda hasil fork.


### Langkah 2: Buka file Colab Notebook yang telah Anda download dari [Auftechnique](https://auftechnnique.com/11-langkah-training-objek-detection-tanpa-highend-komputer-secara-gratis)
- Ubah alamat url yang ada di dalam repository milik Anda, lalu jalankan.


## Bagaimana cara menjalankan inference pada grafik Tensorflow frozen

Requirements:
- `frozen_inference_graph.pb` Model Object Frozen TensorFlow yang di download dari hasil training menggunakan Colab. 
- `label_map.pbtxt` Ini digunakan untuk memetakan nama yang betul untuk index class yang diprediksikan setelah selesai training menggunakan Colab.

Jalankan jupyter notebook ini pada komputer Anda.
```
local_inference_test.ipynb
```
## Run the benchmark


TensorFlow benchmark pada cpu
```
python local_inference_test.py\
     --model ./models/frozen_inference_graph.pb\
     --img ./test/15.jpg\
     --cpu
```

### paddlepaddle yordamida face recognition dasturini ishlab chiqish

#### **Kerakli kutubxonalar:**
Qurilmangizga mos ```paddlepaddle``` versiyasini [paddlepaddle.org.cn](https://www.paddlepaddle.org.cn/en/install/quick?docurl=/documentation/docs/en/install/pip/linux-pip_en.html) saytidan topishingiz mumkin.
```python
 pip install paddlepaddle-gpu
 ...
```

```paddlepaddle``` ishlashi uchun [nccl](https://developer.nvidia.com/nccl/nccl-download) o'rnatilishi kerak ([qo'llanma](https://docs.nvidia.com/deeplearning/nccl/install-guide/index.html)):

```shell
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.0-1_all.deb
$ sudo dpkg -i cuda-keyring_1.0-1_all.deb
$ sudo apt-get update
$ sudo apt install libnccl2 libnccl-dev
```

```paddle``` muvaffaqiyatli ishlayotganini tekshiring:

```python
import paddle
paddle.utils.run_check()
```

#### **Qo'llanma:**
* Kutubxonalarni o'rnatish bo'yicha: [github](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.1/docs/tutorials/INSTALL.md)
* Train bo'yicha: [github](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.1/docs/tutorials/INSTALL.md)
* Qo'llash bo'yicha: [github](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.1/docs/tutorials/INSTALL.md)

#### **Dataset:**
* Tayyor datasetlar - [Baidu](https://github.com/deepinsight/insightface/tree/master/recognition/_datasets_) va [GoogleDrive](https://github.com/deepinsight/insightface/tree/master/recognition/_datasets_)ga joylashtirilgan.
  Datasetni trainga tayyorlash uchun [link](https://github.com/deepinsight/insightface/tree/master/recognition/arcface_paddle#3-data-preparation) (Data Preparation bo'limiga qarang).

* Shaxsiy datasetlar
   1. dataset nomli folder yarating.
     ```console
     dataset
     |_ images
     |  |_ person1
     |  |_ person2
     |  |_ ...
     |  |_ personN
     |_ labels.txt
     ```
   2. person1, person2, ..., personN nomli folderlarda shu personga tegishli rasmlar joylashtiriladi.
   3. labels.txt faylida har bir rasm uchun yo'l (path) ko'rsatiladi.
     ```python
     # delimiter: "\t" (tabulyatsiya)
     # labels.txt fayl quyidagicha ko'rinishda bo'lishi kerak:
     person1/image1.jpg
     person1/image2.jpg
     ...
     person2/image1.jpg
     person2/image2.jpg
     ...
     personN/image1.jpg
     personN/image2.jpg
     ...
     ```
  
  

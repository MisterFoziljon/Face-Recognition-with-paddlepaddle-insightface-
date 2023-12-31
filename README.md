## paddlepaddle yordamida face recognition dasturini ishlab chiqish

### **Kerakli kutubxonalar:**
Qurilmangizga mos ```paddlepaddle``` versiyasini [paddlepaddle.org.cn](https://www.paddlepaddle.org.cn/en/install/quick?docurl=/documentation/docs/en/install/pip/linux-pip_en.html) saytidan topishingiz mumkin.
```python
 pip install paddlepaddle-gpu
 pip install streamlit
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

### **Dataset:**
* Tayyor dataset - [Baidu](https://github.com/deepinsight/insightface/tree/master/recognition/_datasets_) va [GoogleDrive](https://github.com/deepinsight/insightface/tree/master/recognition/_datasets_)ga joylashtirilgan.
  - Tayyor datasetlar yordamida face recognition modelini train qilishingiz mumkin.
  - 
  Datasetni trainga tayyorlash uchun [link](https://github.com/deepinsight/insightface/tree/master/recognition/arcface_paddle#3-data-preparation) (Data Preparation bo'limiga qarang).

* Shaxsiy dataset (Ushbu dataset sizga kerakli bo'lgan personlarni recognition qilib berish uchun yig'iladi.)
   - dataset nomli folder yarating.
  
     ```console
     dataset
     |_ images
     |  |_ person1
     |  |_ person2
     |  |_ ...
     |  |_ personN
     |_ labels.txt
     ```
     
   - person1, person2, ..., personN nomli folderlarda shu personga tegishli rasmlar joylashtiriladi.
  
     ```console
     images
     |_ person1
     |  |_image1.jpg
     |  |_image2.jpg
     |  |_...
     |_ person2
     |  |_image1.jpg
     |  |_image2.jpg
     |  |_...
     |_ ...
     ```
     
   - labels.txt faylida har bir rasm uchun yo'l (path) ko'rsatiladi.
  
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
  
    - Build index yordamida datasetni index.bin faylga o'tkazamiz:
    1. cmd yordamida:
    ```cmd
      python insightface/insightface_paddle --build_index dataset/index.bin --img_dir dataset/images --label dataset/label.txt
    ```

    2. Kod yordamida:
    ```python
      import insightface_paddle as face
    
      parser = face.parser()
    
      args = parser.parse_args()
      args.build_index = "dataset/index.bin"
      args.img_dir = "dataset/images"
      args.label = "dataset/label.txt"
    
      predictor = face.InsightFace(args)
      predictor.build_index()
    ```
    
    - Hosil qilingan ```index.bin``` model predict qilgan natija bilan solishtiriladi. Bunda natijani ```index.bin``` fayl tarkibidagi har bir rasm bilan solishtirib yakuniy xulosa olinadi.
    -  

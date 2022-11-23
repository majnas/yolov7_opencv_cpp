
# yolov7_opencv_cpp
Object Detection using YOLOv7 and OpenCV DNN C++


```bash
git clone --recursive https://github.com/majnas/yolov7_opencv_cpp.git
cd yolov7_opencv_cpp/yolov7

# Install dependencies.
pip install -r requirements.txt
# pip install onnx
```


#### Prepare custom weight
Download my custom yolov7 face detection using this cmd 
```shell
cd yolov7_opencv_cpp/yolov7/cfg/training/
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1INiC_M_ttd8xMpZ9CuSA1FTqUxZT4e1y' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1INiC_M_ttd8xMpZ9CuSA1FTqUxZT4e1y" -O custom_weight.pt && rm -rf /tmp/cookies.txt
```

Or place use your own custom yolov7 weight in following folder.

```shell
└── yolov7
    ├── cfg
    │   ├── baseline
    │   ├── deploy
    │   └── training
    │       ├── custom_weight.pt           <----- Place the custom weight here
    │       ├── yolov7-d6.yaml
    │       ├── yolov7-e6e.yaml
    │       ├── yolov7-e6.yaml
    │       ├── yolov7-tiny.yaml
    │       ├── yolov7-w6.yaml
    │       ├── yolov7x.yaml
    │       └── yolov7.yaml

```


* Moving reparameterization_yolov7.py to yolov7 directory.
* Make a copy of yolov7/cfg/deploy/yolov7.yml and rename to yolov7_custom_weight.yaml then change number of class in line number 2 (nc=1). For my custom weight there is only one class (face).

```shell
mv reparameterization_yolov7.py ./yolov7/reparameterization_yolov7.py
```

### Reparameterization of model
```shell
cd ./yolov7
python reparameterization_yolov7.py
``` 

This will create another model (custom_weight_reparameterized.pt) in cfg/deploy/custom_weight_reparameterized.pt, which is reparameterized version of custom weight.

```shell
└── yolov7
    ├── cfg
    │   ├── baseline
    │   ├── deploy
    │   │   ├── custom_weight_reparameterized.pt   <------------- Reparameterized custom weight 
    │   │   ├── yolov7_custom_weight.yaml    
    │   │   ├── yolov7-d6.yaml
    │   │   ├── yolov7-e6e.yaml
    │   │   ├── yolov7-e6.yaml
    │   │   ├── yolov7-tiny-silu.yaml
    │   │   ├── yolov7-tiny.yaml
    │   │   ├── yolov7-w6.yaml
    │   │   ├── yolov7x.yaml
    │   │   └── yolov7.yaml
    │   └── training
    │       ├── custom_weight.pt                  <------------- Custom weight
    │       ├── yolov7-d6.yaml
    │       ├── yolov7-e6e.yaml
    │       ├── yolov7-e6.yaml
    │       ├── yolov7-tiny.yaml
    │       ├── yolov7-w6.yaml
    │       ├── yolov7x.yaml
    │       └── yolov7.yaml

```

# Export to ONNX
To export ONNX we have to checkout to u5 branch, and export reparameterized version of custom weight to onnx and torchscript, to do this
```shell
cd ./yolov7
  git checkout u5
python export.py --weights cfg/deploy/custom_weight_reparameterized.pt --topk-all 100 --iou-thres 0.65 --conf-thres 0.35 --img-size 640 640
```
No we will have onnx and tochscript version of out base best.pt
```shell
└── yolov7
    ├── cfg
    │   ├── deploy
    │   │   ├── custom_weight_reparameterized.onnx           <------------- onnx version
    │   │   ├── custom_weight_reparameterized.pt             <------------- Reparameterized custom weight
    │   │   └── custom_weight_reparameterized.torchscript    <------------- torchscript version version
    │   └── training
    │       └── custom_weight.pt             <------------- Custom weight

```

# To compile and run cpp version
```bash
    cd cpp
    mkdir build
    cd build
    cmake ..
    make     
    ./app
```

<!-- <div align="center">
  <img src="./data/me_cpp_pred.png" height="500">
</div>
<p align="center">
  Figure 2: cpp prediction for me.png
</p> -->

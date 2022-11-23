
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
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1INiC_M_ttd8xMpZ9CuSA1FTqUxZT4e1y' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1INiC_M_ttd8xMpZ9CuSA1FTqUxZT4e1y" -O best.pt && rm -rf /tmp/cookies.txt
```

Or place use your own custom yolov7 weight in following folder.

```shell
└── yolov7
    ├── cfg
    │   ├── baseline
    │   ├── deploy
    │   └── training
    │       ├── best.pt           <----- Place the custom weight here
    │       ├── yolov7-d6.yaml
    │       ├── yolov7-e6e.yaml
    │       ├── yolov7-e6.yaml
    │       ├── yolov7-tiny.yaml
    │       ├── yolov7-w6.yaml
    │       ├── yolov7x.yaml
    │       └── yolov7.yaml

```


# Export to ONNX.
cd ..
python export.py --weights models/YOLOv5s.pt --include onnx
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

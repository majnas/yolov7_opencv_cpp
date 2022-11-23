
# yolov5_opencv_cpp_python
Object Detection using YOLOv5 and OpenCV DNN (C++ and Python)
[Original Source](https://learnopencv.com/object-detection-using-yolov5-and-opencv-dnn-in-c-and-python/)

# Demo video
https://user-images.githubusercontent.com/31705845/166663140-cf238d84-94ad-49eb-9a24-290528fff70d.mp4



```bash
git clone --recursive https://github.com/majnas/yolov5_opencv_cpp_python.git
cd yolov5_opencv_cpp_python/yolov5

# Install dependencies.
pip install -r requirements.txt
pip install onnx

# Download .pt model.
cd models
wget https://github.com/ultralytics/YOLOv5/releases/download/v6.1/YOLOv5s.pt

# Export to ONNX.
cd ..
python export.py --weights models/YOLOv5s.pt --include onnx
```


# To use python
```python
    cd py
    python main.py
```
<div align="center">
  <img src="./data/me_py_pred.png" height="500">
</div>
<p align="center">
  Figure 1: python prediction for me.png
</p>


# To compile and run cpp version
```bash
    cd cpp
    mkdir build
    cd build
    cmake ..
    make     
    ./app
```

<div align="center">
  <img src="./data/me_cpp_pred.png" height="500">
</div>
<p align="center">
  Figure 2: cpp prediction for me.png
</p>

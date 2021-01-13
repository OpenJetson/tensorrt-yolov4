# OpenJetson

http://openjetson.com/

# yolov4

The Pytorch implementation is from [ultralytics/yolov3](https://github.com/ultralytics/yolov3). It can load yolov4.cfg and yolov4.weights(from AlexeyAB/darknet).

Following tricks are used in this yolov4:

- Three yololayer are implemented in one plugin to improve speed, codes derived from [lewes6369/TensorRT-Yolov3](https://github.com/lewes6369/TensorRT-Yolov3)
- Mish activation, implemented in a plugin.
- Batchnorm layer, implemented by scale layer.

## Excute:

```
1. generate yolov4.wts from pytorch implementation with yolov4.cfg and yolov4.weights

git clone https://github.com/OpenJetson/tensorrt-yolov4.git
git clone https://github.com/ultralytics/yolov3.git
// download yolov4.weights from https://github.com/AlexeyAB/darknet#pre-trained-models
cd yolov3
cp ../tensorrt-yolov4/gen_wts.py .
python gen_wts.py yolov4.weights
// a file 'yolov4.wts' will be generated.
// the master branch of yolov3 should work, if not, you can checkout be87b41aa2fe59be8e62f4b488052b24ad0bd450

2. put yolov4.wts into ./yolov4, build and run

mv yolov4.wts ../tensorrt-yolov4
cd ../tensorrt-yolov4
mkdir build
cd build
cmake ..
make
sudo ./yolov4 -s             // serialize model to plan file i.e. 'yolov4.engine'
sudo ./yolov4 -v             // deserialize plan file and run inference with camera or video.

```

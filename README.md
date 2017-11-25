# caffe-modify-regression
## 记录一下修改caffe，使其可以支持多标签回归【针对坐标点】。

# 1. 首先将tools/convert_imagenet.cpp复制一份，并重命名为：[convert_imageset_regression.cpp](https://github.com/yesyu/caffe-modify-regression/blob/master/convert_imageset_regression.cpp)
 具体修改详见代码。

# 2. 修改[data_layer.cpp](https://github.com/yesyu/caffe-modify-regression/blob/master/data_layer.cpp)文件.
# 3. 修改caffe.proto,找到message DataParameter部分的定义，在最后加上:
  ```python
  optional uint32 label_num = 11;
  ```
# Usage:
The format of train.txt:
```
1.jpg 0.2 0.3 0.04 0.05
...
```
# train_val.prototxt
  ```
  data_param {
    source: "examples/mnist/mnist_train_lmdb"
    batch_size: 64
    backend: LMDB
    label_num: 4
  }
  ```

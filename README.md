# caffe-modify-regression
## 记录一下修改caffe，使其可以支持多标签回归【针对坐标点】。

# 1. 首先将tools/convert_imagenet.cpp复制一份，并重命名为：[convert_imageset_regression.cpp](https://github.com/yesyu/caffe-modify-regression/blob/master/convert_imageset_regression.cpp)
 具体修改详见代码。
# 2. 修改[io.hpp](https://github.com/yesyu/caffe-modify-regression/blob/master/io.hpp)文件，利用函数重载[ReadImageToDatum](https://github.com/yesyu/caffe-modify-regression/blob/97a8fb9aeac30455d181ad9c022a51b23ef19fbb/io.hpp#L103)函数，并修改相应的[io.cpp](https://github.com/yesyu/caffe-modify-regression/blob/master/io.cpp)文件中对应的[函数](https://github.com/yesyu/caffe-modify-regression/blob/97a8fb9aeac30455d181ad9c022a51b23ef19fbb/io.cpp#L145)

# 3. 修改[data_layer.cpp](https://github.com/yesyu/caffe-modify-regression/blob/master/data_layer.cpp)文件.
# 4. 修改caffe.proto,找到message DataParameter部分的定义，在最后加上:
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

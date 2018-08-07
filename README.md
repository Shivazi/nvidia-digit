# nvidia-digit

https://github.com/dusty-nv/jetson-inference#locating-object-coordinates-using-detectnet

https://github.com/NVIDIA/DIGITS

https://github.com/NVIDIA/DIGITS/blob/digits-6.0/docs/BuildProtobuf.md

https://github.com/NVIDIA/DIGITS/blob/digits-6.0/docs/BuildCaffe.md

https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildDigits.md
```
all export file must be set enver and install using sudo for permission

sudo vim ~/.bashrc
Then execute the command below to make the change take effect:
source ~/.bashrc
```
# Test Digit
https://www.youtube.com/watch?v=rNB-cp5fSTw

http://ros-developer.com/2018/05/12/installing-nvidia-digist-ubuntu-16-04/

# Building Caffe
https://www.youtube.com/watch?v=APobbN4CCMw


# Custom Model Execution
model extract to /jetson-inference/data/networks/GoogleNet-ILSVRC12-subset
```
$ NET=networks/GoogleNet-ILSVRC12-subset
$ ./imagenet-console cat.jpeg cat_output_1.jpg \
--prototxt=$NET/deploy.prototxt \
--model=$NET/snapshot_iter_180.caffemodel \
--labels=$NET/labels.txt \
--input_blob=data \
--output_blob=softmax
```

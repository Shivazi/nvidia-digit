# nvidia-digit
https://github.com/NVIDIA/DIGITS

https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildDigits.md

# Building Caffe
https://www.youtube.com/watch?v=APobbN4CCMw
Install some dependencies with Deb packages:
```
sudo apt-get install libatlas-base-dev libatlas-dev
sudo apt-get install protobuf-compiler libprotobuf-dev libprotoc-dev

export PROTOBUF_ROOT=~/.softwares/protobuf
git clone https://github.com/google/protobuf.git $PROTOBUF_ROOT -b '3.2.x'
cd $PROTOBUF_ROOT
./autogen.sh
./configure
make "-j$(nproc)"
make"-j$(nproc)"  install DESTDIR=~
cd python
python setup.py install --cpp_implementation --user

git clone https://github.com/BVLC/caffe
cd caffe && mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON -DCMAKE_INSTALL_PREFIX:PATH=~/usr .. && make -j8 all install

```
# DIGIT
```
sudo apt-get install --no-install-recommends git graphviz python-dev python-flask python-flaskext.wtf python-gevent python-h5py python-numpy python-pil python-pip python-scipy python-tk
```
# Install repo packages
```
CUDA_REPO_PKG=http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
ML_REPO_PKG=http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb

wget "$CUDA_REPO_PKG" -O /tmp/cuda-repo.deb && sudo dpkg -i /tmp/cuda-repo.deb && rm -f /tmp/cuda-repo.deb 
wget "$ML_REPO_PKG" -O /tmp/ml-repo.deb && sudo dpkg -i /tmp/ml-repo.deb && rm -f /tmp/ml-repo.deb
```
# Building DIGITS
```
DIGITS_ROOT=~/.softwares/digits
git clone https://github.com/NVIDIA/DIGITS.git $DIGITS_ROOT
pip install -r $DIGITS_ROOT/requirements.txt --user
cd $DIGITS_ROOT
#The following line is because we have install caffe at <em><strong>~/usr/python </strong></em>and digits need to access caffe
export PYTHONPATH=~/usr/python:$PYTHONPATH 
./digits-devserver
```

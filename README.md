# nvidia-digit
https://github.com/NVIDIA/DIGITS

https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildDigits.md
```

# For Ubuntu 16.04
CUDA_REPO_PKG=http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
ML_REPO_PKG=http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb

# Install repo packages
wget "$CUDA_REPO_PKG" -O /tmp/cuda-repo.deb && sudo dpkg -i /tmp/cuda-repo.deb && rm -f /tmp/cuda-repo.deb
wget "$ML_REPO_PKG" -O /tmp/ml-repo.deb && sudo dpkg -i /tmp/ml-repo.deb && rm -f /tmp/ml-repo.deb

# Download new list of packages
sudo apt-get update

# Install some dependencies with Deb packages:

sudo apt-get install --no-install-recommends git graphviz python-dev python-flask python-flaskext.wtf python-gevent python-h5py python-numpy python-pil python-pip python-scipy python-tk
```
# Building Caffe
https://www.youtube.com/watch?v=APobbN4CCMw
Install some dependencies with Deb packages:
```
sudo apt-get install --no-install-recommends build-essential cmake git gfortran libatlas-base-dev libboost-filesystem-dev libboost-python-dev libboost-system-dev libboost-thread-dev libgflags-dev libgoogle-glog-dev libhdf5-serial-dev libleveldb-dev liblmdb-dev libopencv-dev libsnappy-dev python-all-dev python-dev python-h5py python-matplotlib python-numpy python-opencv python-pil python-pip python-pydot python-scipy python-skimage python-sklearn
```
DIGITS is currently compatiable with Caffe 0.15
```
# example location - can be customized
export CAFFE_ROOT=~/caffe
git clone https://github.com/NVIDIA/caffe.git $CAFFE_ROOT -b 'caffe-0.15'
```
Setting the CAFFE_ROOT environment variable will help DIGITS automatically detect your Caffe installation, but this is optional.
# Python packages
Several PyPI packages need to be installed:
```
sudo pip install -r $CAFFE_ROOT/python/requirements.txt
```
If you hit some errors about missing imports, then use this command to install the packages in order
```
cat $CAFFE_ROOT/python/requirements.txt | xargs -n1 sudo pip install
```
# Build
We recommend using CMake to configure Caffe rather than the raw Makefile build for automatic dependency detection:
```
cd $CAFFE_ROOT
mkdir build
cd build
cmake ..
make -j"$(nproc)"
make install
```

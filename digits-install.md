
# For Ubuntu 16.04
```
CUDA_REPO_PKG=http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
ML_REPO_PKG=http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb
```
# Install repo packages
```
wget "$CUDA_REPO_PKG" -O /tmp/cuda-repo.deb && sudo dpkg -i /tmp/cuda-repo.deb && rm -f /tmp/cuda-repo.deb
wget "$ML_REPO_PKG" -O /tmp/ml-repo.deb && sudo dpkg -i /tmp/ml-repo.deb && rm -f /tmp/ml-repo.deb
```
# Download new list of packages
```
sudo apt-get update
```
# Install some dependencies with Deb packages:
```
sudo apt-get install --no-install-recommends git graphviz python3-dev python3-flask python3-flaskext.wtf python3-gevent python3-h5py python3-numpy python3-pil python3-pip python3-scipy python3-tk
```
# Building Caffe

# Building Protobuf
```
 # These Deb packages must be installed to build Protobuf 3: 
  sudo apt-get install autoconf automake libtool curl make g++ git python3-dev python3-setuptools unzip
```  
Download Source

DIGITS is currently compatiable with Protobuf 3.2.x

```
# example location - can be customized
export PROTOBUF_ROOT=~/protobuf
git clone https://github.com/google/protobuf.git $PROTOBUF_ROOT -b '3.2.x'
```
Building Protobuf
```
cd $PROTOBUF_ROOT
./autogen.sh
./configure
make "-j$(nproc)"
sudo make install
sudo ldconfig
cd python
sudo python3 setup.py install --cpp_implementation
```
This will ensure that Protobuf 3 is installed.


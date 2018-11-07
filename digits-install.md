
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
# Building Caffe
Install some dependencies with Deb packages:
```
sudo apt-get install --no-install-recommends build-essential cmake git gfortran libatlas-base-dev libboost-filesystem-dev libboost-python-dev libboost-system-dev libboost-thread-dev libgflags-dev libgoogle-glog-dev libhdf5-serial-dev libleveldb-dev liblmdb-dev libopencv-dev libsnappy-dev python3-all-dev python3-dev python3-h5py python3-matplotlib python3-numpy  python3-pil python3-pip python3-pydot python3-scipy python3-skimage python3-sklearn
sudo apt-get install libboost-all-dev
sudo apt-get install libboost-all-dev
```

Download source

DIGITS is currently compatiable with Caffe 0.15

# example location - can be customized
```
export CAFFE_ROOT=~/caffe
git clone https://github.com/NVIDIA/caffe.git $CAFFE_ROOT -b 'caffe-0.15'
```
Setting the CAFFE_ROOT environment variable will help DIGITS automatically detect your Caffe installation, but this is optional.
Python packages

Several PyPI packages need to be installed:
```
sudo pip3 install -r $CAFFE_ROOT/python/requirements.txt
```
If you hit some errors about missing imports, then use this command to install the packages in order (see discussion here):
```
cat $CAFFE_ROOT/python/requirements.txt | xargs -n1 sudo pip install
```
Build

We recommend using CMake to configure Caffe rather than the raw Makefile build for automatic dependency detection:
```
cd $CAFFE_ROOT
mkdir build
cd build
cmake ..
sudo make -j"$(nproc)"
sudo make install
```

Download source

# example location - can be customized
```
DIGITS_ROOT=~/digits
git clone https://github.com/NVIDIA/DIGITS.git $DIGITS_ROOT
```
Throughout the docs, we'll refer to your install location as DIGITS_ROOT (~/digits in this case), though you don't need to actually set that environment variable.
Python packages

Several PyPI packages need to be installed:
```
sudo pip3 install -r $DIGITS_ROOT/requirements.txt
```
[Optional] Enable support for plug-ins

DIGITS needs to be installed to enable loading data and visualization plug-ins:
```
sudo pip3 install -e $DIGITS_ROOT
```
Starting the server
```
./digits-devserver
```
Starts a server at http://localhost:5000/.
```
$ ./digits-devserver --help
```
usage: __main__.py [-h] [-p PORT] [-d] [--version]

DIGITS development server

optional arguments:
  -h, --help            show this help message and exit
  -p PORT, --port PORT  Port to run app on (default 5000)
  -d, --debug           Run the application in debug mode (reloads when the
                        source changes and gives more detailed error messages)
  --version             Print the version number and exit

Getting started

Now that you're up and running, check out the Getting Started Guide.
Development

If you are interested in developing for DIGITS or work with its source code, check out the Development Setup Guide
Troubleshooting

Most configuration options should have appropriate defaults. Read this doc for information about how to set a custom configuration for your server.

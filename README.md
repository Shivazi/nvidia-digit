# nvidia-digit
https://github.com/dusty-nv/jetson-inference#installing-docker
# Installing the NVIDIA driver
Add the NVIDIA Developer repository and install the NVIDIA driver.
```
$ sudo apt-get install -y apt-transport-https curl
$ cat <<EOF | sudo tee /etc/apt/sources.list.d/cuda.list > /dev/null
deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64 /
EOF
$ curl -s \
 https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub \
 | sudo apt-key add -
$ cat <<EOF | sudo tee /etc/apt/preferences.d/cuda > /dev/null
Package: *
Pin: origin developer.download.nvidia.com
Pin-Priority: 600
EOF
$ sudo apt-get update && sudo apt-get install -y --no-install-recommends cuda-drivers
$ sudo reboot
```
```
nvidia-smi
```
# Installing Docker
Install prerequisites, install the GPG key, and add the Docker repository.
```
$ sudo apt-get install -y ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository \
 "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
Add the Docker Engine Utility (nvidia-docker2) repository, install nvidia-docker2, set up permissions to use Docker without sudo each time, and then reboot the system.
```
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
$ curl -s -L https://nvidia.github.io/nvidia-docker/ubuntu16.04/amd64/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt-get update
$ sudo apt-get install -y nvidia-docker2
$ sudo usermod -aG docker $USER
$ sudo reboot
```
# NGC Sign-up
Sign up to NGC if you have not.

https://ngc.nvidia.com/signup/register

Generate your API key, and save it somewhere safe. You will use this soon later.

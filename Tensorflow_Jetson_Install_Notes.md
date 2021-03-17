# Installation Notes for the NVIDIA Jetson 

## Important Note

I spent at least a week trying to install Tensorflow on the NVIDIA Jetson with Python 3.8.  I am not saying that this is impossible.  However, what I am saying is, this can be done using Python 3.6 with relative ease.

[This post](https://forums.developer.nvidia.com/t/official-tensorflow-for-jetson-nano/71770) on the NVIDIA Jetson forum states that Tensorflow will install for "Python3.6+JetPack4.5".  Does that mean that it is impossible to install Tensorflow with Python 3.8?  No clue.  But this is what worked for me.

## Revert to Python 3.6

If you have already gone ahead and updated Python past 3.6, here are the steps to remove your Python3 and install Python 3.6.

#### To list all python versions in default locations

$ ls /usr/bin/python* 

#### To remove just python3 package

$ sudo apt-get remove python3.5

#### plus it's dependent packages

$ sudo apt-get remove --auto-remove python3.5

#### plus configuration and/or data files of python3

$ sudo apt-get purge python3.5

#### both configuration and/or data files of python3.5 and it's dependencies

$ sudo apt-get purge --auto-remove python3.5

#### How to install new version of python
$ sudo apt-get update
$ sudo apt-get install python3

#### Check if Python3 is linked

$ python3 --version

#### If Python3 is not linked

$ sudo ln -sf /usr/bin/python3.6 /usr/bin/python3

## Install Tensorflow Dependencies

Before you install TensorFlow for Jetson, ensure you:

#### 1. Install JetPack on your Jetson device.

#### 2. Install system packages required by TensorFlow:

$ sudo apt-get update
$ sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran

#### 3. Install and upgrade pip3.

$ sudo apt-get install python3-pip
$ sudo pip3 install -U pip testresources setuptools==49.6.0 

#### 4. Install the Python package dependencies.

$ sudo pip3 install -U numpy==1.19.4 future==0.18.2 mock==3.0.5 h5py==2.10.0 keras_preprocessing==1.1.1 keras_applications==1.0.8 gast==0.2.2 futures protobuf pybind11

## Install Tensorflow

#### Install TensorFlow using the pip3 command. This command will install the latest version of TensorFlow compatible with JetPack 4.5.

$ sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v45 tensorflow

Note: TensorFlow version 2 was recently released and is not fully backward compatible with TensorFlow 1.x. If you would prefer to use a TensorFlow 1.x package, it can be installed by specifying the TensorFlow version to be less than 2, as in the following command:

$ sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v45 ‘tensorflow<2’

If you want to install the latest version of TensorFlow supported by a particular version of JetPack, issue the following command:

### Other useful links
https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html
https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform-release-notes/tf-jetson-rel.html#tf-jetson-rel

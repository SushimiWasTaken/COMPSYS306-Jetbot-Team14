How to Install scikit-image
https://github.com/scikit-image/scikit-image/issues/4705#issuecomment-821990920
Here's all that worked for me, I am using a l4t container deployed on Jetson Nano 2
Know more about L4T containers here - https://ngc.nvidia.com/catalog/containers/nvidia:l4t-base

Step 1 UTF-8 Setup

apt-get update
apt-get dist-upgarde

apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y locales

sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

nano ~/.bashrc

Move to end of this file and add EXPORT LANG=en_US.UTF-8 , save this file and get back to terminal

Run these commands now

source ~/.bashrc
STEP 2 DEPENDENCIES - IMAGECODECS AND SCIKIT-IMAGE

apt-get install liblapack-dev gfortran

apt-get install python3-pip

pip3 install -U pip

pip3 install Cython numpy

apt-get install libaec-dev libblosc-dev libffi-dev libbrotli-dev libboost-all-dev libbz2-dev
apt-get install libgif-dev libopenjp2-7-dev liblcms2-dev libjpeg-dev libjxr-dev liblz4-dev liblzma-dev libpng-dev libsnappy-dev libwebp-dev libzopfli-dev libzstd-dev

STEP 3 SCIPY, TIFF, SKLEARN setup

wget https://github.com/scipy/scipy/releases/download/v1.3.3/scipy-1.3.3.tar.gz

tar -xzvf scipy-1.3.3.tar.gz scipy-1.3.3

cd scipy-1.3.3/

python3 setup.py install --user

cd ../

wget https://download.osgeo.org/libtiff/tiff-4.1.0.tar.gz

tar -xzvf tiff-4.1.0.tar.gz

cd tiff-4.1.0/

./configure

make

make install

cd ../
STEP 4 IMAGE CODECS [OPTIONAL - USE ONLY IF Step 5 fails with image codecs issue]

Error Message -

 error: command 'aarch64-linux-gnu-gcc' failed with exit status 1
    ----------------------------------------
ERROR: Command errored out with exit status 1: /usr/bin/python3 -u -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-install-iu5szk39/imagecodecs/setup.py'"'"'; __file__='"'"'/tmp/pip-install-iu5szk39/imagecodecs/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' install --record /tmp/pip-record-ttclns6b/install-record.txt --single-version-externally-managed --compile --install-headers /usr/local/include/python3.6/imagecodecs Check the logs for full command output. 
OR

#include "blosc.h"
              ^~~~~~~~~
    compilation terminated.
    error: command 'x86_64-linux-gnu-gcc' failed with exit status 1

Try to run these commands

pip3 install --upgrade pip setuptools wheel
pip3 install imagecodecs
If these commands fails too, you can build imagecodecs from source on ubuntu

apt-get install build-essential python3-dev cython3 python3-setuptools python3-pip python3-wheel python3-numpy python3-pytest python3-blosc python3-brotli python3-snappy python3-lz4 libz-dev libblosc-dev liblzma-dev liblz4-dev libzstd-dev libpng-dev libwebp-dev libbz2-dev libopenjp2-7-dev libjpeg-dev libjxr-dev liblcms2-dev libcharls-dev libaec-dev libbrotli-dev libsnappy-dev libzopfli-dev libgif-dev libtiff-dev libdeflate-dev libavif-dev

wget https://github.com/cgohlke/imagecodecs/archive/refs/tags/v2021.3.31.tar.gz

tar -xzvf imagecodecs-2021.3.31.tar.gz imagecodecs

cd imagecodecs

python3 setup.py install --user

cd ../

STEP 5 Installing SCIKIT-IMAGE

pip3 install scikit-image

IMPORTANT POINTS

Don't use python3-skimge* packages, they are obsolete
Stick to pip3, not pip
Upgrade pip and all other distributions before proceeding
@hmaarrfk do checkout if these solutions can help in other issues as well. Issues including installation of scikit-image and sklearn can be resolved on LINUX ARM-64 based platforms



************************************
sklearn install
***
Inside Docker
***
apt update
apt list --upgradable
apt udpate
apt upgrade

apt remove python3-sklearn

pip3 install sklearn
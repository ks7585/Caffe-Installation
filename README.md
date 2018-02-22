# Caffe-Installation On Ubuntu 16.04 with NVIDIA Titax X GPU 
Installating caffe is a tedious process as it took me around 4-5 hours to figure out the dependancies. 

# Install Nvidia driver and Cuda (Optional)
If you want to use GPU to accelerate, follow instructions here to install Nvidia drivers, CUDA 8RC and cuDNN 5 (skip caffe installation there).

# Install Anaconda
Download Anaconda from here ("https://www.anaconda.com/download/#linux"). Choose Python 2.7 version 64-BIT INSTALLER to install it. Then update it:

```
conda update conda
```
If you want to create an environment such as testcaffe, execute commands:
```
conda create -n caffe
source activate caffe
```
Install OpenCV:
```
conda install -c menpo opencv3
```
Install Dependencies
Installing all the required dependencies are important for installation.
```
sudo apt-get update

sudo apt-get upgrade

sudo apt-get install -y build-essential cmake git pkg-config

sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev protobuf-compiler

sudo apt-get install -y libatlas-base-dev 

sudo apt-get install -y --no-install-recommends libboost-all-dev

sudo apt-get install -y libgflags-dev libgoogle-glog-dev liblmdb-dev
```
# Build Caffe
Go to Caffe Website ( https://github.com/BVLC/caffe ), download zip archive and unpack it. Or clone the source code. 
```
cd caffe
mkdir build
cd build
cmake ..
make all
make install
```
The make commands take a while. Make sure it doesn't throw up any error.

Now change the directory to the caffe/python to install all the Python Packages. 
```
cd caffe/python
``` 
```
conda install cython scikit-image ipython h5py nose pandas protobuf pyyaml jupyter
for req in $(cat requirements.txt); do pip install $req; done
cd ../build
make runtest
```
If you want to use some other packages in the Conda evnviroment, you need to install them now, otherwise the packages might not find the dependences you installed in the evnviroment.

Add the module directory to your $PYTHONPATH by
```
cd ../python
export PYTHONPATH=`pwd`${PYTHONPATH:+:${PYTHONPATH}}
```
Now link the caffe package path to python
```
ln -s /path/to/my/package /path/to/anaconda/lib/python3.6/site-packages/
```
# Testing 
```
$python
>>>import caffe
>>>
```
Now try running the Examples from (http://caffe.berkeleyvision.org/gathered/examples/mnist.html)





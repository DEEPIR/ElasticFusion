编译准备：下载官方给出的依赖如下
sudo apt-get install -y cmake-qt-gui git build-essential libusb-1.0-0-dev libudev-dev openjdk-7-jdk freeglut3-dev libglew-dev cuda-7-5 libsuitesparse-dev libeigen3-dev zlib1g-dev libjpeg-dev

通过git下载源码，命令如下：
git clone https://github.com/mp3guy/ElasticFusion.git 

下载编译安装Pangolin, Pangolin是对OpenGL进行封装的轻量级的OpenGL输入/输出和视频显示的库，可以用于3D视觉和#D导航的视觉图，可以输入各种类型的视频，编译命令如下：git clone https://github.com/stevenlovegrove/Pangolin.git

cd Pangolin

mkdir build

cd build

cmake ../ -DAVFORMAT_INCLUDE_DIR="" -DCPP11_NO_BOOST=ON

make -j8

sudo make install

下载编译安装Openni2:
git clone https://github.com/occipital/OpenNI2.git

cd OpenNI2

make -j8

cd ..

若此时执行OpenNi2/Bin/x64-Release下的NiViewer是不能成功的，需要在按安裝libfreenect2驱动后将libfreenect2/build/lib下的libfreenect2-openni2.so ，libfreenect2-openni2.so.0 , libfreenect2.so.0.2 拷贝到OpenNi2/Bin/x64-Release/OpenNi2/Drivers下。

最后以此编译ElasticFusion中的模块：
核心API模块：
cd ../Core

mkdir build

cd build

cmake ../src

make -j8

sudo make install

GPUTest模块：
cd ../../GPUTest

mkdir build

cd build

cmake ../src

make -j8

GUI图形操作模块：
cd ../../GUI

mkdir build && cd build

cmake ../src && make -j8

编译成功则在build目录下生成名为ElasticFusion的可执行文件，如果在线实时运行，则只需执行./ElasticFusion即可，若跑公开数据集，则执行./ElasticFusion -l + dataPath

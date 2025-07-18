# ***下载的库文件汇总(包括c++和python)*** #

1.libhv
(网络阻隔也可以直接下载预编译的版本, 这里给出源代码编译的方法, 切换到/opt目录)
git clone https://github.com/ithewei/libhv.git
cd libhv
./configure
make -j$(nproc)
sudo make install

2.opencv
(在ubuntu22.04条件下可以默认下载较高的预编译版本4.x, 并且预编译版本自动集成ffmpeg)
sudo apt install -y python3-opencv libopencv-dev
sudo cp -r /usr/include/opencv4/opencv2 /usr/include/
sudo rm -rf /usr/include/opencv4/

## 如果使用源代码编译:
参见https://developer.aliyun.com/article/1394853可以下载4.11.0较新的版本(下载依赖库的一个修正:sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main")
cd opencv-4.11.0
mkdir build
cd build
sudo cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_GENERATE_PKGCONFIG=ON -D BUILD_EXAMPLES=OFF -D INSTALL_PYTHON_EXAMPLES=OFF -D INSTALL_C_EXAMPLES=OFF -D WITH_JPEG=ON -D WITH_PNG=ON -D WITH_TIFF=ON -D WITH_WEBP=ON ..
make -j$(nproc)
sudo make install
sudo echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf
sudo ldconfig

3.yolo相关的
pip install ultralytics

4.ort
(备选的模型转换方案, github上可以选择cpu/gpu版本)
pip install onnx onnxruntime
https://github.com/microsoft/onnxruntime/releases # 在这个网址下载onnxruntime-linux-x64-1.21.0.tgz并放到/opt
tar -xzf ./onnxruntime-linux-x64-1.21.0.tgz
mv onnxruntime-linux-x64-1.21.0/ onnxruntime-cpu
sudo cp -r /opt/onnxruntime-cpu/include/* /usr/local/include/
sudo cp -r /opt/onnxruntime-cpu/lib/* /usr/local/lib/

5.boost
直接在命令行包管理下载:sudo apt install libboost-all-dev
头文件在/usr/include/boost
库文件在/usr/lib/x86_64-linux-gnu/

6.yaml
sudo apt install libyaml-cpp-dev
头文件在/usr/include/yaml-cpp
库文件在/usr/lib/x86_64-linux-gnu/

7.海康威视rtsp路由规则
https://www.cnblogs.com/liushui-sky/p/14241317.html

8.安装软件包的镜像源24.04和它之前的有区别
#
22.04:在/etc/apt/sources.list 版本代号jammy,20.04是focal,再往前是xenial
deb-src http://archive.ubuntu.com/ubuntu/ jammy main restricted #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ jammy main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ jammy main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted multiverse universe #Added by software-properti>deb http://>
deb http://mirrors.aliyun.com/ubuntu/ jammy-updates universe
deb http://mirrors.aliyun.com/ubuntu/ jammy multiverse
deb http://mirrors.aliyun.com/ubuntu/ jammy-updates multiverse
deb http://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse #Added by software-proper>deb http://>
deb-src http://archive.canonical.com/ubuntu jammy partner
deb http://mirrors.aliyun.com/ubuntu/ jammy-security main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ jammy-security main restricted multiverse universe #Added by software-propert>deb http://>
deb http://mirrors.aliyun.com/ubuntu/ jammy-security multiverse

#
24.04:在/etc/apt/sources.list.d/ubuntu.sources
Types: deb
URIs: http://mirrors.aliyun.com/ubuntu/
Suites: noble noble-updates noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg



# ***当前v3版本需要的所有配置*** #

# 0.GNU工具链等最基本配置

# 1.libhv
git clone https://github.com/ithewei/libhv.git
cd libhv
./configure
make -j$(nproc)
sudo make install

# 2.opencv
git clone https://github.com/opencv/opencv.git
# 将当前包含版本号的文件夹名称改为opencv
cd opencv
mkdir build
cd build
sudo cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_GENERATE_PKGCONFIG=ON -D BUILD_EXAMPLES=OFF -D INSTALL_PYTHON_EXAMPLES=OFF -D INSTALL_C_EXAMPLES=OFF -D WITH_JPEG=ON -D WITH_PNG=ON -D WITH_TIFF=ON -D WITH_WEBP=ON ..
make -j$(nproc)
sudo make install
sudo echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf
sudo ldconfig

# 3.boost
sudo apt install libboost-all-dev

# 4.yaml
sudo apt install libyaml-cpp-dev
# Ipopt CasADi Installation

Ipopt、CasADi安装配置，基于Ubuntu20.04.6LTS

## 一、安装Ipopt

### 1. 创建文件夹进行包管理并安装依赖

```bash
mkdir ipopt
cd ipopt
sudo apt install gcc g++ gfortran git patch wget pkg-config libblas-dev liblapack-dev libmetis-dev
```

一些帖子中提到的BLAS和LAPACK已经包含在liblapack-dev依赖中。

### 2. 安装ASL (Ampl Solver Library)

```bash
git clone https://github.com/coin-or-tools/ThirdParty-ASL.git
cd ThirdParty-ASL
./get.ASL
./configure
make
sudo make install
cd ..
```

### 3. 安装HSL (Harwell Subroutines Library)

求解器官网下载免费的MA27版本，点击Free to all的`Yes`，在HSL Archive Licence下点击`ORDER NOW`，按照引导填写信息，最后下载最新的zip archive压缩包文件即可。

官网：https://licences.stfc.ac.uk/product/coin-hsl

```bash
git clone https://github.com/coin-or-tools/ThirdParty-HSL.git
cd ThirdParty-HSL
# 压缩包解压并重命名为coinhsl，放到ThirdParty-HSL目录下 (ThirdParty-HSL/coinhsl)
./configure
make
sudo make install
cd ..
```

### 4. 安装MUMPS Linear Solver 

```bash
git clone https://github.com/coin-or-tools/ThirdParty-Mumps.git
cd ThirdParty-Mumps
./get.Mumps
./configure
make
sudo make install
cd ..
```

### 5. 安装Ipopt

```bash
git clone https://github.com/coin-or/Ipopt.git
cd Ipopt
mkdir build
cd build
../configure
```

检查如下信息：

```bash
...
checking for LAPACK... yes: generic module (lapack.pc blas.pc)
checking for package ASL... yes
checking for package Mumps... yes
...
checking for package HSL... yes
checking for function ma27ad_ in -L/usr/local/lib -lcoinhsl   ... yes
checking for function ma28ad_ in -L/usr/local/lib -lcoinhsl   ... yes
...
```

继续完成编译：

```bash
make 
make test         #可以验证编译是否成功
sudo make install
```

最后去到`/usr/local/include`目录：

```bash
sudo cp coin-or coin -r         #文件夹改名否则会找不到头文件
```

### 参考

官网https://coin-or.github.io/Ipopt/INSTALL.html

https://blog.csdn.net/asd22222984565/article/details/130794329

https://zhuanlan.zhihu.com/p/675009435?utm_id=0


## 二、安装CasADi

```bash
git clone https://github.com/casadi/casadi.git
cd casadi
mkdir build
cd build
cmake .. -DWITH_IPOPT=ON         #不要使用官网教程，会报错
cmake .. -DCMAKE_BUILD_TYPE=RELEASE
make
sudo make install
```

### 参考

官网https://github.com/casadi/casadi/wiki/InstallationLinux

https://blog.csdn.net/shiquan0914/article/details/130521274

https://blog.csdn.net/asd22222984565/article/details/134043389


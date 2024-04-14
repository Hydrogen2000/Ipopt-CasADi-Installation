# Ipopt和CasADi安装配置

基于Ubuntu20.04.6LTS

## 一、安装Ipopt

官网https://coin-or.github.io/Ipopt/INSTALL.html

教程https://blog.csdn.net/asd22222984565/article/details/130794329

教程https://zhuanlan.zhihu.com/p/675009435?utm_id=0

### 1. ipopt除了源码外还使用了一些其他的包，为了方便管理建议专门建立一个文件夹

```
mkdir ipopt
cd ipopt
```

### 2. 安装依赖

```
sudo apt install gcc g++ gfortran git patch wget pkg-config libblas-dev liblapack-dev libmetis-dev
```

### 3. 安装ASL(Ampl Solver Library)

```
git clone https://github.com/coin-or-tools/ThirdParty-ASL.git
cd ThirdParty-ASL
./get.ASL
./configure
make
sudo make install
cd ..
```

### 4. 安装BLAS和LAPACK

包含在liblapack-dev依赖中

### 5. 安装HSL(Harwell Subroutines Library)

官网https://licences.stfc.ac.uk/product/coin-hsl

```
git clone https://github.com/coin-or-tools/ThirdParty-HSL.git
cd ThirdParty-HSL
在官网下载免费的MA27版本(Coin-HSL Archive)，压缩包解压并重命名为coinhsl，放到ThirdParty-HSL目录下(ThirdParty-HSL/coinhsl)
./configure
make
sudo make install
cd ..
```

### 6. 安装MUMPS Linear Solver 

```
git clone https://github.com/coin-or-tools/ThirdParty-Mumps.git
cd ThirdParty-Mumps
./get.Mumps
./configure
make
sudo make install
cd ..
```

### 7. 安装Ipopt

```
git clone https://github.com/coin-or/Ipopt.git
cd Ipopt
mkdir build
cd build
../configure
```

检查如下信息

```
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

继续完成编译

```
make 
make test         #可以验证编译是否成功
sudo make install
```

最后去到/usr/local/include目录

```
sudo cp coin-or coin -r         #把文件夹改名要不会找不到头文件
```

## 二、安装CasADi

官网https://github.com/casadi/casadi/wiki/InstallationLinux

教程https://blog.csdn.net/shiquan0914/article/details/130521274

教程https://blog.csdn.net/asd22222984565/article/details/134043389

```
git clone https://github.com/casadi/casadi.git
cd casadi
mkdir build
cd build
cmake .. -DWITH_IPOPT=ON         #这里不要使用官网教程，会报错
cmake .. -DCMAKE_BUILD_TYPE=RELEASE
make
sudo make install
```


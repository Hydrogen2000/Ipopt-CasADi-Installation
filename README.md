# Ipopt和CasADi安装配置

基于Ubuntu20.04.6LTS

## 一、安装Ipopt

1. ipopt除了源码外还使用了一些其他的包，为了方便管理建议专门建立一个文件夹
```
mkdir ipopt
cd ipopt
```

2. 安装依赖
```
sudo apt install gcc g++ gfortran git patch wget pkg-config libblas-dev liblapack-dev libmetis-dev
```

3. 安装ASL(Ampl Solver Library)
```
git clone https://github.com/coin-or-tools/ThirdParty-ASL.git
cd ThirdParty-ASL
./get.ASL
./configure
make
sudo make install
cd ..
```





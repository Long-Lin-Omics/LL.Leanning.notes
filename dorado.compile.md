
# get new gcc
```
wget https://ftp.gnu.org/gnu/gcc/gcc-9.5.0/gcc-9.5.0.tar.gz
tar -xzvf gcc-9.5.0.tar.gz
cd gcc-9.5.0
wget https://ftp.gnu.org/gnu/gmp/gmp-6.2.1.tar.xz
wget https://ftp.gnu.org/gnu/mpfr/mpfr-4.1.0.tar.xz
wget https://ftp.gnu.org/gnu/mpc/mpc-1.2.1.tar.gz
tar -xf gmp-6.2.1.tar.xz
mv gmp-6.2.1 gmp
tar -xf mpfr-4.1.0.tar.xz
mv mpfr-4.1.0 mpfr
tar -xf mpc-1.2.1.tar.gz
mv mpc-1.2.1 mpc

mkdir gcc-9.5.0-build # can't to be 
cd gcc-9.5.0-build
../gcc-9.5.0/configure  --prefix=/ddn/gs1/home/linl7/bin/gcc-950 --disable-multilib --enable-languages=c,c++
make -j$(nproc)
make install
~/bin/gcc-950/bin/gcc -version
```


# get new cmake
```
cmake --version

wget https://github.com/Kitware/CMake/releases/download/v3.29.4/cmake-3.29.4-linux-x86_64.tar.gz
tar -zxvf cmake-3.29.4-linux-x86_64.tar.gz

./cmake-3.29.4-linux-x86_64/bin/cmake  --version
```


# compile dorado

```
git clone https://github.com/nanoporetech/dorado.git
mkdir dorado/build
cd dorado/build
	# release doesn't have htslib under 3rdparty, have to add it manually
	# wget https://cdn.oxfordnanoportal.com/software/analysis/dorado-1.0.2-linux-x64.tar.gz
	# tar -xvzf dorado-1.0.2-linux-x64.tar.gz
	# cd dorado-1.0.2/build
export LD_LIBRARY_PATH=/ddn/gs1/home/linl7/bin/gcc-950/lib64:$LD_LIBRARY_PATH
~/bin/cmake-3.29.4-linux-x86_64/bin/cmake .. -DCMAKE_C_COMPILER=/ddn/gs1/home/linl7/bin/gcc-950/bin/gcc -DCMAKE_CXX_COMPILER=/ddn/gs1/home/linl7/bin/gcc-950/bin/g++ -DCMAKE_INSTALL_RPATH=/ddn/gs1/home/linl7/bin/gcc-950/lib64 -DZLIB_INCLUDE_DIR=/usr/include -DZLIB_LIBRARY=/lib64/libz.so -DCMAKE_BUILD_RPATH=/ddn/gs1/home/linl7/bin/gcc-950/lib64
make -j$(nproc)
make install
./bin/dorado -h
```


# MSYS2 builds of HDF5

MSYS2 builds of hdf5 using the mingw compiler

## Build instructions

Install required patches

```sh
pacman -S mingw-w64-x86_64-gcc patch diffutils
```

Download hdf5

```sh
cd ~

wget -O https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.5/src/hdf5-1.10.5.tar.gz

wget -O https://github.com/musm/hdf5-builds/blob/master/utf8-windows-filenames.patch
```

Compile and install

```sh
tar zxf hdf5-1.10.5.tar.gz

cd hdf5-1.10.5

patch -p1 < ~/utf8-windows-filenames.patch

autoreconf -i

./configure --host=x86_64-w64-mingw32 --build=x86_64-w64-mingw32 --prefix=$HOME/hdf5 CPPFLAGS="-D_GNU_SOURCE=1"

make -j -l6

make install
```

Then zip the output located in `$HOME/hdf5`

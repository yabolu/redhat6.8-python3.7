### redhat6.8 源码安装python3.7

##### 1. Requirements

```
sudo yum install zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel \
openssl-devel xz xz-devel libffi-devel
```

##### 2. 安装openssl

如果出现以下错误, 需要重新安装最新的openssl, 因为yum 安装的版本不是最新的, 所以建议源码安装

`ERROR: The Python ssl extension was not compled. Missing the OpenSSL lib?`

```
tar zxvf openssl-1.1.1.tar.gz
cd openssl-1.1.1
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl shared zlib
make
make test
make install

mv /usr/bin/openssl /root/
ln -s /usr/local/openssl/bin/openssl /usr/bin/openssl

ln -s /usr/local/openssl/lib/libcrypto.so.1.1 /usr/lib64/libcrypto.so.1.1
ln -s /usr/local/openssl/lib/libssl.so.1.1 /usr/lib64/libssl.so.1.1
```

##### 3. 安装python3.7.0

```
###设置环境变量
echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/openssl/lib" >> $HOME/.bash_profile
source $HOME/.bash_profile

###安装
xz -d Python-3.7.0.tar.xz
tar xvf Python-3.7.0.tar
cd Python-3.7.0
./configure --prefix=/usr/local/sbin/python-3.7 --with-openssl=/usr/local/openssl
make
make install

###验证
/usr/local/sbin/python-3.7/bin/python3

###替换默认python版本
mv /usr/bin/python /root
ln -s /usr/local/sbin/python-3.7/bin/python3 /usr/bin/python
python --version
```







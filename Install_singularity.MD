
# Installing singularity in centos 07
```
sudo yum update -y
sudo yum install -y epel-release
sudo yum update -y
```
```
 sudo yum install -y singularity-runtime singularity
```
Now it will be installed. 
Can crosscheck the same by checking the version 
```
singularity --version
```
# Installing singularity in ubuntu 18.04
### Installing the dependencies
```
sudo apt-get update && sudo apt-get install -y \
    build-essential \
    uuid-dev \
    libgpgme-dev \
    squashfs-tools \
    libseccomp-dev \
    wget \
    pkg-config \
    git \
    cryptsetup-bin
```
### Installing Go
```
    export VERSION=1.19.1 OS=linux ARCH=amd64 && \
    wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz && \
    sudo tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz && \
    rm go$VERSION.$OS-$ARCH.tar.gz
```
set up your environment for Go.
```
    echo 'export GOPATH=${HOME}/go' >> ~/.bashrc && \
    echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc && \
    source ~/.bashrc
```
### Download Singularity from a release
```
    export VERSION=3.10.2 && # adjust this as necessary \
    wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-ce-${VERSION}.tar.gz && \
    tar -xzf singularity-ce-${VERSION}.tar.gz && \
    cd singularity-ce-${VERSION}
```
### Compile singularity 
```
   ./mconfig && \
    make -C ./builddir && \
    sudo make -C ./builddir install
```
### Some times you may encounter the following error
```
glib-2.0 headers are required to build conmon
```
In that case you can install the glib-2.0 headers using 
```
sudo apt-get install libglib2.0-dev
```

### Build a singularity container using the build file 
```
sudo singularity build <container_name>.img Singularity_fenics2017_msucompbiomechlab
```

### After building, loading the image in the container with mounting an external disk or partition
```
singularity shell --bind <partition__directory> <image_name>
```
## After building, loading the image in the container without any  mounting an external
```
singularity run <image_name>
```



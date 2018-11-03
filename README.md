# Data Science - Docker

Data Science Container using ubuntu, python, tensorflow, sklearn, keras in one image.



## Getting Started

These instructions will cover usage information and for the docker container

```shell
# Use latest Python runtime as a parent image
FROM ubuntu:18.04

# Meta-data
LABEL maintainer="C Ferraren <cliferraren@gmail.com>" \
      description="Data Science Container\
      Libraries, data, and code in one image"

RUN apt-get update && apt-get install -y wget ca-certificates \
    build-essential python3.7 python3.7-dev python3-pip \
    git curl vim \
    libpng-dev \
    libjpeg-dev \
    libpnglite-dev \
    libhdf5-dev \
    libfreetype6-dev \
    libhdf5-serial-dev \
    libtool \
    libzmq3-dev \
    pkg-config \
    libgraphviz-dev \
    graphviz \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*


RUN pip3 install --upgrade pip
RUN pip3 install tensorflow numpy==1.14.5 && \
    pip3 install --upgrade pandas scipy matplotlib seaborn jupyter pyyaml h5py Pillow pydotplus pygraphviz graphviz && \
    pip3 install scikit-learn==0.20rc1 && \
    pip3 install keras

# Set the working directory to /app
WORKDIR /app/Notebooks

# Copy the current directory contents into the container at /app
COPY . /app

# Create mountpoint
VOLUME /app/Notebooks

# Jupyter and Tensorboard ports
EXPOSE 8888 6006

# Run jupyter when container launches
CMD ["jupyter", "notebook", "--ip='*'", "--port=8888", "--no-browser", "--allow-root"]
```

### Prerequisities


In order to run this container you'll need docker installed.

* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)


### Usage

#### Container Parameters

List the different parameters available to your container

```shell
docker run -v /your/file/location/:/app/Notebooks -p 8888:8888 -p 6006:6006 --name machine-learning datascience:0.0.1
```

#### Volumes

* `/your/file/location` - File location


## Find Us

* [GitHub](https://github.com/CFerraren)


## Contributing



## Versioning

1.0

## Authors

* **Clifford Ferraren** - *Initial work* - [CFerraren](https://github.com/CFerraren)


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.


FROM rockylinux:8

# This version of tkmatrix requires Python 3.10 which is not avilible
# via the dnf package manager. Instead, we install some extra system
# dependencies and compile Python from source.

RUN dnf install -y \
      gcc \
      gcc-c++ \
      xz \
      findutils \
      openssl-devel \
      bzip2-devel \
      libffi-devel \
      zlib-devel \
      wget \
      make \
      gcc-gfortran

RUN wget https://www.python.org/ftp/python/3.10.5/Python-3.10.5.tar.xz \
    && tar -xf Python-3.10.5.tar.xz \
    && cd Python-3.10.5 \
    && ./configure --enable-optimizations \
    && make -j 4 \
    && make altinstall

# Per the tkmatrix docs, some dependencies must be individually installed
# prior to installing kmatrix itself. Version numbers for these packages are
# pinned to the value defined in the requirements file.

ENV PIP_ROOT_USER_ACTION=ignore
COPY requirements.txt requirements.txt
RUN pip3.10 install numpy==1.23.5 && \
    pip3.10 install ellc==1.8.5 && \
    pip3.10 install -r requirements.txt && \
    pip3.10 install tkmatrix==0.7.0

RUN mkdir tkm
WORKDIR /tkm
ENTRYPOINT ["python3.10", "-m", "tkmatrix"]

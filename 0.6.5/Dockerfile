FROM rockylinux:8

RUN dnf install -y \
      gcc-gfortran \
      python39 \
      python39-devel

# Per the tkmatrix docs, some dependencies must be individually installed
# prior to installing kmatrix itself. Version numbers for these packages are
# pinned to the value defined in the requirements file.

COPY requirements.txt requirements.txt
RUN pip3 install numpy==1.23.5 && \
    pip3 install ellc==1.8.5 && \
    pip3 install -r requirements.txt && \
    pip3 install tkmatrix==0.6.5 

RUN mkdir tkm
WORKDIR /tkm
ENTRYPOINT ["python3.9", "-m", "tkmatrix"]


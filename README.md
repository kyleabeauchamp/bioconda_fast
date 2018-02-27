# bioconda_fast

```bash
docker pull gcc
export IID=XYZ  #  Look up image ID via docker image list
docker run -it --entrypoint bash $IID

# Inside the VM
cd ~/
git clone https://github.com/kyleabeauchamp/bioconda_fast.git
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b
source ~/miniconda3/bin/activate root
conda install conda-build=2.1.17 -y  # Need to use old version that doesn't use conda-based compilers.

export CONDA_ZLIB=1.2.8
cd ~/bioconda_fast/recipes/bwa/
conda-build ./0.7.3a/


# Outside the VM
export CID=XYZ  #  Look up container ID via docker ps
docker cp $CID:/root/miniconda3/conda-bld/linux-64/bwa-0.7.3a-1.tar.bz2 ./

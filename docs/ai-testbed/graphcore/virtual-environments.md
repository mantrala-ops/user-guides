# Virtual Environments

## Poplar SDK Setup

The Poplar SDK is downloaded onto the graphcore systems at the `/software/graphcore/poplar_sdk/` location. The default poplar
version (3.1.0) is enabled automatically upon logging into a graphcore node.

Check if **Poplar** is setup correctly:

```bash
popc --version
```

One should see:

```console
POPLAR version 3.1.0 (e12d5f9f01)
clang version 15.0.0 (bab932b4fc4cdb58bb009370384b2c41579bd9d9)
```

If the Poplar SDK is not enabled, it can be enabled with
```bash
source /software/graphcore/poplar_sdk/3.1.0/enable
```

To disable the current Poplar SDK, e.g. if one wants to use a different Poplar SDK,

```bash
unset POPLAR_SDK_ENABLED
```

## Miscellaneous Environment Variables

```bash
mkdir ~/tmp
export TF_POPLAR_FLAGS=--executable_cache_path=~/tmp
export POPTORCH_CACHE_DIR=~/tmp

export POPART_LOG_LEVEL=WARN
export POPLAR_LOG_LEVEL=WARN
export POPLIBS_LOG_LEVEL=WARN

export PYTHONPATH=/software/graphcore/poplar_sdk/3.1.0/poplar-ubuntu_20_04-3.1.0+6824-9c103dc348/python:$PYTHONPATH
```

## PopTorch Environment Setup

PopTorch is an extension of the Pytorch framework that is optimized for the IPU specific functionality. To activate the PopTorch environment, first create a virtual environment and activate it.

```bash
mkdir -p ~/venvs/graphcore
virtualenv ~/venvs/graphcore/poptorch31_env
source ~/venvs/graphcore/poptorch31_env/bin/activate
```

Use the following commands to install the PopTorch environment.

```bash
POPLAR_SDK_ROOT=/software/graphcore/poplar_sdk/3.1.0
export POPLAR_SDK_ROOT=$POPLAR_SDK_ROOT
pip install $POPLAR_SDK_ROOT/poptorch-3.1.0+98660_0a383de63f_ubuntu_20_04-cp38-cp38-linux_x86_64.whl
```

## TensorFlow 2 Environment Setup

The Poplar SDK provides TensorFlow and Keras wheels built on 2.6 that includes the IPU specific functionality and optimized for the AMD processors. It can be installed as follows.

Create virtual environment.

```bash
virtualenv ~/venvs/graphcore/tensorflow2_31_env
source ~/venvs/graphcore/tensorflow2_31_env/bin/activate
```

Install the TensorFlow and Keras wheels.

```bash
POPLAR_SDK_ROOT=/software/graphcore/poplar_sdk/3.1.0
export POPLAR_SDK_ROOT=$POPLAR_SDK_ROOT
pip install $POPLAR_SDK_ROOT/tensorflow-2.6.3+gc3.1.0+246224+2b7af067dae+amd_znver1-cp38-cp38-linux_x86_64.whl
pip install $POPLAR_SDK_ROOT/keras-2.6.0+gc3.1.0+246230+88e2debf-py2.py3-none-any.whl
```

### Verify Installation

```bash
python -c "from tensorflow.python import ipu"
```

You should see:

```console
2023-04-24 23:13:36.091496: I tensorflow/compiler/plugin/poplar/driver/poplar_platform.cc:43] Poplar version: 3.1.0 (e12d5f9f01) Poplar package: 9c103dc348
```

## Installing Packages

Install packages in the normal manner such as:

```bash
python3 -m pip install "some_package"
```

For more details see [Use pip for installing](https://packaging.python.org/en/latest/tutorials/installing-packages/#use-pip-for-installing).

To install a different version of a package that is already installed in one's environment, one can use:

```bash
pip install --ignore-installed  ... # or -I
```

> **Note**: Conda is not supported on the Graphcore system.

---
layout: post
title: "Setting up M1 mac for both TensorFlow and PyTorch"
date:   2021-01-29 02:16:00 +0900
author: "Sihyung Park"
categories: [machine learning]
---

Macs with ARM64-based M1 chip, launched shortly after Apple's initial announcement of their plan to migrate to Apple Silicon, got quite a lot of attention both from consumers and developers. It became headlines especially because of its outstanding performance, not in the ARM64-territory, but in all PC industry. 

As a student majoring in statistics with coding hobby, the one somewhere inbetween an consumer tech enthusiast and a programmer, I was one of the people who was dazzled by the benchmarks and early reviews emphasizing it. So after (almost) 7 years spent with my MBP (mid 2014), I decided to leave Intel and join M1.

This is the post written for myself, after running about in confutsion to set up the environment for machine learning on M1 mac. What I tried to achieve was

* *Not* using the "system python" (`‌/usr/bin/python`).
* [TensorFlow running natively on Apple Silicon](https://github.com/apple/tensorflow_macos).
* PyTorch running on Rosetta 2[^1].
* Running everything else natively if possible.

It is not an elegant solution, but I am satisfied for the result, for now.

<br>

## Install `TensorFlow-macOS` for Apple Silicon M1

It is easy to install it with the system python since the installation script is given by Apple. However, my goal was to install it with other python so that I can install additional packages for data science without difficulty. 

I mainly followed instructions from [here](https://laptrinhx.com/tensorflow-2-4-on-apple-silicon-m1-installation-under-conda-environment-2235153130/) to install tensorflow-macos, and then created ipykernel of it so that I can run this environment any time by switching the kernel inside jupyter notebook.

1. First install [miniforge, which natively supports M1](https://github.com/conda-forge/miniforge#download). The installation defaults to directory `~/miniforge3/`.

2. Create virtual environment named `tf_macos` with conda and install Python 3.8.\
```zsh
conda create -n tf_macos
conda activate tf_macos
conda install -y python=3.8
```
I specified the version 3.8 so that it matches requirement of `tensorflow-macos`.

3. Download and install `tensorflow-macos` from [Apple Github](https://github.com/apple/tensorflow_macos).\
```zsh
git clone https://github.com/apple/tensorflow_macos.git
cd tensorflow_macos/arm64
```
```zsh
pip install --force pip==20.2.4 wheel setuptools cached-property six
pip install --upgrade --no-dependencies --force numpy-1.18.5-cp38-cp38-macosx_11_0_arm64.whl grpcio-1.33.2-cp38-cp38-macosx_11_0_arm64.whl h5py-2.10.0-cp38-cp38-macosx_11_0_arm64.whl tensorflow_addons-0.11.2+mlcompute-cp38-cp38-macosx_11_0_arm64.whl
pip install absl-py astunparse flatbuffers gast google_pasta keras_preprocessing opt_einsum protobuf tensorflow_estimator termcolor typing_extensions wrapt wheel tensorboard typeguard
pip install --upgrade --force --no-dependencies tensorflow_macos-0.1a1-cp38-cp38-macosx_11_0_arm64.whl
```

4. Add the environment as jupyter kernel.
```zsh
pip install jupyter
```
```zsh
python -m ipykernel install --name=tf_macos
```
Then merly switching the kernel to `tf_macos` allows us to use TensorFlow optimized for M1 without a hassle.

5. Install additional packages (optional)
```zsh
conda install scipy pandas matplotlib
```

<br>

## Install PyTorch for x86_64 (Rosetta 2)

Miniforge installed when installing `tensorflow-macos` defaults to python for ARM64 architecture. PyTorch for Rosetta 2 emulation requires Python for x86_64. Although the system python supports both architectures, to avoid using it I chose to install another miniforge, this time built for x86_64.

[**Open Terminal with Rosetta 2**](https://www.byran.tech/techblogs/MakeRosetta2Terminal.html) and follow the instruction below.

1. Install miniforge for x86_64. \
```zsh
# install miniforge x86_64 in another directory
/bin/bash Miniforge3-MacOSX-x86_64 -p /Users/$(whoami)/miniforge_x86_64
```
Be careful not to install it in the same directory as previously installed miniforge (ARM64).

2. Create virtual environment.\
```zsh
conda create --name=pytorch_x86
conda activate pytorch_x86
conda install -y python=3.8
```
The prefixed `arch -x86_64` is for Rosetta 2 emulation of the command.

3. Install PyTorch and related packages.\
```zsh
pip install torch torchvision
```
and that's it for the package installation.

4. Install jupyter and add ipykernel.\
```zsh
pip install jupyter
python -m ipykernel install --name=pytorch_x86
```
Finish the kernel setup by editing the associated json file: Replace the content of `/usr/local/share/jupyter/kernels/pytorch_x86/kernel.json` to
```json
{
 "argv": [
  "arch",
  "-x86_64",
  "/Users/$(whoami)/miniforge3_x86_64/envs/pytorch_x86/bin/python",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "pytorch_x86",
 "language": "python"
}
```

5. Revert miniforge back to ARM64 version (optional)\
Since my goal was to run the other programs natively as possible, I reverted miniforge back to M1 build.<br>
Just comment out the part of `~/.zshrc` to be
```bash
# >>> conda initialize >>>
# # !! Contents within this block are managed by 'conda init' !!
# __conda_setup="$('/Users/$(whoami)/miniforge3_x86_64/bin/conda' 'shell.zsh' 'hook' 2> /dev/null)"
# if [ $? -eq 0 ]; then
#     eval "$__conda_setup"
# else
#     if [ -f "/Users/$(whoami)/miniforge3_x86_64/etc/profile.d/conda.sh" ]; then
#         . "/Users/$(whoami)/miniforge3_x86_64/etc/profile.d/conda.sh"
#     else
#         export PATH="/Users/$(whoami)/miniforge3_x86_64/bin:$PATH"
#     fi
# fi
# unset __conda_setup
# # <<< conda initialize <<<
```
(or change the content of `~/.bash_profile` similarly if you are using bash). Uncomment it whenever x86_64 version of miniforge is required.

Then all is well! If you want to work on TensorFlow (runs natively, utilizing full potential of M1), activate `tf_macos` or select the jupyter kernel in notebook or ipython. If you want x86_64 environment with bug-free PyTorch, do the similar but with `pytorch_x86`.
<br><br>

---

[^1]: The reason I gave up installing PyTorch running natively on M1 is because it had an error that made the input layer of a neural net detached from the rest of the architecture. Although building from the source and installation of the wheel was successful, I could not handle this bug which made it useless.
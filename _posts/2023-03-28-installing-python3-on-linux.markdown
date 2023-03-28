---
layout: post
comments: true
title:  "Installing Python3 On Linux"
date:   2020-01-26 00:04:58 +0530
categories: general
---


# Installing Python

- $ sudo apt-get install software-properties-common
- $ sudo add-apt-repository ppa:deadsnakes/ppa
- $ sudo apt-get update
- $ sudo apt-get install python3.10 
- $ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.10 1
- $ sudo ln -f /usr/bin/python3.10 /usr/bin/python3

# Check Python version
- $ python3 --version (it should be 3.10.# )


note: The packages provided here are loosely based on the debian upstream packages with some modifications to make them more usable as non-default pythons 
and on ubuntu.  As such, the packages follow debian's patterns and often do not include a full python distribution with just `apt install python#.#`.  
Here is a list of packages that may be useful along with the default install:

- `python#.#-dev`: includes development headers for building C extensions
- `python#.#-venv`: provides the standard library `venv` module
- `python#.#-distutils`: provides the standard library `distutils` module
- `python#.#-lib2to3`: provides the `2to3-#.#` utility as well as the standard library `lib2to3` module
- `python#.#-gdbm`: provides the standard library `dbm.gnu` module
- `python#.#-tk`: provides the standard library `tkinter` module

Ex: sudo apt-get install python3.10-distutils

# Setuptools & Pip

- $ sudo apt-get install python3-pip -y 
- $ sudo python3 -m pip install --upgrade pip 

# Note: If you are getting error while installing pip use this method
- $ curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10
- $ python3 -m pip install --upgrade pip


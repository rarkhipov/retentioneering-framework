# Installation

## C++ compiler

Fistly you need to download c++ compiler

### Mac

Install [homebrew](https://brew.sh/)

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Then you should install gcc

```bash
brew install gcc
```

You also need python if you haven't it

```bash
brew install python3
```

And git

```bash
brew install git
```

### Windows

Install [Microsoft Visual Studio Build tools](https://visualstudio.microsoft.com/ru/downloads/). You can find it at `Инструменты для Visual Studio 2017 > Build Tools для Visual Studio 2017`.

If you need python then install it from [here](https://www.python.org/downloads/release/python-368/). Please, be sure that you select `Add python to path` in the bottom of installer.

And git from [here](https://git-scm.com/downloads).

## Python package

- To install Python package from github, you need to clone that repository
```bash
git clone https://github.com/appintheair/aita-ml-retentioneering-python.git
```
- Install dependencies from requirements.txt file from that directory
```bash 
pip install -r requirements.txt --user
```
or if previous command don't work
```bash 
pip3 install -r requirements.txt --user
```
- Then just run the setup.py file from that directory
```bash
python setup.py install --user
```
or if previous command don't work
```bash
python3 setup.py install --user
```

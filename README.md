# PySpark on Apple Silicon

This quick tutorial will guide how to install and simple use PySpark on apple silicon architecture.

## Install Homebrew

Installation instructions at: <https://brew.sh/>

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Set brew to path:

```shell
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Check latest installed version:

```shell
brew --version
```

Update homebrew:

```shell
brew update
brew upgrade
```

## Install Java

Reference: <https://medium.com/@kirebyte/using-homebrew-to-install-java-jdk11-on-macos-2021-4a90aa276f1c>

For java 11 install, run:

```shell
brew install java11
```

Symlink it and add to PATH:

```shell
sudo ln -sfn /usr/local/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
echo 'export PATH="/opt/homebrew/opt/openjdk@11/bin:$PATH"' >> ~/.zshrc
```

Test it out

```shell
java --version
```

## Install Python (pyenv and virtualenv)

### Python

Check existing installation

```sh
python --version
# or
python3 --version
```

Install Python, if not there yet

```sh
brew install python
```

### PYENV

In order to work with other python versions, setup pyenv to choose a specific version.

Reference: <https://laict.medium.com/install-python-on-macos-11-m1-apple-silicon-using-pyenv-12e0729427a9>

```sh
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
cd ~/.pyenv && src/configure && make -C src
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
pyenv --version
pyenv install -l | grep 3.9
pyenv install 3.9.15
pyenv versions
```

### VIRTUALENV

Python virtual environment allows to have specific project dependencies for proper behavior.

Reference: <https://rogulski.it/blog/python-virtualenv-management/>

```shell
brew install pyenv-virtualenv
```

Initiate a virtual environment in a specific version

```shell
pyenv virtualenv 3.10.8 test-venv-3.10.8
```

Activate a specific environment

```shell
pyenv activate test-venv-3.10.8
```

Activate a current active environment

```shell
pyenv deactivate
```

List all virtual environments

```shell
pyenv virtualenvs
```

Drop specific virtual environment

```shell
pyenv virtualenv-delete test-venv-3.10.8
```

## Install PySpark

Install spark with Python API

Reference: <https://sparkbyexamples.com/pyspark/how-to-install-pyspark-on-mac/>

```shell
brew install apache-spark
```

Initialize pyspark shell

```shell
pyspark
```

## Validate Installation

```python
data = [("Java", "20000"), ("Python", "100000"), ("Scala", "3000")]
df = spark.createDataFrame(data)
df.show()
exit()
```

On <http://localhost:4040> check the job status.

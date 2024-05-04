---
title: "Install pyenv"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
![Ansible](/images/snake.jpg)

 Install Python environment with pyenv

[Install python - Realpython](Pythonhttps://realpython.com/intro-to-pyenv/)

**How to install pyenv on RHEL9**

**Install rpms**
```
$ sudo dnf install -y \
        make \
        gcc \
        zlib-devel \
        bzip2 \
        bzip2-devel \
        readline-devel \
        sqlite \
        sqlite-devel \
        openssl-devel \
        tk-devel \
        libffi-devel \
        git
```

**Start installer**
```
$ curl https://pyenv.run | bash
```

**Adjust .bashrc**


```
# Python pyenv
# Load pyenv automatically by appending
# Load pyenv automatically by appending
# the following to
# ~/.bash_profile if it exists, otherwise ~/.profile (for login shells)
# and ~/.bashrc (for interactive shells) :

export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"

# Load pyenv-virtualenv automatically by adding
# the following to ~/.bashrc:

eval "$(pyenv virtualenv-init -)" 
```  

**Testen:**
```
$ pyenv

$ pyenv install 3.7.6
$ pyenv shell 3.7.6
$ python --version 
$ pip3.7 install --upgrade pip 
```

{{< button relref="/" >}}Go Home{{< /button >}}
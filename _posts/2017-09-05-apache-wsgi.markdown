---
title: apacheでwsgiの構築
layout: post
date: 2017-09-05 11:36:15
category: Web
tags: [apache, python, wsgi]
---

## wsgiは?

pythonのウェブアプリケーションを動かすApacheのモジュールである。

## 準備

```
$ yum groupinstall -y "Development tools"
$ yum install -y zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel
```

## pyenv のインストール


[https://github.com/pyenv/pyenv](https://github.com/pyenv/pyenv)

## pythonのインストール 

`--enable-shared`　を付けないとwsgi をコンパイル出来ない。

```bash
$ env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 3.5.0

#　場所は他でもいい

$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
```




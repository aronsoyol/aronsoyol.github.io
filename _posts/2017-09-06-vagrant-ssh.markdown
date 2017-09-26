---
title: Vagrantでssh公開鍵を登録
layout: post
tags: [ssh, vagrant]
---

## 1. 問題
vagrantのゲストOSのCentos6のpublic networkを設定し、他のPCからsshでログインしようとした。自分の常用の公開鍵でログインできるといいな。

## 2. ssh 公開鍵の登録

ゲストOSの`~/.ssh/authorized_keys`ファイルに自分の公開鍵を追加

## 3. 新しい問題発見

公開鍵のパスワードを知らなくてもゲストOSのユーザパスワードでログイン出来ちゃう、それならSSHでやる意味がない。


```
[user@HostOS]$ ssh -2 vagrant@192.168.0.14
[user@HostOS]$ Enter passphrase for key '/Users/aron/.ssh/id_rsa':
[user@HostOS]$ vagrant@192.168.0.14\'s password:
[user@HostOS]$ Last login: Wed Sep  6 09:26:17 2017 from 192.168.0.9
[vagrant@localhost ~]$ログイン出来ちゃったけど嬉しくないよ！
```

## 4. ゲストOSのユーザパスワードでログインを禁止する方法

`/etc/ssh/sshd_config`の66行の
`PasswordAuthentication yes`を
`PasswordAuthentication no` に変えて

```
sudo service sshd restart
```
して、再びログイン

```
ssh -2 vagrant@192.168.0.14
Enter passphrase for key '/Users/aron/.ssh/id_rsa':
Permission denied (publickey).
```

今度はssh秘密鍵のパスワードが間違ったら、ログイン出来なくなった。




以上！




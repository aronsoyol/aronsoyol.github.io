---
title: Vagrant boxが立ち上がらない件
layout: post
date: 2017-11-17
tag: [windows, docker, hyper-v, vagrant, "virtual box"]
---

今日Windowsを再起動したらVagrantBox が立ち上がらなくなった。色々いじってみたけど、やはり駄目。


DockerでHyper-V を有効にした覚えがあってDockeを止めて,更にHyper-V managerからHyper-Vをストップさせたけど、やはり駄目でした。

続けて調べたら、Windowsの機能添削パネルからHyper-Vをアンインストールすればいいという記事を読んで、試してみたら無事立ち上がりました。

めでたし、めでたし...
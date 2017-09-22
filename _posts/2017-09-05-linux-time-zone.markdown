---
title: Linuxのタイムゾーンの変更
layout: post
category: Linux
date: 2017-09-05
tags: [date, time, linux, server]
---

### オリジナルをバックアップ
`cp /etc/localtime /etc/localtime.org`

### タイムゾーンファイルの変更
`ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime`
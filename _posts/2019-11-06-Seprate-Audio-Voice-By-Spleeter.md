---
layout: post
title: 分离歌曲音频中的人声和背景音乐
date: 2019-11-06
tags: 工具
music-id: 536622304
---

*  目录
{:toc}

# 从一首歌中分离人声和BGM(背景音乐)
> 6

![Spleeter](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/img/spleeter_logo.png)

## 介绍

想要K歌却苦于找不到喜欢的音乐的纯BGM？想要去除歌曲中的各种乐器的背景音乐，来个清唱版？不如试试这个开源项目吧

来自法国的音乐流媒体公司 Deezer 开源了一个音轨分离软件 spleeter，只需输入一段命令就可以将音乐的人声和各种乐器声分离，支持 mp3、wav、ogg 等常见音频格式。

这款软件基于 TensorFlow 开发，效果拔群，有网友说自己曾经试过无数类似软件，spleeter 是最好用的一个。

我在配置好环境后，测试了一下，效果拔群，几乎是我使用过的最好的分离人声和消除背景音的工具。我使用的测试歌曲是米津玄师的《Lemon》

点击蓝字播放↓
转换前：[原声](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/audio/Lemon-%E7%B1%B3%E6%B4%A5%E7%8E%84%E5%B8%88.mp3)
转换后的人声部分：[人声MP3](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/audio/vocals.mp3)
转换后的背景音乐部分：[背景音MP3](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/audio/accompaniment.mp3)

虽然网页上的音频经过了压缩，音质不太好，但是可以很明显的感受到，分离的效果是非常明显的，人声的音频几乎听不到BGM了，BGM的音频也只能听到一点点的不和谐。

spleeter 还支持 GPU 加速。如果在 GPU 上运行，会比实时分解速度快 100 倍，也就是说分解一首 5 分钟的歌曲只需要 3 秒。即使是使用CPU，分解这样一首4分钟的音频，也只用了不到1分钟的时间，个人使用上来说过绝对足够了。

GitHub项目地址：[Spleeter人声分离](https://github.com/deezer/spleeter)

# 使用方法
## 环境配置
**操作系统**： Mac OS / Windows / Linux
**Python**： Version3.7 / Version 2.7
**Conda**： Miniconda

## 步骤
1. 安装Conda环境
2. 从GitHub上Clone项目到本地
3. 使用Conda命令运行Spleeter完成人声音频分离


## 详细安装步骤
> 这里只以MacOS为例，Windows的步骤大同小异，有问题可以留言。

1. 在Conda的官网上下载自己计算机对应版本的Conda安装程序，或者包管理器进行安装，Conda官网地址点击这里[Conda](https://docs.conda.io/en/latest/conda.html)，或者点击这里的下载页进行下载：[Miniconda下载地址](https://docs.conda.io/en/latest/miniconda.html)

    如下图，点击蓝字进行下载，32位的系统就下载32位的，64位的就下载64位的，Mac OS系统的直接下载.pkg文件就行。由于是国外的官网，可能下载会中断，耐心多下载几次即可，是在无法下载的可以在本文下面留言邮箱地址，我看到会把安装包发到你的邮箱📮里。
![](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/img/20191106193236.png)

2. 下载完成后，点击安装
![](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/img/20191106193303.png)
    如果遇到未信任的程序，无法安装，请到系统偏好设置->安全与隐私->允许从以下位置下载应用勾选AppStore和被认可的开发者
![](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/img/20191106193211.png)

1. 安装完成后，打开命令行工具iTerm，在命令行中输入：conda -V,如果输出不是command not found，那么Conda环境就安装成功了
![](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/img/20191106194445.png)

1. 如果本机有git，那么直接输入
    `git clone https://github.com/deezer/spleeter`
    克隆git仓库到本地，没有安装git的话点击：[Spleeter人声分离](https://github.com/deezer/spleeter)，点击DownloadZIP，下载到本地
    ![](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/img/20191106194708.png)

5.进入项目所在的文件夹，打开命令行，在命令行中输入命令：
    `conda env create -f spleeter/conda/spleeter-cpu.yaml`
    按回车后，再输入命令
    `conda activate spleeter-cpu`
    

如果想换成 GPU 环境，只需将上述代码中的 spleeter-cpu 换成 spleeter-gpu。

最后再输入：
`spleeter separate -i audio_example.mp3 -o audio_output -p spleeter:4stems`

在分离音轨的命令中，加入选项 - p spleeter:4stems 来指定音轨数量，如果不加，系统默认分离为 2 个音轨。

最终乐器和人声将以 wav 文件的格式保存在 audio_output 文件夹中。
分离过程可以在 GPU 或 CPU 上执行。在 GPU 上运行，速度非常快，可以实现 100 倍的加速。
![](https://es-blogimg.oss-cn-hangzhou.aliyuncs.com/img/20191106195126.png)
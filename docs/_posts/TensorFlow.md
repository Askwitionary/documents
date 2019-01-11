---
title: Tensorflow Related
---

# 基本介绍 

简单介绍一下TensorFlow（TF）以及其安装。以防以后的小朋友掉进坑里。
## 什么是TF 
* TF其实是个处理数学模型的包包。要理解Tensor可以从矩阵的角度出发。简单来说，矩阵是二维向量组成的方块，tensor是n维向量组成的“多维体”
* 矩阵都属于Tensor，而Tensor不一定都是向量
* Flow顾名思义，就是流动，摇摆，TF就是对tensor这种数据结构进行快速处理的一套工具，让他们一起“摇摆”。
## 为什么用TF 
* AI离不开机器学习，而机器学习离不开处理大量的数据。TF提供了一个可以大大提高运算效率的平台。没错，java和C++粉们估计要撇嘴了：你Python一个script language凭什么跟我们说运算效率？对，Python作为一个一行一行执行的语言确实很慢，但是TF之所以效率高和Python其实没有太大关系。我们在利用TF解决问题时，也并没有在用Python去做实际的运算。简单来说，我们只利用Python代码来告诉TF我们要解决的问题整体是什么样的（包括输入数据是什么，用什么模型，如果是DNN那么要用多少hidden layers等等等等）。等到我们把一个问题完完整整地描述完了，TF再把这一整个问题带去后台运算，最后给出一个结果。
* 由于上述原因，Google的程序猿就开发了这个开源平台，很多别的程序猿也为这个平台做了很多贡献，做了许多机器学习的模型。我们可以直接拿来，或者做一定的修改之后使用。
## 如何安装TF 
* 首先推荐使用Linux系统。TF对windows的支持还是更新得比较慢的。Google官方支持的模型比较有限，如果想使用GitHub上别的大神做好的模型的话，最安全的方法就是使用Linux系统。而且Linux系统在使用服务器进行运算的过程有很多便利。
* 安装过程Windows和Linux差不多。由于有时候要使用非官方的模型，而新版本的TF可能会不支持GitHub大神几年前写的代码，所以我们就经常需要安装多个TF版本。要实现这个最好就是使用Anaconda创建虚拟环境。
* [点这里下载Anaconda](https://www.anaconda.com/download/#windows)，下载完成后[点开这里](https://www.tensorflow.org/install/)
### Windows用户请看这里： 


* 安装完Anaconda后，请重启电脑。然后打开Anaconda Prompt，按照TF网上的教程“Installing with Anaconda”进行前三步

* 这时你应该已经在你刚刚创建的环境里了，这时不要输入官网给的命令，因为他们的服务器我们用起来很慢。CPU版本用这个：

    ```bash
    - pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ tensorflow
    ```

* GPU版本用这个：

    ```bash
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ tensorflow-gpu
    ```

    + 如果需要安装不同的版本，则在上述链接后加上“==1.X.X”（你需要的版本号）

* 大功告成。建议同时安装pandas，处理数据很可能会用到。命令和上述一样，把最后的tensorflow改成pandas就行了

* 多啰嗦一句，'''真的真的用Linux或者Mac吧。'''Mac请自己排雷，Linux目前用来最舒服。如果你看这篇wiki已经过了很久，windows支持已经做得很好了，那么当我没说。

### Linux用户请看这里： 

* Linux版本不是特别重要，别太低了就行。请在做任何事之前先把驱动啥的弄好。我用的是时下最新的Ubuntu 18.04
* 同样下载安装Anaconda，（将conda加入到path）完成之后重启电脑。
* 这时打开terminal，输入conda回车，应该不会报错了。
* '''cd到你想要安装环境的directory！！！'''与Windows的Anaconda不同，Linux不会自动把环境装到Conda文件夹里。我没做这一步最后home目录下一堆隐藏文件夹乱七八糟的。不是强迫症的当我没说。
    * 与windows不同， Linux不会自动给你选环境安装在哪里。而且安装环境的文件夹默认是隐藏的。需要显示隐藏文件才能看到。
* 跟着官网Ubuntu选项卡下面“Installing with Anaconda”安装。如果官网给的链接慢，也可以使用上述清华的镜像安装。
* 别忘了安装pandas，大功告成！
    * 安装完成之后，可以把官网给的“Hello World”的代码粘下来跑一跑，如果没有报错，就说明你已经安装成功TF并且打开了“新世界”的大门了
## 如何使用TF 
这个比较需要分类讨论。以后慢慢说。
（未完待续）

# PyCharm Remote Intepreter
好了介绍了半天TF是什么以及如何使用，我们来讨论一个比较实际的问题。那就是不管我再怎么吹TF的效率高，在处理实际问题时，尤其在训练时，我们自己炫酷的超薄笔记本的配置还是会大大影响训练时间的。肿么办！
好在Pycharm可以使用远程Interpreter，这样我们就可以把我们的代码deploy到服务器上，然后用服务器肥硕的配置来跑我们的程序了。这样我们的炫酷小本其实就只是个文档编辑器加显示器了。
其实现在我就在使用TF的CNN模型跑一个图像识别的训练，本机CPU稳定在10%以下，网络使用几乎为0。在创建模型时完全不影响我做别的事情。而服务器那边忙得不亦乐乎：40个核开了82个任务，332个进程。
废话不多说，我们来说说干货。

* 首先之前，请确认将Ubuntu apt-get的国内源添加进去
    * [请参考本文，源链接也在这里](https://askwitionary.github.io/ubuntu_related/#Ubuntu-18-04-Desktop-gt-Server)

    * 打开terminal

    * 安装文本编辑器，随便选**一个**

      ```bash
      apt-get install vim
      apt-get install vi
      ```

    * cd到存放源地址文件的目录

      ```bash
      cd /etc/apt
      ```

    * 修改source.list文件

      ```bash
      vim sources.list
      ```

    * 按`a`进入`insert mode`， 找到光标到文件最前端，回车出两个个空行，然后将上述链接中的源链接复制到文件最前面。我用的是阿里源。复制好了之后按Esc建进入command mode，输入

      ```
      :wq
      ```

    * 写入并退出，大工告成

* 首先你需要一个配置好的服务器。我这里的服务器上跑的是Ubuntu 16.04。今后会用18.04吧，改进还是很多的。相信支持很快能做好。服务器上需要安装ssh

    ```bash
    apt-get update
    apt-get install sshd
    ```

* 我拿到这个服务器的时候这些基本的都已经装好了，我自己没有从头配置过。但是考虑到其实当时服务器也很干净，我猜测很多东西Ubuntu都自带了。

* 装好后在本地测试一下是不是能通过ssh链接到这个服务器：
    * ssh root@<server IP>
    * 这里先测试一下，能连上就可以了。正常使用推荐先创建一个用户,后面详细说

* 下一步在服务器是更新pip/pip3，准备安装需要的包包。这一步在root下就好，省事。

    ```bash
    pip install --upgrade pip
    pip3 install --upgrade pip
    ```

* 现在pip最新版本是18.装好了之后就要安装你需要的包包了，这里只拿tensorflow为例

    ```bash
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ tensorflow
    pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple/ tensorflow
    ```

    * 这样默认安装最新版，需要以前版本的话请参照上文描述执行命令。

* 一切安装好后，下一步请创建一个新的用户，在root下输入
    * `adduser <username>`
    * 跟着提示输入两遍密码。建议弄个短一点的，以后会经常输入
    * 然后系统会让你确认一下各种乱七八糟的信息，没问题的话跟系统确认一下，用户就创建好了

* 下一步就是在本地配置Pycharm了
    * 安装，打开Pycharm
    * `File -> Settings -> Project: ''<YOUR_PROJECT_NAME>'' -> Project Interpreter`
    * 找到右上的小齿轮按钮，点开，选择`add...`
    * 在弹出的对话框选择`SSH Interpreter`
    * 填写你服务器的IP地址，选择端口，填写刚才创建的用户名，点击下一步
    * 填写密码并勾选记住密码，下一步
    * 选择Interpreter，一般放在你用户文件夹的bin目录下，有时候系统会既有Python2还有Python3，建议点开旁边的`...`手动选择
      `/usr/bin/Python3.6`
    * 选择Sync Folder，这个文件夹就是你本地的文件会被同步到服务器的什么文件夹，默认的是在root下的tmp。你也可以改到你自己的用户文件夹下。做一个负责任的人，请保管好你的代码，别弄得机器里哪都是 ：）
    * 勾选自动上传文件，选上方便点，其实也不是实时的。所以不建议使用远程服务器做测试。会很麻烦。
    * 点击完成，大功告成！现在Pycharm会自动扫描这个系统下已经安装的包包，确认你能找到我们刚才装的tensorflow和tensorboard，应该就没啥问题啦！
    * 依旧在Settings里，找到`Build, Execution, Deployment`，点小三角打开下拉菜单，点`Options`
    * 找到`Create empty directories`，勾选，点击`Apply`，然后`OK`
    * 如果Pycharm没有自动开始上传你的project，可以点击`Tools -> Deployment -> Upload to <Your Server>`
    * 写个Hello World试试吧！记得刚刚更新的文件不会马上上传到服务器，新更新后要立即运行记得手动上传一次。

# 关于Docker 

大多数情况下，服务器要用来做很多事情，所以直接用服务器做自己的Interpreter还是很不科学的。万一不小心把服务器玩坏了，重装一下系统，别人的东西也跟着没了，别人一定会把你举高高再用小拳拳教你用Docker的。
使用Docker确实会增加些许麻烦，毕竟为了Docker本身的轻便，配置Docker的时候你需要告诉系统你都需要什么样的依赖包，这样Docker会为你利用各个包的镜像帮你创建一个容器。好处是这样你的程序就相当于机器的一个进程了，不会影响到别的程序。如果你的程序不小心嗝屁了，你可以直接把这个容器干掉，从而完全不会影响别的程序。
好啦，搞起来吧，首先安装Docker
[教程点这里](https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository)
具体的可以以后有机会详细说，这里现介绍一下常用的命令，Docker基本都需要sudo权限

```bash
sudo docker ps		# 查看所有正在运行的Docker列表
sudo docker ps -a	# 查看所有（包括已结束、退出、报错）的Docker列表
sudo docker pull ubuntu:16.04	# 下载镜像，例如ubuntu:16.04
sudo docker build -t ''<Your image tag>'' .		# 注意最后的空格点儿" ."
sudo docker run -d -p <port inside docker>:<server port> <image tag>	# # 这个例子是创建一个API服务的例子
sudo docker run –it –p 8022:22 ubuntu:16.04		# 这个例子是创建一个bin/bash命令行的例子
```

前面一个端口号是映射到容器的端口号，通过这个端口号进入容器；后面一个端口号是服务器的端口号，本地机器通过这个端口号进入服务器。把这两个端口号连在一起可以直接连入容器。

[参见这里](https://docs.docker.com/v17.12/edge/engine/reference/commandline/build/#use-a-dockerignore-file)	Docker ignore file

[参见这里](https://docs.docker.com/v17.12/edge/engine/reference/commandline/run/)	Docker run

参考：
* [Docker深度学习环境篇第二弹：PyCharm + Docker + GPUs](https://zhuanlan.zhihu.com/p/27114995)
* [Faster writing and testing machine learning applications.](http://www.pinchofintelligence.com/faster-writing-and-testing-machine-learning-applications/)
* [Remote Python Debug to Docker Container over Ssh by using PyCharm](https://medium.com/@furkanpur/remote-python-debug-to-docker-container-over-ssh-by-using-pycharm-44a9b6e82206)
* [PyCharm远程调试Tensorflow](https://www.tuicool.com/articles/feUJZbI)
* [一步步从零开始：使用PyCharm和SSH搭建远程TensorFlow开发环境](http://www.sohu.com/a/129277803_465975)
* [Docker: Using Docker as a Remote Interpreter](https://www.jetbrains.com/help/pycharm/using-docker-as-a-remote-interpreter.html)
* [PyCharmでの開発でDockerを使う](https://www.rhoboro.com/2017/01/21/pycharm-docker.html)
* [Work remotely with PyCharm, TensorFlow and SSH](https://medium.com/@erikhallstrm/work-remotely-with-pycharm-tensorflow-and-ssh-c60564be862d)

## Docker 
* 不同版本镜像：https://hub.docker.com/r/tensorflow/tensorflow/tags/

# 教程 
## 安装 
* [在 Ubuntu 上安装 TensorFlow](https://www.tensorflow.org/install/install_linux?hl=zh-cn#InstallingDocker)
## 使用 
* [A beginner introduction to TensorFlow (Part-1)](https://towardsdatascience.com/a-beginner-introduction-to-tensorflow-part-1-6d139e038278)
* [Simple Reinforcement Learning with Tensorflow Part 0: Q-Learning with Tables and Neural Networks](https://medium.com/emergent-future/simple-reinforcement-learning-with-tensorflow-part-0-q-learning-with-tables-and-neural-networks-d195264329d0)
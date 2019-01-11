---
title: Setting up Your Coding Environment
---
<br>

说在前面
======

**写代码是一个基于英文语言环境的活儿。从今天开始，凡是与代码相关的，如编译器、环境、文档中与代码相关的内容，请尽量使用英文，以给自己创造这个语言环境**

<br>

**开始会是一个非常艰难的过程，坚持3个月回望，一定会看到不一样**

<br>

Anaconda
======

Installation
------
+ Download the installer
  + For Windows:
  Go to https://www.anaconda.com/download/#windows
  + For Linux:
  Go to https://www.anaconda.com/download/#linux
  (To be Continued)
  + For Max OS:
  Go to https://www.anaconda.com/download/#macos
  <br>
  + Download Anaconda 5.3.1 (as of Dec. 12th 2018) 64-bit version for **Python 3.7**
  + It should be a single file of roughly 630 to 640 megabytes

### Windows Users

+ Run the installer once the download is finished
+ Click on "Next" until you are asked "Install for:", then pick "All Users"
+ It is recommended to install your Anaconda on your **system disk**, namely **disk C** if your are using Windows
+ Go with the default setup for the rest of configurations
+ **Do not install MS VSCode**

### Linux(Ubuntu) Users

+ Locate the file you have downloaded

+ **Right Click** the downloaded file and select `Properties`

+ Select `Permissions` tab and make sure to check `Allow Executing file as program`

+ Open up a terminal at the directory of your downloaded file

+ run the `.sh` file

  ```bash
  ./Anaconda3-2018.12-Linux-x86_64.sh			# Note that file name could be different
  ```

+ Follow the the installation steps and you will be good
+ Make sure you choose `Yes` when the installer ask you whether to **add Anaconda to the PATH** or not. Otherwise you will need to add it manually for Anaconda to work
  + To add it manually, use your favorite text editor and edit `sudo vim ~/.bashrc`
  + Add the line `export PATH="~/anaconda3/bin:$PATH"`
  + Save the file and exit
+ **Remember not to install MS VSCode unless you really use it**
+ You might need to restart or refresh path to make `conda` work in command line

## Setting up a Basic Python 3.6 Env

+ Find "Anaconda Prompt" in your Start menu and **open it as administrator**

+ Type in `conda --version` to check if your version is 4.5.11

  + If not, execute `conda update conda` to update your anaconda

+ Create your very first conda environment by executing

  ```bash
  conda create --name <env_name> python=3.x
  ```

+ Replace `<env_name>` with environment name and `x` with specific python version you want

+ The following is a simple example

  ```bash
  conda create --name happy python=3.6
  ```

+ Go ahead and type `y` to confirm creating the environment

+ Now conda should be downloading required packages for you automatically

+ When it is finished, you can type `conda activate happy` to activate your environment

+ Now you should see the environment name at the front of line has been changed from `(base)` to `(happy)` 

+ If you want to make sure it is truly working without any problem, you can try to follow the steps below within your environment "happy"

  + Checking python version

    ```bash
    python -V
    ```

    + Make sure you get something like `Python 3.6.7 :: Anaconda, Inc.`

  + Run a simple "Hello World" in Python

    + Execute `python` and wait for the line header to be something like `>>>`

    ```python
    print("Hello World, mi amigo!")
    ```

    + Make sure it is printing the string you entered correctly without any errors
    + BTW mi amigo 是我的朋友的意思

  + Type `exit()` to exit to command line prompt of your environment

+ Now you can deactivate your environment by executing

  ```bash
  conda deactivate
  ```

+ Now you should see the environment name at the front of line has been changed from `(happy)` back to `(base)` 

+ **It is the best to create a separate environment for each project unless multiple projects are using exactly the same packages. Many packages has conflicts and some packages may cause unstable issues. There are even more reasons why we need to make "small rooms" for each of our projects, but there is no good to explain it in detail here (我也说不清楚哈哈). This is why Python scripts are mostly deployed within a "container" using docker**， which we will talk about in the future.



<br>

Pycharm
======
Installation
------
+ 请使用英文版请使用英文版请使用英文版！！！
  + 未来看文档大多都会是英文版的。慢慢开始熟悉，别图一时之快以后天天郁闷。
+ Download the installer
  + For Windows:
  Go to https://www.jetbrains.com/pycharm/download/#section=windows
  + For Linux:
  Go to https://www.jetbrains.com/pycharm/download/#section=linux
  + For Max OS:
  Go to https://www.jetbrains.com/pycharm/download/#section=mac
  <br>
  + Download **Pycharm Professional 64-bit version**
+ Run the installer once the download is finished
+ Click on "Next" until you are asked where you want your Pycharm to be installed
+ You do not need to install your Pycharm on your system disk
+ Click on "Next" and choose "64-bit launcher" to be created on your desktop
+ Go with the default setup for the rest of configurations

## First time running Pycharm

+ Run Pycharm after it is completely installed
+ Choose "Do not import settings" if you are first time using Pycharm
+ Accept everything and continue
+ The next step does not matter, choose whatever you what. Personally I prefer to go with not sending them usage statistics because I think my coding style is too dumb and I feel ashamed to let others know how I code.
+ Choose your color theme
+ Activate your Pycharm
  + Now Pycharm should be asking you to activate the product
  + Go to http://idea.lanyus.com/
    + **Windows:** Go to `C:\Windows\System32\drivers\etc` on your system and open file named `hosts` with your favorite text editor like Notepad++ as administrator
    + **Linux:** `sudo vim /etc/hosts`
  + At the very end of the file, insert a new line with `0.0.0.0 account.jetbrains.com`
  + Save and exit
  + Click on "获得注册码"
  + Copy your key
  + Go back to Pycharm and choose "activation key" and paste your key below
  + Now your Pycharm should be **illegally activated** 
    + 这么注册当然是非法的啦，但是中国人的智慧不用白不用，不然这软件也太贵了=-=

## Create your first project

+ Choose "+ Create New Project"

+ Choose "Pure Python" from the left

+ Change your project location at the top to be something like `D:\PycharmProjects\test` 

  + Note that you do not need to put your scripts in your system directory
  + It is better to use `PycharmProjects` folder to keep all your projects organized

+ Change your project name from "untitled" to "test", or any other name you prefer in the future. For now for simplicity, let's just use "test"

+ Click on the little triangle right below "Location"

+ Choose "Existing interpreter". Now we need to tell Pycharm to use the python interpreter we created inside our environment "happy"

+ Click on "..." button, a window titled "Add Python Interpreter" will pop up

+ Choose "Conda Environment

+ Locate where your python is inside your environment. For me it is located at `C:\ProgramData\Anaconda3\envs\happy\python.exe`

  + Note that you may need to show hidden files to see the folders

  + If you cannot find your python.exe, follow the steps below

    + Open up your Anaconda prompt like we mentioned above

    + Activate our environment like we mentioned above

    + Execute `where python` after you see your line header to be `(happy)`

      ```bash
      C:\ProgramData\Anaconda3\envs\happy\python.exe
      C:\ProgramData\Anaconda3\python.exe
      ```

    + Use the first path to find your python.exe

+ Now confirm you have chosen the right interpreter, then you should be able to click on "create"

+ You should be able to find a folder icon on the left named "test". Right click on it and choose "New" then "Python File"

+ Name your new Python file "hello" and click "OK"

+ Now you should be able to see hello.py

+ Type in the following python code

  ```python
  print("Hello, 很棒，你已经完成了Python环境和编译器的配置")
  ```

+ Right click the blank screen and select "Run 'hello'"

+ You should be able to see a string at the bottom in the "Run" subwindow

### Linux Users (Important)

Once inside Pycharm, Click on `Tools`, and click on `Create Desktop Entry` to create an icon for Pycharm so that we won't need to use command line to launch Pycharm everytime

<br>

Using `pip`, a python package manager
======

Python is famous for a lot of things. One of the most important aspect is that it has a pretty good package management tool. 

<br>

Check if you already have `pip` installed
------
+ Execute the following command **inside your environment**
```bash
(happy) lduan@lduan-G750JHA:~$ pip -V		# Just to show that you need to run the command within your environment
pip -V										# This is the actual command
```
+ You should get something that looks like (Note that if your are using windows, the start of the path should be different)

  ```bash
  pip 18.1 from /home/lduan/anaconda3/envs/happy/lib/python3.6/site-packages/pip (python 3.6)
  ```



  + If you have pip version lower than 18.1 (as of 2018.12) you can consider upgrade it (not important if it is not too far behind)
  ```bash
  pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ -U pip
  ```


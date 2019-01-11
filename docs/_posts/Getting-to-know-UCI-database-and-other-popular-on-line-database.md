---
title: Getting to know UCI database and other popular on-line database
---

<br>

那么我们唠叨了这（就）么（一）多（个）基础模型，如何付诸实践呢？

* 美国加州大学尔湾分校([https://uci.edu UCI])为我们提供了海量免费数据库供我们实验使用。没错，尔湾分校（UCI: University of California, Irvine. AKA: University of (RICH) Chinese Immigrants）不仅以中国富二代留学生多而著名，他们对机器学习的研究也是全球最早的几个。
  + [http://archive.ics.uci.edu/ml/datasets.html 点这里]可以带你进入数据的海洋。
    [[文件:UciMain.png|缩略图|点击看大图]]
    * 左边的一列是数据库根据行业/学科的分组
    * 中间那些个大大的就是实际的数据库了
    * 右上搜索条可以根据关键字搜索数据库
    * 在这里能看到一些数据库的重要基本信息方便我们选择
      * Name：名字
      * Data Types：数据类型（单变量、多变量、文字、图像等）
      * Default Task：默认任务类型（分类、分组、回归等）
      * Attribute Type：特征类型（整数、实数、分组（男、女）等）
      * #Instances：（数据量）
      * #Attributes：（特征量）

* 简单实例：信用批准问题（Credit Approval）。
  * 我们知道，美国个人中小额贷款大多为信用贷款而非抵押贷款。那么“信用”该如何量化，对于不同的人该如何确定是否批准他的信用贷款呢？
    * 请点击：[http://archive.ics.uci.edu/ml/datasets/Credit+Approval Credit Approval]： 
      [[文件:CreditApproval.png|缩略图|点击看大图]]
    * 这里我们最需要关注的就是最上面的两个按钮和那个小图表了
    * Data Folder：点开进入下载页面，这里面就是实际的数据库和可能有的说明文件
    * Data Description：解释数据的详细信息，如每个特征的可能变量和具体代表
    * 小图表中包含了更详细的数据库的详细信息。
    * 确定了一个要用的数据库，我们就可以在Data Folder里下载，整理（清理）并使用啦！

总得来说这些数据在初级阶段实验各种模型还是很有用的。有一个对某个数据库来说看起来美好的模型，我们在抓取数据的时候也可以以这个“某个数据库”为蓝本做工作。

还有很多别的提供数据库的网站，这里不一一赘述了。贴一个连接抛砖引玉：[https://www.kaggle.com/ 近几年很火的网站Kaggle]
---
title: Tasks
---

<br>

# 写在前面的

- **学英语、算法以及代码都是一个缓慢的过程。如果任何时候你感觉时间不够，节奏不对，或者身体不适，虎躯一震，我们可以放慢脚步。但是请千万不要糊弄，耽误大家的时间和精力**
  - 10个小时的活只有好好干10个小时才能获得10分收获
  - 10个小时的活急急忙忙干3个小时，保证转天就忘
  - 做强逻辑性的活儿千万不要死背，死记任何东西。尽量去理解，去梳理逻辑，自然而然就记住了。我们最后的目的不是点亮技能说我会多少多少种模型算法，而是遇到一个实际问题你能想到几个可能可以用的模型，并且知道其基本逻辑以及应该去哪里找相关的文献
- **如果需要帮助在下能帮得上的肯定知无不言，千万不要羞涩**
- **如果有任何typo，语法错误请不吝赐教，我会尽快更正 ：）**

<br>

# Task 0: Setting up your coding environment

If you haven't already done so, please refer to [this post](https://askwitionary.github.io/python_environment/). And check if you have done the same. Make sure you have a separate new environment each time you develop a project

# Task 1: Basic data cleanup

Dec. 11th 2018

那我们就直接上手吧~这有个[网上开放数据库](https://askwitionary.github.io/2018/12/13/Getting-to-know-UCI-database-and-other-popular-on-line-database/)的介绍。你们可以去看看，然后就用里面提到的那个数据库，下载下来，写一个方法。

## Making data machine readable

+ Input: crx.data file

+ Output: A **2-D list**

  + It should look like 

    ```python
    >>> output
    [[data_0], [data_1], [data_2], ...]
    ```

  + Individual data example

    ```python
    >>> data_[0]
    ['b', 30.83, 0, 'u', 'g', 'w', 'v', 1.25, 't', 't', '01', 'f', 'g', '00202', 0, '+']
    ```

+ Mind the data types. Do not make all of them string. 

+ For now we will use pure python. We will try to improve our code when we are handling larger scale of data.

## Skim through other datasets

The task above should be relatively simple. If you should have more time, you can go deeper into the dataset website. Try to look for interesting data and compare differences of datasets that are by default used for different purposes, i.e., regression, classification and so on. 

多看看别的数据，比较一下常用于分类、回归等问题的数据有什么样的区别。

# Task 2: Implementing helper functions

Dec. 18th 2018

## Before you do anything

It is important for you to at least have a rough idea of what kind of data you are dealing with. For instance, if you have read through all the files in the data folder and the description on the website, you should at least know that: 

+ This dataset consists of 690 credit card applicants' personal information and whether or not they are approved for the credit card. 
+ Each data entry has 15 attributes, and data types of each attribute are on the website
  + we see that A2, A3, A8, A11, A14, A15 are continuous (number)
  + All others are categorical (choices)
+ 37 cases (5%) have one or more missing values
+ This dataset has 2 classes, positive and negative, meaning approved and declined

If you haven't already read through all these information, **go back and try to capture and understand your dataset first**

Here is the link: 

```http
https://archive.ics.uci.edu/ml/datasets/Credit+Approval
```

## Back to  the point

### Where we are

+ We now know one mathematical model: **decision tree (DT)**
  + DT is a **supervised** learning method, thus we need labeled data
  + It is one process only thus it is not good for giant datasets
  + It is pretty good on small and clean datasets

+ We have a cleaned dataset: UCI credit approval data set
  + 690 data entries, relatively small dataset
  + 15 attributes, pretty tiny to be honest
  + missing value is only 5%
  + 2 class data
+ By looking at these two, we know DT should work well for our dataset

### What I will provide

+ I will provide a skeleton project this time, with detailed docstring stating what your input and output should be
+ I will also provide a printer function to print your tree at the end

### What you need to do

+ **Comment on lines in any one of the following circumstances:**

  + **It took you more than 3 minutes to think**
  + **You have to seek help on the Internet or from somebody else**
  + **You are feeling brilliant**
  + **You've got a bug that is not caused by a typo**

+ **在下列情景下请务必动动小手，写好注释。注释请麻烦高亮显示，救救孩子们的眼睛吧！**

  + **某一步骤花费了你超过3分钟去思考**
  + **你不得不找度娘和谷哥寻求帮助**
  + **你感觉你写了几行吊炸天的代码，简直聪明至极**
  + **测试的时候出现了bug，而且不是因为你不小心打错了这种原因**

+ I assume you have already finished your Task 1

  + Copy and paste your code to function `readfile(file_name)` under the comment `# Your code here`. 
  + Make sure your input and output matches how I descirbed in the docstring
  + Make a minor improvement to handle missing data, in this case let's use string `"missing"` to represent missing data. Note that it is given as `"?"`

+ Implement `is_missing(value)`,  `class_counts(rows)`,  `is_numeric(value)` as directed in the docstring

+ Implement class `Determine`. This object represents a **node** of our DT. 这个对象表示的是决策树的节点。

  + It has 2 inputs and a function. 有两个输入，一个方法
  + We can think of it as the **Question** we are asking at each node. 可以理解成决策树中每个节点我们所提出的“问题”
  + Recall the questions we asked in the play/not play dataset
    + Is it Sunny, overcast, or rainy?
    + Is it hot, mild or cold?
    + Is the wind strong or weak?
    + etc.
  + 为了更好地解释，我们参照下面这一组数据

  | name | gender | age  | internet | income | label |
  | :--: | :----: | :--: | :------: | :----: | :---: |
  | 大壮 |   M    |  34  |   1.3    |  23k   |   -   |
  | 二花 |   F    |  28  |   2.6    |  17k   |   +   |
  | 三胖 |   M    |  22  |   6.7    |   7k   |   +   |
  | 四妞 |   F    |  17  |   5.9    |   1k   |   -   |

  + 这是随便编的一个网络营销广告效果的数据，我们有四个用户，两男两女，以及他们的年龄，每天上网时间，收入以及是否购买了我们营销的产品

  + For each possible column and value, we can have:

    + Column: 3, Value: 4 means we are looking at column 3 and the threshhold value is 4. 

    + If now we run the `match(self, example)` method, such as:

      ```python
      obj = Determine(3, 4)	# Question is about column 3 and the threshold is 4
      row = ["三胖", "M", 22, 6.7, "7k", "+"]
      obj.match(row)			# Is row[3] greater than the threshold?
      ```

    + If the question is categorical, such as:

      ```python
      obj = Determine(1, 'F')	# Question is about column 1 and the threshold is 'F'
      row = ["三胖", "M", 22, 6.7, "7k", "+"]
      obj.match(row)			# Is row[1] same as the threshold?
      ```

  + `__init__` is already given

  + Please implement the method `match`

    + Be careful for missing data
    + Make sure to check input data type. It should be at least 2 cases (numeric and categorical/string)

+ Implement the method `partition(rows, question)`as described in the docstring

  + Use Determine class to partition data into 2 groups

+ Implement the method `gini(rows)` as described in the docstring

  + Here is the formula for Gini impurity: <a href="https://www.codecogs.com/eqnedit.php?latex=\mathit{Gini}&space;=&space;1&space;-&space;\sum_{i=1}^{n}p_i^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathit{Gini}&space;=&space;1&space;-&space;\sum_{i=1}^{n}p_i^2" title="\mathit{Gini} = 1 - \sum_{i=1}^{n}p_i^2" /></a>
    + where `n` is the number of classes
    + <a href="https://www.codecogs.com/eqnedit.php?latex=p_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_i" title="p_i" /></a> is the percentage of the given class `i`

+ Implement the method `info_gain(left, right, current_uncertainty)` as described in the docstring

  + Here is the formula for Information Gain: <a href="https://www.codecogs.com/eqnedit.php?latex=IG&space;=&space;U_0&space;-&space;p_l&space;\cdot&space;G_l&space;-&space;p_r&space;\cdot&space;G_r" target="_blank"><img src="https://latex.codecogs.com/gif.latex?IG&space;=&space;U_0&space;-&space;p_l&space;\cdot&space;G_l&space;-&space;p_r&space;\cdot&space;G_r" title="IG = U_0 - p_l \cdot G_l - p_r \cdot G_r" /></a> 
    + where <a href="https://www.codecogs.com/eqnedit.php?latex=p_r&space;=&space;1-p_l" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_r&space;=&space;1-p_l" title="p_r = 1-p_l" /></a> 
    + <a href="https://www.codecogs.com/eqnedit.php?latex=U_0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?U_0" title="U_0" /></a> is current_uncertainty
    + <a href="https://www.codecogs.com/eqnedit.php?latex=p_l" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_l" title="p_l" /></a> is the percentage/probability of left branch, same story for <a href="https://www.codecogs.com/eqnedit.php?latex=p_r" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_r" title="p_r" /></a> 

### Happy Coding :)

# Task 3

Dec. 24th 2018	Merry Christmas

+ Implement `find_best_split(rows)`. This is the core of our DT algorithm. We need to find the best "question" to be asked. Please follow the steps below and comment on all the lines you feel necessary. 
  + Initialize all variables. You may need to store the best information gain, the best Determine object and more
  + Loop through all the columns
  + Find all possible values of each column. Note that we do **NOT** want duplicate values here
  + Loop through each value you have found in the previous step
  + Define a new `Determine` object with the current column and value
  + Find and store `true_rows` and `false_rows` with `partition` function
  + Examine if your rows got any split. i.e. if any of the `true_rows` and `false_rows` has length 0. 
    + If yes, do nothing and continue executing your loop
    + If not, calculate information gain with the method you have implemented in Task 2
  +  Check if the value you've got is better
  + After all the loop, return the best information gain and the best Determine object associated with the best information gain
+ Implement the class `Leaf`
  + This object represents a decision node when it has reached to a leaf node
  + You either cannot split any more, or the prediction is already certain (100%)
  + Implement `__init__(self, rows)`. You just need to tell us what `self.prediction` is
  + Our prediction now is simply based on which labels lie in this leaf and how many data entries for each label are there in this leaf. Say we have 3 data entries all fall into this leaf, as follows,
    + data_0: bla bla bla +
    + data_1: bla bla bla -
    + data_2: bla bla bla +
  + Then whenever we have a testing data that falls into this leaf, we know that there is approximately 66.67% chance it is a "+" and 33.33% chance it is a "-"
  + Recall that we have implemented a function called `class_counts(rows)` which might be useful
+ Implement the class `DecisionNode`
  + `DecisionNode` has 3 inputs
  + We will need to compare different `DecisionNode` objects. We define a method `__eq__()` to allow `==` to be used
    + We compare if all three attributes of `self` and `other` are the same and return a **boolean**(True/False)
+ Implement the function `build_tree(rows)`. This is the function we use to actually build our tree. Please follow the steps below,
  + We will be using recursive function here (递归函数)
  + Find the best split using the method we implemented before, store information gain and the question to a local variable
  + Define the ending condition. If there is no gain, i.e. `gain == 0`, return a leaf node `Leaf(rows)`
  + Otherwise, get the partition of the tree at the current node with the best question(`Determine` object that we got before)
  + We use **DFS(Depth First Search)** to build the tree, and do the true_branch **recursively** first.
  + We then split the false_branch **recursively**
  + At last, we need to return something. We will return a `DecisionNode` object here since the starting point is also a `DecisionNode`
  + Notes:
    + This function might take you some time and thinking. Be patient
    + You need to understand the logic behind our DT before you even start to think. Talk to me if you are not feeling confident enough
    + Look up **recursive function** and **depth first search** if necessary. 
+ I will implement `print_tree`. You don't need to worry about it at all
+ Implement the method `classify(row, node)`. This is the method we use to predict our testing/validation/real dataset. Follow the steps below
  + First define ending scenario. If we have reached a `leaf node`, return the `prediction`
  + If input is not a leaf node, then it should be a `DecisionNode`. 
  + Use the `match` function we defined before to determine whether it will be classified to the true_branch or the false_branch
  + recursively return `classify(row, node.<branch>)` while if the previous step gives you a `True`, you use the true_branch for `<branch>` ; and if the previous step gives you a `False`, you use the false_branch for `<branch>` 

+ I will provide all the code you need for `print_leaf(counts)`
+ Happy coding!

# Task 4

Dec. 31st 2018	Happy New Year!

Now we have all the tools we need for our decision tree. It's time for us to use it to do some magic!

## Data Splitting

+ We first split our data into 2 sets, training set and testing set
+ You can first just use the first 85% of data as training data and the remaining as testing data
+ You will need to try to make them random selected

```python
fraction = 0.15					# 15% of data will be used as testing set
data = 							# Please complete this line to read data from file
training_data = 				# Please complete this line to extract training set
testing_data = 					# Please complete this line to extract testing set
```

## Making our tree readable

+ Now we define column labels. Note that this is only used for printing your tree

```python
# Column labels.
# These are used only to print the tree.
header = []
for _ in range(len(testing_data[0])):
	header.append('Attribute{}'.format(_))
```

## Building our tree

+ OK, we are good to build our tree using our training data

```python
my_very_first_decision_tree = 	# Please complete this line to build your tree
```

## Calculating accuracy of our tree with testing data

+ Now we have our tree ready. It's time to test how our tree works

```python
corr = 0						# Used to store how many correct prediction we will get
for row in testing_data:		# Loop through all testing data
    actual = 					# Store the actual label, which should be the last column
    # Get all possibilities predicted by our tree with the given testing data
    possibilities = print_leaf(classify(row, my_very_first_decision_tree))
    # You can print out the possibilities and see what they look like
    # Now loop through all possibilities and get the prediction with the highest possibility
    for case in possibilities:
        # Your code here
        predictioin = None
        pass
    # Now test if our prediction is the same as the actual output
    if  ==	:					# Please complete this line
    	# Your code here
        pass					# If our prediction is correct, add 1 to corr
    else:
        # Print out the wrong predictions
        # Replace the Nones with correct variables
        # We need the actual label, predicted label, and the probability of the prediction, in that order
        print("Actual: {} === Predicted: {} === Prob: {}",format(None, None, None))
```

## Overall accuracy

+ Finally, we need to see the overall accuracy of our model

```python
# Replace the None with calculated overall accuracy
print("Overall Accuracy: {}%".format(None))
```

# Task 5

## Reflections and future work

+ How did it go? How is your model accuracy?
+ 运行得怎么样？（耗时、内存/CPU使用）最后模型的准确率怎么样？
+ Try using random selected testing data and training data. Do you see significant difference in accuracy?
+ 试试用**随机抽取的**85%的数据做训练，剩下的15%的数据做测试，看看模型准确率有没有明显变化？
+ Try to use at least 2 other datasets from UCI database to see how decision tree works for them. Do you see any similarities in the datasets that perform well?
+ 尝试从UCI数据库中选择至少两个别的数据，并用决策树对其训练并分析效率与准确率。你能总结出什么？决策树效果好的数据有什么特点？
+ Try to implement the very basic random forest using our decision tree model as the baseline model
+ 调用我们的决策树模型，尝试开发一个最基本的随机森林模型，
+ Future reading and presentation: 
+ 延展阅读学习以及**演讲**
  + Takeaways from this project
  + 这个项目中学到了什么
  + Issues of decision tree
  + 决策树的问题
  + Possible techniques to resolve these issues
  + 可能的解决办法
  + What kind of problems are best suited for decision trees?
  + 什么样的问题最适合决策树

<br>

# References

+ Developers, G. (2017, September 13). Let's Write a Decision Tree Classifier from Scratch - Machine Learning Recipes #8. Retrieved from https://www.youtube.com/watch?v=LDRbO9a6XPU

+ Chiharu, S. (1992, March 19). [Japanese Credit Screening (examples & domain theory)]. Published raw data.
+ 


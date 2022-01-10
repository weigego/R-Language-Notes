Hi, what's up. 我是R语言小白一枚。近期参加了一个R语言学习小组，我也将开始使用CSDN记录每次课的学习笔记和遇到的问题，希望能对您有所帮助~
@[TOC](熟悉规则与R语言入门)
# R、RStudio的安装
R、RStudio、相关Packaged如何安装的教程见链接: [link](https://rlearning.netlify.app/task-00.html#%E5%AE%89%E8%A3%85).
本次学习记录中的内容主要是一个问题：**中文路径导致的RStudio安装失败**
## 中文路径下RStudio、packages安装失败的问题
由于我windows账户默认的用户名是中文，中文路径导致了安装Rtools过程中出现了很多麻烦。
为此，参照网上的方法，我进行了以下两种尝试：
1. 直接进入windows系统管理员模式（教程链接：[link](https://www.zhihu.com/question/51241293)），重命名了c盘user文件夹下的计算机名称，但是效果并不好。修改了名称之后，电脑上的OneDrive就罢工了，Office全家桶也无法正常工作。网上说要一并更新windows中其他含有该中文路径的注册表，才能解决其他软件的出现异常的问题，我嫌麻烦，于是乎采取下面的方法。
2. 新建一个windows管理员账户（教程链接：[link](https://www.zhihu.com/question/51241293)），在这个新的、名称为英文的账户中，操作使用R、RStudio，目前的使用感觉良好。

2021/08/16
end~






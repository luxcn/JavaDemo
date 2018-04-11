# WebIDE Java 项目配置指南

[TOC]

本指南介绍如何在 WebIDE 里安装配置 Java 项目。

> 如果你当前阅读的 Markdown 源文件，请打开 https://coding.net/u/tanhe123/p/JavaDemo/git ，渲染以后的效果能看见图片

## 1. 准备 Java + Maven 环境（Java Demo 已默认使用）

在运行环境列表中选择 `ide-tty-java-maven` 环境

 ![图片](https://dn-coding-net-production-pp.qbox.me/08d92b92-3dd9-4294-b2ec-9899b950dd73.png)

切换成功后打开 WebTerminal，即可使用 java + maven

```shell
java -version && mvn -v
```



 ![图片](https://dn-coding-net-production-pp.qbox.me/81fde7d9-6f5c-49da-a8e1-8d07cc090a8a.png) 

## 2. 设置项目类型

目前项目只支持 java（暂时不支持 maven、gradle、android 等）。

操作步骤为：打开 java 项目的 workspace，依次选择菜单栏中的文件、项目类型：

![图片](https://dn-coding-net-production-pp.qbox.me/0f61dc64-aa60-4620-afb0-db4b78fe8757.png)

在弹出的界面依次设置 `项目类型`、`Source Folder`、`Library Folder`

![图片](https://dn-coding-net-production-pp.qbox.me/a5d1dcf6-782a-49f1-a636-b7c2d4321d45.png)

这里简单介绍下参数的含义：

>**项目类型**: 项目的类型，目前两种项目类型，即 **Blank** 和 **Java**。当选择 Java 后，会出现 Source Folder 和 Library Folder 的配置。  
>**Source Folder**: Java 项目的源码目录，只有在该目录的 java 文件才会被分析，代码提示、定义跳转等功能才会有效。  
>**Library Folder**: Java 的 library 目录。该目录用来放一些项目依赖的 jar 文件。设置项目类型时，会加载所有 library 目录中的所有 jar 到 classpath。代码提示、定义跳转等功能支持（或将会支持）library 中包含的 jar。该参数若省略则为默认值 lib。    

## 3. 代码提示

设置完毕即可进行代码补全了。当输入 `.` 后会自动弹出代码提示，或者使用快捷键 `alt + /` 进行代码提示：

 ![图片](https://dn-coding-net-production-pp.qbox.me/fc61d8ae-ff35-4b72-a8ef-4c42553c411e.gif) 

**Tip: 进行代码提示时，输入法最好切换到英文状态。**

弹出代码提示后，如果想使用某一条进行代码补全，有两种方式：

1. **鼠标单击、回车**：将补全的内容插入到光标后，光标后的内容会在新插入的内容后面。
2. **Tab**: 将补全的内容插入到光标后，并智能替换光标后的内容。

为了演示这两种方式，我们假设有如下代码，光标在 `.` 后且在 `xxx` 之前：

 ![图片](https://dn-coding-net-production-pp.qbox.me/faddf044-a7f4-4a55-a2d0-003417522687.png) 

使用回车代码补全的效果如下：

 ![图片](https://dn-coding-net-production-pp.qbox.me/1878c2e6-6847-44e2-9938-06247b2dc918.gif) 

使用 tab 的效果为:

 ![图片](https://dn-coding-net-production-pp.qbox.me/6c691edc-5c64-4e66-93a5-9bf9430d4f25.gif) 

可以看到，使用 tab 的方式会智能替换掉原有代码。其它场景，回车与 tab 可以替换使用。

代码补全时，如果引入了新的类，WebIDE 会智能的在源码文件顶部 import 该类：

 ![图片](https://dn-coding-net-production-pp.qbox.me/91815ee1-1532-4328-b20e-6614a72e236a.gif) 

有一些补全比较特殊，并不能仅仅将补全内容插入到源码文件，还需要和用户经过几个步骤的交互才算补全完成，比如一个方法包含多个参数这种情况，又或者像 for 循环这种模板。这里我们拿 for 循环演示，补全后会有几处位置，WebIDE 将其高亮显示：

 ![图片](https://dn-coding-net-production-pp.qbox.me/9314c41a-4afe-478e-adec-4aceda5250e2.gif) 

WebIDE 从第一个高亮开始，插入用户输入的内容，用户输入完成后，使用 `Tab` 跳转到下一个位置，直到所有位置都被用户处理，才算完成本次的代码补全。

## 4. 错误提示

对于包含错误的代码，WebIDE 给予一定程度的错误提示，并在指定的位置标红，鼠标放到左侧红色的图标上，会显示更详细的错误信息：

 ![图片](https://dn-coding-net-production-pp.qbox.me/350bd17a-1824-4223-bb93-de6fff33b186.gif) 

除了错误提示，WebIDE 还会向用户发出**可以忽略的"警告"**：

 ![图片](https://dn-coding-net-production-pp.qbox.me/734589a5-75fe-403b-b25e-47680ccf2427.png) 

## 5. 定义跳转

WebIDE 支持代码类、方法的跳转，跳转的范围为项目的源码或第三方 jar。

具体使用方法为：

打开 java 源代码，按住 `shift + cmd`（mac）或 `shift + ctrl`（win），鼠标点击想要跳转的类或方法即可。当点击位置可以跳转，会自动跳转到指定位置。

1. 如果跳转的目标在项目内，则自动打开该文件，并用高亮渐隐的方式突出显示。
2. 如果跳转的目标在第三方 jar，则显示反汇编的内容。

下面是第一种跳转的演示：

 ![图片](https://dn-coding-net-production-pp.qbox.me/7cedb297-5fbf-473d-a24b-3b0f487ba912.gif) 

## 6. 配置 classpath

如果想要修改项目的 classpath，可以依次选择文件、配置 Classpath，配置页面如下所示：

 ![图片](https://dn-coding-net-production-pp.qbox.me/7bfef68e-27ef-4bce-bf60-bc35c889457c.png) 

在这里，可以手动添加、删除 classpath 中的 jar 包。也可以添加、修改、删除项目的源码目录位置。

## 7. 运行

输入以下命令即可运行此 Demo ，默认运行在 8080端口， 之后使用*访问链接*功能对此端口进行映射，即可在外部进行访问。

```Shell
mvn spring-boot:run
```


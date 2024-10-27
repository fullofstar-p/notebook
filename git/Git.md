# Git 常用命令

## Git全局设置

设置用户信息

```Git
git config --global user.name "itcast"
git config --global user.email "hello@itcast.cn"
```

查看配置信息

```Git
git config --list
```

## 获取Git仓库

获取Git仓库通常有两种方式:

1. 在本地仓库初始化一个Git仓库(不常用)

   ```Git
   git init
   ```

2. 远程仓库克隆(**常用**)

   ```
   git clone [远程Git仓库地址]

## 工作区、暂存区、版本库概念

版本库：.git隐藏文件夹就是版本库,版本库中储存了很多配置信息、日志信息和文件版本信息。。

工作区：包含.git文件夹的目录就是工作区，也称为工作目录，主要用于存放开发的代码

暂存区：.git文件夹中有很多文件，其中有一个index文件就是暂存区，也可以叫做stage。暂存区是一个临时保存修改文件的地方

## Git工作区中文件的状态

Git工作区中的文件存在两种状态：

untracked 未追踪 （未被纳入版本控制）

tracked 已追踪（被纳入版本控制）

1. Unmodified 未被修改状态
2. Modified 已修改状态
3. Staged 已暂存状态

==注意==：**这些文件的状态会随着我们执行Git的命令发生变化**

## 本地仓库操作

**查看文件状态**

```git
git status
```

**将文件的修改加入暂存区**

```git
git add [文件名]
```

**将暂存区的文件取消暂存或者是切换到指定版本**

```git
git reset [文件名]
git reset --hard 版本号 [文件名]
```

**将暂存区的文件修改提交到版本库**

```git
git commit -m "提交信息" [文件名]
```

**查看日志**

```git
git log
```

## 远程仓库操作

**查看远程仓库**

```git
git remote
git remote -v
```

**添加远程仓库**

```git
git remote add [shortname] [url]
```

**从远程仓库克隆**

```git
git clone [url]
```

**从远程仓库拉取**

```git
git pull [short-name] [branch-name]
```

==注意:==**如果当前本地仓库不是从远程仓库克隆,而是本地创建的仓库,并且仓库中存在文件,此时再从远程仓库拉取文件是会报错(fatal:refusing to merge unrelated histories)**

解决此问题可以在git pull命令后加入参数 `--allow-unrelated-histories`

**推送到远程仓库**

```git
git push [remote-name] [branch-name]
```

## 分支操作

通过git init命令创建本地仓库时默认会创建一个master分支

**查看分支**

```git
git branch		列出所有本地分支
git branch -r	列出所有远程分支
git branch -a 	列出所有本地分支和远程分支
```

**创建分支**

```git
git branch [name]
```

**切换分支**

```git
git checkout [name]
```

**推送至远程仓库分支**

```git
git push [shortName] [name]
```

**合并分支**

```git
git merge [name]
```

## 标签操作

**列出已有的标签**

```git
git tag
```

**创建标签**

```git
git tag [name]
```

**将标签推送至远程仓库**

```git
git push [shortName] [name]
```

**检出标签**

```git
git checkout -b [branch] [name]
```

#  在IDEA中使用Git

## 获取Git本地仓库

获取Git仓库通常有两种方式:

1. 本地初始化仓库

   ![image-20241024224558781](./images/image-20241024224558781.png)

2. 从远程仓库克隆

   ![image-20241024224530835](./images/image-20241024224530835.png)

## 本地仓库操作

**将文件加入暂存区**

![image-20241027210222779](./images/image-20241027210222779.png)

**将暂存区的文件提交到版本库**

![image-20241027210325894](./images/image-20241027210325894.png)

![image-20241027210647382](./images/image-20241027210647382.png)

**查看日志**

![image-20241027210613771](./images/image-20241027210613771.png)

## 远程仓库操作

**查看远程仓库**

![image-20241027211005255](./images/image-20241027211005255.png)

**添加远程仓库**

![image-20241027211110036](./images/image-20241027211110036.png)

**推送至远程仓库**

![image-20241027211238821](./images/image-20241027211238821.png)

![image-20241027211348220](./images/image-20241027211348220.png)

**从远程仓库拉取**

![image-20241027211655713](./images/image-20241027211655713.png)

![image-20241027211718090](./images/image-20241027211718090.png)

![image-20241027211814907](./images/image-20241027211814907.png)

## 分支操作

**查看分支**

![image-20241027212134806](./images/image-20241027212134806.png)

![image-20241027212233060](./images/image-20241027212233060.png)

![image-20241027212310771](./images/image-20241027212310771.png)

**创建分支**

![image-20241027212340841](./images/image-20241027212340841.png)

![image-20241027212358697](./images/image-20241027212358697.png)

**切换分支**

![](images/Snipaste_2024-10-27_21-31-39.png)

**将分支推送到远程仓库**

![](images/Snipaste_2024-10-27_21-33-41.png)

**合并分支**

![](images/Snipaste_2024-10-27_21-34-59.png)
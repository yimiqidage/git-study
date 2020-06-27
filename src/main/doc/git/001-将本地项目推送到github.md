# 1.将本地项目推送到github

## 1.操作步骤

1. 前置条件

   1. 需要确认本地项目为git项目；

   2. 确认有master分支；

   3. 如果本地项目不是git项目，采取如下命令进行添加：

      ```bash
      git init  ## 此步骤的目的是本地创建git项目
      git checkout -b master  ## 此步骤是在本地创建一个分支，分支的名称是 'master'
      git add a.txt  ## 此步骤是将本地的 a.txt 项目，添加到索引空间。需要将a.txt替换为自己的项目名称
      git commit -m "init my project" ## 将索引空间的文件，进行提交，其中 "init my project" 是提交的备注
      ```

2. 将本地git项目，推送远程仓库

   ```bash
   git remote add origin https://github.com/yimiqidage/git-study.git  ## 其中 https的地址，是你的github项目地址
   git push -u origin master ## 将本地的master分支和远程的master分支建立关联
   ```

## 2.可能遇到问题

### 1.failed to push some refs xxx

1. 现象

```
To https://github.com/yimiqidage/git-study.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/yimiqidage/git-study.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

2. 产生原因

   本地代码同远程代码

3. 产生步骤

   ```bash
   1. 本地创建一个项目，并创建一些文件；
   2. 使用git init 命令进行初始化；
   3. 添加本地文件添加到索引空间； git add a.txt
   4. 提交本地文件 git commit a.txt -m  "git add a.txt"
   5. 将本地代码同远程分支建立关系：
   	git remote add origin https://github.com/yimiqidage/git-study.git  ## 其中 https的地址，是你的github项目地址
   	git push -u origin master ## 将本地的master分支和远程的master分支建立关联
   6. 提示上面的错误
   ```

4. 解决方式

   ```bash
   git pull # 尝试将远程代码，更新到本地
   git branch --set-upstream-to=origin/master # 将本地代码当前分支同远程分支建立关联关系
   git pull origin master --allow-unrelated-histories #将远程代码更新到本地，允许覆盖本地文件
   	输入命令后，会进入文本编辑模式，此时，按下 'esc' 键，然后输入':'，继续输入 'wq' 保存退出即可。
   git push  # 进行代码提交
   ```


### 2. src refspec master does not match any

1. 现象

   ```bash
   error: src refspec master does not match any
   error: failed to push some refs to 'https://github.com/yimiqidage/git-study.git'
   ```


> 该错误的原因是，目录中没有文件，空目录是不能提交上去的

2. 解决方式

   ```bash
   git add a.txt  ## 此步骤是将本地的 a.txt 项目，添加到索引空间。需要将a.txt替换为自己的项目名称
   git commit -m "init my project" ## 将索引空间的文件，进行提交，其中 "init my project" 是提交的备注
   ```

3. 重新进行提交

   ```bash
   git push -u origin master ## 将本地的master分支和远程的master分支建立关联
   ```

   

##  3.小技巧

如果重试几次后，都无法推送，可以删除项目根目录下的 .git 项目，然后重新开始操作。。

```bash
rm -rf .git
```

# 2.如何使用git，进行代码合并

## 1.代码合并场景

> 将主干（master）代码合并到开发（dev）分支

| 分支   | 名称     | 说明                                   |
| :----- | -------- | :------------------------------------- |
| master | 主干     | 主干代码，跟线上保持一致               |
| dev    | 开发分支 | 开发分支，用于开发。开发分支可能有多个 |

## 2.代码合并操作步骤

### 1.使用git命令进行合并

```bash
git checkout master # 检出master分支
git pull # 从远程仓库，同步最新代码到本地
git checkout dev # 检出自己的开发分支
git merge master # 同步master分支代码到 dev分支。 即： master -> dev (注意方向不要反了)
git push # 将本地合并的代码，push到远程仓库
```



# 3.代码合并冲突

## 1.冲突产生的原因

| 分支   | 代码结构                           | 说明                         |
| :----- | ---------------------------------- | :--------------------------- |
| master | `String name = "zhangsan-master";` | 主干代码，通过别的分支合并过 |
| dev    | `String name = "zhangsan-dev";`    | 开发分支，修改相同行的代码   |





## 2.如何解决合并冲突

### 1.查找到冲突的文件

```bash
git merge master # 合并master代码到dev分支时，会提示合并冲突
```



### 2.逐个文件解决

## 3.撤销本次合并






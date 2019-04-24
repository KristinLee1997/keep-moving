# git分支替换

## **背景**

想要删除master分支上的所有提交，先创建了一个新分支，然后将master分支删除，将新分支替换成master分支

## **步骤**

### 1.创建一个新分支last\_branch

```text
git checkout --orphan latest_branch
```

### 2.将当前所有文件添加到新分支    

```text
git add -A
```

### 3. 提交更改

```text
git commit -m "commit message"
```

### 4.删除想要被替换的分支

```text
git branch -D master
```

###  5.将新建的分支更改名字 

```text
git branch -m master
```

### 6.强制更新git远程仓库 

```text
git push -f origin master
```






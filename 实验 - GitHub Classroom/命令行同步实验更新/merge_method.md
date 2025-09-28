# Git 手动合并修改指南

### 首先进入您的代码仓库目录：
```bash
cd 你的目录名
```

**强烈推荐**：使用 VSCode 打开项目，便于后续查看和解决冲突
```bash
code .
```
### 步骤 0：add .
由于您大概更改了`bits.c，
使用`git add .`把更改添加到暂存区
```bash
git add .
git commit -m "你的更改信息"
```
### 步骤 1：添加远程仓库
```bash
git remote add template https://github.com/RUCICS/Datalab-2025Fall.git
```
> ⚠️ **注意**：此命令只需执行一次

### 步骤 2：获取远程仓库更新
```bash
git fetch template main
```

### 步骤 3：合并远程仓库更新

使用 rebase  
```bash
git rebase template/main
```
这时候会看到如下报错，我们需要解决冲突
![alt text](hint.png)
### 步骤 4：解决冲突
#### 情况一：使用 VSCode 解决冲突

如果您已经运行了 `code .`，可以直接在 VSCode 中解决冲突。
1. **查看冲突文件**
   - 在左侧面板的 `SOURCE CONTROL: CHANGES` 中查看所有冲突文件。（如果没有这个板块，如图所示，找到标红的两个文件`decl.c`和`README.md`）。此次合并中，这两个文件有冲突。
首先打开一个文件，看到如下图所示的冲突提示：
注：如果找不到这样的提示，ctrl + F,搜索 `<<<<<<< HEAD` 即可。
![alt text](solve_conflict.png)

2. **解决冲突**
   - 点击打开冲突文件
   - 在冲突区域选择 **Accept Current Change**
   
   > **说明**：以后根据实际情况，您可以选择：
   > - `Accept Current Change` - 采用当前更改
   > - `Accept Incoming Change` - 采用传入更改
   > - `Accept Both Changes` - 接受双方的修改
   > 
   > 当前建议选择 `Accept Current Change`

3. **添加到暂存区**
- 方法一：
   - 点击文件右侧的 "+" 号，将修改添加到暂存区（注，如果有人找不到这个页面，使用方法二）。
![alt text](add.png)
- 方法二：
   - 使用命令行。如果你解决的是`decl.c`，运行：
   ```bash
   git add decl.c
   ```   
   如果你解决的是`README.md`，运行：
   ```bash 
   git add README.md
   ```
当你把两个文件都解决完后，就完成了这一步。
### 步骤五：解决完冲突后...
1. 检查确认文件无误后，暂存所有更改
```
git add .
```
2. 将这些更改追加到当前正在编辑的提交中，并且不修改提交信息
```
git commit --amend --no-edit
```
3. 继续 rebase 过程
```
git rebase --continue
```
4. 把之前stash的pop出来
```bash
git stash pop
```
### 如果出现命令编辑器...

**如果是 Vim：**
- 按 `Esc` 键退出插入模式
- 输入 `:wq` 保存并退出

**如果是 Nano：**
- 按 `Ctrl + X` 退出
- 按 `Y` 确认保存
- 按 `Enter` 确认文件名

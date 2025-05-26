Git 上传代码到远程仓库的基本流程如下，适用于 Git 和 GitHub / Gitee 等远程仓库平台：

---

### ✅ 一、首次上传（本地项目 ➜ Git 远程仓库）

1. **初始化 Git 仓库**（如果还没有）

    ```bash
    git init
    ```

2. **添加远程仓库地址**

    ```bash
    git remote add origin <远程仓库地址>
    ```
  
3. **添加所有文件**

    ```bash
    git add .
    ```

4. **提交代码**

    ```bash
    git commit -m "首次提交"
    ```

5. **推送到远程仓库（首次推送，需指定分支）**

    ```bash
    git push -u origin master
    ```

    > 如果是 `main` 分支，则：

    ```bash
    git push -u origin main
    ```


---

### ✅ 二、常规上传流程（更新后继续推送）

当你修改了代码后，执行以下步骤：

1. 查看状态（可选）：
    
    ```bash
    git status
    ```
    
2. 添加改动：
    
    ```bash
    git add .
    ```
    
3. 提交：
    
    ```bash
    git commit -m "更新说明"
    ```
    
4. 推送：
    
    ```bash
    git push
    ```
    

---

### ✅ 三、常见补充命令

- **克隆远程仓库**
    
    ```bash
    git clone <远程仓库地址>
    ```
    
- **查看当前远程仓库地址**
    
    ```bash
    git remote -v
    ```
    
- **切换分支**
    
    ```bash
    git checkout -b <新分支名>
    ```
    
- **拉取远程分支更新**
    
    ```bash
    git pull origin <分支名>
    ```
    

---



## 🧹 一、清理工作目录中未跟踪的文件（即未 `git add` 的）

### 1. 清除未跟踪的文件（不包括 `.gitignore` 忽略的文件）：

```bash
git clean -f
```

### 2. 清除未跟踪的目录：

```bash
git clean -fd
```

### 3. 模拟清理（先查看将删除哪些文件，不执行）：

```bash
git clean -n
```

---

## 🧹 二、清除修改但未提交的内容（恢复工作区）

### 1. 撤销对已修改但未添加（`add`）的文件的修改：

```bash
git checkout -- <文件名>
```

或恢复所有文件：

```bash
git checkout -- .
```

### 2. 清除已 `add` 但未 `commit` 的内容（即清空暂存区）：

```bash
git reset
```

---

## 🧹 三、重置 commit（谨慎操作）

### 1. 删除最近一次提交，但保留文件更改：

```bash
git reset --soft HEAD~1
```

### 2. 删除提交及更改（慎用）：

```bash
git reset --hard HEAD~1
```

---

## 🧹 四、清理合并冲突中遗留的内容

### 清理合并失败的状态：

```bash
git merge --abort
```

---

## 🧹 五、删除本地和远程分支

### 删除本地分支：

```bash
git branch -d <分支名>
```

### 强制删除本地分支：

```bash
git branch -D <分支名>
```

### 删除远程分支：

```bash
git push origin --delete <分支名>
```

---

## 🧹 六、清除 Git 缓存（如 .gitignore 后仍被追踪）

### 1. 删除缓存并重新添加

```bash
git rm -r --cached .
git add .
git commit -m "清除缓存重新提交"
```


Git 中的“查看”操作主要用于观察项目当前状态、提交历史、远程仓库、分支等内容。以下是最常用的查看命令汇总，分为几类帮你快速掌握：

---

## 👀 一、查看项目状态

### 1. 查看当前 Git 状态（最常用）

```bash
git status
```

---

## 📜 二、查看提交记录

### 1. 简洁查看提交历史

```bash
git log --oneline
```

### 2. 查看完整提交记录（默认格式）

```bash
git log
```

### 3. 图形化查看提交历史（推荐加 `--all`）

```bash
git log --graph --oneline --all
```

---

## 🌿 三、查看分支

### 1. 查看本地分支

```bash
git branch
```

### 2. 查看远程分支

```bash
git branch -r
```

### 3. 查看本地 + 远程分支

```bash
git branch -a
```

---

## 🌐 四、查看远程仓库信息

### 1. 查看远程地址

```bash
git remote -v
```

### 2. 查看远程详细信息

```bash
git remote show origin
```

---

## 📁 五、查看修改内容（diff）

### 1. 查看工作区中未提交的更改

```bash
git diff
```

### 2. 查看已 `add` 到暂存区的更改

```bash
git diff --cached
```

### 3. 查看某个文件的更改

```bash
git diff <文件名>
```

---

## 📌 六、查看某个文件的提交记录

```bash
git log <文件名>
```

---

## 🧾 七、查看某次提交具体改动

### 方式一：根据 commit hash 查看

```bash
git show <commit_id>
```

### 方式二：图形化工具查看（如 `tig`，需安装）

```bash
tig
```

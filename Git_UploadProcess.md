
# 🚀 Git 更新与上传代码流程整理

---

## ✅ 一、首次上传项目到远程仓库

适用于新建项目第一次上传：

```bash
echo "# 项目名" >> README.md          # 初始化说明文件
git init                              # 初始化本地 Git 仓库
git add README.md                     # 添加文件
git commit -m "first commit"          # 提交说明
git branch -M main                    # 设置分支为 main
git remote add origin <仓库地址>      # 添加远程地址
git push -u origin main               # 推送到远程 main 分支
```

---

## ✅ 二、常规开发上传流程（已有仓库）

适用于每次开发过程中的代码更新：

```bash
git pull origin main                  # 拉取远程分支最新代码，避免冲突
git add .                             # 添加所有修改文件
git commit -m "描述本次更新的内容"      # 提交修改
git push -u origin main              # 推送到远程仓库
```

---

## ✅ 三、分支开发推荐流程（多人协作常用）

```bash
git pull origin main                        # 确保主分支是最新的
git checkout -b feature/功能名             # 创建并切换到新分支
# 修改、开发中…
git add .                                   # 添加改动
git commit -m "开发功能说明"                # 提交修改
git push origin feature/功能名             # 推送到远程分支
# 后续可发起 Pull Request 合并到主分支
```

---

## ✅ 四、常用查看命令

|功能|命令|
|---|---|
|查看当前状态|`git status`|
|查看提交历史|`git log` 或 `git log --oneline`|
|图形化查看提交|`git log --graph --oneline --all`|
|查看本地分支|`git branch`|
|查看远程分支|`git branch -r`|
|查看所有分支|`git branch -a`|
|查看远程仓库地址|`git remote -v`|
|查看某文件提交记录|`git log 文件名`|
|查看某次提交内容|`git show 提交ID`|
|查看工作区差异|`git diff`|
|查看暂存区差异|`git diff --cached`|

---

## 🧹 五、常用清理命令（高级操作）

|场景|命令|
|---|---|
|清除未跟踪文件|`git clean -f`|
|清除未跟踪目录|`git clean -fd`|
|模拟清除（预览）|`git clean -n`|
|恢复已修改未提交的文件|`git checkout -- .`|
|撤销暂存区改动|`git reset`|
|撤销最近一次提交但保留改动|`git reset --soft HEAD~1`|
|强制撤销提交及改动|`git reset --hard HEAD~1`|
|中止合并冲突|`git merge --abort`|
|删除本地分支|`git branch -d 分支名`|
|强制删除本地分支|`git branch -D 分支名`|
|删除远程分支|`git push origin --delete 分支名`|
|清除 `.gitignore` 后仍被追踪文件|`git rm -r --cached .`|

---

## 🧠 使用建议

- 每次开发前先拉取主分支代码（`git pull`）；
    
- 每项新功能使用独立分支（`feature/xxx`）；
    
- 提交信息要清晰、具备描述性；
    
- 使用 `git status` 和 `git log` 随时掌握项目状态；
    
- 慎用 `reset --hard`，操作前建议备份；
    

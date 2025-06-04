# Git 版本控制操作指南

## 版本回退操作

### 1. 查看提交历史
```bash
# 查看简洁的提交历史
git log --oneline

# 查看详细的提交历史
git log

# 查看所有操作历史（包括回退操作）
git reflog
```

### 2. 版本回退方法

#### 方法一：使用 git reset（推荐用于本地版本回退）
```bash
# 硬回退（完全回退，丢弃所有更改）
git reset --hard <commit_id>

# 软回退（保留更改但撤销提交）
git reset --soft <commit_id>

# 混合回退（保留更改但撤销暂存）
git reset --mixed <commit_id>
```

#### 方法二：使用 git revert（推荐用于远程版本回退）
```bash
# 创建新的提交来撤销之前的更改
git revert <commit_id>
```

### 3. 实际案例：数据库重构版本回退

#### 回退到上一个版本
```bash
# 1. 查看提交历史
git log --oneline
# 输出示例：
# 3f413ca 重构数据库结构：将材料属性分为主表、电气表、热能表和机械表
# 33a122c Initial commit

# 2. 回退到上一个版本
git reset --hard 33a122c
```

#### 恢复到回退前的版本
```bash
# 1. 查看操作历史
git reflog
# 输出示例：
# 33a122c HEAD@{0}: reset: moving to 33a122c
# 3f413ca HEAD@{1}: commit: 重构数据库结构：将材料属性分为主表、电气表、热能表和机械表

# 2. 恢复到之前的版本
git reset --hard 3f413ca
```

## 注意事项

1. `git reset --hard` 会丢失所有未提交的更改，使用前请确保已备份重要文件
2. 如果已经推送到远程仓库，建议使用 `git revert` 而不是 `git reset`
3. 使用 `git reflog` 可以找回任何操作历史，包括已经回退的提交
4. 在进行重要操作前，建议先创建分支进行测试

## 常用 Git 命令

```bash
# 查看当前状态
git status

# 查看分支
git branch

# 切换分支
git checkout <branch_name>

# 创建并切换分支
git checkout -b <branch_name>

# 添加文件到暂存区
git add <file_name>

# 提交更改
git commit -m "提交说明"

# 推送到远程仓库
git push origin <branch_name>

# 拉取远程更新
git pull origin <branch_name>
```

## 最佳实践

1. 在进行重要更改前创建新分支
2. 经常提交代码，保持提交信息清晰明确
3. 在回退版本前先使用 `git log` 确认目标版本
4. 如果不确定操作结果，可以先创建备份分支
5. 重要操作前先使用 `git status` 检查工作区状态 
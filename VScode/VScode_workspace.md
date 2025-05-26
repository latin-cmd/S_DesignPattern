## VS Code Workspace（工作区）简介

主要目的：分割语言环境，块化扩展，dev_containers的代替方案
### 什么是 VS Code 工作区？

https://code.visualstudio.com/docs/editing/workspaces/workspaces
VS Code 工作区是 Visual Studio Code 用来管理项目设置、文件和文件夹的一种机制。它可以帮助你更好地组织和配置你的开发环境，尤其适合多文件夹、多项目的情况。

```json
{
  "folders": [
    {
      "path": "."
    }
  ],
  "settings": {
    "[python]": {
      "editor.formatOnSave": true,
      "python.linting.enabled": true,
      "python.linting.pylintEnabled": true
    },
    "[sql]": {
      "editor.defaultFormatter": "mtxr.sqltools"
    },
    "[html]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    }
  },
  "extensions": {
    "recommendations": [
      "ms-python.python",
      "ms-python.vscode-pylance",
      "mtxr.sqltools",
      "esbenp.prettier-vscode"
    ],
    "unwantedRecommendations": [
    ]
  }
} 
```
---

### 工作区的类型

1. **单文件夹工作区（Single-folder Workspace）**
    
    - 你直接打开一个文件夹，VS Code 会自动将其作为一个工作区。
        
    - 这种情况下，工作区设置和扩展都是针对这个文件夹的。
        
2. **多文件夹工作区（Multi-root Workspace）**
    
    - 你可以同时打开多个文件夹，组合成一个工作区。
        
    - 这时你需要保存一个 `.code-workspace` 文件来保存这些文件夹及其配置信息。
        
    - 适合管理相关的多个项目或模块。
        

---

### 工作区的特点

- **配置统一管理**  
    工作区可以保存特定的设置（如编辑器配置、调试配置、任务配置、扩展设置等），这些设置会覆盖全局用户设置，但仅对该工作区有效。
    
- **方便团队协作**  
    你可以将 `.code-workspace` 文件放入版本控制，这样团队成员打开同一工作区时会获得一致的环境配置。
    
- **支持多根目录**  
    方便管理多个相关文件夹，特别适合微服务、前后端分离项目或多个子模块的开发。
    

---

### `.code-workspace` 文件结构示例

```json
{
  "folders": [
    {
      "path": "frontend"
    },
    {
      "path": "backend"
    }
  ],
  "settings": {
    "editor.tabSize": 2,
    "files.exclude": {
      "**/*.log": true
    }
  }
}
```

- `folders`：定义工作区包含的文件夹路径
    
- `settings`：定义仅对该工作区生效的配置
    

---

### 如何创建工作区

1. 打开一个或多个文件夹
    
2. 在菜单栏选择 **文件 > 添加文件夹到工作区...**
    
3. 配置完成后，选择 **文件 > 另存为工作区**，将配置保存为 `.code-workspace` 文件
    
4. 以后打开该 `.code-workspace` 文件即可加载相应的工作区环境
    

---


## 在 VS Code Workspace 里指定编程语言的方法

### 1. 指定某种语言的默认设置（语言特定设置）

在 `.code-workspace` 的 `settings` 里，可以通过语言标识符（language identifier）来为该语言指定专属设置。

示例：

```json
{
  "folders": [
    { "path": "." }
  ],
  "settings": {
    "[python]": {
      "editor.tabSize": 4,
      "editor.formatOnSave": true
    },
    "[javascript]": {
      "editor.tabSize": 2
    }
  }
}
```

- `[python]` 代表针对 Python 语言的设置
    
- `[javascript]` 代表针对 JavaScript 的设置
    
- 这些只影响该工作区内相应语言文件的编辑行为
    

---

### 2. 关联文件扩展名到特定语言

如果你的项目里有自定义扩展名或没有被 VS Code 默认识别的文件类型，你可以在工作区设置里声明文件扩展名与语言的映射：

```json
{
  "folders": [
    { "path": "." }
  ],
  "settings": {
    "files.associations": {
      "*.myext": "python",
      "*.abc": "javascript"
    }
  }
}
```

- 这样打开 `.myext` 结尾的文件时，VS Code 会当作 Python 文件处理。
    
- 这个配置写在工作区设置里，只有打开这个工作区时生效。
    

---

### 3. 通过扩展配置语言服务器

如果你有安装语言扩展（比如 Python 插件、C++ 插件等），通常它们会自动根据语言文件识别启动语言服务器。如果需要自定义语言服务器参数，也可以在工作区设置里修改。

---

### 4. 用 `launch.json` 配置调试语言（间接指定）

在多语言项目中，你也可以在 `.vscode/launch.json` 或工作区调试配置里指定不同语言的调试器，比如 Python、Node.js、C++ 等。但这属于调试配置范畴，不是直接“指定语言”。

---

## 总结

|操作目标|配置位置|配置示例|说明|
|---|---|---|---|
|针对某语言设置编辑器参数|`.code-workspace` settings|`[python]`: {...}|只影响对应语言的编辑设置|
|关联自定义文件扩展名到语言|`.code-workspace` settings|`"files.associations": {...}`|让某扩展名文件用指定语言打开|
|指定调试语言环境|`.vscode/launch.json`|`"type": "python"`|用于调试，启动对应语言调试器|



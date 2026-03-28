---
title: uv
date: 2026-01-01
tags: [python]
---



## 简介

**uv** 是由 [Astral](https://astral.sh/) 团队（Ruff 的开发者）使用 Rust 编写的极速 Python 包和项目管理器。它旨在成为 pip、pip-tools、pipx、poetry、pyenv、virtualenv 等工具的统一替代方案。

### 核心特点

- 🚀 **极速**：比 pip 快 10-100 倍
- 📦 **统一管理**：集成包管理、虚拟环境、Python 版本管理于一体
- 🔒 **可靠的依赖解析**：生成跨平台的锁文件
- 💾 **全局缓存**：节省磁盘空间，避免重复下载
- 🔧 **兼容性**：支持 pip 命令和 `pyproject.toml`

---

## 安装

| 平台 | 命令 |
|------|------|
| macOS / Linux | `curl -LsSf https://astral.sh/uv/install.sh \| sh` |
| Windows | `powershell -c "irm https://astral.sh/uv/install.ps1 \| iex"` |
| pip | `pip install uv` |
| Homebrew | `brew install uv` |

验证：`uv --version`

---

## 常用命令

### 项目管理

#### 创建新项目

```bash
# 在新目录创建项目
uv init hello-world
cd hello-world

# 或在当前目录初始化
mkdir hello-world && cd hello-world
uv init
```

uv 会自动创建以下文件结构：

```
.
├── .gitignore
├── .python-version
├── README.md
├── main.py
└── pyproject.toml
```

#### 运行项目

```bash
# 运行 main.py
uv run main.py

# 运行带参数的脚本
uv run python script.py --arg value
```

首次运行时，uv 会自动创建虚拟环境 `.venv` 和锁文件 `uv.lock`。

### 依赖管理

```bash
# 添加依赖
uv add requests
uv add pandas numpy

# 添加开发依赖
uv add --dev pytest ruff

# 添加指定版本
uv add "requests>=2.28.0"

# 移除依赖
uv remove requests

# 同步依赖（根据锁文件安装）
uv sync

# 更新锁文件
uv lock
```

### Python 版本管理

```bash
# 查看可用的 Python 版本
uv python list

# 安装指定版本
uv python install 3.12

# 固定项目 Python 版本
uv python pin 3.12
```

### 包管理（pip 兼容模式）

```bash
# 安装包（类似 pip install）
uv pip install requests

# 从 requirements.txt 安装
uv pip install -r requirements.txt

# 生成 requirements.txt
uv pip compile pyproject.toml -o requirements.txt

# 查看已安装的包
uv pip list

# 卸载包
uv pip uninstall requests
```

### 工具管理（替代 pipx）

```bash
# 全局安装工具
uv tool install ruff
uv tool install black

# 运行工具（无需安装）
uvx ruff check .
uvx black --check .

# 查看已安装的工具
uv tool list
```

### 虚拟环境管理

```bash
# 创建虚拟环境
uv venv

# 指定 Python 版本创建
uv venv --python 3.12

# 指定目录
uv venv .venv-test
```

---

## 国内源配置

由于网络原因，建议配置国内镜像源以加速下载。

#### 1. **项目级配置**（仅当前项目，在 `pyproject.toml` 中）
```
[[tool.uv.index]]
url = "https://pypi.tuna.tsinghua.edu.cn/simple"
default = true  # 可选：替换官方 PyPI
```
#### 2.  命令行临时指定（单次）
```
uv pip install xxx --default-index https://pypi.tuna.tsinghua.edu.cn/simple
```
#### 3. **全局配置**
编辑用户级 `uv.toml` 文件：
- **Linux/macOS**：`~/.config/uv/uv.toml`
- **Windows**：`%APPDATA%\uv\uv.toml`（通常 `C:\Users\你的用户名\AppData\Roaming\uv\uv.toml`）

内容（以清华大学镜像为例，**完全替换官方 PyPI**）：
```
[[index]]
url = "https://pypi.tuna.tsinghua.edu.cn/simple"
default = true  # 这会排除官方 PyPI，即使镜像未同步某些包也会失败（适合完全信任镜像）
```

或者**优先国内镜像 + 官方 PyPI 作为备用**（更安全，推荐）：
```
[[index]]
url = "https://pypi.tuna.tsinghua.edu.cn/simple"
# 官方 PyPI 作为 fallback（默认就是这样，无需显式添加）
```
保存后生效，无需重启。

### 常见国内镜像（优先级：清华 > 阿里 > 腾讯）
- 清华大学：`https://pypi.tuna.tsinghua.edu.cn/simple`
- 阿里云：`https://mirrors.aliyun.com/pypi/simple/`
- 腾讯云：`https://mirrors.cloud.tencent.com/pypi/simple/`
- 豆瓣：`https://pypi.douban.com/simple/`
- 中科大：`https://pypi.mirrors.ustc.edu.cn/simple/`


## 快速参考

| 命令 | 说明 |
|------|------|
| `uv init` | 初始化项目 |
| `uv add <pkg>` | 添加依赖 |
| `uv remove <pkg>` | 移除依赖 |
| `uv sync` | 同步依赖 |
| `uv lock` | 更新锁文件 |
| `uv run <script>` | 运行脚本 |
| `uv python install` | 安装 Python |
| `uv venv` | 创建虚拟环境 |
| `uvx <tool>` | 运行工具 |

---

## 更多资源

- 📖 [官方文档](https://docs.astral.sh/uv/)
- 🐙 [GitHub 仓库](https://github.com/astral-sh/uv)
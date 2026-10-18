<a id="cjfcodexswitcher"></a>

<div align="center">

# CodexSwitcher · Codex 账号切换工具

**集中查看账号余量，按当前任务切换 Codex 账号。**

账号切换 · 余量查看 · CLI 操作 · 本地管理

[![中文说明](https://img.shields.io/badge/%E8%AF%B4%E6%98%8E-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-059669)](#readme-detail-17)
[![项目类型](https://img.shields.io/badge/%E9%A1%B9%E7%9B%AE-CLI-6366f1)](#readme-detail-17)
[![版本发布](https://img.shields.io/github/v/release/mileson/CodexSwitcher?display_name=tag)](https://github.com/mileson/CodexSwitcher/releases)
[![许可证](https://img.shields.io/github/license/mileson/CodexSwitcher)](./LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-3776AB?logo=python&logoColor=white)](./pyproject.toml)
[![Homebrew](https://img.shields.io/badge/Homebrew-installable-FBB040?logo=homebrew&logoColor=black)](https://github.com/mileson/homebrew-codexswitcher)
[![GitHub Stars](https://img.shields.io/github/stars/mileson/CodexSwitcher?style=social)](https://github.com/mileson/CodexSwitcher/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/mileson/CodexSwitcher)](https://github.com/mileson/CodexSwitcher/commits/main)
[![Downloads](https://img.shields.io/github/downloads/mileson/CodexSwitcher/total)](https://github.com/mileson/CodexSwitcher/releases)

[✨ 核心特性](#readme-detail-17) · [✅ 适用场景](#readme-detail-audience) · [🚀 一句话安装](#readme-detail-19) · [🧩 模块速查](#readme-detail-33) · [🔒 安全说明](#readme-detail-37) · [🚀 新手安装教程](#readme-detail-21)

</div>

---

多个 Codex 账号快速切换与余量查看工具




![CJFCodexSwitcher 截图](docs/images/overview.png)

<a id="readme-section-1"></a>

<a id="功能亮点"></a>

<a id="readme-detail-17"></a>

## ✨ 核心特性

- 实时查看所有账号的 5 小时 / 每周余量与下次重置时间
- 启动后直接进入账号列表页面，无需先进入主菜单
- 当前账号用 `[当前]` 标记，并固定显示在最前，同时与其他账号空一行区分
- 切换成功后自动刷新页面
- 多个账号并发实时刷新，减少等待时间
- 支持在余量页直接调用官方 `codex login` 添加新账号，并自动归档到切换器
- 提供 Agent 友好的非交互 CLI：`--list`、`--json`、`--best`、`--switch`、`--save-current`
- 项目内置专用 Skill，方便 Agent 按统一规则操作

<a id="readme-detail-audience"></a>

## ✅ 适用场景

适合需要管理多个 Codex 账号的使用者。

<a id="readme-section-2"></a>

<a id="一句话安装"></a>

<a id="readme-detail-19"></a>

## 🚀 一句话安装

从下面的现有入口开始，按顺序准备环境、配置并完成首次运行。

```bash
brew tap mileson/codexswitcher && brew install cjfcodexswitcher
```

```bash
pipx install git+https://github.com/mileson/CodexSwitcher.git
```

如果不用 `pipx`，也可以直接安装：

```bash
python3 -m pip install "git+https://github.com/mileson/CodexSwitcher.git"
```

<a id="readme-section-3"></a>

<a id="新手安装教程"></a>

<a id="readme-detail-21"></a>

## 🚀 新手安装教程

前置要求：

- Python 3.8+
- 本机可用 `codex` 命令

从源码安装：

```bash
git clone https://github.com/mileson/CodexSwitcher.git
cd CJFCodexSwitcher
python3 install.py
source ~/.zshrc  # 或 ~/.bashrc
codex-switcher
```

<a id="readme-section-4"></a>

<a id="使用说明"></a>

<a id="readme-detail-23"></a>

## 📚 使用说明

工具启动后会直接进入“查看所有账号余量”页面，并显示统一账号列表。

页面中的核心字段：

- `邮箱`：账号邮箱
- `SPACE`：账号当前主要 workspace / organization 标识
- `PLAN`：计划类型，例如 `TEAM`
- `5小时`：当前 5 小时额度剩余数量与下次重置时间
- `每周`：当前每周额度剩余数量与下次重置时间
- `[当前]`：当前正在使用的账号，并固定显示在最前

底部操作：

- `Enter`：刷新当前页面
- 输入 `a`：调用官方 `codex login` 添加账号，登录成功后自动归档并保持当前账号
- 输入 `#` 序号：切换到对应账号
- 输入 `0`：退出工具

说明：

- 当前账号如果尚未存档，进入查看余量页时会自动创建存档
- 添加账号复用官方浏览器登录流程；如果处于远程 / 无头环境，可手动使用 `codex login --device-auth`

<a id="readme-section-5"></a>

<a id="agent--cli-快捷命令"></a>

<a id="readme-detail-25"></a>

## 🔧 Agent / CLI 快捷命令

```bash
codex-switcher --list
codex-switcher --list --json
codex-switcher --best
codex-switcher --best --json
codex-switcher --switch 2
codex-switcher --switch user@example.com
codex-switcher --switch best
codex-switcher --switch best --json
codex-switcher --save-current
codex-switcher --refresh
```

排序规则：

1. 先按 5 小时剩余数量降序
2. 相同则按 1 周剩余数量降序
3. 最后按邮箱升序作为 tie-breaker

<a id="readme-section-6"></a>

<a id="技术栈"></a>

<a id="readme-detail-27"></a>

## 🏗️ 技术栈

CodexSwitcher 的实现按下列技术与模块组织，接入和维护时可据此定位。

| 层级 | 技术 |
|------|------|
| Runtime | Python 3 |
| Network | Python 标准库 `urllib` |
| Packaging | `pyproject.toml` + `setuptools` |
| UI | Terminal TUI |

<a id="readme-section-7"></a>

<a id="给-agent-的可复制提示词"></a>

<a id="readme-detail-29"></a>

## 🤖 给 Agent 的可复制提示词

```text
请帮我安装并配置 CJFCodexSwitcher，然后使用项目内 Skill `/Users/mileson/codex-switcher/.codex/skills/codex-switcher-help/SKILL.md` 作为操作规范。优先使用非交互 CLI，不要手动驱动 TUI。步骤要求：
1. 安装或校验 `codex-switcher` 命令可用
2. 运行 `codex-switcher --list --json` 检查账号列表
3. 运行 `codex-switcher --best --json` 判断当前最佳账号
4. 如有需要，运行 `codex-switcher --switch best --json`
5. 最后请你自己验证命令执行通过，并反馈：
   - 验证是否成功
   - 当前最佳账号是谁
   - 如果发生切换，切换到了哪个账号
   - 后续我还可以如何使用这个工具
```

<a id="readme-section-8"></a>

<a id="项目结构"></a>

<a id="readme-detail-31"></a>

## 📁 项目结构

下面按实现职责列出目录位置，便于把修改放回对应模块。

```text
CJFCodexSwitcher/
├── codex_switcher.py
├── codex-switcher.py
├── install.py
├── pyproject.toml
├── README.md
├── README_CN.md
├── .codex/skills/codex-switcher-help/
└── docs/
```

<a id="readme-section-9"></a>

<a id="仓库导航"></a>

<a id="readme-detail-33"></a>

## 🧩 模块速查

按要处理的工作选择入口，先看模块职责，再进入对应文件或目录。

| 模块入口 | 负责什么 | 什么时候看 |
| --- | --- | --- |
| [`docs/`](docs/) | 项目说明与参考文档 | 查阅运行、设计与维护约定 |
| [`pyproject.toml`](pyproject.toml) | Python 包与工具配置 | 核对依赖、工程目标与现有命令 |

<a id="readme-section-10"></a>

<a id="release"></a>

<a id="版本发布"></a>

<a id="readme-detail-35"></a>

## 📤 版本发布

当前推荐版本 release notes：

- [v0.1.10 版本说明](docs/releases/v0.1.10.md)

<a id="readme-section-11"></a>

<a id="安全说明"></a>

<a id="readme-detail-37"></a>

## 🔒 安全说明

更多信息见 [SECURITY.md](./SECURITY.md)

<a id="readme-section-12"></a>

<a id="贡献方式"></a>

<a id="readme-detail-39"></a>

## 🤝 贡献方式

更多信息见 [CONTRIBUTING.md](./CONTRIBUTING.md)

<a id="readme-section-13"></a>

<a id="license"></a>

<a id="许可证"></a>

<a id="readme-detail-41"></a>

## 📄 许可证

MIT

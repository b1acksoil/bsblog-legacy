---
title: GitHub CLI 的安装与使用
date: 2021-09-25 16:42:14
abbrlink: 42150d02
tags:
  - 工具
  - GitHub
  - CLI
categories:
  - 工具分享
top_img: https://cdn.jsdelivr.net/gh/b1acksoil/bsblog-assets/img/article/42150d02/top_img.jpg
cover: https://cdn.jsdelivr.net/gh/b1acksoil/bsblog-assets/img/article/42150d02/top_img.jpg
---

> GitHub CLI 是一个命令行工具，可将拉取请求、议题、GitHub Actions 和其他 GitHub 功能引入终端，使您可以在一个地方完成所有工作。

![GitHub CLI](https://cdn.jsdelivr.net/gh/b1acksoil/bsblog-assets/img/article/42150d02/preview.png)

GitHub CLI 包含许多 GitHub 功能，例如：
- 查看、创建(create)、克隆(clone)和复刻(fork)仓库
- 创建、关闭和列出议题(issue)和拉取请求(pull request)
- 审查、差异(diff)和合并(merge)拉取请求
- 运行、查看和列出工作流程(workflow)
- 创建、列出、查看和删除版本(release/tag)
- 创建、编辑、列出、查看和删除 Gist

# 安装

## Windows
在 Windows 系统上，可以通过包管理器或 `msi` 安装包的形式安装 CLI。

### 使用包管理器安装
#### WinGet

| 安装                | 升级                 |
| ------------------- | --------------------|
| `winget install gh` | `winget upgrade gh` |

#### scoop

| 安装                | 升级                |
| ------------------ | ------------------ |
| `scoop install gh` | `scoop update gh`  |

#### Chocolatey

| 安装                | 升级               |
| ------------------ | ------------------ |
| `choco install gh` | `choco upgrade gh` |

### 使用 msi 安装包安装
如果你此前并未听说或使用过 Windows 下的包管理器，也可以通过下载独立的 `msi` 安装包的形式安装 CLI。

最新的安装包可以到 [GitHub Release](https://github.com/cli/cli/releases/latest) 下载 `gh_<version>_windows_<arch>.msi`。

## Linux & BSD
Linux 上由于发行版众多，包管理器不统一，写起来篇幅过长，可以去 GitHub CLI 的官方仓库查看[安装说明](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)

也可以去 [GitHub Release](https://github.com/cli/cli/releases/latest) 上下载最新的安装包或二进制文件。(deb/rpm/.tar.gz)

对于 Termux，直接 `pkg install gh` 即可。

## macOS

对于 macOS，可以使用包管理器或去 [GitHub Release](https://github.com/cli/cli/releases/latest) 上下载最新的二进制文件。(.tar.gz)

### 使用包管理器
#### Homebrew

| 安装               | 更新:             |
| ----------------- | ----------------- |
| `brew install gh` | `brew upgrade gh` |

#### MacPorts

| 安装                    | 更新                  |
| ---------------------- | --------------------- |
| `sudo port install gh` | `sudo port selfupdate && sudo port upgrade gh` |

#### Conda

| 安装            | 更新               |
|----------------|--------------------|
| `conda install gh --channel conda-forge` | `conda update gh --channel conda-forge` |

更多的 Conda 安装选项可以参考 [gh-feedstock 页面](https://github.com/conda-forge/gh-feedstock#installing-gh)。

## 检查安装
按照上面的步骤安装成功后，可以输入以下命令来检查是否安装成功：
```bash
$ gh --version
gh version 2.0.0 (2021-08-24)
https://github.com/cli/cli/releases/tag/v2.0.0
```
如果出现和上面类似的提示信息，则已安装成功。

# 登录
成功安装 GitHub CLI 后，我们需要先进行登陆：
```bash
$ gh auth login

# 使用上下箭头选择，回车键确认
# 选择登陆的服务器，一般选择 GitHub.com
? What account do you want to log into?  [Use arrows to move, type to filter]
> GitHub.com
  GitHub Enterprise Server

# 选择进行 git 操作使用的协议，若已配置 ssh 则可以选择 SSH ，其他情况下选择 HTTPS
? What is your preferred protocol for Git operations?  [Use arrows to move, type to filter]
> HTTPS
  SSH

# 如果选择 HTTPS
# 是否使用 GitHub 的证书验证 git，推荐选择是
# 输入 y 或 n 并回车确认
? Authenticate Git with your GitHub credentials? (Y/n)

# 如果选择 SSH
# 是否将 SSH 公钥绑定到 GitHub 账号上
# 选择 ssh 公钥的路径，若以前进行过绑定则可以选择 Skip 跳过
? Upload your SSH public key to your GitHub account?  [Use arrows to move, type to filter]
> /home/b1acksoil/.ssh/id_rsa.pub
  Skip

# 选择验证 GitHub CLI 的方式
# 一般选择第一个（浏览器内验证）即可，如果以前在 https://github.com/settings/tokens 生成过令牌也可以选择第二个直接粘贴验证
? How would you like to authenticate GitHub CLI?  [Use arrows to move, type to filter]
> Login with a web browser
  Paste an authentication token

# 记下给出的一次性的八位验证码，随后按回车键打开验证页面
! First copy your one-time code: 0287-9E22
- Press Enter to open github.com in your browser...
```

![输入验证码](https://cdn.jsdelivr.net/gh/b1acksoil/bsblog-assets/img/article/42150d02/device-auth-code.png)

输入八位验证码后点击 Continue

![确认信息](https://cdn.jsdelivr.net/gh/b1acksoil/bsblog-assets/img/article/42150d02/device-auth-check.png)

点击 Authorize github，并确认密码，完成

![验证完成](https://cdn.jsdelivr.net/gh/b1acksoil/bsblog-assets/img/article/42150d02/device-auth-done.png)

此时终端内出现以下信息：

```bash
# 按回车键继续
✓ Authentication complete. Press Enter to continue...

- gh config set -h github.com git_protocol ssh
✓ Configured git protocol
✓ Uploaded the SSH key to your GitHub account: /home/b1acksoil/.ssh/id_rsa.pub
✓ Logged in as b1acksoil
```
恭喜，你已经登录成功了！

{% note info %}
**Tips:** 以后也可以使用 `gh auth status` 查看登录状态，`gh auth logout` 登出。
{% endnote %}

# 使用
由于篇幅限制，本节只介绍较为常用的几种命令。更多的使用方法及详细说明请前往[官方手册](https://cli.github.com/manual/)查看。

关于各个命令的参数帮助，可以使用 `gh 命令 --help` 查看。如 `gh repo create --help`。

## 仓库操作
### 创建
使用 `gh repo create` 在本地和 GitHub 服务器上同步创建创建一个仓库。

用法：
```bash
$ gh repo create [<name>] [flags]
```

示例：
```bash
# 使用当前目录的名称创建仓库
$ git init my-project
$ cd my-project
$ gh repo create

# 指定名称创建仓库
$ gh repo create my-project

# 在组织(organization)中创建仓库
$ gh repo create cli/my-project

# 关闭仓库的 issues，wiki 功能
$ gh repo create --enable-issues=false --enable-wiki=false
```

### 克隆
使用 `gh repo clone` 将 GitHub 上的仓库克隆到本地。

用法：
```bash
$ gh repo clone <repository> [<directory>] [-- <gitflags>...]
```

示例：
```bash
# 克隆当前登录账号下的仓库
$ gh repo clone mgs-site

# 克隆指定仓库 (owner/repo)
$ gh repo clone ppy/osu

# 使用 git 选项
# 注：git 选项前需要加上 '--'，例如
$ gh repo clone ppy/osu -- --depth=1
```

### 查看
使用 `gh repo view` 命令查看仓库的信息。

用法：
```bash
$ gh repo view [<repository>] [flags]
```

示例：
```bash
# 查看 b1acksoil(拥有者) 的 mgs-site(仓库名)
$ gh repo view b1acksoil/mgs-site

# 查看当前处于的仓库
$ gh repo view

# 在浏览器中打开（使用 -w 或 --web）
$ gh repo view --web
```

### Fork
使用 `gh repo fork` 命令 Fork 一个仓库。

用法：
```bash
$ gh repo fork [<repository>] [-- <gitflags>...] [flags]
```

示例：
```bash
# Fork 仓库 ppy/osu 并克隆到本地
$ gh repo fork ppy/osu

# Fork 当前处于的仓库
$ gh repo fork

# Fork 但不克隆到本地
$ gh repo fork ppy/osu --clone=false
```

## Pull Requests
### 创建
使用 `gh pr create` 命令创建一个 Pull Request。

用法：
```bash
$ gh pr create [flags]
```

示例：
```bash
# 指定标题和内容
$ gh pr create --title "The bug is fixed" --body "Everything works again"

# 分开输入标题和内容
$ gh pr create
Creating pull request for feature-branch into main in owner/repo
? Title <标题>
? Body [(e) to launch nano, enter to skip]
http://github.com/owner/repo/pull/1
```

### 合并
使用 `gh pr merge` 命令合并一个 Pull Request。

用法：
```bash
$ gh pr merge [<number> | <url> | <branch>] [flags]
```

示例：
```bash
# 合并 id 为 5 的 Pull Request
$ gh pr merge 5

# 合并名为 dev 的分支
$ gh pr merge dev
```

### 状态
使用 `gh pr status` 查看当前仓库的 Pull Requests 状态。

用法：
```bash
$ gh pr status [flags]
```

示例：
```bash
$ gh pr status
Current branch
  #12 Remove the test feature [user:patch-2]
   - All checks failing - Review required

Created by you
  You have no open pull requests

Requesting a code review from you
  #13 Fix tests [branch]
  - 3/4 checks failing - Review required
  #15 New feature [branch]
   - Checks passing - Approved
```

### 查看
使用 `gh pr view` 命令查看指定的 Pull Request 信息。

用法：
```bash
$ gh pr view [<number> | <url> | <branch>] [flags]
```

示例：
```bash
# 查看 id 为 5 的 Pull Request
$ gh pr view 5

# 在浏览器内查看（使用 -w 或 --web）
$ gh pr view 5 --web

# 查看当前分支的 PR
$ gh pr view
```

## Issues
### 创建
使用 `gh issue create` 命令创建 Issue

用法：


示例：
```bash
# 指定标题和内容创建
$ gh issue create --title "I found a bug" --body "Nothing works"

# 分开输入标题和内容
$ gh issue create
Creating issue in owner/repo
? Title <标题>
? Body [(e) to launch nano, enter to skip]
http://github.com/owner/repo/issues/1

# 指定标签创建（可使用多个 --label，若写在一起则用逗号分隔）
$ gh issue create --label "bug,help wanted"
$ gh issue create --label bug --label "help wanted"
```

### 关闭
使用 `gh issue close` 关闭一个 Issue。

用法：
```bash
$ gh issue close {<number> | <url>} [flags]
```

示例：
```bash
# 关闭 id 为 2 的 issue
$ gh issue close 2
```

### 查看
使用 `gh issue view` 命令查看指定的 Pull Request 信息。

用法：
```bash
$ gh issue view {<number> | <url>} [flags]
```

示例：
```bash
# 查看 id 为 20 的 issue
$ gh issue view 20

# 在浏览器内查看（使用 -w 或 --web）
$ gh issue view 5 --web
```

GitHub CLI 还有很多实用的功能，如 `gh release`，`gh browse`，`gh workflow` 等等。可以前往[官方手册](https://cli.github.com/manual/)获取更多信息。

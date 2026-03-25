<span style="font-size:1.2em; margin-right:8px; color:#000;">&#xf70e;</span> # MkDocs 建站教程

### 一、完整操作步骤（Windows 系统，文件存放 D 盘）

#### 1. 环境准备（前提：安装 Python）

mkdocs 是 Python 编写的工具，需先安装 Python（建议 3.8+），安装时务必勾选「Add Python to PATH」。

验证 Python 安装：

bash

```
# 打开CMD命令提示符，执行
python --version  # 或 python3 --version
pip --version     # 验证pip是否可用
```

安装 mkdocs：

bash

```
pip install mkdocs  # 核心工具
pip install mkdocs-material  # 推荐美观的主题（可选，提升网站颜值）
```

#### 2. 在 D 盘创建 mkdocs 项目

bash

```
# 1. 切换到D盘
D:

# 2. 创建mkdocs项目（项目名自定义，比如my-github-site）
mkdocs new my-github-site

# 3. 进入项目目录（后续操作都在这个目录下）
cd my-github-site
```

项目创建后，D 盘会生成 `D:\my-github-site` 目录，结构如下：

已生成代码

#### 3. 配置 mkdocs（修改 mkdocs.yml）

打开 `D:\my-github-site\mkdocs.yml`，替换为以下内容（基础配置，可按需修改）：

yaml

```
# 网站标题
site_name: 我的个人网站
# 网站描述（可选）
site_description: 基于mkdocs+GitHub Pages的个人站点
# 使用Material主题（需提前安装mkdocs-material）
theme:
  name: material
# 导航栏配置（对应docs下的markdown文件）
nav:
  - 首页: index.md
  - 关于我: about.md  # 后续可在docs下创建about.md
# 代码高亮（可选）
markdown_extensions:
  - codehilite
  - toc:
      permalink: true
```

#### 4. 编写 Markdown 内容

- 修改首页：编辑 `D:\my-github-site\docs\index.md`，替换默认内容为你的个人介绍、博客等。
- 添加新页面：比如在 docs 目录下创建 `about.md`，写入你的个人信息，导航栏会自动匹配（对应上面 yml 的配置）。

#### 5. 本地预览网站（验证效果）

bash

```
# 在项目目录（D:\my-github-site）下执行
mkdocs serve
```

执行后会提示：`Serving on http://127.0.0.1:8000`，打开浏览器访问该地址，即可实时预览 Markdown 转成的 Web 页面（修改 md 文件后刷新页面即可生效）。

#### 6. 构建静态 Web 文件

本地预览无误后，生成最终的静态 HTML 文件（存放在 site 目录）：

bash

```
# 在项目目录下执行
mkdocs build
```

执行后，`D:\my-github-site` 会生成 `site` 目录，里面是完整的静态 Web 文件（可直接部署到任何 Web 服务器）。

#### 7. 部署到 GitHub 生成个人网站

##### 步骤 1：创建 GitHub 仓库

- 打开 GitHub，新建仓库，仓库名必须为：`你的GitHub用户名.github.io`（比如我的用户名是 test123，仓库名就是 test123.github.io）。
- 仓库设置为公共（Public），勾选「Add a README file」（可选）。

##### 步骤 2：关联本地项目到 GitHub 仓库

bash

```
# 1. 在项目目录（D:\my-github-site）初始化git仓库
git init

# 2. 关联远程GitHub仓库（替换为你的仓库地址）
git remote add origin https://github.com/你的用户名/你的用户名.github.io.git

# 3. 提交所有文件
git add .
git commit -m "初始化mkdocs项目"

# 4. 推送到GitHub（首次推送可能需要登录GitHub账号）
git push -u origin main  # 若默认分支是master，替换为master
```

##### 步骤 3：部署静态文件到 GitHub Pages

方式 1：使用 mkdocs 自带的部署命令（推荐）

bash

```
# 在项目目录下执行（自动将site目录的内容部署到GitHub Pages）
mkdocs gh-deploy
```

方式 2：手动上传 site 目录（备用）

- 进入 `D:\my-github-site\site` 目录，将所有文件上传到 GitHub 仓库的 `main`（或 `gh-pages`）分支。

##### 步骤 4：访问个人网站

部署完成后，等待 1-2 分钟，访问 `https://你的用户名.github.io`，即可看到你的 Markdown 转成的 Web 网站。

### 二、关键注意事项

1. **路径问题**：全程确保操作目录在 D 盘的项目文件夹下（`D:\my-github-site`），避免路径错误导致文件生成到其他盘。
2. **GitHub 仓库命名**：必须是 `用户名.github.io`，否则无法作为个人网站访问。
3. **部署失败排查**：
    
    - 检查 git 是否已登录（`git config --global user.name`/`git config --global user.email`）。
    - 确保 mkdocs build 生成的 site 目录完整，无报错。
    - 查看 GitHub 仓库的 Settings → Pages，确认部署源是 gh-pages 分支（mkdocs gh-deploy 会自动创建）。
    

### 总结

1. 核心流程：D 盘创建 mkdocs 项目 → 配置 yml → 编写 Markdown → 本地预览 → 构建静态文件 → 部署到 GitHub Pages。
2. 关键配置：mkdocs.yml 决定网站主题和导航，仓库命名必须为「用户名.github.io」。
3. 部署方式：推荐使用`mkdocs gh-deploy`自动部署，无需手动处理静态文件。
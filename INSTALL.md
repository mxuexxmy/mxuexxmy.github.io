# 环境安装指南

这是一个 Jekyll 项目，需要安装 Ruby 和 Bundler 才能运行。

## 安装步骤

### 方法 1: 使用 Snap（推荐，简单快速）

```bash
# 安装 Ruby
sudo snap install ruby --classic

# 安装 Bundler
sudo gem install bundler

# 安装项目依赖
cd /home/lx/project/mxuexxmy.github.io
bundle install
```

### 方法 2: 使用 apt（系统包管理器）

```bash
# 更新包列表
sudo apt update

# 安装 Ruby 和开发工具
sudo apt install -y ruby ruby-dev build-essential

# 安装 Bundler
sudo gem install bundler

# 安装项目依赖
cd /home/lx/project/mxuexxmy.github.io
bundle install
```

### 方法 3: 使用 rbenv（推荐用于开发，可管理多个 Ruby 版本）

```bash
# 安装 rbenv 和 ruby-build
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/HEAD/bin/rbenv-installer | bash

# 添加到 PATH（添加到 ~/.bashrc 或 ~/.zshrc）
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc

# 安装 Ruby（推荐使用 3.1 或更高版本）
rbenv install 3.1.0
rbenv global 3.1.0

# 安装 Bundler
gem install bundler

# 安装项目依赖
cd /home/lx/project/mxuexxmy.github.io
bundle install
```

## 验证安装

安装完成后，运行以下命令验证：

```bash
ruby --version
bundler --version
bundle install
```

## Ruby 3.4+ 兼容性说明

如果你使用的是 Ruby 3.4 或更高版本，项目已经配置了必要的依赖（csv、logger、base64、bigdecimal、webrick），这些在 Ruby 3.4+ 中不再是默认 gem。

如果遇到 `Gemfile.lock` 版本不匹配的问题（例如从 Windows 迁移到 Linux），可以删除并重新生成：

```bash
rm Gemfile.lock
bundle install
```

## 运行项目

安装完成后，可以使用以下命令启动 Jekyll 服务器：

```bash
bundle exec jekyll serve
```

然后在浏览器中访问 `http://localhost:4000` 查看网站。

## 常见问题

### 问题：Bundler 版本不匹配

如果遇到 Bundler 版本错误，安装最新版本的 Bundler：

```bash
gem install bundler
```

### 问题：缺少标准库 gem（Ruby 3.4+）

如果遇到 `cannot load such file` 错误，确保 `Gemfile` 中已包含所需的标准库 gem。本项目已配置了所有必需的依赖。


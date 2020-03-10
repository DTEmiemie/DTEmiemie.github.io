---
title: 使用数据文件 和 git 子模块 更新 NexT 主题
categories:
  - 博客
date: 2020-03-10 23:51:30
tags:
---

{% note danger %}

#### 要求：Hexo 版本号 3.0 以上

{% endnote %}

# Data Files

### Data Files 的使用场景

> 官方文档：
> 有时您可能需要在主题中使用某些资料，而这些资料并不在文章内，并且是**需要重复使用**的，那么您可以考虑使用 Hexo 3.0 新增的「数据文件」功能。此功能会载入 `source/_data` 内的 **YAML** 或 **JSON** 文件，如此一来您便能在网站中复用这些文件了。

如上，每次更新NexT主题，为保证主题 NexT 文件夹下的配置文件 `_config.yml` 不需要手动修改，可以复用，所以采取使用 **Data Files** 

## 步骤

1. 复制正在使用的 `_config.yml` （`/themes/next`）到 `source/_data` (站点目录下的 `source` 目录)
   {% note default %}

   如果没有 `_data` 就创建一个 `_data` 文件夹置于站点目录里的 `source/` 下
   {% endnote %}

2. 把 `themes/` 目录下的 NexT 文件夹备份一个，然后删除，以便于克隆子模块命令顺利进行 （可选）

3. 在 `themes/` 目录下输入

   ```bash
   $ git submodule add https://github.com/theme-next/hexo-next/hexo-theme-next next
   ```

   此时显示

   ```bash
   Cloning into '$YourThemes/next'...
   remote: Enumerating objects: 42, done.
   remote: Counting objects: 100% (42/42), done.
   remote: Compressing objects: 100% (42/42), done.
   remote: Total 12121 (delta 10), reused 13 (delta 0), pack-reused 12079
   Receiving objects: 100% (12121/12121), 6.74 MiB | 134.00 KiB/s, done.
   Resolving deltas: 100% (7775/7775), done.
   warning: LF will be replaced by CRLF in .gitmodules.
   The file will have its original line endings in your working directory
   ```

   等待完成后，输入 `git status`

   ```bash
   $ git status
   On branch master
   Your branch is up-to-date with 'origin/master'.
   
   Changes to be committed:
     (use "git reset HEAD <file>..." to unstage)
   
   	new file:   .gitmodules
   	new file:   next
   ```

   子模块添加完成

4. 重新生成去 `localhost:4000` 看看是否Ok

   ```bash
   $ hexo clean && hexo g && hexo s
   ```



{% note danger %}

### 如果你的语言未显示中文！

手动调整子模块 `/themes/next/languages` 目录下的 `zh-CN.yml` ，将其与 站点目录下的 `_config.yml` 里的 `language:` 配置保持一致！

{% endnote %}
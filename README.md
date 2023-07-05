# [Hugo Portfolio Theme](https://github.com/wowchemy/starter-hugo-portfolio-theme)

[![Screenshot](./preview.png)](https://wowchemy.com/hugo-themes/)

The **Hugo Portfolio Template** empowers you to easily create a portfolio website. Make it your own by choosing a color theme and grid layout!

️**Trusted by 250,000+ researchers, educators, and students.** Highly customizable via the integrated **no-code, widget-based Wowchemy page builder**, making every site truly personalized ⭐⭐⭐⭐⭐

[![Get Started](https://img.shields.io/badge/-Get%20started-ff4655?style=for-the-badge)](https://wowchemy.com/hugo-themes/)
[![Discord](https://img.shields.io/discord/722225264733716590?style=for-the-badge)](https://discord.com/channels/722225264733716590/742892432458252370/742895548159492138)  
[![Twitter Follow](https://img.shields.io/twitter/follow/wowchemy?label=Follow%20on%20Twitter)](https://twitter.com/wowchemy)

[Check out the latest demo](https://hugo-portfolio-theme.netlify.app/) of what you'll get in less than 10 minutes, or [view the showcase](https://wowchemy.com/creators/).

The integrated [**Wowchemy**](https://wowchemy.com) website builder and CMS makes it easy to create a beautiful website for free. Edit your site in the CMS (or your favorite editor), generate it with [Hugo](https://github.com/gohugoio/hugo), and deploy with GitHub or Netlify. Customize anything on your site with widgets, light/dark themes, and language packs.

- 👉 [**Get Started**](https://wowchemy.com/hugo-themes/)
- 📚 [View the **documentation**](https://wowchemy.com/docs/)
- 💬 [Chat with the **Wowchemy research community**](https://discord.gg/z8wNYzb) or [**Hugo community**](https://discourse.gohugo.io)
- ⬇️ **Automatically import citations from BibTeX** with the [Hugo Academic CLI](https://github.com/wowchemy/hugo-academic-cli)
- 🐦 Share your new site with the community: [@wowchemy](https://twitter.com/wowchemy) [@GeorgeCushen](https://twitter.com/GeorgeCushen) [#MadeWithWowchemy](https://twitter.com/search?q=%23MadeWithWowchemy&src=typed_query)
- 🗳 [Take the survey and help us improve #OpenSource](https://forms.gle/NioD9VhUg7PNmdCAA)
- 🚀 [Contribute improvements](https://github.com/wowchemy/wowchemy-hugo-themes/blob/main/CONTRIBUTING.md) or [suggest improvements](https://github.com/wowchemy/wowchemy-hugo-themes/issues)
- ⬆️ **Updating?** View the [Update Guide](https://wowchemy.com/docs/hugo-tutorials/update/) and [Release Notes](https://github.com/wowchemy/wowchemy-hugo-themes/releases)

## We ask you, humbly, to support this open source movement

Today we ask you to defend the open source independence of the Wowchemy website builder and themes 🐧

We're an open source movement that depends on your support to stay online and thriving, but 99.9% of our creators don't give; they simply look the other way.

[❤️ Click here to become a GitHub Sponsor, unlocking awesome perks such as _exclusive academic templates and widgets_](https://github.com/sponsors/gcushen)

# 配置方法（Win）

## 配置Go环境

- [下载Go环境安装包](https://go.dev/dl/)

- 解压到`./go`，将`./go/bin`加入系统环境变量，使用```go version```查看版本

## 配置Hugo

- [下载extended版本的Hugo](https://github.com/gohugoio/hugo/releases)
- 将解压得到的exe文件放到`./hugo/bin`中，并加入到环境变量，使用```hugo version```查看版本

## 创建项目

- 克隆喜欢的hugo项目模板
- 在本地项目根目录下直接使用```hugo server -D```即可预览效果
  
## 部署网页

- 新建`.github/workflows/gh-pages.yml`，内容如下

```
name: github pages
 
on:
  push:
    branches:
      - main  # Set a branch that will trigger a deployment
  pull_request:
 
jobs:
  deploy:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod
 
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true
 
      - name: Build
        run: hugo --minify
 
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

- 根据仓库名修改`config.yaml`中的`baseURL: 'https://polarispw.github.io/' # Website URL`
- 执行如下指令

```

hugo                      // 发布网站到public目录中，Hugo建站的时候会读取public目录中的内容
git add .                 // 将所有内容添加到本地git仓库中
git commit -m "site init" // 提交信息
// 创建gh-pages分支
// GitHub Actions会从main分支获取内容执行一些操作，生成的内容会推送到gh-pages分支
git checkout --orphan gh-pages
git push -u origin main   // 将本地网站推送至远程库
```

- 进入仓库设置，`Pages/Build and deployment | Source: Deploy from a branch | Branch: gh-pages`
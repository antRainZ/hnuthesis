# 说明
记录自己写论文时，使用记录, 项目基本结构参考[湖南大学硕士学位论文 LaTeX 模板](https://github.com/hnuthesis/hnuthesis)


## 关键文件说明

- `main.tex`: 主文件，编译入口；
- `hnuthesis.cls`: 撰写规范，需要调整格式在该文件中对应修改；
- `references.bib`: 参考文献列表；
- `chapters/`: 论文章节文件夹，分章有利于保持 TeX 文件的整洁；
- `figures/`: 插图文件夹，LaTeX 支持多种格式，如 EPS、PDF、PNG 等；
- `main.pdf`: 编译生成的论文 PDF 文件；
- `main-for-word.pdf`: 编译生成的适用于转 Word 的论文 PDF 文件（栅格化公式，防止转 Word 后*不忍直视*）。

## 编译

### 1. 本地编译（版本最新，推荐）

1. 安装 LaTeX 发行版；

2. 对于非 Windows 系统，需要额外安装字体，以 Debian/Ubuntu 为例：

   ```bash
   sudo apt-get update

   # 自动同意 Microsoft EULA 并安装 ttf-mscorefonts-installer
   echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | sudo debconf-set-selections
   sudo apt-get install -y ttf-mscorefonts-installer

   # 手动下载安装 SimSun（中易宋体）、SimHei（中易黑体）字体
   mkdir simfonts && wget -qO- https://github.com/yusanshi/hnuthesis/files/6371620/SimFonts.tar.gz | tar xz -C simfonts
   mkdir -p ~/.local/share/fonts && mv simfonts ~/.local/share/fonts
   fc-cache -f
   ```

3. 下载模板：

   ```bash
   git clone https://github.com/yusanshi/hnuthesis
   cd hnuthesis
   ```

4. 编译主版本：

   ```bash
   latexmk -xelatex -shell-escape main.tex
   ```

   或者在 vscode 下安装 [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) 插件后 _complie on save_（本项目的 `.vscode/settings.json` 已经对其做了配置）。

5. 编译主版本和转 Word 版：

   ```bash
   ./run.sh
   ```

   > 注意：脚本的运行需要 Unix style 的命令行环境，对于 Windows 用户，可以使用安装完 Git 客户端之后的 Git Bash。

### 2. Overleaf（版本可能较旧）

<https://www.overleaf.com/latex/templates/hu-nan-da-xue-shuo-shi-xue-wei-lun-wen-latex-mo-ban-hnuthesis/dbjwjghhvmmd>

### 3. GitHub Actions

1. 通过 `Use this template` 或 Fork 创建项目；

2. 通过 push tag 触发 compile & publish 过程，如：

   ```
   git tag v0.x.x
   git push --tags
   ```

   待 GitHub Actions 结束后在 releases 中下载新编译的 `main.pdf` 和 `main-for-word.pdf` 文件。

   ![image](https://user-images.githubusercontent.com/36265606/116044616-b6b30e00-a6a3-11eb-82ff-e8bba576da16.png)

## 转 Word 文件

使用 <https://www.adobe.com/hk_zh/acrobat/online/pdf-to-word.html> 转换 `main-for-word.pdf` 文件。第二次转换文件时需要登录 Adobe 账号才能下载，建议在浏览器的“无痕浏览”“隐私模式”等模式下访问以跳过强制登录。


# overleaf 使用记录
+ [overleaf中如何设置宋体](https://blog.csdn.net/weixin_45893881/article/details/135082097)

# 相关工具

## 英文润色
+ [在线语法检查器(edge ctrl+shift+n 无痕模式打开)](https://wordvice.ai/cn/proofreading/)

## 符号自查
+ `[，。、？！；]{2}` 连续的字符出现

# 参考
+ [GB/T 7714-2015 参考文献著录和标注的biblatex样式包](https://github.com/hushidong/biblatex-gb7714-2015)
+ [清华大学学位论文 LaTeX 模板，包括本科综合论文训练、硕士论文、博士论文以及博士后出站报告.](https://github.com/tuna/thuthesis)
+ [LaTeX 入门与进阶](https://latex.lierhua.top/)


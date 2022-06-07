# `PKUMpLtX`, [项目页]
*A LaTeX document class for 'Modern Physics Laboratory' in PKU based on [`revtex4-2`]*

+ Copyright (C) 2013. Modern Phys. Lab, School of Phys., Peking Univ.
+ Copyright (C) Sun Sibai <niasw_at_pku.edu.cn>
+ Copyright (C) Cao Chuanwu <>
+ Copyright (C) 2021--2022. Lin Xuchen <linxc_at_pku.edu.cn>

This work is licensed under the Creative Commons Attribution-ShareAlike 4.0 International
License. To view a copy of this license, visit [`LICENSE.md`]
or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

希望本模板能帮助同学们专注报告内容, 减少对格式等的不必要的时间消耗.

- [下载](#下载)
  - [\[可选\] 安装](#可选-安装)
- [文件内容](#文件内容)
- [使用方法](#使用方法)
  - [字体选项](#字体选项)
  - [标点选项](#标点选项)
  - [编译](#编译)
- [自动调用的宏包](#自动调用的宏包)
  - [其他需要注意的外部宏包](#其他需要注意的外部宏包)
- [反馈](#反馈)

## 下载

+ 稳定版: 前往 [Releases](https://github.com/CastleStar14654/PKUMpLtX/releases) 页面下载最新版本的 `Source code` 文件.
+ 最新: 在[项目页]下载最新源代码.
+ `git clone`: 如果会使用 git, 可以直接 `git clone` 本项目. 之后可以直接 `pull` 获取更新.

### \[可选\] 安装

+ 不想折腾的话直接将 [`mpltx.cls`] 复制/链接到编写报告的当前文件夹, 然后按[使用方法](#使用方法)中描述的那样在 `*.tex` 中调用即可.
+ 如果想要正经地安装这个宏包, 从而不用每次手动复制/链接:
  + 请找到用户的 $\mathrm{\TeX}$ 根目录位置 (`$TEXMF`).
    + 保险起见, 建议创建一个新的供自定义宏包使用的 `$TEXMF`. 不同的发行版可能有不同的创建方式, 比如 $\mathrm{MiK\TeX}$ 的相关文档是[这个页面](https://miktex.org/faq/local-additions).
  + 将整个 `PKUMpLtX` 文件夹移动到 `$TEXMF/tex/latex`.
    + 所以, 实际上可以直接在 `$TEXMF/tex/latex` 进行 `git clone`.
  + 可能需要刷新缓存.

## 文件内容

+ [`mpltx.cls`]\: 模板文件.
+ `README.md`: 本文件, 说明文档.
+ [`template.tex`], [`template.pdf`]: 示例报告模板兼说明文档.
  + [`bibli.bib`]\: 用于参考文献生成的文件.
  + [`fig/`]\: 示例报告用到的图片.
+ [`figgen.py`]\: 生成其中一张图片用的脚本.
  + [`fig.mplstyle`]\: 相应的格式设置.

## 使用方法

只需将 [`mpltx.cls`] 复制/链接到当前文件夹, (如果[安装](#可选-安装)了, 则不用做复制或链接), 然后使用该文档类
```latex
\documentclass[<options>]{mpltx}
```
`[<options>]` 为可选的选项列表, 可以给入标准文档类 `article` 以及 [`revtex4-2`] 可接受的任何参数.
但只建议传 [`mpltx.cls`] 定义的中文字体参数和标点符号参数 (见下).
使用前推荐先仔细查看 [`template.tex`] 和 [`template.pdf`] 文件.
如果有魔改需求可以自定义 [`mpltx.cls`]

如果初次使用 $\mathrm{\LaTeX{}}$, 推荐以下入门文档:
1. [lshort-zh-cn]
2. [lnotes2]

### 字体选项
+ `default`: 默认选项, 使用 [`xeCJK`] 默认的开源 Fandol 字体.
  需要安装 [`fandol`] 宏包. 如果你使用 Overleaf, 用这个选项或者下方的 `notofandol` 都可以.
+ `noto`: 使用 Noto CJK SC 系列的宋体与黑体. 这是一款优秀的开源中文字体, 可在[其主页](https://github.com/googlefonts/noto-cjk/releases)下载最新版的 Noto CJK Serif SC (即思源宋体) 和 Noto CJK Sans SC (即思源黑体),
  或者安装 [`notocjksc`] 宏包也可以 (但宏包的字体版本是 18 年的).
  但仿宋体和楷体 Noto 未提供, 故将自动使用 Windows 或 macOS 自带的相应字体. **Linux 用户很可能会因为没有相应的商业仿宋体和楷体字体而出错**, 请改用下方的 `notofandol`, 或改用 `diy` 自行使用 `\setCJK*font` 等命令配置.
  + `notofandol`: 用 Fandol 的仿宋体和楷体搭配 Noto 系列的宋体与黑体.
+ `windows`: 使用 Windows 系统自带字体 (宋体为中易宋体, 粗体为华文中宋; 黑体为等线).
+ `macos`: 使用 macOS 系统自带字体 (黑体为苹方).
+ `diy`: 自己使用 `\setCJK*font` 命令配置.

比如, Windows 用户就可以这样子调用
```latex
\documentclass[windows]{mpltx}
```

各平台可以支持的字体选项如下 (叹号表示需要安装特定的字体宏包获开源字体)
|    选项    | Windows | macOS | Linux | Overleaf |
| :--------: | :-----: | :---: | :---: | :------: |
|  default   |   ✓!    |  ✓!   |  ✓!   |    ✓     |
|    noto    |   ✓!    |  ✓!   |   ✗   |    ✗     |
| notofandol |   ✓!    |  ✓!   |  ✓!   |    ✓     |
|  windows   |    ✓    |   ✗   |   ✗   |    ✗     |
|   macos    |    ✗    |   ✓   |   ✗   |    ✗     |
|    diy     |    ✓    |   ✓   |   ✓   |    ✓     |

### 标点选项
报告要求是 "全文标点符号除 '顿号' 外, 其他用英文半角标点符号".
但也可能有人想使用全角标点, 或者使用全角标点但把句号从 "。" 改为 "．".
+ 如果你想完全用半角标点, 不用任何选项, 直接用半角标点输入.
+ 如果你想完全用符合 GB/T 15834-2011 的全角标点, 直接用全角标点输入.
+ 如果你想像 GB/T 15834-1995 所说, "在科技文档中用实心全角圆点 '．' 替代句号 '。'", 
  + 如果你有方便的直接输入 "．" 的方法, 直接输入;
  + 如果没有, 使用 `quanjiao` 选项, 在源文件中直接用 "。" 做句号.
    [`xeCJK`] 会自动帮你做替换.

### 编译
由于使用了 [`xeCJK`], 需用 `xelatex` 编译:
1. 常规编译: `xelatex %DOC%` 一次;
2. 更新超链接: `xelatex %DOC%` 两次;
3. 更新参考文献引用: `xelatex %DOC%` 一次, `bibtex %DOC%` 一次, `xelatex %DOC%` 两次.

以上的 `%DOC%` 均为 `*.tex` 主文件去掉拓展名后的剩余部分.
绝大多数 $\mathrm{\LaTeX{}}$ 编辑器在适当配置后可以为你完成这些工作.

比如, 示例文档的编译为
```bash
xelatex template
bibtex template
xelatex template
xelatex template
```

## 自动调用的宏包

模板已提前调用了很多为撰写报告提供便利的宏包, 请前往 [`mpltx.cls`] 查看, 其中含有解释其功能的注释.
一些特殊说明如下:

+ [`physics`] 提供了众多方便的物理符号与公式输入,
如导数符号命令 `\dv{f}{x}`, 自动调整大小的括号 `\qty()` 等.
具体请参考其文档.

+ [`siunitx`] 用于便利地打出格式良好的物理量的值和单位, 如 `\qnty{299792.458}{\km\per\s}`， `$g=\qnty{9.801}{m.s^{-2}}$`.
注意, 此宏包定义的 "物理量" 命令 `\qty` 与 `physics` 的 "自动调整括号大小" 命令重名.
所以, 本模板将本宏包的命令**重命名**为 `\qnty`.

+ [`dcolumn`] $\mathrm{\LaTeX{}}2\epsilon$ 基础包的一个, 提供按小数点对齐的表格列格式.
`siunitx` 其实也提供了类似功能, 感兴趣的可以参考两者文档.

### 其他需要注意的外部宏包

+ [`caption`] 存在与本模板的基础 `revtex4-2` 不兼容的情况, 避免使用.

+ [`subfig`] 默认会自动调用 `caption`.
调用时请使用选项 `caption=false`.

## 反馈

如果使用中发现问题或有建议, 请联系 Lin Xuchen <linxc_at_pku.edu.cn>, 或到[项目页]提 issue.
如果有大佬愿意改进这个写得稀烂的文档类, 也欢迎动手.

[项目页]: https://github.com/CastleStar14654/PKUMpLtX

[`mpltx.cls`]: mpltx.cls
[`template.tex`]: template.tex
[`template.pdf`]: template.pdf
[`bibli.bib`]: bibli.bib
[`fig/`]: fig/
[`figgen.py`]: figgen.py
[`fig.mplstyle`]: fig.mplstyle
[`LICENSE.md`]: LICENSE.md

[`revtex4-2`]: https://www.ctan.org/pkg/revtex
[lshort-zh-cn]: http://mirrors.ctan.org/info/lshort/chinese/lshort-zh-cn.pdf
[lnotes2]: https://github.com/huangxg/lnotes/blob/master/lnotes2.pdf
[`xeCJK`]: https://www.ctan.org/pkg/xecjk
[`fandol`]: https://www.ctan.org/pkg/fandol
[`notocjksc`]: https://www.ctan.org/pkg/notocjksc
[`physics`]: https://www.ctan.org/pkg/physics
[`siunitx`]: https://www.ctan.org/pkg/siunitx
[`caption`]: https://www.ctan.org/pkg/caption
[`subfig`]: https://www.ctan.org/pkg/subfig
[`dcolumn`]: https://www.ctan.org/pkg/dcolumn

# Poetry TeX Template

[English README](./README.en.md)

本仓库包含一套基于 `LuaLaTeX + LuaTeX-ja` 的中文诗集排版方案，支持：
- 诗题自动入目录
- 诗文单页居中排版
- 诗注（脚注）可选
- 插图分页展示
- 中文数字页码/图号

面向他人复用时，建议直接从模板文件开始：
- `src/poetry.template.tex`：通用模板（可直接改名后使用）
- `src/poetry.tex`：作者当前诗集成稿（示例参考）
- `poetry.ltjruby`：历史 Lua 脚本（可选，不是基础编译必需）

## 1. 环境准备

请先安装：
- TeX Live（或等价发行版），并确保可用 `lualatex`
- `luatexja`、`luatexja-fontspec`、`luatexja-ruby`
- 中文字体（至少 1 套宋体 + 楷体）

模板默认字体是：
- 正文字体：`STSONG`
- 粗体：`STZHONGS`
- 楷体：`KaiTi`

如果你的系统没有这些字体，请在 `src/poetry.template.tex` 的“可配置区”改成你本机字体名。

## 2. 快速开始（给新用户）

1. 复制模板并创建你的文稿：
```powershell
Copy-Item src/poetry.template.tex src/my-poetry.tex
```

2. 打开 `src/my-poetry.tex`，替换以下内容：
- 标题（`你的詩集標題`）
- 自序正文
- 示例诗词与图注
- 字体配置（如有需要）

3. 在仓库根目录编译：
```powershell
lualatex --interaction=nonstopmode --halt-on-error src/my-poetry.tex
```

说明：
- 为了让目录/引用稳定，通常需要编译 2 次。
- 若你在 `src/` 目录内编译，可直接执行同样命令并把文件名改为 `my-poetry.tex`。

## 3. 模板命令说明

### `\PoemWithNote`

```tex
\PoemWithNote{標題}{詩文內容}{註釋}
```

- `標題`：会进入目录。
- `詩文內容`：建议每行用 `\par` 换行。
- `註釋`：可留空，留空写 `{}`。

示例：
```tex
\PoemWithNote{月夜}{
月落疏鐘靜\par
江清一雁遲\par
}{此詩作於某年秋夜。}
```

### `\PoemFigure`

```tex
\PoemFigure[旋轉角度][圖片寬度]{圖片路徑}{圖題}{label}
```

示例：
```tex
\PoemFigure[90][0.8\textwidth]{../img/anshun.png}{山寺夜景}{fig:example}
```

## 4. 常见问题

### Q1: 编译报字体不存在

修改模板顶部字体配置：
```tex
\newcommand{\PoetryMainFont}{你的宋体字体名}
\newcommand{\PoetryBoldFont}{你的粗体字体名}
\newcommand{\PoetryKaiFont}{你的楷体字体名}
```

### Q2: 目录页码不对或目录为空

先确认文档中有 `\tableofcontents`，然后连续编译两次。

### Q3: 图片不显示

检查图片路径相对 `tex` 文件是否正确，Windows 路径建议统一用 `/`。

## 5. 许可与使用建议

如需二次发布模板，建议保留本仓库链接并注明你修改了哪些样式项（纸张尺寸、字体、脚注样式等），方便后续维护者追踪。

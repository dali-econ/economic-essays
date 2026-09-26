# 《经济学随笔》 / Economic Essays

这是一个用 Quarto Book 制作的中文在线经济学随笔集。每篇文章都是独立的 `.qmd` 文件；书籍目录、搜索、侧边栏目录和“上一章 / 下一章”导航由 Quarto 自动生成。无需编辑 HTML 或 JavaScript。

## 文件结构

```text
economic-essays/
├── _quarto.yml                 # 书名、目录（parts / chapters）与输出设置
├── index.qmd                   # 扉页式首页
├── preface.qmd                 # 序言
├── essays/                     # 每篇随笔一个文件
├── references.bib              # 文献引用库
├── styles.css                  # 全书视觉样式
└── .github/workflows/publish.yml # GitHub Pages 自动部署
```

## 新增一篇文章

1. 新建 `essays/06-new-essay.qmd`，并使用与现有文章相同的 YAML 元数据。
2. 用普通 Markdown / Quarto Markdown 写作。
3. 在 `_quarto.yml` 相应 `chapters:` 列表中加入：

   ```yaml
   - essays/06-new-essay.qmd
   ```

4. 本地运行 `quarto preview` 检查效果。

## 删除文章

从 `_quarto.yml` 的目录配置中删除该文件所在行即可。源文件可以保留，便于日后恢复；确认不再需要时再手动删除文件。

## 调整文章顺序

直接调整 `_quarto.yml` 中同一辑下 `chapters:` 的顺序。Quarto 会据此更新左侧目录与前后章导航。

## 新增一辑（Part）

在 `book.chapters` 中增加一段：

```yaml
- part: "第四辑：新主题"
  chapters:
    - essays/06-new-essay.qmd
```

## 本地预览与生成网站

先安装 [Quarto](https://quarto.org/docs/get-started/)。在项目根目录运行：

```powershell
quarto preview
```

Quarto 会启动本地服务器，并在终端显示预览地址（通常为 `http://localhost:4200/`）。保存 `.qmd` 或 `styles.css` 后，浏览器会自动刷新。

要生成静态网站文件，运行：

```powershell
quarto render
```

生成结果位于 `_book/`；该目录是构建产物，不需要作为主要源代码维护。

同一份源文件也可尝试生成其他格式：

```powershell
quarto render --to pdf
quarto render --to epub
```

PDF 输出通常还需要本机可用的 LaTeX 环境。

## 发布到 GitHub Pages

1. 在 GitHub 创建一个新仓库（建议名为 `economic-essays`），并将本项目推送到仓库的 `main` 分支。
2. 在仓库 **Settings → Pages** 中，将 **Source** 选为 **GitHub Actions**。
3. 推送后，`.github/workflows/publish.yml` 会自动渲染并部署 `_book/`。
4. 在仓库的 **Actions** 页面等待工作流完成；部署地址会显示在运行结果中。

工作流不需要手工上传 HTML 文件，也不会把 `_book/` 当作需要维护的源代码。

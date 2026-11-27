# YUGE ARCHIVE. 

张予歌的个人主页。站点使用原生 HTML、CSS、JavaScript、JSON 和 SVG，可直接由静态服务器提供，无需安装前端依赖。

## 本地预览

在项目根目录运行：

```powershell
python -m http.server 8765 --bind 127.0.0.1
```

在浏览器打开 [本地序厅](http://127.0.0.1:8765/) 或 [数字档案库](http://127.0.0.1:8765/archive.html)。如果 Windows 上的 Python 命令是 `py`，可改用 `py -m http.server 8765 --bind 127.0.0.1`。按 Ctrl+C 可停止服务。

## 页面与目录

| 页面 | 文件 |
| --- | --- |
| 序厅 | `index.html` |
| 常设展厅 | `galleries.html` |
| 数字档案库 | `archive.html` |
| 展品详情 | `exhibit.html?id=EX.001` |
| 成长年表 | `timeline.html` |
| 策展人介绍 | `about.html` |
| 策展手记 | `notes.html` |
| 404 | `404.html` |

- `data/` 保存展厅、展品、年表、手记及网站简介和公开联系方式。
- `css/` 拆分设计变量、基础样式、组件、页面及响应式布局。
- `js/` 包含公共导航和数据加载、档案检索、详情模板、时间轴和图表。
- `assets/` 存放原创示意 SVG 与日后补充的公开素材。封面、图像、录屏和 PDF 的维护方法见 [内容维护指南](CONTENT_GUIDE.md)。

档案库支持 `q`、`gallery`、`year`、`status`、`sort`、`view` 查询参数。例如 `archive.html?q=成语&gallery=ai&year=2026`。跨年作品匹配起止年份之间的各年。最新按结束日期排序，最早按开始日期排序，缺日期的展品排在最后。详情页的 `id` 接受档案编号或唯一 slug。

## GitHub Pages

准备发布时，检查整个发布目录中的 JSON、代码和媒体是否可公开。将站点源文件提交至 GitHub 仓库的 `main` 分支，在仓库 **Settings → Pages → Build and deployment** 下选择 **Deploy from a branch**，然后选择 `main` 与 `/(root)` 并保存。保留根目录的 `.nojekyll`。发布完成后可从 Pages 设置复制访问地址。项目站点的通常形式为 `https://<用户名>.github.io/<仓库名>/`。 [GitHub Pages 官方配置说明](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

首次发布后，从项目站点的实际地址检查首页、`archive.html`、`exhibit.html?id=EX.007` 和一条不存在的路径。Python 自带的 HTTP 服务会对不存在的路径返回自己的错误页，本地可以直接访问 `/404.html` 预览站点错误页。

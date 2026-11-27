# 内容维护指南

数据文件使用 UTF-8 JSON。编辑后从本地 HTTP 预览检查实际页面。JSON 的字符串使用双引号，数组或对象的最后一项后省略逗号。

## 新增或修改作品

打开 `data/exhibits.json`，复制一条完整作品记录并放入顶层数组。在作品编号序列中选一个未使用的 `id`，例如 `EX.009`，再填写唯一的英文 `slug`。修改已有作品时，保留原编号和 slug，以维持已分享的链接。

| 字段 | 填写方式 |
| --- | --- |
| `title`、`titleEn`、`summary` | 中文名称、可选英文名与一段简明摘要 |
| `galleries`、`tags` | 分类 ID 数组与关键词数组。同一作品可归入多个分类 |
| `startDate`、`endDate`、`displayDate` | 用等宽 ISO 日期 `YYYY`、`YYYY-MM` 或 `YYYY-MM-DD` 归档，并填写易读的显示日期 |
| `updatedAt` | 实际修改档案的日期，格式为 `YYYY-MM-DD`。留空会跳过首页最近更新 |
| `status`、`role`、`projectType`、`tools` | 项目状态、个人角色、项目类型和工具数组。未知状态可用“待补充” |
| `sections` | 支持 `background`、`goals`、`process`、`contribution`、`outcomes`、`notes`，每项可填字符串或段落数组 |
| `metrics` | 只录入确认的公开数据。音乐图表从 `metrics.music` 读取 `year`、`hours`、`songs` |
| `cover`、`coverAlt` | 站点根目录相对路径和可选图片描述 |
| `featured` | 设为 `true` 即显示在首页的精选作品，顺序沿用数据文件 |
| `visibility` | `public` 即可通过网站公开浏览 |
| `relatedExhibits` | 填写相关作品编号数组，例如 `["EX.001","EX.007"]` |
| `demo` | 可选的作品页演示入口，包含 `title` 与 `url`。本地演示路径形如 `projects/news-search/index.html`。 |

团队项目的 `contribution` 填写个人负责的工作，`outcomes` 填写整个团队的成果。可选字段留空时，详情模板会跳过相应内容。

## 封面、图片、视频、PDF 与链接

将可公开的素材放入 `assets/images/exhibits/`、`assets/videos/` 或 `assets/documents/`。建议文件名使用短小的字母、数字和连字符。替换封面时更新 `cover`，例如 `assets/images/exhibits/ex-009-cover.webp`。媒体资料可以在对应数组中加入多条记录，结构如下：

```json
{
  "images": [
    {"src":"assets/images/exhibits/ex-009-home.webp","title":"系统首页","alt":"顶部导航下方是关键词输入框"},
    {"src":"assets/images/exhibits/ex-009-results.webp","title":"检索结果","alt":"按相关性排列的检索结果列表"}
  ],
  "videos": [
    {"src":"assets/videos/ex-009-demo.mp4","title":"操作录屏","captions":"assets/videos/ex-009-demo.vtt","transcript":"assets/documents/ex-009-transcript.pdf"}
  ],
  "documents": [
    {"src":"assets/documents/ex-009-report.pdf","title":"公开项目报告（PDF）"}
  ],
  "links": []
}
```

有真实 GitHub 仓库或其他公开链接时，在 `links` 数组添加包含 `title` 和 `url` 的对象，使用完整 HTTPS 地址。添加资料前核对文件名大小写、实际路径和访问权限。无字幕的录屏可以省略 `captions`，并为有语音的内容提供文字稿。

`images` 中的图片可在作品页点击打开原图。课程项目演示页使用静态相对路径。新闻检索演示的数据为虚构样例，课程项目的原始新闻语料应留在站点目录之外。

## 作品分类、成长记录、随笔与联系方式

- 在 `data/galleries.json` 编辑分类的标题、介绍、编号和封面。通过作品的 `galleries` 数组调整分类，同一作品的编号和详情地址可保持不变。更改分类 ID 时同步改动引用它的作品及已发布的入口。
- 在 `data/timeline.json` 加入形如 `{"year":2027,"events":["经历内容"]}` 的记录，或在已有年份的 `events` 中添加一条。页面从近到远展示。
- 在 `data/notes.json` 的 `entries` 数组中添加对象，填写 `title`、`category`、`date`、`paragraphs` 和 `visibility`。日期用 `YYYY-MM-DD`，正文用字符串数组，栏目从 `categories` 选择。
- 在 `data/site.json` 的 `contacts.github` 与 `contacts.email` 填写愿意公开的 GitHub HTTPS 地址与邮箱。空值会隐藏对应链接。
- 在 `data/site.json` 的 `honors` 中维护代表性荣誉，每条填写 `year`、`name`、`organization` 和 `level`。在 `libraryPractice` 中维护图书馆实践，每条填写 `period` 和 `description`。如需同时显示在成长记录，将同一经历加入 `data/timeline.json` 的对应年份。

## 下架与隐私

将 `visibility` 设为 `hidden` 可从分类、检索、详情和推荐中撤下记录。准备公开部署时，从发布目录中移除私密草稿的 JSON 记录和关联文件。访客仍可直接读取服务器上的文件，包括前端没有渲染的内容。删除记录后更新 `relatedExhibits`。未发表论文数据、访谈材料、团队未授权成果、新闻语料库、企业内部数据及个人敏感信息应保存在发布目录之外。

当前作品封面使用原创 SVG 示意图。毕业设计的模型指标及实机素材、新闻搜索系统的截图和录屏、失物招领系统的团队素材、知识图谱的授权材料，可在核实后按以上步骤补充。

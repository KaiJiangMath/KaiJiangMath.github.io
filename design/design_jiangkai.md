# 个人介绍博客一键部署开发文档（蒋凯版本，给 AI 直接执行）

## 1. 目标与范围

目标：基于现有 al-folio 模板，快速部署蒋凯老师的学术个人主页，并支持后续长期维护。

信息来源：
- 教师简介页面：https://math.xtu.edu.cn/info/1010/4004.htm

本项目建议保留以下内容结构：
- About：简洁个人介绍 + 研究方向 + 招生信息 + 快速链接
- CV：完整学习/工作经历、荣誉、学术服务、课程
- Publications：论文全集入口
- Talks：学术报告与会议报告
- Activities：学术活动、组织与服务
- News：首页动态摘要

## 2. 关键约束（必须遵守）

### 2.1 技术与构建约束
- 优先使用 Docker 本地预览。
- 生产发布走 GitHub Actions + GitHub Pages。
- 页面内容使用 Markdown + YAML frontmatter。
- 保持 al-folio 原有结构，不重构主题核心。

### 2.2 内容与风格约束
- 首页采用第一人称（I / My）表达。
- 首页简洁，不重复大段论文清单。
- 详细履历统一放在 CV 页面。
- News 条目必须可读，禁止空白内容。
- 新活动优先写入 Activities，可同步到 News。

### 2.3 YAML 约束（高优先级）
- frontmatter 中字段值若包含英文冒号 :，必须加双引号。
- 示例：
  - 正确：title: "Research Update: Quasiperiodic Systems"
  - 错误：title: Research Update: Quasiperiodic Systems

### 2.4 Git 约束
- 只提交本次需求相关文件。
- 不提交无关临时文件、脚本、缓存文件。
- 每次修改后检查状态再 commit。

## 3. 目录与文件职责

核心文件：
- 首页内容：_pages/about.md
- 新闻列表模板：_includes/news.liquid
- 首页布局模板：_layouts/about.liquid
- 履历页：_pages/cv.md
- 论文页：_pages/publications.md
- 学术报告页：_pages/talks.md
- 活动页：_pages/activities.md
- 新闻目录：_news
- 站点配置：_config.yml

## 4. 蒋凯老师内容映射（从教师简介到网站）

### 4.1 基本信息（About 页）
- 姓名：Kai Jiang（蒋凯）
- 职称：Professor
- 邮箱：kaijiang@xtu.edu.cn
- 办公室：数学楼 B-511
- 个人关键词：Applied Mathematics, Quasiperiodic Systems, Soft Matter Modeling, AI for Science

### 4.2 个人简介（About 页建议文案）
I am Kai Jiang, a Professor at Xiangtan University. My research focuses on applied mathematics driven by irrational numbers, computable modeling and simulation for soft-matter systems, and AI for Science. I currently lead projects including a National Key R&D topic and multiple NSFC grants.

### 4.3 学习与工作经历（CV 页）
教育经历：
- 2002.09-2006.06，湘潭大学，本科，信息与计算科学
- 2006.09-2011.06，湘潭大学，博士，计算数学
- 2007.01-2011.06，北京大学，联合培养博士，计算数学

工作经历：
- 2019.12-至今，湘潭大学，教授
- 2015.01-2019.11，湘潭大学，副教授
- 2015.08-2017.12，新加坡国立大学，客座研究员
- 2013.07-2014.12，湘潭大学，讲师
- 2011.07-2013.06，北京大学，博士后

### 4.4 研究方向（About + CV）
- 无理数引发的应用数学研究
- 软物质体系可计算建模与模拟
- AI for Science

### 4.5 招生方向（About + 可选 Students 页）
课题组长期招收：
- 博士后
- 数学类博士生
- 数学类学术硕士生
- 应用统计专业硕士生
- 本科生

### 4.6 课程（CV 页）
本科生课程：
- 高等代数 I/II
- 复变函数
- 实变函数
- 高等数学
- 线性代数

研究生课程：
- 软物质材料科学计算导论
- 常微分方程定性理论
- 最优化计算

### 4.7 荣誉与学术服务（CV 页）
- 国家高层次青年人才
- 中国计算数学学会优秀青年论文一等奖
- 宝钢优秀教师奖
- 湖南省优秀博士论文指导教师
- 《计算数学》编委

### 4.8 论文（Publications 页）
- 由来源页代表性论文导入 bib 或 markdown 列表。
- 首页仅显示 selected papers 或不显示论文细节。

## 5. 一键部署流程（人工可执行）

### 5.1 获取代码
~~~bash
git clone https://github.com/<your-account>/<your-repo>.git
cd <your-repo>
~~~

### 5.2 校验站点配置
检查 _config.yml：
- url: https://<github-username>.github.io
- baseurl: ""

### 5.3 本地预览（推荐 Docker）
~~~bash
docker compose pull
docker compose up --build
~~~
访问：http://localhost:8080

### 5.4 提交与发布
~~~bash
git add <changed-files>
git commit -m "Initialize Kai Jiang personal homepage"
git push
~~~

### 5.5 GitHub Pages 设置
- Settings -> Pages -> Source 选择 GitHub Actions。
- 确保 Actions workflow 有写权限。

## 6. 内容更新 SOP

### 6.1 更新首页简介
编辑 _pages/about.md：
- 保持第一人称
- 保留研究方向与招生入口
- 加上邮箱、Google Scholar、ORCID 等快速链接

### 6.2 新增新闻
在 _news 下新建：
~~~text
YYYY-MM-DD-short-title.md
~~~

模板：
~~~yaml
---
layout: post
date: 2026-03-17
title: "News Title: With Optional Colon"
inline: true
related_posts: false
---
One sentence summary. [Details](https://example.com).
~~~

### 6.3 更新活动
- 先更新 _pages/activities.md。
- 再按需同步一条 _news 动态。

### 6.4 更新论文
- 优先维护 _bibliography/papers.bib（若仓库采用 bib 流程）。
- 或在 publications 页面维护结构化 markdown 列表。

## 7. 验收清单

- 首页展示姓名、职称、邮箱、研究方向、招生信息。
- 首页叙述为第一人称，无冗长论文列表。
- CV 页面完整包含教育/工作/课程/荣誉。
- Publications、Talks、Activities 可从导航进入。
- News 不出现空白条目。
- 深色模式可读，不出现硬编码白底白字冲突。
- GitHub Actions 构建成功并可访问。

## 8. 可直接发给 AI 的一键执行提示词

将以下内容发给 AI（替换尖括号参数）：

---
你现在是本仓库的实施工程师，请在不改动无关文件的前提下，完成蒋凯老师个人介绍博客初始化与部署。

仓库信息：
- 仓库地址：<repo-url>
- 目标域名：https://<github-username>.github.io
- 技术栈：Jekyll + al-folio + GitHub Pages
- 信息来源：https://math.xtu.edu.cn/info/1010/4004.htm

强约束：
1) 只修改以下范围：_pages, _news, _includes/news.liquid, _layouts/about.liquid, _config.yml, _data/socials.yml。
2) 首页 about 使用第一人称，保持简洁，不重复展示 publications 明细。
3) 详细履历放到 CV 页，包含 Education/Appointments/Courses/Honors/Service。
4) News 必须可读，禁止空白条目。
5) _news frontmatter 若 title 含冒号必须加双引号。
6) 新增活动写入 Activities 页，并可选同步为 News。
7) 深色模式可读，不允许硬编码白底白字冲突。
8) 只提交本次相关文件。

执行步骤：
- 校验并更新 _config.yml 中 url/baseurl。
- 校验导航与页面存在：About/CV/Publications/Talks/Activities。
- 根据信息来源填充 about、cv、activities、talks、publications 的初始内容。
- 新建 3-6 条可读 news 作为初始化动态。
- 运行本地构建（优先 docker compose up --build）。
- 输出变更文件清单、关键 diff 摘要、部署后访问链接。

验收输出：
- 列出 About、CV、Publications、Talks、Activities、News 的入口地址。
- 给出后续新增一条活动与一条新闻的操作示例。
---

## 9. 初始 News 建议（可直接用）

- Joined as Professor at Xiangtan University and established a research group on irrationality-driven applied mathematics.
- New preprint or accepted paper update in SIAM Journal on Numerical Analysis / Journal of Computational Physics.
- Open recruitment for postdocs, PhD students, master students, and undergraduates.
- Course update for graduate class: Introduction to Computational Soft Matter.
- Invited talk or workshop participation in computational mathematics and AI for Science.

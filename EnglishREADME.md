## 当前机制

自动化执行任务: 获取掘金指定用户指定专栏的文章， 并将文章目录链接更新至GitHub pages

自动化运行时间: 北京时间下午 `16:20` 左右

## 项目介绍

项目名：**自动化同步文章平台（auto-sync-blog）**

作用：实现在写作平台（如掘金、CSDN、简书等）的每日能进行自动同步数据（文章标题和链接）；同时，对文章进行友好的分类，并实现更直观的浏览那些年写过的文章。（目前仅支持掘金平台的同步，其他还在开发。）

涉及技术：**github actions**, **github pages**, **node**, **vuepress**

## 部署流程

### 直接部署流程（GitHub Fork）

1. [Fork 仓库](https://github.com/tea-blog/tea-blog.github.io)
2. 仓库 -> Settings -> Secrets -> New repository secret, 添加 Secrets 变量如下:

    | Name                 | Value                                                         | Required |
    | -------------------- | ------------------------------------------------------------- | -------- |
    | JUEJIN_USER_ID       | 掘金用户id                                                    | 是       |
    | JUEJIN_COLUMN_ID     | 掘金专栏id                                                    | 可选     |
    | PRESS_TOKEN_TEA_BLOG | GitHub Personal access tokens，用户推送仓库，同步GitHub pages | 是       |

3. 更新仓库的 actions 权限：Settings -> Secret -> Actions -> General -> Workflow permissions -> 勾选 Read and write permissions -> Save.
4. 仓库 -> Actions, 检查 Workflows 并启用。
5. Settings -> Pages -> Branch -> gh-pages （如果不出现 gh-pages 分支，重复第四步并检查是否已经完成。）-> Save 

### 本地部署流程（Be Developer）

1. 执行主入口，生成 vuepress 相关配置（其中 juejin_user_id 是对应掘金个人首页的user/后面带的一串数字 ）
```cmd
node .\main.js --juejin_user_id=2819602825362840 --juejin_column_id=7140398633710518302
```
2. 安装依赖
```cmd
npm install
```
3. 启动项目
```cmd
npm start
```
4. 访问地址
```http
http://localhost:8080/
```

## 目录结构

```cmd
 ./
├─main.js // 主入口
├─package-lock.json 
├─package.json // 相关依赖和启动方式
├─README.md // 介绍 
├─Q&A.md // 问题统计与解决方法
├─public // 主要部分
|   ├─z-test // 测试
|   |   └test.js
|   ├─utils // 方法调用
|   |   ├─ArticleUtils. // 文章数据处理
|   |   ├─DateUtils.js // 时间处理
|   |   ├─FileUtils.js // 文件处理
|   |   ├─Http.js // 请求
|   |   ├─minimist.js // node 入参处理
|   |   └VuepressUtils.js // 生成 vuepress 相关配置
|   ├─template // 模板
|   |    ├─vuepress // 生成 vuepress 相关配置的模板
|   |    |    ├─config-template.js
|   |    |    └readme-template.md
|   |    ├─article // 生成 markdown 文件的模板
|   |    |    ├─all-template.md
|   |    |    ├─year-month-template.md
|   |    |    └year-template.md
|   ├─src // 主要部分的主入口
|   |  └catch-main.js
|   ├─base // 基础数据
|   |  ├─base-data.js // 静态的数据
|   |  └cover.jpg // 静态图片
├─docs // 以下是本地执行 node 后，会生成的文件夹和文件
|  ├─README.md // vuepress 的相关配置
|  ├─sort // 主要 markdown 文件
|  |  ├─all.md
|  |  ├─2023
|  |  |  ├─2023.md
|  |  |  ├─202301.md
|  |  |  └202302.md
|  |  ├─2022
|  |  |  ├─2022.md
|  |  |  └202201.md
|  ├─.vuepress // vuepress 的相关配置
|  |     ├─config.js
|  |     ├─public
|  |     |   └cover.jpg
```

## 后续开发计划

1. 实现多个专栏（指定多个专栏，指定用户的所有专栏）
2. 实现收藏分类（指定收藏集）
3. 实现邮箱订阅（有更新给订阅的邮箱发送）
4. 实现更灵活的 vuepress 配置文件（更方便修改等）
5. 实现支持更多平台的同步（如CSDN、简书等）
6. 实现更多便捷配置（百度统计，天气，音乐）



## 贡献者

<!-- readme: collaborators,contributors -start -->
<table>
<tr>
    <td align="center">
        <a href="https://github.com/tea-blog">
            <img src="https://avatars.githubusercontent.com/u/68322136?v=4" width="100;" alt="tea-blog"/>
            <br />
            <sub><b>南方者</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/Ylimhs">
            <img src="https://avatars.githubusercontent.com/u/42811965?v=4" width="100;" alt="Ylimhs"/>
            <br />
            <sub><b>Ylimhs</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/NanFangZhe404">
            <img src="https://avatars.githubusercontent.com/u/86654383?v=4" width="100;" alt="NanFangZhe404"/>
            <br />
            <sub><b>南方者</b></sub>
        </a>
    </td></tr>
</table>
<!-- readme: collaborators,contributors -end -->
欢迎各位英雄豪杰加入，共建更完美的 **自动化同步文章平台（auto-sync-blog）** 。

## 问题回答（Question & Answer）
<a title="Q&A" href="Q&A.md">Question & Answer</a>

## License
auto-sync-blog is under the [GPL license](LICENSE).


GitHub Copilot: 这是一个名为“自动化同步文章平台（auto-sync-blog）”的项目的README文件。该项目的目标是实现在写作平台（如掘金、CSDN、简书等）的每日自动同步数据（文章标题和链接），同时对文章进行友好的分类，并实现更直观的浏览那些年写过的文章。

该项目使用了github actions、github pages、node和vuepress等技术。提供了直接部署和本地部署两种部署方式。直接部署需要在GitHub上fork仓库，然后在仓库设置中添加一些必要的Secrets变量，然后更新仓库的actions权限，最后在仓库的Settings中设置Pages。本地部署则需要在本地运行一些命令来启动项目。

该项目的目录结构清晰，主要包括主入口、相关依赖和启动方式、介绍、问题统计与解决方法、主要部分、模板、主要部分的主入口、基础数据等部分。



captainfod: 翻译成英文

GitHub Copilot: # Hackertab.dev — All developer news at a glance!

[![Website hackertab.dev](https://img.shields.io/website-up-down-green-red/https/hackertab.dev.svg)](https://hackertab.dev/)
[![Apache 2 license](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://github.com/medyo/hackertab.dev/blob/master/LICENSE)
[![Mozilla Add-on](https://img.shields.io/amo/v/hackertab-dev?style=plastic)](https://bit.ly/hackertab-ff)
[![Chrome Web Store](https://img.shields.io/chrome-web-store/v/ocoipcahhaedjhnpoanfflhbdcpmalmp?style=plastic)](https://bit.ly/hackertab-ch)
[![Chrome Web Store Rating](https://img.shields.io/chrome-web-store/stars/ocoipcahhaedjhnpoanfflhbdcpmalmp.svg?colorB=%234FC828&label=rating&style=flat)](https://chrome.google.com/webstore/detail/hackertabdev/ocoipcahhaedjhnpoanfflhbdcpmalmp/reviews)

**Hackertab makes it easy to stay up-to-date with the latest developer news, tools, jobs, and events.**

As a developer, keeping up with everything happening in your field can be challenging. Hackertab makes it easy by allowing you to customize your default tab with news, tools, and events from top sources like GitHub Trendings, Hacker News, DevTo, Medium, and Product Hunt. No matter what type of developer you are, you can find valuable and relevant information in Hackertab. Don't miss out - try it today!

## How to use

- Install the extension from the [Chrome Store](https://bit.ly/hackertab-ch) or [Mozilla Add-on](https://bit.ly/hackertab-ff)
- Open a new tab
- The extension should now be running and visible
- Choose your preferred programming languages and sources
- Enjoy

## Features

- Daily updated content
- Customizable by programming language, framework, and topic
- Curated content from the best sources
- Save for later reading
- Dark mode for night time
- AI recommendations tailored to your preferences

More features to come in the future!

## Data sources

- Github Trendings
- Hackernews
- DevTo
- Hashnode
- Lobsters
- Confs.tech
- Product Hunt
- Reddit
- Freecodecamp
- Medium
- Indiehackers
- **Or create an issue to request a new data source**

## Support

If you have any questions, report bugs, or suggestions, feel free to ask, or send an email to hello@hackertab.dev

## Development

Please use the develop branch. Create a .env file with the necessary content

```bash

```

captainfod: 翻译成英文版本

GitHub Copilot: ## Current Mechanism

Automated task execution: Fetch articles from a specified column of a specified user on Juejin, and update the article directory link to GitHub pages.

Automated run time: Around 16:20 Beijing time.

## Project Introduction

Project name: **Automated Article Synchronization Platform (auto-sync-blog)**

Function: Achieve daily automatic synchronization of data (article titles and links) on writing platforms (such as Juejin, CSDN, JianShu, etc.); at the same time, categorize articles in a user-friendly manner, and provide a more intuitive browsing experience for articles written over the years. (Currently only supports synchronization of the Juejin platform, others are under development.)

Involved technologies: **github actions**, **github pages**, **node**, **vuepress**

## Deployment Process

### Direct Deployment Process (GitHub Fork)

1. [Fork the repository](https://github.com/tea-blog/tea-blog.github.io)
2. Repository -> Settings -> Secrets -> New repository secret, add Secrets variables as follows:

    | Name                 | Value                                                         | Required |
    | -------------------- | ------------------------------------------------------------- | -------- |
    | JUEJIN_USER_ID       | Juejin user id                                                | Yes      |
    | JUEJIN_COLUMN_ID     | Juejin column id                                              | Optional |
    | PRESS_TOKEN_TEA_BLOG | GitHub Personal access tokens, used to push to the repository, synchronize GitHub pages | Yes      |

3. Update the repository's actions permissions: Settings -> Secret -> Actions -> General -> Workflow permissions -> Check Read and write permissions -> Save.
4. Repository -> Actions, check Workflows and enable them.
5. Settings -> Pages -> Branch -> gh-pages (If the gh-pages branch does not appear, repeat the fourth step and check if it has been completed.) -> Save 

### Local Deployment Process (Be Developer)

1. Execute the main entry, generate vuepress related configuration (where juejin_user_id corresponds to a string of numbers after user/ on the personal homepage of Juejin)
```cmd
node .\main.js --juejin_user_id=2819602825362840 --juejin_column_id=7140398633710518302
```
2. Install dependencies
```cmd
npm install
```
3. Start the project
```cmd
npm start
```
4. Visit the address
```http
http://localhost:8080/
```

## Directory Structure

```cmd
 ./
├─main.js // Main entry
├─package-lock.json 
├─package.json // Related dependencies and startup methods
├─README.md // Introduction 
├─Q&A.md // Problem statistics and solutions
├─public // Main part
|   ├─z-test // Test
|   |   └test.js
|   ├─utils // Method calls
|   |   ├─ArticleUtils. // Article data processing
|   |   ├─DateUtils.js // Time processing
|   |   ├─FileUtils.js // File processing
|   |   ├─Http.js // Request
|   |   ├─minimist.js // Node parameter processing
|   |   └VuepressUtils.js // Generate vuepress related configuration
|   ├─template // Template
|   |    ├─vuepress // Template for generating vuepress related configuration
|   |    |    ├─config-template.js
|   |    |    └readme-template.md
|   |    ├─article // Template for generating markdown files
|   |    |    ├─all-template.md
|   |    |    ├─year-month-template.md
|   |    |    └year-template.md
|   ├─src // Main entry of the main part
|   |  └catch-main.js
|   ├─base // Basic data
|   |  ├─base-data.js // Static data
|   |  └cover.jpg // Static image
├─docs // Below are the folders and files generated after executing node locally
|  ├─README.md // Vuepress related configuration
|  ├─sort // Main markdown files
|  |  ├─all.md
|  |  ├─2023
|  |  |  ├─2023.md
|  |  |  ├─202301.md
|  |  |  └202302.md
|  |  ├─2022
|  |  |  ├─2022.md
|  |  |  └202201.md
|  ├─.vuepress // Vuepress related configuration
|  |     ├─config.js
|  |     ├─public
|  |     |   └cover.jpg
```

## Future Development Plan

1. Implement multiple columns (specify multiple columns, all columns of specified users)
2. Implement favorite classification (specify collection)
3. Implement email subscription (send to subscribed email when updated)
4. Implement more flexible vuepress configuration files (easier to modify, etc.)
5. Implement support for more platform synchronization (such as CSDN, JianShu, etc.)
6. Implement more convenient configurations (Baidu statistics, weather, music)

## Contributors

<!-- readme: collaborators,contributors -start -->
<table>
<tr>
    <td align="center">
        <a href="https://github.com/tea-blog">
            <img src="https://avatars.githubusercontent.com/u/68322136?v=4" width="100;" alt="tea-blog"/>
            <br />
            <sub><b>南方者</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/Ylimhs">
            <img src="https://avatars.githubusercontent.com/u/42811965?v=4" width="100;" alt="Ylimhs"/>
            <br />
            <sub><b>Ylimhs</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/NanFangZhe404">
            <img src="https://avatars.githubusercontent.com/u/86654383?v=4" width="100;" alt="NanFangZhe404"/>
            <br />
            <sub><b>南方者</b></sub>
        </a>
    </td></tr>
</table>
<!-- readme: collaborators,contributors -end -->
欢迎各位英雄豪杰加入，共建更完美的 **自动化同步文章平台（auto-sync-blog）** 。

## 问题回答（Question & Answer）
<a title="Q&A" href="Q&A.md">Question & Answer</a>

## License
auto-sync-blog is under the [GPL license](LICENSE).

# Tuture

Tuture 是一个基于 Git 仓库生成高质量技术教程的工具。

*其他语言版本*：[English](README.md)。

## 特色

Tuture 革新了技术教程写作的方式。

- **直接从真实的代码库中生成**：你的教程会真实地反映代码库。只需从一个 Git 仓库开始，搭建一个有趣的东西，并且写好提交信息，Tuture 就会把所有的精彩带到你的教程中。随着灵感的累积，你的代码库会成长，你的教程也会。

- **自动提取代码变化**：写教程最大的痛点之一便是要手动提取每一步骤中每个文件的代码变化。幸运的是，Tuture 会为你处理这个艰巨且容易出错的任务，因此你只需专注于书写优秀的教程。

- **用编程的方式写作**：在过去，写作更多的是一种随意并且个性化的过程。但是有了 Tuture，你可以用一种非常接近编程的方式来书写教程。整个教程可以完全被一个 YAML 文件确定下来，因此你只需填写所需的字段。

- **浏览器中炫酷的渲染**：由于 JavaScript 相关技术的快速发展，[tuture-renderer](https://github.com/tutureproject/renderer) 完全能够将你的教程以一种优美且具有交互性的方式展现出来。

## 安装

确保你已经安装了 [Node.js](https://nodejs.org/) (>= 8.0.0) 和 [npm](https://www.npmjs.com/) (>= 5.0.0)。

- **通过 npm 安装**

```bash
$ npm i -g tuture
```

- **通过源代码安装**

将本仓库 clone 到本地后，执行以下命令安装：

```bash
$ npm i -g
```

## 使用 Tuture 命令行工具

以下命令假定你处在一个 Git 仓库中。如果你还没有安装 Git，请从[此处](https://git-scm.com/downloads)下载。

### `tuture init`

初始化一个 Tuture 教程。

初始化过程中会触发一系列询问如下：

| 询问               | 对应字段   | 必要/可选 | 默认值             | 含义                                                         |
| ------------------ | ---------- | --------- | ------------------ | ------------------------------------------------------------ |
| Tutorial Name?     | `name`     | 必要      | My Awesome Project | 此教程的标题                                                 |
| Tutorial Language? | `language` | 必要      | English            | 此教程的语言                                                 |
| Topics?            | `topics`   | 可选      | -                  | 此教程的主题，不同的主题用空格或逗号分隔，例如 `express,mongodb` |
| Maintainer email?  | `email`    | 可选      | -                  | 此教程维护者的电子邮件                                       |

然后会生成以下文件：

-  **tuture.yml** 文件，用于记录教程的元数据和每一步的讲解，实例结构如下。

```yaml
name: 教程的名称
language: 教程的语言
topics:
  - 主题 A
  - 主题 B
maintainer: 教程维护者的电子邮箱
steps:
  - name: commit ae05546 的提交信息
    commit: ae05546
    explain: 讲解第一步做了什么
    diff:
      - file: 发生变化的文件 A
        explain: 讲解为什么要增加或修改这个文件
      - file: 发生变化的文件 B
        explain: 讲解为什么要增加或修改这个文件
  - name: commit ae05546 的提交信息
    commit: a45bec1
    explain: 讲解第二步做了什么
    diff:
      - file: 发生变化的文件 A
        explain: 讲解为什么要增加或修改这个文件
      - file: 发生变化的文件 B
        explain: 讲解为什么要增加或修改这个文件
      - file: 发生变化的文件 C
        explain: 讲解为什么要增加或修改这个文件
```

-  **.tuture** 目录，用于存放 Tuture 所需的 diff 数据。

```
.tuture
└── diff
    ├── 084a277.diff
    ├── e4a9539.diff
    ├── f898719.diff
    └── fefe569.diff
```

同时，会在你的 `.gitignore` 中添加以下规则（如果没有会为你创建）：

```
# Tuture supporting files
.tuture
```

### `tuture up`

生成教程并在浏览器打开。

### `tuture destroy`

删除所有 Tuture 相关文件。

## 如何编写 Tuture 教程

编写 Tuture 教程是一件非常轻松愉悦的事情。

1. 初始化一个 Git 仓库（或者在一个已有的仓库中展开）

2. 编写代码并提交，每次提交信息应有意义

3. 运行 `tuture init` 来初始化 Tuture 教程

4. 在 tuture.yml 的相应 `explain` 字段中填写你的讲解

5. 运行 `tuture up` ，就会打开浏览器并渲染你的教程

6. 编辑 `tuture.yml` 并保存，即可修改教程中的内容

## 许可证

[MIT](LICENSE)。

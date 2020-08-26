---
title: R Markdown
description: 如何在 Visual Studio 中创建 R Markdown 文档，以生成高质量的报表、演示文稿和仪表板。
ms.date: 11/16/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 2cfad81c44822e59abb704e5e830357bfd32067d
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801550"
---
# <a name="create-r-markdown-documents"></a>创建 R Markdown 文档

[R Markdown](https://rmarkdown.rstudio.com/) 是一种文档格式，可将 R 中的分析转化为高质量的文档、报告、演示文稿和仪表板。

针对 Visual Studio 的 R 工具 (RTVS) 提供了 R Markdown 项模板、编辑器支持（包括编辑器中适用于 R 代码的 IntelliSense）、文件生成功能和实时预览。

## <a name="using-r-markdown"></a>使用 R Markdown

1. 关闭 Visual Studio。
1. （仅一次）从 [pandoc.org](https://pandoc.org/installing.html) 安装 `pandoc`。
1. 重启 Visual Studio，它应该获取 pandoc 安装程序。
1. 安装 `knitr` 和 `rmarkdown` 包，可从[交互窗口](interactive-repl-for-r-in-visual-studio.md)执行安装操作：

    ```R
    install.packages("knitr")
    install.packages("rmarkdown")

    ```

1. 要创建新的 R Markdown 文件，请使用“文件” > “新建” > “文件”菜单命令，并在列表中选择”R” > ”R Markdown”。 访问项目的上下文，在解决方案资源管理器中右键单击项目，选择“添加 R Markdown”（或“添加” > “新项目”，再在列表中选择”R Markdown”）。

1. 新文件的默认内容如下：

    <!-- markdownlint-disable MD048 -->
    ~~~markdown
    ---
    title: "Untitled"
    output: html_document
    ---

    This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and Microsoft Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

    When you select the **R Tools | Publish | Preview** button, a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

    ```{r}
    summary(cars)
    ```

    You can also embed plots, for example:

    ```{r, echo=FALSE}
    plot(cars)
    ```

    Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.

    ~~~
    <!-- markdownlint-disable MD048 -->

## <a name="previews"></a>预览版

Visual Studio 2017 版本 15.5 以及更高版本自动提供 R Markdown 的实时预览。 要启用编辑器与预览之间的自动同步，请选择“R 工具” > “Markdown” > “自动同步”(Ctrl+Shift+Y)。 如果没有使用自动同步，可使用“R 工具” > “Markdown” > “重载 R Markdown 预览”来刷新预览。

还可以通过在编辑器中右键单击并选择一个“预览”命令，在 HTML、PDF 和 Microsoft Word 格式中预览文件  。 还可通过“R 工具” > “Markdown”菜单获取相同命令。 （在早期版本的 Visual Studio 中，这些命令位于“R 工具” > “发布”菜单。）

![R Markdown 实时预览和其他预览菜单命令](media/rmarkdown-live-preview.png)

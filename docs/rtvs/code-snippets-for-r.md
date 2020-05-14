---
title: R 的代码片段
description: Visual Studio 中的 R 的代码片段提供快捷方式，可用于快速插入任意长度的代码块，有助于避免反复键入相似的代码。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 05a21da94dd643b04cea94b7840ca26d9379cb5a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62969435"
---
# <a name="code-snippets"></a>代码片段

Visual Studio 中的代码片段提供了一些快捷方式，可用于快速插入任意长度的代码块，有助于避免反复键入相似的代码。 针对 Visual Studio 的 R 工具 (RTVS) 向 Visual Studio 的集合添加了许多有用的 R 代码片段。

要插入代码片段，请键入代码片段的缩写名称（提供 IntelliSense），然后按 Tab 插入  。

一些简单示例如下：

- 键入 `=` 然后按 Tab，RTVS 会将其展开为 `<-` 赋值运算符。
- 键入 `>` 然后按 Tab，RTVS 会将其展开为 `%>%` 管道运算符。

代码片段的用途远不只是拼写完字符。 例如，如果使用一个通过 `read.csv` 函数读取 CSV 文件的代码片段，便不用记住名称或参数：

![使用代码片段插入对 read.csv 的调用的动画](media/code-snippet-expansion.gif)

在这种情况下，当键入 `readc` 时，IntelliSense 将显示一个完成列表。 在下拉菜单中选择该完成列表，按 Tab 选择 **，然后再次按 Tab 展开代码片段**`readc`  。 （因此，通常认为展开代码片段是“键入代码片段并按 Tab 两次”）。 在大多数情况下，第一次按 Tab 完成 IntelliSense 选择，第二次按 Tab 触发展开。

要查看所有可用的代码片段，请打开“工具” **“代码片段管理器”对话框（Ctrl**K、B），并为“语言”选择“R” >    +     。 展开组并选择单独的代码片段，查看说明和快捷方式文本：

![R 的代码片段对话框](media/code-snippet-dialog.png)

要创建自定义代码片段，请按照[演练：创建代码片段](../ide/walkthrough-creating-a-code-snippet.md)中的说明进行操作。 最终，代码片段只是一个 XML 文件。 例如，以下代码是管道操作（快捷方式 `>`）的代码片段：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>Dplyr pipe</Title>
      <Shortcut>&gt;</Shortcut>
      <Description>Code snippet for '%&gt;%' operator</Description>
      <Author>Microsoft Corporation</Author>
      <SnippetTypes>
        <SnippetType>Expansion</SnippetType>
       </SnippetTypes>
    </Header>
    <Snippet>
      <Code Language="R">
        <![CDATA[ %>% $end$]]>
      </Code>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
```

用于所有代码片段的 XML 文件是随 RTVS 一起安装的；“代码片段管理器”  中的“位置”  字段提供了相关路径。 也可以在 [src/Package/Impl/Snippets](https://github.com/Microsoft/RTVS/tree/master/src/Package/Impl/Snippets) 下 GitHub 的 RTVS 源代码中找到它们。

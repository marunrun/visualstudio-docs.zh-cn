---
title: R Tools for Visual Studio
description: 针对 Visual Studio 的 R 工具 2017 (RTVS) 是一个免费的开源扩展，提供多种语言功能，包括 IntelliSense、调试和远程工作区。
ms.date: 11/13/2017
ms.topic: overview
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 1132a7a0363e2d508d6eff1026192aad3407fca4
ms.sourcegitcommit: f8e3715c64255b476520bfa9267ceaf766bde3b0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "73189250"
---
# <a name="work-with-r-in-visual-studio"></a>在 Visual Studio 中使用 R

R 是用于统计计算和图形的高度可扩展语言和环境。 它是使用 GNU 通用公共许可证免费分发的工具，提供强大的社区支持，并因能够生成发布质量的绘图（包括数学符号和公式）而闻名。 若要了解详细信息，请参阅 [r-project.org](https://www.r-project.org/about.html) 和 [R 简介](https://cran.r-project.org/doc/manuals/r-release/R-intro.html)。

针对 Visual Studio 的 R 工具 (RTVS) 是使用 MIT 许可证发布的[开源](https://github.com/microsoft/RTVS)插件，适用于 Visual Studio 2017 和 Visual Studio 2015 Update 3（或更高版本）。 （还有一个链接到 R 解释器二进制文件的开放源代码组件 [RHost](https://github.com/microsoft/R-Host)，它是使用 GNU 公共许可证 V2 进行发布的。）

> [!Note]
> RTVS 目前仅在 Windows 上的 Visual Studio 2017 中受支持，在 Visual Studio for Mac 中不受支持。 不适用于 Visual Studio 2019。

若要在 Visual Studio 中使用 R，请执行以下操作：

- [安装 R 工具](installing-r-tools-for-visual-studio.md)。
- 请按照[入门](getting-started-with-r.md)指南、[示例](getting-started-samples.md)和[获取帮助](getting-started-help.md)文章操作。

然后，单击下面的链接，详细了解与 R 相关的功能，以及 Visual Studio 本身的常规功能。

| 功能 | 描述 | Visual Studio 常规文档 |
| --- | --- | --- |
| [Visual Studio 项目系统](r-projects-in-visual-studio.md) | 利用方便使用的结构整理和管理相关文件，并利用实用项目模板，如 R 代码、R 文档、R Markdown、SQL 查询和存储过程。 此外，还可以使用[包管理器](r-package-manager-in-visual-studio.md)和 [SQL Server 集成](integrating-sql-server-with-r.md)。  | [Visual Studio 中的解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md) |
| [工作区](r-workspaces-in-visual-studio.md) | RTVS 可以绑定到本地和远程工作区，以便使用较小的数据集在本地开发 R 代码，然后在基于云且功能更强大的计算机上使用较大的数据集运行此代码。 | n/a |
| [R 工具选项](options-for-r-tools-in-visual-studio.md) | 控制 RTVS 的各个方面。 | [“选项”对话框](../ide/reference/options-dialog-box-visual-studio.md) |
| [丰富编辑、IntelliSense 和代码片段](editing-r-code-in-visual-studio.md) | 包括语法着色、跨所有代码和库的 [IntelliSense](r-intellisense.md)、代码格式设置、签名帮助、转到定义、查找所有引用和[代码片段](code-snippets-for-r.md)等。 | [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md) |
| [R Markdown](rmarkdown-with-r-in-visual-studio.md) | R Markdown 文档有助于共享数据结果，其中 Markdown 代码块包含集成的 R 代码。 | n/a |
| [交互窗口](interactive-repl-for-r-in-visual-studio.md) | 提供 R 的完整 REPL 体验，以便可以在交互窗口内轻松运行源文件中的代码。 | n/a |
| [可视化数据](visualizing-data-with-r-in-visual-studio.md) | 绘图是 R 体验不可或缺的一部分，RTVS 支持使用多个独立绘图窗口（每个窗口均有各自的历史记录）和跨窗口移动绘图功能。 可以将绘图保存为位图和 PDF 文件，也可以将绘图以位图或元文件的形式复制到剪贴板中。  | n/a |
| [变量资源管理器](variable-explorer.md) | 在全局或包特定范围中检查变量，同时还允许查看可排序的表，并将其导出为 CSV 格式。 | n/a |
| [功能完备的调试](debugging-r-in-visual-studio.md) | 包括与交互窗口的集成。 | [在 Visual Studio 中进行调试](../debugger/debugger-feature-tour.md) |

另请参阅[常见问题](faq.md)。

|   |   |
|---|---|
| ![视频摄影机图标](../install/media/video-icon.png "观看视频") | [观看视频 (youtube.com)](https://www.youtube.com/watch?v=dll3IS1bfWQ)，获取有关用于 Visual Studio 的 R 工具的概述（12 分 36 秒）。 另请参阅[更多 R 工具视频](https://www.youtube.com/results?search_query=R+Tools+for+visual+studio)。 |

## <a name="send-us-your-feedback"></a>向我们发送反馈！

1. **GitHub 问题**：联系 RTVS 团队的最佳方式是[在 GitHub 中上报问题](https://github.com/Microsoft/RTVS/issues)或使用“R 工具”   > “反馈”  菜单。

1. **发送一个笑脸/哭脸图标**：使用“R 工具” > “反馈”菜单，可以快速发送反馈，并附加 RTVS 日志文件，以帮助我们诊断所遇到的问题   。 （如果要单独发送，请将日志写入 %temp%/RTVSlogs.zip。  ）如果已使用“帮助” > “反馈” > “设置”菜单命令或在安装期间选择禁用了 Visual Studio 遥测，日志记录也会被禁用    。

1. **电子邮件**：可以直接向团队发送反馈，地址是 *rtvsuserfeedback (at) microsoft.com*。

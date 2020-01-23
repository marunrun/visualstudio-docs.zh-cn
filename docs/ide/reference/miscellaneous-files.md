---
title: 杂项文件
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.newfile
- VS.OpenWith
- MiscellaneousFilesProject
helpviewer_keywords:
- solutions, miscellaneous files
- standalone files
- Solution Explorer, miscellaneous files
- Miscellaneous Files folder
- files [Visual Studio], miscellaneous
ms.assetid: 5b96640b-8efe-48a4-8d0a-1ae3f9587e44
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 793500faf217c74772506b4b7394d926447ffd40
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585292"
---
# <a name="miscellaneous-files"></a>杂项文件

你可能需要使用 Visual Studio 编辑器独立于项目或解决方案来处理文件。 打开某个解决方案后，可以打开和修改文件，而不必将其添加到解决方案或项目中。 要独立处理的文件称为杂项文件。 杂项文件位于解决方案和项目的外部，不包括在生成中，而且无法包括在受源代码管理的解决方案中。

由于各种原因，独立于项目或解决方案来打开文件很有用。 你可能有一个需要在开发基于项目的解决方案时查看的文件，但它对于解决方案的开发并非必不可少。 常见示例包括开发备注或说明、数据库架构和代码剪辑。 此外，可能还需要创建独立文件。

![解决方案项目](../../ide/reference/media/projects_solutions_misc.gif)

如果启用了相应的文件夹选项，则解决方案资源管理器可为这类文件显示一个“杂项文件”文件夹  。 可从[“选项”对话框 ->“环境”->“文档”对话框](../../ide/reference/documents-environment-options-dialog-box.md)中设置这些选项。 关闭某个杂项文件后，该文件与任何特定解决方案或项目都不再关联，除非也启用了使之关联的选项。

“杂项文件”文件夹将文件表示为链接  。 尽管此文件夹不是解决方案的一部分，但当打开某解决方案时，上次关闭该解决方案时打开的部分或全部杂项文件会重新打开，具体取决于该文件夹的设置。

> [!NOTE]
> 有些没有在“杂项文件”文件夹中显示的文件是不能在 IDE 中修改的文件，例如 .zip 文件和 .doc 文件  。 IDE 不会跟踪那些只能通过外部编辑器修改的文件。

## <a name="commands-available-in-the-ide"></a>IDE 中可用的命令

根据打开的文件的格式，它们包含的菜单、工具栏和命令会发生变化。 例如，打开一个文本文件时，会出现“文本编辑器”工具栏而且其命令可用。 如果接着打开 XML 架构文件，则出现“XML 架构”工具栏。 编辑 XML 架构时，“文本编辑器”工具栏的命令（或该工具栏本身）不可用。 XML 架构是活动窗口，因此具有当前选定内容上下文。 当从项目文件切换到杂项文件时，所有与项目相关的命令将消失，仅显示那些直接与杂项文件相关的命令。

## <a name="folder-display-options"></a>文件夹显示选项

可以设置“杂项文件”文件夹的显示选项，以便即使未打开任何杂项文件时也显示该文件夹  。 解决方案文件不永久管理杂项文件列表。 它使用一项可选功能，该功能使它记住每个用户最近使用过 (MRU) 的文件列表。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中开发代码而无需项目或解决方案](../develop-code-in-visual-studio-without-projects-or-solutions.md)
- [解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)
- [“选项”对话框 ->“环境”->“文档”](../../ide/reference/documents-environment-options-dialog-box.md)

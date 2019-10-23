---
title: 选项，文本编辑器，文件扩展名
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.File_Extension
helpviewer_keywords:
- file extensions, associating to editor
- Editing Experience
- Options dialog box
- Editing Experience, selecting
ms.assetid: 05298fc5-fc4e-4bb2-b942-1f7d2dcdff0f
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b023ad4b14d6c890c14726f645a2ebf3c99f6f7d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666266"
---
# <a name="options-text-editor-file-extension"></a>选项，文本编辑器，文件扩展名

通过此“选项”对话框，可以指定 Visual Studio 集成开发环境 (IDE) 对具有特定文件扩展名的所有文件的处理方式。 对于输入的每个“扩展名”，可以选择一个编辑体验  。 这样便可选择在某种类型的哪些文档中打开 IDE 编辑器或设计器。 若要显示这些选项，请从“工具”菜单中选择“选项”，展开“文本编辑器”节点并选择“文件扩展名”     。

选中“使用编码”选项后，每当打开该类型的文档时，都会显示一个对话框，用户可以为该文档选择编码方案。 在准备不同版本的项目文档以用于不同的平台或不同的目标语言时，此选项将很有帮助。

## <a name="uielement-list"></a>UIElement 列表

**扩展**

键入要定义在 IDE 中的编辑体验的文件扩展名。

编辑器 

选择打开具有此文件扩展名的文档所使用的 IDE 编辑器或设计器。 选中“使用编码”选项后，每当打开此类文档时，都会显示一个对话框，用户可以选择编码方案。

**添加**

向扩展名列表添加包含指定的“扩展名”和“编辑体验”的条目   。

**移除**

从扩展名列表中删除所选条目。

**扩展名列表**

列出所有已指定编辑体验的扩展名。

将无扩展名文件映射到 

若要指定 IDE 将如何处理无扩展名的文件，请选择此选项。

无扩展名文件选项 

提供与“编辑器”相同的列表  。 选择打开不具有此文件扩展名的文档所使用的 IDE 编辑器或设计器。

## <a name="see-also"></a>请参阅

- [如何：管理编辑器模式](../../ide/how-to-manage-editor-modes.md)
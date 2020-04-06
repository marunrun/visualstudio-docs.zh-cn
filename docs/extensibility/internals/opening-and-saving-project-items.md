---
title: 打开和保存项目项目 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], file persistence
- files [Visual Studio], opening and saving
- editors [Visual Studio SDK], file persistence
ms.assetid: f71898ad-335f-4c43-a177-4da87078afd1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bbb89d99e401be6bae7d8ee9be8ee33fa7574723
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706971"
---
# <a name="opening-and-saving-project-items"></a>打开和保存项目项
添加新项目类型时，必须在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 中管理项目文件的打开和保存。 以下主题讨论打开和保存文件的不同方法。

## <a name="in-this-section"></a>本节内容
- [使用“打开文件”命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

 提供 IDE 如何处理**Open File**命令以及项目在响应此命令中的作用的分步说明。

- [使用“通过命令打开”显示文件](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)

 提供 IDE 如何处理 **"打开随用"** 命令的详细分步说明，从而提示打开具有一些标准编辑器选择的文件。

- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)

 提供分步说明，用于指定应使用特定于项目的编辑器打开项目中特定类型的文件。

- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

 提供分步说明，说明如何指定如何使 IDE 为项目类型中的文件打开标准编辑器。

- [如何：打开开放文档的编辑器](../../extensibility/how-to-open-editors-for-open-documents.md)

 提供分步说明，用于打开打开的文件的项目特定编辑器。

- [保存标准文档](../../extensibility/internals/saving-a-standard-document.md)

 详细说明 IDE 如何处理标准编辑器中打开的文档的 **"保存**、**保存为**"和 **"保存所有"** 命令。

- [保存自定义文档](../../extensibility/internals/saving-a-custom-document.md)

 提供一个图表，并详细说明 IDE 如何处理在自定义编辑器中打开的文档**的保存**、**保存为**和**保存所有**命令。

- [确定使用哪个编辑器打开项目中的文件](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)

 讨论 IDE 为文件选择适当的编辑器或设计器的过程。

## <a name="related-sections"></a>相关章节
- [创建自定义编辑器和设计器](../../extensibility/creating-custom-editors-and-designers.md)

 列出 IDE 可以承载的四种编辑器类型，并给出每个编辑器的说明。

- [项目类型](../../extensibility/internals/project-types.md)

 讨论项目如何控制代码的编译和生成方式、编辑器的打开方式以及如何设置项目项目的格式。

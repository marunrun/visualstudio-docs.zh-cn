---
title: 打开和保存项目项 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], file persistence
- files [Visual Studio], opening and saving
- editors [Visual Studio SDK], file persistence
ms.assetid: f71898ad-335f-4c43-a177-4da87078afd1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 77a3417bc15bc9c4c6149b4e77dc4fdcebe5cd6e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314935"
---
# <a name="opening-and-saving-project-items"></a>打开和保存项目项
当添加新的项目类型时，必须管理的打开和保存项目文件都位于[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE)。 以下主题讨论打开和保存文件的不同方法。

## <a name="in-this-section"></a>本节内容
- [使用“打开文件”命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

 提供了在 IDE 的处理方式的分步说明**打开的文件**命令和响应此命令中的项目的角色。

- [使用“通过命令打开”显示文件](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)

 提供了在 IDE 的处理方式的详细的分步说明**打开**命令，提示具有某些选择的标准编辑器的文件打开。

- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)

 提供用于指定后，应使用特定于项目的编辑器打开你的项目中的特定类型文件的分步说明。

- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

 提供用于指定如何能够在您的项目类型中打开文件的标准编辑器在 IDE 的分步说明。

- [如何：打开开放文档的编辑器](../../extensibility/how-to-open-editors-for-open-documents.md)

 提供分步说明，以打开特定于项目的编辑器为打开的文件。

- [保存标准文档](../../extensibility/internals/saving-a-standard-document.md)

 提供了在 IDE 的处理方式的详细的说明**保存**，**另存为**，并**全部保存**的标准编辑器中打开文档的命令。

- [保存自定义文档](../../extensibility/internals/saving-a-custom-document.md)

 提供了关系图和详细的说明了 IDE 如何处理**保存**，**另存为**，并**全部保存**的自定义编辑器中打开的文档的命令。

- [确定使用哪个编辑器打开项目中的文件](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)

 讨论 IDE 遵循选择适当的编辑器或设计器的文件的过程。

## <a name="related-sections"></a>相关章节
- [创建自定义编辑器和设计器](../../extensibility/creating-custom-editors-and-designers.md)

 列出了四种类型的编辑器 IDE 可以托管并提供每个编辑器的说明。

- [项目类型](../../extensibility/internals/project-types.md)

 讨论项目如何控制代码的编译和生成方式、 如何编辑器处于打开状态，以及如何设置项目项的格式。
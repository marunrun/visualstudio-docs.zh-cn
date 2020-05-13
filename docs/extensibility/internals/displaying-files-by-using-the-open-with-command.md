---
title: 使用"打开"命令显示文件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open With command
- Open With command
- persistence, supporting Open With command
ms.assetid: 53794bc3-1b73-4d40-954e-cfade1abddcf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4051793077e613981e1dd5b44f1736878f5853e9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708582"
---
# <a name="display-files-by-using-the-open-with-command"></a>使用"打开使用"命令显示文件
项目可以要求 IDE 显示 **"打开"** 对话框。 此请求提示用户打开具有标准编辑器选择的文件。 以下步骤描述了此过程：

1. 项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>，指定 参数的值`OSE_UseOpenWithDialog``OSEOpenDocEditor`。

2. 根据文档的文件名扩展名，IDE 确定注册表中列出的哪些编辑器可以打开指定的文档，并在 **"打开使用"** 对话框中显示此信息。

    > [!NOTE]
    > 具有必须包含在"**打开使用"** 对话框中的内在编辑器的项目必须为每个此类编辑器注册一个编辑器工厂。 内部编辑器仅与特定类型的项目一起运行，在<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法的实现中强制执行。 IDE 具有用于核心文本编辑器和二进制编辑器的内置编辑器工厂。 IDE 还代表每个已注册的 Windows 文件关联创建编辑器工厂的实例。 此类文件的一个示例是 Microsoft Word。

3. 用户从 **"打开使用"** 对话框中选择项目后，IDE 就会通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法打开文档。 有关详细信息，请参阅[如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)。

## <a name="see-also"></a>请参阅
- [打开并保存项目项目项](../../extensibility/internals/opening-and-saving-project-items.md)
- [使用"打开文件"命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

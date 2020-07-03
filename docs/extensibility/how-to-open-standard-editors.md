---
title: 如何：打开标准编辑器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening
- projects [Visual Studio SDK], opening standard editors
ms.assetid: d5ce10f9-047a-4b74-aa1d-295128898b89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c12e831654e7e138289d33b6e6f0409328e22c8c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905785"
---
# <a name="how-to-open-standard-editors"></a>如何：打开标准编辑器
打开标准编辑器时，可以让 IDE 为指定的文件类型确定标准编辑器，而不是为文件指定特定于项目的编辑器。

 完成以下过程以实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> 方法。 这会在标准编辑器中打开项目文件。

## <a name="to-implement-the-openitem-method-with-a-standard-editor"></a>使用标准编辑器实现 OpenItem 方法

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> （ `RDT_EditLock` ）以确定文档数据对象文件是否已打开。

2. 如果文件已打开，则通过调用方法来 resurface 文件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> ，并 `IDO_ActivateIfOpen` 为参数指定值 `grfIDO` 。

     如果文件已打开，并且文档由与调用项目不同的项目所拥有，则您的项目将收到一条警告，指出正在打开的编辑器来自其他项目。 然后，将显示 "文件" 窗口。

3. 如果文档未打开或未在正在运行的文档表中，则调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法（ `OSE_ChooseBestStdEditor` ）以打开文件的标准编辑器。

     调用方法时，IDE 会执行以下任务：

    1. IDE 会在注册表中扫描 editor/{guidEditorType}/Extension 子项，以确定可以打开文件的编辑器，并且具有执行此操作的最高优先级。

    2. IDE 确定可以打开文件的编辑器后，IDE 会调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 。 此方法的编辑器实现将返回 IDE 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> 和站点新打开的文档所需的信息。

    3. 最后，IDE 使用常用持久性接口（如）加载文档 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 。

    4. 如果 IDE 之前确定层次结构或层次结构项可用，则 IDE 将对项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> 方法，以获取项目级上下文 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 指针，以通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> 方法调用传入。

4. <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> 如果希望让编辑器从项目获取上下文，请在 ide 调用项目时返回指向 ide 的指针。

     执行此步骤后，项目可以向编辑器提供其他服务。

     如果文档视图或文档视图对象已成功放置在窗口框架中，则会通过调用将对象初始化为其数据 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.LoadDocData%2A> 。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [打开并保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开项目特定的编辑器](../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开打开的文档的编辑器](../extensibility/how-to-open-editors-for-open-documents.md)
- [使用 "打开文件" 命令显示文件](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

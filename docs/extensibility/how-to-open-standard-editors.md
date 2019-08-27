---
title: 如何：打开标准编辑器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], opening
- projects [Visual Studio SDK], opening standard editors
ms.assetid: d5ce10f9-047a-4b74-aa1d-295128898b89
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1c85ab7f10881d76fbefea471851007f3d13da9b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325453"
---
# <a name="how-to-open-standard-editors"></a>如何：打开标准编辑器
当您打开标准编辑器时，您让 IDE 确定指定的文件类型，而不是指定文件的特定于项目的编辑器的标准编辑器。

 请完成以下步骤来实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>方法。 这将在标准编辑器中打开项目文件。

## <a name="to-implement-the-openitem-method-with-a-standard-editor"></a>若要使用标准编辑器实现 OpenItem 方法

1. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>(`RDT_EditLock`) 来确定文档数据对象文件是否已打开。

2. 如果该文件已打开，通过调用 resurface 文件<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>方法，指定的值`IDO_ActivateIfOpen`为`grfIDO`参数。

     如果文件已打开，并且该文档拥有的不同于调用项目的项目，您的项目得到从另一个项目正在打开的编辑器是一条警告。 然后显示文件窗口中。

3. 如果文档未打开或未在运行文档表中，调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法 (`OSE_ChooseBestStdEditor`) 以打开该文件的标准编辑器。

     当调用该方法时，IDE 将执行以下任务：

    1. IDE 将扫描编辑器 / {guidEditorType} / 扩展子项中注册表，以确定哪个编辑器可以打开文件，并具有执行此操作的最高优先级。

    2. IDE 已确定哪个编辑器可以打开该文件后，IDE 会调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>。 在编辑器实现此方法的返回信息所需的 IDE 来调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>和站点的新打开的文档。

    3. 最后，IDE 将文档加载使用常规持久性接口，如<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>。

    4. 如果 IDE 先前已确定的层次结构或层次结构项是可用，IDE 会调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A>方法的项目获取项目级上下文<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>指针将传递回用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>方法调用。

4. 返回<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>指针，指向 IDE 时 IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A>上你项目中，如果你想要让编辑器获取上下文从你的项目。

     执行此步骤允许项目的产品/服务到编辑器的其他服务。

     如果在窗口框架中，已成功放置文档视图或文档视图对象，则对象初始化其数据与通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.LoadDocData%2A>。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [打开和保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开项目特定的编辑器](../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开编辑器的打开的文档](../extensibility/how-to-open-editors-for-open-documents.md)
- [使用打开文件命令显示文件](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
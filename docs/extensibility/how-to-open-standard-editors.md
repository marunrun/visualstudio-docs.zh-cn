---
title: 如何：打开标准编辑器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], opening
- projects [Visual Studio SDK], opening standard editors
ms.assetid: d5ce10f9-047a-4b74-aa1d-295128898b89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f42cfa64106acc41358568f4c8f6bca2cd1141fd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710787"
---
# <a name="how-to-open-standard-editors"></a>如何：打开标准编辑器
打开标准编辑器时，允许 IDE 确定指定文件类型的标准编辑器，而不是为文件指定特定于项目的编辑器。

 完成以下过程以实现该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>。 这将在标准编辑器中打开项目文件。

## <a name="to-implement-the-openitem-method-with-a-standard-editor"></a>使用标准编辑器实现 OpenItem 方法

1. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>`RDT_EditLock`（ ） 以确定文档数据对象文件是否已打开。

2. 如果文件已打开，则通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>方法重新显示文件，为`IDO_ActivateIfOpen``grfIDO`参数指定 值。

     如果文件处于打开状态，并且文档由与调用项目不同的项目所有，则项目将收到一条警告，指出正在打开的编辑器来自另一个项目。 然后，文件窗口将浮出水面。

3. 如果文档未打开或在正在运行的文档表中打开，请调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法 （`OSE_ChooseBestStdEditor`） 以打开文件的标准编辑器。

     调用 方法时，IDE 将执行以下任务：

    1. IDE 扫描注册表中的编辑器/[guidEditorType]/扩展子键，以确定哪个编辑器可以打开该文件，并且具有执行此操作的最高优先级。

    2. 在 IDE 确定哪个编辑器可以打开该文件后，IDE 将<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>调用 。 此方法的编辑器实现返回 IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>新打开的文档并进行站点所需的信息。

    3. 最后，IDE 使用通常的持久性接口（如<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>） 加载文档。

    4. 如果 IDE 以前确定层次结构或层次结构项可用，则 IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A>项目上的方法，以获取项目级上下文<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>指针以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>方法调用传递。

4. 如果要让<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>编辑器从项目中获取上下文，则当<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A>IDE 调用项目时，返回指向 IDE 的指针。

     执行此步骤可以使项目向编辑器提供其他服务。

     如果文档视图或文档视图对象已成功驻留在窗口框架中，则通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.LoadDocData%2A>使用 其数据初始化该对象。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [打开并保存项目项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开特定于项目的编辑器](../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开打开文档的编辑器](../extensibility/how-to-open-editors-for-open-documents.md)
- [使用"打开文件"命令显示文件](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

---
title: 确定哪个编辑器在项目中打开文件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af7037a3b4bfbae1801e802256af240d017d2789
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708662"
---
# <a name="determine-which-editor-opens-a-file-in-a-project"></a>确定哪个编辑器在项目中打开文件
当用户在项目中打开文件时，环境将经历轮询过程，最终打开该文件的相应编辑器或设计器。 对于标准和自定义编辑器，环境使用的初始过程是相同的。 轮询要使用哪个编辑器来打开文件时，环境使用各种条件，并且 VSPackage 必须在此过程中与环境协调。

 例如，当用户从 **"文件"** 菜单中选择**Open**命令，然后选择*filename.rtf（* 或具有 *.rtf*扩展名的任何其他文件）时，环境将调用每个项目<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>的实现，最终循环遍解决方案中的所有项目实例。 项目返回一组标志，这些标志按优先级标识文档上的声明。 使用最高优先级，环境调用适当的<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>方法。 有关轮询过程的详细信息，请参阅[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

 "杂项文件"项目声明其他项目未声明的所有文件。 这样，自定义编辑器可以在标准编辑器打开文档之前打开文档。 如果"杂项文件"项目声明文件，则环境将调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法以使用标准编辑器打开文件。 环境检查其内部注册的编辑器列表，以查找处理 *.rtf*文件。 此列表位于注册表中，位于以下键：

 **HKEY_LOCAL_MACHINE_软件_微软_VisualStudio\\\<版本>_\\\<编辑器工厂 guid>\扩展**

 环境还检查**HKEY_CLASSES_ROOT_CLSID**键中的类标识符，以检查具有子键**DocObject**的任何对象。 如果找到文件扩展名，则在 Visual Studio 中就地创建应用程序的嵌入式版本，如 Microsoft Word。 这些文档对象必须是实现接口的<xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>复合文件，或者该对象必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>接口。

 如果注册表中没有 *.rtf*文件的编辑器工厂，则环境将在**HKEY_CLASSES_ROOT\\.rtf**键中查找，并打开其中指定的编辑器。 如果在**HKEY_CLASSES_ROOT**中找不到文件扩展名，则环境使用 Visual Studio 核心文本编辑器打开该文件（如果该文件是文本文件）。

 如果核心文本编辑器失败（如果文件不是文本文件，则发生这种情况），则环境会对其文件使用其二进制编辑器。

 如果环境在其注册表中确实找到了 *.rtf*扩展的编辑器，它将加载实现此编辑器工厂的 VSPackage。 环境调用新<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>VSPackage 上的方法。 VSPackage 调用`QueryService` `SID_SVsRegistorEditor`，使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>方法将编辑器工厂注册到环境中。

 环境现在重新检查其注册编辑器的内部列表，以查找*新注册的编辑器工厂.rtf*文件。 环境调用方法的实现，<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>传入要创建的文件名和视图类型。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>
- <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>

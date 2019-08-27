---
title: 确定哪个编辑器在项目中打开文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e54a922cfa36aad8c8c7e68e87012926a8ab715
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351599"
---
# <a name="determine-which-editor-opens-a-file-in-a-project"></a>确定哪个编辑器打开文件在项目中
当用户打开文件时在项目中时，环境都要通过轮询处理过程，最终打开适当的编辑器或设计器中的为该文件。 受雇于环境的初始过程是相同的标准和自定义编辑器。 在环境中使用的各种条件轮询的编辑器，用于打开文件时，VSPackage 必须在此过程中协调环境。

 例如，如果用户选择**开放**命令**文件**菜单中，，再选择*filename.rtf* (或者任何其他文件，其中 *.rtf*扩展名)，环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>实现为每个项目，最终循环解决方案中的所有项目实例。 项目返回一组按优先级别标识声明上文档的标志。 使用最高优先级，环境在调用适当<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>方法。 轮询处理过程的详细信息，请参阅[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

 杂项文件项目声明不声明由其他项目的所有文件。 这样一来，标准编辑器打开它们之前，自定义编辑器可以打开文档。 杂项文件项目声明一个文件，如果环境在调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法使用标准编辑器打开该文件。 在环境检查已注册编辑器中提供一个处理其内部列表 *.rtf*文件。 此列表位于注册表中的以下项：

 **HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\\<版本 > \Editors\\\<编辑器工厂 guid > \Extensions**

 在环境还检查类标识符**HKEY_CLASSES_ROOT\CLSID**有一个子项的任何对象的键**DocObject**。 如果在其中找到的文件扩展名，该应用程序，如 Microsoft Word 的嵌入式的版本是 Visual Studio 中创建的就地。 这些文档对象必须实现的复合文件<xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>接口或该对象必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>接口。

 如果没有编辑器工厂 *.rtf*文件在注册表中，然后在环境中所示**HKEY_CLASSES_ROOT\\.rtf**密钥，然后打开编辑器中指定。 如果在找不到文件扩展名**HKEY_CLASSES_ROOT**，则该环境使用 Visual Studio 核心文本编辑器打开该文件，如果它是一个文本文件。

 如果失败核心文本编辑器，就会出现如果文件不是一个文本文件，然后在环境中使用其二进制编辑器的文件。

 如果在环境找到编辑器 *.rtf*其注册表中的扩展，它会加载实现此编辑器工厂的 VSPackage。 环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>上新的 VSPackage 的方法。 VSPackage 调用`QueryService`有关`SID_SVsRegistorEditor`，并使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>方法以向环境注册编辑器工厂。

 在环境现在重新检查已注册的编辑器中，找到的新注册的编辑器工厂其内部列表 *.rtf*文件。 环境调用你的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法，传入要创建的文件名称和视图类型。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>
- <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>
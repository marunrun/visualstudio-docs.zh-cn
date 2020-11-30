---
title: 确定在项目中打开文件的编辑器 |Microsoft Docs
description: 了解 Visual Studio 用来确定在项目中打开文件的编辑器的注册表项和 Visual Studio SDK 方法。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: f9574a3319d3c43c17d7351e462b6956ae899d84
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328400"
---
# <a name="determine-which-editor-opens-a-file-in-a-project"></a>确定在项目中打开文件的编辑器
当用户打开项目中的文件时，环境将经历一个轮询过程，最后打开该文件的相应编辑器或设计器。 环境使用的初始过程对于标准编辑器和自定义编辑器都是相同的。 环境在轮询用于打开文件的编辑器时使用各种条件，而 VSPackage 必须在此过程中与环境进行协调。

 例如，当用户从 "**文件**" 菜单中选择 "**打开**" 命令，然后选择 " *filename* " (或扩展名为 *.rtf*) 的其他任何文件时，环境将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 为每个项目调用实现，最终循环遍历解决方案中的所有项目实例。 项目返回一组标志，这些标志按优先级标识文档中的声明。 使用最高优先级时，环境将调用适当的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> 方法。 有关轮询过程的详细信息，请参阅 [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

 "杂项文件" 项目声明了其他项目未声明的所有文件。 这样，自定义编辑器可以在标准编辑器打开文档之前打开它们。 如果杂项文件项目声明文件，则环境将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法以使用标准编辑器打开文件。 环境检查其已注册编辑器的内部列表，其中一个用于处理 *.rtf* 文件的编辑器。 此列表位于注册表中的以下项：

 **HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ \<version> \Editors \\ \<editor factory guid> \Extensions**

 环境还会检查 **HKEY_CLASSES_ROOT\CLSID** 项中具有子项 **DocObject** 的任何对象的类标识符。 如果在此处找到文件扩展名，则会在 Visual Studio 中就地创建应用程序的嵌入式版本，如 Microsoft Word。 这些文档对象必须是实现接口的复合文件 <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage> ，或者对象必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 接口。

 如果在注册表中没有针对 *.rtf* 文件的编辑器工厂，则环境将查找 **HKEY_CLASSES_ROOT \\ .rtf** 密钥并打开其中指定的编辑器。 如果在 **HKEY_CLASSES_ROOT** 中找不到该文件扩展名，则该环境将使用 Visual Studio core 文本编辑器打开该文件（如果它是文本文件）。

 如果核心文本编辑器失败（如果文件不是文本文件，则会发生这种情况），环境将为文件使用其二进制编辑器。

 如果环境在其注册表中找到了 *.rtf* 扩展名的编辑器，则会加载实现此编辑器工厂的 VSPackage。 环境在新的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> VSPackage 上调用方法。 VSPackage 调用 `QueryService` `SID_SVsRegistorEditor` ，使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> 方法向环境注册编辑器工厂。

 该环境现在复查列为其内部注册编辑器的列表，以便查找 *.rtf* 文件的新注册编辑器工厂。 环境调用方法的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> ，并传入要创建的文件名称和视图类型。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>
- <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>

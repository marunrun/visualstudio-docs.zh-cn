---
title: 确定哪个编辑器在项目中打开文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1c79860f770a6b04a17786cfb281fc3c0e4dffda
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196762"
---
# <a name="determining-which-editor-opens-a-file-in-a-project"></a>确定使用哪个编辑器打开项目中的文件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当用户打开文件时在项目中时，环境都要通过轮询处理过程，最终打开适当的编辑器或设计器中的为该文件。 受雇于环境的初始过程是相同的标准和自定义编辑器。 在环境中使用的各种条件轮询的编辑器，用于打开文件时，VSPackage 必须在此过程中协调环境。  
  
 例如，如果用户选择**开放**命令**文件**菜单中，再选择`filename`.rtf （或任何其他文件扩展名为.rtf），环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>对于每个项目，通过在解决方案中的所有项目实例最终循环的实现。 项目返回一组按优先级别标识声明上文档的标志。 使用最高优先级，环境在调用适当<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>方法。 有关进一步信息轮询过程中，[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。  
  
 杂项文件项目声明不声明由其他项目的所有文件。 这样一来，标准编辑器打开它们之前，自定义编辑器可以打开文档。 杂项文件项目声明一个文件，如果环境在调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法使用标准编辑器打开该文件。 环境会检查其内部的已注册编辑器可处理.rtf 文件的列表。 此列表位于注册表中的以下项：  
  
 [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\<`version`>\Editors\\{<`editor factory guid`>}\Extensions]  
  
 环境还会检查 HKEY_CLASSES_ROOT\CLSID 项具有子项 DocObject 的任何对象中的类标识符。 如果在其中找到的文件扩展名，该应用程序，如 Microsoft Word 的嵌入式的版本是 Visual Studio 中创建的就地。 这些文档对象必须实现的复合文件<xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>接口或该对象必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>接口。  
  
 如果没有编辑器工厂的.rtf 文件在注册表中，则环境会查找在 HKEY_CLASSES_ROOT \\.rtf 密钥，然后打开编辑器中指定。 如果在 HKEY_CLASSES_ROOT 中找不到文件扩展名，环境将使用 Visual Studio 核心文本编辑器打开该文件，如果它是一个文本文件。  
  
 如果失败核心文本编辑器，就会出现如果文件不是一个文本文件，然后在环境中使用其二进制编辑器的文件。  
  
 如果在环境找到编辑器.rtf 扩展在其注册表中，它会加载实现此编辑器工厂的 VSPackage。 环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>上新的 VSPackage 的方法。 VSPackage 调用`QueryService`有关`SID_SVsRegistorEditor`，并使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>方法以向环境注册编辑器工厂。  
  
 现在可以在环境重新检查已注册的编辑器中，找到.rtf 文件的新注册的编辑器工厂其内部列表。 环境调用你的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法，传入要创建的文件名称和视图类型。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>   
 <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>

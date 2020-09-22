---
title: 使用 "打开方式" 命令显示文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open With command
- Open With command
- persistence, supporting Open With command
ms.assetid: 53794bc3-1b73-4d40-954e-cfade1abddcf
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: de43b6c4f441f8c6bde2d6c248274aed3937a7ee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840414"
---
# <a name="displaying-files-by-using-the-open-with-command"></a>使用“通过命令打开”显示文件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目可以要求 IDE 显示 " **打开方式** " 对话框。 此请求将提示用户打开具有选定标准编辑器的文件。 以下步骤介绍了此过程。  
  
1. 项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> ，并为参数指定 OSE_UseOpenWithDialog 的值 `OSEOpenDocEditor` 。  
  
2. 根据文档的文件扩展名，IDE 将确定注册表中列出的哪些编辑器可以打开指定的文档，并在 " **打开方式** " 对话框中显示此信息。  
  
    > [!NOTE]
    > 具有必须包含在 " **打开方式** " 对话框中的内部编辑器的项目必须为每个此类编辑器注册编辑器工厂。 内部编辑器仅与特定类型的项目一起工作，这在方法的实现中强制执行 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 。 IDE 为 core 文本编辑器和二进制编辑器提供内置编辑器工厂。 IDE 还代表每个已注册的 Windows 文件关联创建编辑器工厂的实例。 此类文件的一个示例是 Microsoft Word。  
  
3. 一旦用户从 " **打开方式** " 对话框中选择一个项，IDE 就会通过调用方法打开该文档 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 。 有关详细信息，请参阅 [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)。  
  
## <a name="see-also"></a>另请参阅  
 [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)   
 [使用 "打开文件" 命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)   
 [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

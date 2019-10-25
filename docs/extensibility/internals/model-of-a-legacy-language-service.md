---
title: 旧版语言服务的模型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, model
ms.assetid: d8ae1c0c-ee3d-4937-a581-ee78d0499793
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5b87106060d3fd66b3659f5d49159ebbb9be9ef6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726379"
---
# <a name="model-of-a-legacy-language-service"></a>旧版语言服务模型
语言服务定义特定语言的元素和功能，并用于向编辑器提供特定于该语言的信息。 例如，编辑器需要了解语言的元素和关键字，以便支持语法着色。

 语言服务与编辑器所管理的文本缓冲区和包含编辑器的视图紧密协作。 Microsoft IntelliSense **Quick Info**选项是语言服务提供的功能的一个示例。

## <a name="a-minimal-language-service"></a>最小语言服务
 最基本的语言服务包含以下两个对象：

- *语言服务*实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 接口。 语言服务包含有关该语言的信息，包括其名称、文件扩展名、代码窗口管理器和 colorizer。

- *Colorizer*实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。

  以下概念绘图显示了基本语言服务的模型。

  ![语言服务模型图形](../../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel")基本语言服务模型

  文档窗口承载编辑器的*文档视图*，在本例中为 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 核心编辑器。 文档视图和文本缓冲区由编辑器所有。 这些对象通过一个名为 "*代码窗口*" 的专用文档窗口处理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 "代码" 窗口包含在由 IDE 创建和控制的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 对象中。

  加载具有给定扩展名的文件时，编辑器将查找与该扩展关联的语言服务，并通过调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> 方法将其传递到代码窗口。 语言服务将返回一个*代码窗口管理器，该管理器*实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 接口。

  下表概述了模型中的对象。

| 组件 | 对象 | 函数 |
|------------------| - | - |
| 文本缓冲区 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> | Unicode 读/写文本流。 文本可能会使用其他编码。 |
| “代码”窗口 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> | 包含一个或多个文本视图的文档窗口。 在多文档界面（MDI）模式下 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 时，代码窗口是一个 MDI 子级。 |
| 文本视图 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> | 允许用户使用键盘和鼠标导航并查看文本的窗口。 文本视图将作为编辑器显示给用户。 您可以在普通编辑器窗口、"输出" 窗口和 "即时" 窗口中使用文本视图。 此外，还可以在代码窗口中配置一个或多个文本视图。 |
| 文本管理器 | 由你从中获取 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> 指针的 <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> 服务管理 | 维护前面介绍的所有组件共享的公共信息的组件。 |
| 语言服务 | 依赖实现;实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> | 一个对象，该对象为编辑器提供特定于语言的信息，如语法突出显示、语句完成和大括号匹配。 |

## <a name="see-also"></a>请参阅
- [自定义编辑器中的文档数据和文档视图](../../extensibility/document-data-and-document-view-in-custom-editors.md)
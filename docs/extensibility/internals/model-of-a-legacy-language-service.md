---
title: 传统语言服务模型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, model
ms.assetid: d8ae1c0c-ee3d-4937-a581-ee78d0499793
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7f024a02641902843f673ce3ff8583a4bce3b135
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707039"
---
# <a name="model-of-a-legacy-language-service"></a>旧版语言服务模型
语言服务定义特定语言的元素和功能，并用于向编辑器提供特定于该语言的信息。 例如，编辑器需要知道语言的元素和关键字，以支持语法着色。

 语言服务与编辑器管理的文本缓冲区和包含编辑器的视图密切合作。 Microsoft IntelliSense**快速信息**选项是语言服务提供的功能的示例。

## <a name="a-minimal-language-service"></a>最小语言服务
 最基本的语言服务包含以下两个对象：

- *语言服务*实现接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>。 语言服务包含有关该语言的信息，包括其名称、文件名扩展名、代码窗口管理器和着色器。

- *着色器*实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>接口。

  以下概念图显示了基本语言服务的模型。

  ![语言服务模型图形](../../extensibility/media/vslanguageservicemodel.gif "vs 语言服务模型")基本语言服务模型

  文档窗口承载编辑器*的文档视图*，在这种情况下，则承载[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]核心编辑器。 文档视图和文本缓冲区归编辑器所有。 这些对象通过称为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]*代码窗口*的专用文档窗口进行使用。 代码窗口包含在由 IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>创建和控制的对象中。

  加载具有给定扩展名的文件时，编辑器将查找与该扩展名关联的语言服务，并通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>方法传递给它代码窗口。 语言服务返回一个*代码窗口管理器*，该管理器实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>接口。

  下表概述了模型中的对象。

| 组件 | Object | 函数 |
|------------------| - | - |
| 文本缓冲区 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> | Unicode 读/写文本流。 文本可以使用其他编码。 |
| 代码窗口 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> | 包含一个或多个文本视图的文档窗口。 当[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]处于多文档接口 （MDI） 模式时，代码窗口是 MDI 子窗口。 |
| 文本视图 | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> | 允许用户使用键盘和鼠标导航和查看文本的窗口。 文本视图以编辑器形式显示给用户。 您可以在普通编辑器窗口、"输出"窗口和"立即"窗口中使用文本视图。 此外，您还可以在代码窗口中配置一个或多个文本视图。 |
| 文本管理器 | 由<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>服务管理，从中获取<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager>指针 | 维护前面描述的所有组件共享的常见信息的组件。 |
| 语言服务 | 依实施;实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> | 向编辑器提供特定于语言的信息的对象，如语法突出显示、语句完成和大括号匹配。 |

## <a name="see-also"></a>请参阅
- [自定义编辑器中的文档数据和文档视图](../../extensibility/document-data-and-document-view-in-custom-editors.md)

---
title: 自定义编辑器中的语法着色 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - syntax coloring
ms.assetid: 74900b9a-baef-432a-8231-4568fb5e19ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6296c8451684a121ac42dbde6619c0ebbb421908
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699336"
---
# <a name="syntax-coloring-in-custom-editors"></a>自定义编辑器中的语法着色
Visual Studio 环境 SDK 编辑器（包括核心编辑器）使用语言服务来识别特定的语法项，并为给定的文档视图以指定的颜色显示它们。

## <a name="colorization-requirements"></a>着色要求
 实现语言服务的 colorizer 的所有编辑器都必须：

1. 使用实现的对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 管理要着色的文本，并使用实现的对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 来提供文本文档视图。

2. 通过使用语言服务的标识 GUID 查询 VSPackage 的服务提供程序，获取特定语言服务的接口。

3. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> 实现的对象的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 。 此方法将语言服务与 VSPackage 用于 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 管理要着色的文本的实现相关联。

## <a name="core-editor-usage-of-a-language-services-colorizer"></a>语言服务的 Colorizer 的核心编辑器用法
 当使用 colorizer 的语言服务由核心编辑器的实例获取时，会自动分析和呈现语言服务的 colorizer 的文本，而无需任何进一步的干预。

 IDE 以透明方式：

- 根据需要调用 colorizer，以便分析和分析文本，因为它是在的实现中添加或修改的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 。

- 确保 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 使用 colorizer 返回的信息更新并重新绘制由实现提供的文档视图提供的显示器。

## <a name="non-core-editor-usage-of-a-language-services-colorizer"></a>语言服务的 Colorizer 的非核心编辑器用法
 非核心编辑器实例还可以使用语言服务的语法着色服务，但它们必须显式检索和应用服务的 colorizer，并自行重绘其文档视图。

 为此，非核心编辑器必须：

1. 获取用于实现和)  (语言服务的 colorizer <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> 。 VSPackage 通过 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> 在语言服务的接口上调用方法来实现此功能。

2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 方法以请求将某个特定范围的文本着色。

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法返回值的数组，其中每个字母都是着色的文本范围。 它还将文本跨距标识为特定类型的可着色项，例如注释、关键字或数据类型。

3. 使用返回的着色信息 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 重绘并显示其文本。

> [!NOTE]
> 除了使用语言服务的 colorizer 外，VSPackage 还可以选择使用通用 Visual Studio 环境 SDK 文本着色机制。 有关此机制的详细信息，请参阅 [使用字体和颜色](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015)。

## <a name="see-also"></a>另请参阅

- [在旧版语言服务中进行语法着色](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [实现语法着色](../extensibility/internals/implementing-syntax-coloring.md)
- [如何：使用内置的可着色项](../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [自定义可着色项](../extensibility/internals/custom-colorable-items.md)

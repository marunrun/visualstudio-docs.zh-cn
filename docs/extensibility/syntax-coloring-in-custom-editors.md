---
title: 自定义编辑器中的语法着色 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699336"
---
# <a name="syntax-coloring-in-custom-editors"></a>自定义编辑器中的语法着色
Visual Studio 环境 SDK 编辑器（包括核心编辑器）使用语言服务来标识特定的语法项目，并显示它们具有给定文档视图的指定颜色。

## <a name="colorization-requirements"></a>着色要求
 实现语言服务着色器的所有编辑必须：

1. 使用对象实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>来管理要着色的文本和对象实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>以提供文本的文档视图。

2. 通过使用语言服务的标识 GUID 查询 VSPackage 的服务提供商，获取特定语言服务的接口。

3. 调用对象<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A>实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>的方法。 此方法将语言服务与 VSPackage<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>用于管理要着色的文本的实现关联。

## <a name="core-editor-usage-of-a-language-services-colorizer"></a>语言服务着色器的核心编辑器使用
 当核心编辑器的实例获得带有着色器的语言服务时，语言服务的着色器会自动解析和呈现文本，而无需您进行任何进一步的干预。

 IDE 透明化：

- 根据需要调用着色器，以在 中添加或修改文本时对其进行分析<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>和分析。

- 确保使用着色器返回的信息更新和重新绘制<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>实现提供的文档视图提供的显示。

## <a name="non-core-editor-usage-of-a-language-services-colorizer"></a>语言服务着色器的非核心编辑器使用
 非核心编辑器实例也可以使用语言服务的语法着色服务，但它们必须显式检索和应用服务的着色器，并重新绘制其文档视图本身。

 为此，非核心编辑器必须：

1. 获取语言服务的着色器对象（实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2>）。 VSPackage 通过在语言服务的接口上<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>调用方法来实现此。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法以请求对特定文本范围进行着色。

     该方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>返回一个值数组，对于正在着色的文本范围中的每个字母一个。 它还将文本范围标识为特定类型的可着色项，如注释、关键字或数据类型。

3. 使用 返回<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>的着色信息重新绘制和显示其文本。

> [!NOTE]
> 除了使用语言服务的着色器外，VSPackage 还可以选择使用通用的可视化工作室环境 SDK 文本着色机制。 有关此机制的详细信息，请参阅[使用字体和颜色](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015)。

## <a name="see-also"></a>请参阅

- [在旧版语言服务中进行语法着色](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [实现语法着色](../extensibility/internals/implementing-syntax-coloring.md)
- [如何：使用内置的可着色项](../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [自定义可着色项](../extensibility/internals/custom-colorable-items.md)

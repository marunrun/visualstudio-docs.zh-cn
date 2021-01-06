---
title: 旧版语言服务中的语法着色 |Microsoft Docs
description: 了解 Visual Studio 如何实现旧版语言服务中的语法着色服务来识别语言的元素，并在编辑器中以颜色显示它们。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring
- language services, syntax coloring
ms.assetid: f65ff67e-8c20-497a-bebf-5e2a5b5b012f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bbf063efe30d90c84848222ff931be43834efbad
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876384"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>在旧版语言服务中进行语法着色

Visual Studio 使用着色服务来识别语言的元素，并在编辑器中用指定的颜色显示它们。

## <a name="colorizer-model"></a>Colorizer 模型
 语言服务实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口，然后由编辑器使用。 此实现是语言服务的单独对象，如下图所示：

 ![SVC 着色程序图](../../extensibility/internals/media/figlgsvccolorizer.gif)

> [!NOTE]
> 语法着色服务独立于着色文本的通用 Visual Studio 机制。 有关支持着色的常规机制的详细信息 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ，请参阅 [使用字体和颜色](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015)。

 除 colorizer 外，语言服务还可以提供由编辑器使用的自定义可着色项，方法是公布它提供自定义可着色项。 为此，可以 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> 在实现接口的同一对象上实现接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 。 当编辑器调用方法时，它会返回自定义可着色项的数目 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> ，当编辑器调用方法时，它将返回单个自定义可着色项 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> 。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>方法返回实现接口的对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 。 如果语言服务支持24位或高颜色值，则它必须 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 在与接口相同的对象上实现接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 。

## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>VSPackage 如何使用语言服务 Colorizer

1. VSPackage 必须获取适当的语言服务，这需要 language service VSPackage 来执行以下操作：

    1. 使用实现接口的对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 获取要着色的文本。

         通常使用实现接口的对象显示文本 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。

    2. 通过查询 VSPackage 的服务提供程序来获取语言服务 GUID。 语言服务在注册表中按文件扩展名进行标识。

    3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>通过调用其方法将语言服务与相关联 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> 。

2. VSPackage 现在可以获取并使用 colorizer 对象，如下所示：

    > [!NOTE]
    > 使用核心编辑器的 Vspackage 不必显式获取语言服务的 colorizer 对象。 当核心编辑器的实例获取适当的语言服务后，它就会执行此处显示的所有着色任务。

    1. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> 通过 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> 对语言服务的对象调用方法，获取语言服务的 colorizer 对象，该对象可实现和接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 。

    2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 方法可获取特定范围文本的 colorizer 信息。

         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 返回一组值，每个值对应于文本跨距中要着色的每个字符。 这些值是可着色项列表的索引，它是由核心编辑器维护的默认可着色项列表或由语言服务本身维护的自定义可着色项列表。

    3. 使用方法返回的着色信息 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 显示选定的文本。

> [!NOTE]
> 除了使用 language service colorizer 外，VSPackage 还可以使用一般用途的 Visual Studio 文本着色机制。 有关此机制的详细信息，请参阅 [使用字体和颜色](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015)。

## <a name="in-this-section"></a>本节内容
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)

 讨论编辑器如何访问语言服务的语法着色，以及语言服务必须实现哪些功能才能支持语法着色。

- [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

 演示如何在语言服务中使用内置的可着色项。

- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)

 讨论如何实现自定义可着色项。

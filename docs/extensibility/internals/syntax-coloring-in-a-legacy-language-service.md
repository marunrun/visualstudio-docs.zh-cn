---
title: 旧版语言服务中的语法着色 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring
- language services, syntax coloring
ms.assetid: f65ff67e-8c20-497a-bebf-5e2a5b5b012f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 47d7164df48011907f8bea408c0acf08250d0657
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331304"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>在旧版语言服务中进行语法着色

Visual Studio 使用着色服务识别的语言的元素并将其用在编辑器中指定的颜色显示。

## <a name="colorizer-model"></a>着色器模型
 语言服务实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>接口，然后由编辑器。 此实现是语言服务中，从一个单独的对象，如下图中所示：

 ![SVC 着色程序图](../../extensibility/internals/media/figlgsvccolorizer.gif)

> [!NOTE]
> 语法突出显示服务是独立于用于对文本着色的常规 Visual Studio 机制。 有关常规详细信息[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]机制支持着色，请参阅[使用的字体和颜色](../../extensibility/using-fonts-and-colors.md)。

 除了着色器，语言服务可以提供由编辑器中，通过它提供自定义可着色项的广告的自定义可着色项。 您可以执行此操作通过实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>接口上实现的相同对象<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口。 当在编辑器调用时，它返回自定义可着色项的数目<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>方法，并返回单个自定义可着色项，当在编辑器调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>方法。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>方法返回一个对象，实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>接口。 如果语言服务支持 24 位或高颜色值，它必须实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>上与相同的对象的接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>接口。

## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>VSPackage 如何使用语言服务着色器

1. VSPackage 必须获取相应的语言服务，后者需要语言服务 VSPackage 以执行以下操作：

    1. 使用一个对象，实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>接口，用于获取要进行着色的文本。

         通常使用实现的对象显示文本<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口。

    2. 通过查询语言服务 GUID 的 vspackage 的服务提供程序获取语言服务。 语言服务由文件扩展名标识注册表中。

    3. 将使用的语言服务相关联<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>通过调用其<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A>方法。

2. VSPackage 现在可以获取并使用着色器对象，如下所示：

    > [!NOTE]
    > 使用核心编辑器的 Vspackage 无需显式获取一种语言服务的着色器对象。 只要核心编辑器的实例获取适当的语言服务，它将执行如下所示的所有颜色设置任务。

    1. 获取语言服务的着色器对象，用于实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>，并<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2>接口，通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>语言服务上的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>对象。

    2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法来获取特定范围的文本的着色器信息。

         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 返回一个值，一个用于着色文本跨距中的每个字符数组。 值是由核心编辑器维护的默认可着色项列表或维护语言服务本身的自定义可着色项列表的可着色项列表的索引。

    3. 使用返回的着色信息<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法来显示所选的文本。

> [!NOTE]
> 除了使用的语言服务 colorizer，VSPackage 还可以使用常规用途的 Visual Studio 文本着色机制。 有关此机制的详细信息，请参阅[使用字体和颜色](../../extensibility/using-fonts-and-colors.md)。

## <a name="in-this-section"></a>本节内容
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)

 讨论如何编辑器访问语言服务的语法颜色设置和语言服务必须实现此方法可以支持语法着色。

- [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

 演示如何使用内置的可着色项从语言服务。

- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)

 讨论如何实现自定义可着色项。

## <a name="see-also"></a>请参阅

- [使用字体和颜色](../../extensibility/using-fonts-and-colors.md)
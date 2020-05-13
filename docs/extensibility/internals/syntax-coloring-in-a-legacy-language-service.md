---
title: 旧语言服务中的语法着色 |微软文档
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
ms.openlocfilehash: 2589ec24f230287306e0ff7e802d381fb6ab18b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704761"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>在旧版语言服务中进行语法着色

Visual Studio 使用着色服务来标识语言的元素，并在编辑器中使用指定的颜色显示它们。

## <a name="colorizer-model"></a>着色器模型
 语言服务实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>接口，然后由编辑器使用。 此实现是语言服务中的单独对象，如下图所示：

 ![SVC 着色程序图](../../extensibility/internals/media/figlgsvccolorizer.gif)

> [!NOTE]
> 语法着色服务与用于着色文本的一般 Visual Studio 机制是分开的。 有关支持着色的一般[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]机制的详细信息，请参阅[使用字体和颜色](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015)。

 除了着色器之外，语言服务还可以通过通告提供自定义可着色项目来提供编辑器使用的自定义可着色项目。 可以通过在实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems><xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口的同一对象上实现接口来实现此目的。 当编辑器调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>方法时，它返回自定义可着色项的数量，并在编辑器调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>方法时返回单个自定义可着色项。

 该方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>返回实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>接口的对象。 如果语言服务支持 24 位或高颜色值，则必须在接口的同<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>一对象上实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>接口。

## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>VS 包如何使用语言服务着色器

1. VSPackage 必须获得适当的语言服务，这需要语言服务 VSPackage 执行以下操作：

    1. 使用实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>接口的对象使文本着色。

         文本通常使用实现接口的对象显示<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。

    2. 通过查询语言服务 GUID 的 VSPackage 的服务提供商来获取语言服务。 语言服务在注册表中通过文件扩展名标识。

    3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>通过调用语言<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A>服务的方法将语言服务与 关联。

2. VSPackage 现在可以获取和使用着色器对象，如下所示：

    > [!NOTE]
    > 使用核心编辑器的 VS 包不必显式获取语言服务的着色器对象。 一旦核心编辑器的实例获得适当的语言服务，它将执行此处显示的所有着色任务。

    1. 通过在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>语言服务<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2><xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>的对象上调用方法，获取实现 和 接口的语言服务的着色器对象。

    2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法以获取特定文本范围的着色器信息。

         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>返回一个值数组，对于着色的文本范围中的每个字符，一个。 这些值是索引到可着色项列表，该列表是核心编辑器维护的默认可着色项列表，或者由语言服务本身维护的自定义可着色项列表。

    3. 使用 方法返回的<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>着色信息显示所选文本。

> [!NOTE]
> 除了使用语言服务着色器外，VSPackage 还可以使用通用视觉工作室文本着色机制。 有关此机制的详细信息，请参阅[使用字体和颜色](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015)。

## <a name="in-this-section"></a>本节内容
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)

 讨论编辑器如何访问语言服务的语法着色，以及语言服务必须实现什么来支持语法着色。

- [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

 演示如何使用语言服务中的内置可着色项。

- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)

 讨论如何实现自定义可着色项。

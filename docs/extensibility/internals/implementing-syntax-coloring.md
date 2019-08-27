---
title: 实现语法着色 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring, implementing
- editors [Visual Studio SDK], colorizing text
- text, colorizing in editors
ms.assetid: 96e762ca-efd0-41e7-8958-fda4897c8c7a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f577f4cf21110a1b40680059b385d413c9c6902
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324237"
---
# <a name="implementing-syntax-coloring"></a>实现语法着色
时语言服务都会提供语法着色，分析器将一行文本转换为可着色项的数组，并返回与这些可着色项相对应的令牌类型。 分析器应返回属于可着色项列表的令牌类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 根据分配给相应的标记类型的着色器对象的属性在代码窗口中显示每个可着色项。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 不指定分析器接口，并且分析器实现完全取决于您。 但是，Visual Studio 语言包项目提供默认分析器实现。 对于托管代码，托管的包框架 (MPF) 提供用于对文本着色的完整支持。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现语法着色的新方法的详细信息，请参阅[演练：突出显示文本](../../extensibility/walkthrough-highlighting-text.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="steps-followed-by-an-editor-to-colorize-text"></a>后跟一个编辑器，用于为文本着色的步骤

1. 在编辑器通过调用来获取 colorizer<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>对象。

2. 编辑器调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A>方法，以确定着色器是否需要着色器外部维护每个行的状态。

3. 如果着色器要求外部着色器维护状态，编辑器将调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A>方法以获取在第一行的状态。

4. 对于每个缓冲区中的行，在编辑器调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法，后者将执行以下步骤：

    1. 文本行传递给扫描程序以将文本转换为标记。 每个令牌指定的令牌文本和标记类型。

    2. 标记类型转换为可着色项列表的索引。

    3. 令牌信息用于填充数组中，以便每个元素的数组的对应行中的字符。 数组中存储的值可着色项列表的索引。

    4. 在行末尾处的状态的每个行返回。

5. 如果着色器需要维护状态，编辑器将缓存行的状态。

6. 编辑器中呈现的文本使用从返回的信息行<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法。 这需要执行以下步骤：

    1. 在行中的每个字符，获取可着色项索引。

    2. 如果使用默认可着色项，请访问编辑器的可着色项列表。

    3. 否则，调用语言服务<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>方法来获取可着色项。

    4. 使用可着色项中的信息要呈现到显示的文本。

## <a name="managed-package-framework-colorizer"></a>托管的包框架着色器
 托管的包框架 (MPF) 提供了实现着色程序所需的所有类。 语言服务类应继承<xref:Microsoft.VisualStudio.Package.LanguageService>类，实现所需的方法。 必须通过实现提供扫描器和分析器<xref:Microsoft.VisualStudio.Package.IScanner>接口，并返回从该接口的实例<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>方法 (必须在中实现的方法之一<xref:Microsoft.VisualStudio.Package.LanguageService>类)。 有关详细信息，请参阅[旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。

## <a name="see-also"></a>请参阅
- [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
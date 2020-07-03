---
title: 实现语法着色 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- syntax coloring, implementing
- editors [Visual Studio SDK], colorizing text
- text, colorizing in editors
ms.assetid: 96e762ca-efd0-41e7-8958-fda4897c8c7a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bb3f26f59d7cbc994da1d2537e0ab352ce12205e
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905211"
---
# <a name="implementing-syntax-coloring"></a>实现语法着色
当语言服务提供语法着色时，分析器会将一行文本转换为可着色项的数组，并返回对应于这些可着色项的标记类型。 分析器应返回属于可着色项列表的标记类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]根据 colorizer 对象分配给相应标记类型的属性，在代码窗口中显示每个可着色项。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]不指定分析器接口，并且分析器实现完全由你完成。 但是，Visual Studio 语言包项目中提供了默认的分析器实现。 对于托管代码，托管包框架（MPF）提供了对着色文本的完整支持。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要深入了解如何实现语法着色，请参阅[演练：突出显示文本](../../extensibility/walkthrough-highlighting-text.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="steps-followed-by-an-editor-to-colorize-text"></a>步骤后跟随编辑器来着色文本

1. 编辑器通过对对象调用方法来获取 colorizer <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> 。

2. 编辑器调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A> 方法来确定 colorizer 是否需要在 colorizer 外维护每行的状态。

3. 如果 colorizer 要求在 colorizer 外维护状态，则编辑器将调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A> 方法以获取第一行的状态。

4. 对于缓冲区中的每一行，编辑器都调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 方法，该方法执行以下步骤：

    1. 文本行会传递到扫描仪，以将文本转换为标记。 每个令牌指定令牌文本和令牌类型。

    2. 标记类型转换为可着色项列表中的索引。

    3. 标记信息用于填充数组，使数组的每个元素对应于行中的一个字符。 存储在数组中的值是可着色 items 列表中的索引。

    4. 为每行返回该行末尾的状态。

5. 如果 colorizer 需要维护状态，则编辑器将缓存该行的状态。

6. 编辑器使用从方法返回的信息呈现文本行 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> 。 这需要执行以下步骤：

    1. 对于行中的每个字符，获取可着色项索引。

    2. 如果使用默认的可着色项，则访问编辑器的可着色 items 列表。

    3. 否则，调用语言服务的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> 方法以获取可着色项。

    4. 使用可着色项中的信息将文本呈现到显示内容中。

## <a name="managed-package-framework-colorizer"></a>托管包框架 Colorizer
 托管包框架（MPF）提供了实现 colorizer 所需的所有类。 语言服务类应继承 <xref:Microsoft.VisualStudio.Package.LanguageService> 类并实现所需的方法。 必须通过实现接口提供一个扫描程序和分析器 <xref:Microsoft.VisualStudio.Package.IScanner> ，并从方法返回该接口的实例 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> （必须在类中实现的方法之一 <xref:Microsoft.VisualStudio.Package.LanguageService> ）。 有关详细信息，请参阅[旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。

## <a name="see-also"></a>另请参阅
- [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

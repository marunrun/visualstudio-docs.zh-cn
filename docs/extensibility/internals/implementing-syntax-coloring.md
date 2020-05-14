---
title: 实现语法着色 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 83ce66dd6a31e3ef852feb91e2ba304e6688a723
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707644"
---
# <a name="implementing-syntax-coloring"></a>实现语法着色
当语言服务提供语法着色时，解析器会将文本行转换为可着色项数组，并返回对应于这些可着色项的令牌类型。 解析器应返回属于可着色项列表的令牌类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]根据着色器对象分配给相应令牌类型的属性，在代码窗口中显示每个可着色项。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]不指定解析器接口，解析器实现完全由您决定。 但是，在可视化工作室语言包项目中提供了默认解析器实现。 对于托管代码，托管包框架 （MPF） 提供对文本着色的完全支持。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现语法着色的新方法的更多，请参阅[演练：突出显示文本](../../extensibility/walkthrough-highlighting-text.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="steps-followed-by-an-editor-to-colorize-text"></a>步骤后跟由编辑器着色文本

1. 编辑器通过在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>对象上调用方法来获取着色器。

2. 编辑器调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A>该方法以确定着色器是否需要在着色器外部维护每行的状态。

3. 如果着色器要求在着色器外部保持状态，则编辑器调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A>方法以获取第一行的状态。

4. 对于缓冲区中的每一行，编辑器调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法，该方法执行以下步骤：

    1. 文本行将传递到扫描仪，以将文本转换为标记。 每个令牌指定令牌文本和令牌类型。

    2. 令牌类型将转换为可着色项列表。

    3. 令牌信息用于填充数组，以便数组的每个元素对应于行中的字符。 数组中存储的值是可着色项列表中的索引。

    4. 每行返回行末尾的状态。

5. 如果着色器要求维护状态，编辑器将缓存该行的状态。

6. 编辑器使用从<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法返回的信息呈现文本行。 这需要执行以下步骤：

    1. 对于行中的每个字符，获取可着色项索引。

    2. 如果使用默认的可着色项，则访问编辑器的可着色项列表。

    3. 否则，调用语言服务<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>的方法以获取可着色项。

    4. 使用可着色项中的信息将文本呈现到显示屏中。

## <a name="managed-package-framework-colorizer"></a>托管包框架着色器
 托管包框架 （MPF） 提供实现着色器所需的所有类。 您的语言服务类应继承该<xref:Microsoft.VisualStudio.Package.LanguageService>类并实现所需的方法。 必须通过实现<xref:Microsoft.VisualStudio.Package.IScanner>接口来提供扫描仪和解析器，并从<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>方法返回该接口的实例（必须在<xref:Microsoft.VisualStudio.Package.LanguageService>类中实现的方法之一）。 有关详细信息，请参阅[旧语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。

## <a name="see-also"></a>请参阅
- [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

---
title: 自定义可着色项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, custom colorable items
ms.assetid: b4d0ddee-c04b-48dc-ba82-f6068570cef0
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 24a4db907ec859c6075c06956f86939047379897
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63409373"
---
# <a name="custom-colorable-items"></a>自定义可着色项
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

您可以实现自定义可着色项为语言服务的一部分，着色，例如关键字和注释，覆盖类型的列表。  
  
## <a name="user-settings-of-colorable-items"></a>用户设置的可着色项  
 可以显示**字体和颜色**对话框中的选择**选项**上**工具**菜单中，然后选择**字体和颜色**下**环境**。 当您选择显示，如**文本编辑器**或**命令窗口**，则**显示项**列表框显示来显示的可着色的所有项。 您可以查看和更改字体、 大小、 前景颜色和每个可着色项的背景色。 在注册表中缓存中存储和访问按可着色项名称所做的选择。  
  
## <a name="presentation-of-colorable-items"></a>表示法的可着色项  
 因为 IDE 可处理的可着色项中的用户重写**字体和颜色**对话框中，你需要仅提供一个名称与每个自定义可着色项。 此名称将会出现在**显示的项**列表。 可着色项按字母顺序显示。 语言服务的自定义可着色的项目进行分组，可以开始使用你的语言名称，每个名称，例如**NewLanguage-注释**并**NewLanguage-关键字**。  
  
> [!CAUTION]
> 要避免与现有的可着色项名称发生冲突的可着色项名称中，应包括的语言名称。 如果在开发过程中更改了一可着色项的名称，必须重置缓存创建第一次访问了你可着色的项。 你可以重置实验性使用 CreateExpInstance 工具随 Visual Studio SDK，通常在目录中缓存  
>   
> **C:\Program Files (x86)\Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin**  
>   
> 若要重置缓存，请调用`CreateExpInstance /Reset`。 CreateExpInstance 有关详细信息，请参阅[CreateExpInstance 实用工具](../../extensibility/internals/createexpinstance-utility.md)。  
  
 从未引用的可着色项在列表中的第一个项。 第一项对应于可着色项索引为 0，和[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]始终提供的默认文本颜色和该项的属性。 处理未引用该项的最简单方法是提供作为第一项列表中的占位符可着色项。  
  
## <a name="implementing-custom-colorable-items"></a>实现自定义可着色项  
  
1. 定义什么必须在你的语言，例如关键字、 运算符和标识符着色。  
  
2. 创建这些可着色项的枚举。  
  
3. 将由分析器或扫描程序使用枚举值时返回的令牌类型相关联。  
  
    例如，表示令牌的类型的值可能是自定义可着色项枚举中的相同值。  
  
4. 中的实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>中的方法在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>对象，请使用对应于从分析器或扫描程序返回的令牌类型在自定义可着色项枚举的值填充属性列表。  
  
5. 在同一个类实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口，实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>接口和其两个方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>。  
  
6. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 接口。  
  
7. 如果你想要支持 24 位或高颜色值，还实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>接口。  
  
8. 在语言服务对象，创建一个列表，其中包含你<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>对象、 一个用于您的分析器或扫描程序可以确定每个可着色项。  
  
    可以使用自定义可着色项枚举中的相应值来访问列表中的每个项。 使用作为索引到列表的枚举值。 永远不会访问列表中的第一项，因为它对应于默认文本样式的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]始终处理本身。 可以通过在列表的开头插入一个占位符可着色项对此进行补偿。  
  
9. 实现中<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>方法中，自定义可着色项列表中返回的项数。  
  
10. 实现中<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>方法，从列表中返回所请求的可着色项。  
  
    有关如何实现的示例<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>并<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>接口，请参阅<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>。  
  
## <a name="see-also"></a>请参阅  
 [旧版语言服务模型](../../extensibility/internals/model-of-a-legacy-language-service.md)   
 [自定义编辑器中的语法着色](../../extensibility/syntax-coloring-in-custom-editors.md)   
 [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)   
 [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)   
 [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

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
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "91102534"
---
# <a name="custom-colorable-items"></a>自定义可着色项
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

可以通过将自定义可着色项作为语言服务的一部分实现，来重写着色的类型列表，如关键字和注释。  
  
## <a name="user-settings-of-colorable-items"></a>可着色项的用户设置  
 可以通过在 "**工具**" 菜单上选择 "**选项**"，然后选择 "**环境**" 下的 "**字体和颜色**"，来显示 "**字体和颜色**" 对话框。 选择显示（如 **文本编辑器** 或 " **命令窗口**"）时，" **显示项** " 列表框将显示该显示的所有可着色项。 您可以查看和更改每个可着色项的字体、字号、前景色和背景色。 你的选择存储在注册表的缓存中，并由可着色项名称访问。  
  
## <a name="presentation-of-colorable-items"></a>可着色项的显示  
 由于 IDE 处理 " **字体和颜色** " 对话框中可着色项的用户覆盖，因此只需提供名称为的每个自定义可着色项。 此名称将显示在 " **显示项** " 列表中。 可着色项按字母顺序显示。 若要将语言服务的自定义可着色项分组，可以用语言名称开始每个名称，例如 **NewLanguage** 和 **NewLanguage 关键字**。  
  
> [!CAUTION]
> 应在可着色项名称中包含语言名称，以避免与现有可着色项名称冲突。 如果在开发过程中更改某个可着色项的名称，则必须重置在第一次访问可着色项时创建的缓存。 可以通过与 Visual Studio SDK 一起安装的 CreateExpInstance 工具重置实验缓存，该工具通常在目录中  
>   
> **C:\Program 文件 (x86) \Microsoft Visual Studio 14.0 \ VSSDK\VisualStudioIntegration\Tools\Bin**  
>   
> 若要重置缓存，请调用 `CreateExpInstance /Reset` 。 有关 CreateExpInstance 的详细信息，请参阅 [CreateExpInstance 实用工具](../../extensibility/internals/createexpinstance-utility.md)。  
  
 永远不会引用可着色项列表中的第一项。 第一项对应于可着色项索引0，并且 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 始终为该项提供默认文本颜色和特性。 处理此未引用项的最简单方法是将列表中的占位符可着色项提供为第一项。  
  
## <a name="implementing-custom-colorable-items"></a>实现自定义可着色项  
  
1. 定义语言中必须着色的内容，例如关键字、运算符和标识符。  
  
2. 创建这些可着色项的枚举。  
  
3. 将从分析器或扫描程序返回的标记类型与枚举值关联起来。  
  
    例如，表示标记类型的值可能与自定义可着色项枚举中的值相同。  
  
4. 在对象的方法实现中 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ，用自定义可着色 items 枚举中的值填充 "属性" 列表，这些值对应于从分析器或扫描程序返回的标记类型。  
  
5. 在实现接口的同一类中 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> ，实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> 接口及其两种方法： <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> 。  
  
6. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 接口。  
  
7. 如果要支持24位或高颜色值，还需要实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 接口。  
  
8. 在您的语言服务对象中，创建一个包含您的对象的列表 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> ，每个对象对应您的分析器或扫描程序可以识别的可着色项。  
  
    可以通过使用自定义可着色项枚举中的相应值来访问列表中的每个项。 使用枚举值作为列表中的索引。 永远不会访问列表中的第一项，因为它对应于始终处理自身的默认文本样式 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 通过在列表的开头插入一个占位符可着色项，可以对此进行补偿。  
  
9. 在方法的实现中 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> ，返回自定义可着色项列表中的项数。  
  
10. 在方法的实现中 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> ，从列表返回请求的可着色项。  
  
    有关如何实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 和接口的示例 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> ，请参见 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 。  
  
## <a name="see-also"></a>另请参阅  
 [旧版语言服务的模型](../../extensibility/internals/model-of-a-legacy-language-service.md)   
 [自定义编辑器中的语法着色](../../extensibility/syntax-coloring-in-custom-editors.md)   
 [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)   
 [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)   
 [如何：使用内置的可着色项](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

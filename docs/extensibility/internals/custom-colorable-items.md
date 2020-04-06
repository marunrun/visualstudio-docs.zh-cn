---
title: 自定义可着色物品 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, custom colorable items
ms.assetid: b4d0ddee-c04b-48dc-ba82-f6068570cef0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: feecd9e8f8178045f66999b775e2d0792f50b288
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708999"
---
# <a name="custom-colorable-items"></a>自定义可着色项目
您可以通过在语言服务中实现自定义可着色项来覆盖着色类型列表，例如关键字和注释。

## <a name="user-settings-of-colorable-items"></a>可着色项目的用户设置
 您可以通过在 **"工具"** 菜单上选择 **"选项**"，然后在 **"环境**"下选择 **"字体和颜色**"对话框来显示"**字体和颜色**"对话框。 当您选择显示（如**文本编辑器**或**命令窗口**）时，"**显示项目"** 列表框显示该显示的所有可着色项。 您可以查看和更改每个可着色项的字体、大小、前景颜色和背景颜色。 您的选择存储在注册表中的缓存中，并由可着色的项目名称访问。

## <a name="presentation-of-colorable-items"></a>提供可着色物品
 由于 IDE 处理"**字体和颜色"** 对话框中可着色项的用户覆盖，因此只需为每个自定义可着色项提供名称。 此名称是 **"显示项目**"列表中显示的内容。 可着色项按字母顺序显示。 要对语言服务的自定义可着色项目进行分组，可以使用语言名称开始每个名称，例如 **"新建语言 -注释**"和 **"新建语言 - 关键字**"。

> [!CAUTION]
> 应在可着色项名称中包含语言名称，以避免与现有可着色项名称发生冲突。 如果在开发期间更改了其中一个可着色项的名称，则必须重置首次访问可着色项时创建的缓存。 您可以使用**CreateExpA 工具**重置实验缓存，该工具通常安装在 Visual Studio SDK 中， 通常位于目录中：
>
> *C：\程序文件 （x86）\微软视觉工作室 14.0_VSSDK_视觉工作室集成\工具\Bin*
>
> 要重置缓存，请输入 **"创建实例/重置**"。 有关**CreateExp实例**的详细信息，请参阅[创建说明实用程序](../../extensibility/internals/createexpinstance-utility.md)。

 永远不会引用可着色项列表中的第一项。 第一个项对应于可着色项索引 0，并且[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]始终提供该项目的默认文本颜色和属性。 处理此未引用项的最简单方法是将列表中的占位符可着色项作为第一项提供。

## <a name="implement-custom-colorable-items"></a>实现自定义可着色项目

1. 定义语言中必须着色的内容，例如关键字、运算符和标识符。

2. 创建这些可着色项的枚举。

3. 将从解析器或扫描仪返回的令牌类型与枚举值相关联。

    例如，表示令牌类型的值可以是自定义可着色项枚举中相同的值。

4. 在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>对象中方法的实现中，使用自定义可着色项中的值填充属性列表，枚举与从解析器或扫描仪返回的标记类型对应。

5. 在实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口的同一类中，实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>接口及其两种方法，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>。

6. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> 接口。

7. 如果要支持 24 位或高颜色值，还要实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>接口。

8. 在语言服务对象中，创建一个包含对象<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>的列表，该列表针对解析器或扫描仪可以标识的每个可着色项创建一个列表。

    您可以使用自定义可着色项枚举中的相应值访问列表中的每个项。 将枚举值用作列表中的索引。 列表中的第一项永远不会被访问，因为它对应于[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]始终处理自身的默认文本样式。 您可以通过在列表的开头插入占位符可着色项来补偿这一点。

9. 在实现 方法时<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>，返回自定义可着色项列表中的项目数。

10. 在实现 方法时<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>，从列表中返回请求的可着色项。

    有关如何实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>接口的示例，请参阅。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>

## <a name="see-also"></a>请参阅
- [传统语言服务的模型](../../extensibility/internals/model-of-a-legacy-language-service.md)
- [自定义编辑器中的语法着色](../../extensibility/syntax-coloring-in-custom-editors.md)
- [旧语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)
- [如何：使用内置的可着色项目](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

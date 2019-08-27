---
title: 如何：使用内置的可着色项 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ae1c327c14ed2b349ee02566c5cdfd38b9a07859
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311967"
---
# <a name="how-to-use-built-in-colorable-items"></a>如何：使用内置的可着色项
使用内置的可着色项之前，您必须首先向发出信号，集成的开发环境 (IDE) 不提供此示例将为你自己自定义可着色项<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>对象。 通过设置语言服务的注册表项执行此操作。

## <a name="to-use-built-in-colorable-items"></a>若要使用内置的可着色项

1. 下**HKEY_LOCAL_MACHINE\VisualStudio\\< X.Y > \Languages\Language 服务\\< 语言名称\>** ，其中\<X.Y > 是版本[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和\<语言名称 > 是的名称的语言，创建名为的 DWORD 注册表项值**RequestStockColors**。

2. 设置**RequestStockColors**注册表项值为*1*。

    创建的注册表项，您的着色器的后<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>方法可以使用的成员<xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS>枚举，以供在编辑器的颜色属性的数组中填充。

   > [!NOTE]
   > 如果你要提供自定义可着色项未设置此注册表项。 有关详细信息，请参阅[自定义可着色项](../../extensibility/internals/custom-colorable-items.md)。

## <a name="see-also"></a>请参阅
- [自定义编辑器中的语法着色](../../extensibility/syntax-coloring-in-custom-editors.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)
- [自定义可着色项](../../extensibility/internals/custom-colorable-items.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)
---
title: 如何：使用内置的可着色物品 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34e07894c3306f544396e53001990f7b9a2df5a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707790"
---
# <a name="how-to-use-built-in-colorable-items"></a>如何：使用内置的可着色项目
在使用内置的可着色项之前，必须先向集成开发环境 （IDE） 发出信号，指出您没有提供自己的自定义可着色项，在这种情况下，这些项将是<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>对象。 为此，您可以为语言服务设置注册表项。

## <a name="to-use-built-in-colorable-items"></a>使用内置的可着色项目

1. 在**HKEY_LOCAL_MACHINE_VisualStudio<\\ X.Y>_语言服务\\<语言名称\>** 下，\<其中 X.Y>[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]是\<语言名称>是您的语言的名称，请创建一个名为 **"RequestStockColors"** 的 DWORD 注册表条目值。

2. 将 **"请求StockColors"** 注册表项值设置为*1*。

    创建注册表项后，着色器<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>的方法可以使用枚举的成员<xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS>来填充颜色属性数组，供编辑器使用。

   > [!NOTE]
   > 如果要提供自定义可着色项，请不要设置此注册表项。 有关详细信息，请参阅[自定义可着色项](../../extensibility/internals/custom-colorable-items.md)。

## <a name="see-also"></a>请参阅
- [自定义编辑器中的语法着色](../../extensibility/syntax-coloring-in-custom-editors.md)
- [旧语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [实现语法着色](../../extensibility/internals/implementing-syntax-coloring.md)
- [自定义可着色项目](../../extensibility/internals/custom-colorable-items.md)
- [注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)

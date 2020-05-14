---
title: 属性窗口按钮 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aaa4db159ccb0ecf3d0e9c9243e23fcd0dacc455
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706176"
---
# <a name="properties-window-buttons"></a>属性窗口按钮
根据开发语言和产品类型，某些按钮默认显示在 **"属性"** 窗口的工具栏上。 在所有情况下，将显示 **"分类**、**字母表"、****属性**和**属性页**按钮。 在"视觉 C#"和"可视基本"中，还会显示 **"事件**"按钮。 在某些视觉C++项目中，将显示**VC++ 消息**和**VC 覆盖**按钮。 可能显示其他项目类型的按钮。 有关 **"属性"** 窗口中的按钮的详细信息，请参阅[属性窗口](../../ide/reference/properties-window.md)。

## <a name="implementation-of-properties-window-buttons"></a>属性窗口按钮的实现
 单击 **"分类"** 按钮时，Visual Studio 会<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>调用具有焦点的对象上的接口，以便按类别对其属性进行排序。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>在显示到`IDispatch`**"属性"** 窗口的对象上实现。

 有 11 个预定义的属性类别，这些类别具有负值。 您可以定义自定义类别，但我们建议您为其分配正值，以将其与预定义的类别区分开来。

 该方法<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A>返回指定属性的相应属性类别值。 该方法<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A>返回包含类别名称的字符串。 您只需要支持自定义类别值，因为 Visual Studio 知道标准属性类别值。

 单击 **"字母"** 按钮时，属性按名称按字母顺序显示。 根据本地化排序算法检索`IDispatch`名称。

 当 **"属性"** 窗口打开时，"**属性**"按钮将自动显示为所选。 在环境的其他部分，将显示相同的按钮，您可以单击它以显示 **"属性"** 窗口。

 如果未`ISpecifyPropertyPages`为所选对象实现，则"**属性页**"按钮不可用。 属性页显示通常与解决方案和项目关联的与配置相关的属性，但它们也可以与项目项相关联（例如，在 Visual C++中）。

> [!NOTE]
> 不能使用非托管代码将工具栏按钮添加到 **"属性"** 窗口。 要添加工具栏按钮，必须创建派生自<xref:System.Windows.Forms.Design.PropertyTab>的托管对象。

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)

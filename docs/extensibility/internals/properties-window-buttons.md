---
title: "\"属性\" 窗口按钮 |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f2a41917a58a6fc5780b62c2c9e3db8aa52d407
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725259"
---
# <a name="properties-window-buttons"></a>属性窗口按钮
默认情况下，在 "**属性**" 窗口的工具栏上显示某些按钮，具体取决于开发语言和产品类型。 在所有情况下，将显示 "已**分类**"、"按**字母顺序** **" 和 "** **属性页**" 按钮。 在 Visual C#和 Visual Basic 中，还会显示 "**事件**" 按钮。 在某些视觉C++对象中，会显示**Vc + + 消息**和**vc 重写**按钮。 对于其他项目类型，可能会显示其他按钮。 有关 "**属性**" 窗口中的按钮的详细信息，请参阅 "[属性" 窗口](../../ide/reference/properties-window.md)。

## <a name="implementation-of-properties-window-buttons"></a>"属性" 窗口按钮的实现
 单击 "**分类**" 按钮时，Visual Studio 将调用对象上的 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> 接口，该对象具有焦点以便按类别对其属性进行排序。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> 在显示到 "**属性**" 窗口的 `IDispatch` 对象上实现。

 有11个预定义的属性类别，它们具有负值。 您可以定义自定义类别，但是我们建议您为它们指定正值，以将它们与预定义的类别区分开来。

 @No__t_0 方法为指定的属性返回相应的属性类别值。 @No__t_0 方法返回包含类别名称的字符串。 你只需提供对自定义类别值的支持，因为 Visual Studio 会知道标准属性类别的值。

 单击 "按**字母**顺序" 按钮时，属性将按名称的字母顺序显示。 根据本地化的排序算法 `IDispatch` 检索名称。

 当 "**属性**" 窗口处于打开状态时，"**属性**" 按钮会自动显示为选中状态。 在环境的其他部分中，将显示同一个按钮，你可以单击该按钮以显示 "**属性**" 窗口。

 如果未为所选对象实现 `ISpecifyPropertyPages`，"**属性页**" 按钮将不可用。 属性页显示与解决方案和项目通常关联的依赖于配置的属性，但它们也可以与项目项关联（例如，在视觉对象C++中）。

> [!NOTE]
> 不能使用非托管代码将工具栏按钮添加到 "**属性**" 窗口。 若要添加工具栏按钮，您必须创建一个派生自 <xref:System.Windows.Forms.Design.PropertyTab> 的托管对象。

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)
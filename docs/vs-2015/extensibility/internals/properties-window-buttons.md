---
title: "\"属性\" 窗口按钮 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b66015ef2e2ab0c8105b6f84486fa890adbf8b1f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840544"
---
# <a name="properties-window-buttons"></a>属性窗口按钮
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

默认情况下，在 " **属性** " 窗口的工具栏上显示某些按钮，具体取决于开发语言和产品类型。 在所有情况下，将显示 "已**分类**"、"按**字母顺序** **" 和 "****属性页**" 按钮。 在 Visual c # 和 Visual Basic 中，还会显示 " **事件** " 按钮。 在某些 Visual C++ 的项目中，将显示 " **vc + +" 消息** 和 " **vc 替代** " 按钮。 对于其他项目类型，可能会显示其他按钮。 有关 " **属性** " 窗口中的按钮的详细信息，请参阅 " [属性" 窗口](../../ide/reference/properties-window.md)。  
  
## <a name="implementation-of-properties-window-buttons"></a>"属性" 窗口按钮的实现  
 单击 " **分类** " 按钮时，Visual Studio 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> 对象上的接口，该接口具有焦点以便按类别对其属性进行排序。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> 在 `IDispatch` 呈现到 " **属性** " 窗口的对象上实现。  
  
 有11个预定义的属性类别，它们具有负值。 您可以定义自定义类别，但是我们建议您为它们指定正值，以将它们与预定义的类别区分开来。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A>方法为指定的属性返回相应的属性类别值。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A>方法返回包含类别名称的字符串。 你只需提供对自定义类别值的支持，因为 Visual Studio 会知道标准属性类别的值。  
  
 单击 "按 **字母** 顺序" 按钮时，属性将按名称的字母顺序显示。 `IDispatch`根据本地化的排序算法检索名称。  
  
 当 " **属性** " 窗口处于打开状态时，" **属性** " 按钮会自动显示为选中状态。 在环境的其他部分中，将显示同一个按钮，你可以单击该按钮以显示 " **属性** " 窗口。  
  
 如果未为所选对象实现，则 " **属性页** " 按钮不可用 `ISpecifyPropertyPages` 。 属性页显示与解决方案和项目相关的依赖于配置的属性，但它们也可以与项目项关联 (例如 Visual C++) 中。  
  
> [!NOTE]
> 不能使用非托管代码将工具栏按钮添加到 " **属性** " 窗口。 若要添加工具栏按钮，您必须创建一个派生自的托管对象 <xref:System.Windows.Forms.Design.PropertyTab> 。  
  
## <a name="see-also"></a>另请参阅  
 [扩展属性](../../extensibility/internals/extending-properties.md)

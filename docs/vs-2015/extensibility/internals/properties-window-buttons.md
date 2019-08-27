---
title: 属性窗口按钮 |Microsoft Docs
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438393"
---
# <a name="properties-window-buttons"></a>属性窗口按钮
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

具体取决于开发语言和产品类型，某些按钮显示的工具栏上的默认情况下**属性**窗口。 在所有情况下，**按分类顺序**， **Alphabetized**，**属性**，以及**属性页**按钮的显示。 在 Visual C# 和 Visual Basic**事件**按钮还会显示。 某些视觉对象中C++项目中， **VC + + 消息**并**VC 重写**显示按钮。 对于其他项目类型可能会显示其他按钮。 有关中的按钮的详细信息**属性**窗口中，请参阅[属性窗口](../../ide/reference/properties-window.md)。  
  
## <a name="implementation-of-properties-window-buttons"></a>属性窗口按钮的实现  
 当您单击**按分类顺序**按钮，Visual Studio 调用<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>上具有焦点，若要对其属性按类别进行排序的对象的接口。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> 上实现`IDispatch`对象，它提供给**属性**窗口。  
  
 有 11 的预定义的属性类别，具有负的值。 可以定义自定义类别，但我们建议你将为其分配正值，以区别于预定义的类别。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A>方法将返回指定属性的相应的属性类别值。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A>方法返回包含类别名称的字符串。 只需为自定义类别的值提供支持，因为 Visual Studio 知道标准的属性类别值。  
  
 当您单击**Alphabetized**按钮，按名称显示的属性按字母顺序。 检索名称`IDispatch`根据本地化排序算法。  
  
 当**属性**窗口处于打开状态，**属性**按钮自动显示为选中状态。 在环境的其他部分，将显示相同的按钮，然后可以单击它以显示**属性**窗口。  
  
 **属性页**按钮将不可用如果`ISpecifyPropertyPages`尚未实现对所选对象。 属性页显示配置相关属性通常与解决方案和项目，但它们是也可以是与项目项相关联 (例如，在视觉对象C++)。  
  
> [!NOTE]
> 不能添加到工具栏按钮**属性**使用非托管的代码的窗口。 若要添加的工具栏按钮，您必须创建派生的托管的对象<xref:System.Windows.Forms.Design.PropertyTab>。  
  
## <a name="see-also"></a>请参阅  
 [扩展属性](../../extensibility/internals/extending-properties.md)

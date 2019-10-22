---
title: 示例 Excel 扩展：PropertyProvider 类 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 075d9b8d-8658-4fca-8711-08304dbac1c5
caps.latest.revision: 11
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8ae254f85b00c47ba00250641f7afe0a638ceabc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660423"
---
# <a name="sample-excel-extension-propertyprovider-class"></a>示例 Excel 扩展：PropertyProvider 类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此内部类扩展 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> 类，并为 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 元素提供属性服务，以录制和播放用户界面 (UI) 测试。

## <a name="getcontrolsupportlevel-method"></a>GetControlSupportLevel 方法
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetControlSupportLevel%2A> 方法返回一个数字，指示属性提供程序可为所提供的控件提供的支持级别。 返回的值越大，属性提供程序可以为控件提供更多支持。 在这种情况下，该方法检查所提供的控件的 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IUITechnologyElement.TechnologyName%2A> 属性值。 如果值为“Excel”，并且 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IUITechnologyElement.ControlTypeName%2A> 指示控件为 `CellElement`，那么该方法返回最大值；否则，返回零，表示不提供任何支持。

## <a name="getpropertynames-method"></a>GetPropertyNames 方法
 返回 Excel 单元格控件的支持的属性的属性名称和属性描述符的字典。

## <a name="getpropertydescriptor-method"></a>GetPropertyDescriptor 方法
 测试框架调用此方法来获取所提供的属性名称的预定义的属性描述符。

## <a name="getpropertyvalue-and-setpropertyvalue-methods"></a>GetPropertyValue 和 SetPropertyValue 方法
 `GetPropertyValue` 方法使用此扩展的 `Communicator` 类从 Excel 返回属性值。 `SetPropertyValue` 方法使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard> 类和 `Communicator` 组件设置属性值。 这些方法由测试框架调用。

## <a name="code-generation-customization-methods"></a>代码生成自定义方法
 未针对此扩展实现这些方法。 因此，它们将返回 `null` 或引发 <xref:System.NotImplementedException>。

## <a name="see-also"></a>请参阅
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard>
 [扩展编码的 UI 测试和操作录制以支持 Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

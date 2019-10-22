---
title: 示例 Excel 扩展：TechnologyManager 类 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 8a7b760d-b5ac-4451-9593-6ac1a0b95cdb
caps.latest.revision: 11
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ac9a4517fcf13dbb0e1d7a6f994092168723e660
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672154"
---
# <a name="sample-excel-extension-technologymanager-class"></a>示例 Excel 扩展：TechnologyManager 类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此类扩展 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager> 类，并负责为 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 扩展提供核心服务。 尽管此基类具有很多方法，但是此示例中只使用其中一些方法。

 其中一些方法仅返回属性值。 许多方法旨在允许开发人员在编码的 UI 测试引擎中重写默认的算法版本。 这些方法引发 <xref:System.NotSupportedException> 或者返回 `null`，以指示框架使用默认算法。

 根据基础技术的复杂性，开发技术管理器代码可能需要几个星期到几个月。 通过 Excel 可以创建可能应用很广泛的技术管理器。 本示例有意仅限使用 Excel 工作表和单元格，并使用有限的格式设置。

 如果可能，技术管理器代码使用由 `Communicator` 类打开的 .NET 远程处理信道从 Excel 进程中运行的外接程序中提取信息。

## <a name="com-visibility"></a>COM 可见性
 请注意，此类和扩展 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> 类的每个元素类都具有值为 `true` 的 <xref:System.Runtime.InteropServices.ComVisibleAttribute>，以确保这些类对 COM 可见。

## <a name="technologyname-property"></a>TechnologyName 属性
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.TechnologyName%2A?displayProperty=fullName> 属性的此替代必须提供一个唯一且有意义的名称，用于标识扩展的其余组件的基础技术。 对于此扩展，值为“Excel”。

## <a name="getcontrolsupportlevel-method"></a>GetControlSupportLevel 方法
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetControlSupportLevel%2A?displayProperty=fullName> 方法的替代返回一个数字，指示技术管理器能够为由提供的图柄表示的控件提供的支持级别。 返回的值越大，技术管理器可以为控件提供更多支持。 在此情况下，此方法检查包含控件的窗口，如果是 Excel 工作表，则此方法返回最大值；否则，返回零，表示不提供任何支持。

## <a name="methods-to-get-an-element"></a>用于获取元素的方法
 编码的 UI 测试框架使用一些重要方法，通过提供一个句柄、屏幕上的一个点或不同技术的元素来获取特定于技术的元素。 这些方法的代码是自解释的。 基本方法如下所示：

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetFocusedElement%2A?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetElementFromPoint%2A?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetElementFromWindowHandle%2A?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetElementFromNativeElement%2A?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.ConvertToThisTechnology%2A?displayProperty=fullName>

## <a name="parsequeryid-method"></a>ParseQueryId 方法
 创建编码的 UI 测试后，用户可以指定测试中部分或全部控件的属性值。 测试框架使用这些属性值创建称为搜索属性的名称/值对，这些属性用来在测试期间查找特定 UI 控件。 所有搜索属性都一起表示技术中每个元素的 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A?displayProperty=fullName> 属性的值，其中包括每个控件。 由于在测试期间一个控件可能要查找几次，因此技术管理器可通过此方法来优化给定控件的搜索属性解析。 此方法也返回 cookie，框架可将此 cookie 用于针对控件的后续搜索。 该方法的此实现使用 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.AndCondition.Match%2A?displayProperty=fullName> 方法来分析搜索属性。

## <a name="matchelement-method"></a>MatchElement 方法
 若要通过技术管理器执行控件搜索，可以实现 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.Search%2A?displayProperty=fullName> 方法以返回可能的匹配数组，或者引发 <xref:System.NotSupportedException>，让其通知框架使用自己的搜索算法。 无论哪种方式，都必须实现 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.MatchElement%2A> 方法，该实现会在其中再次使用 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.AndCondition.Match%2A?displayProperty=fullName> 方法。

## <a name="navigation-methods"></a>导航方法
 这些方法从 UI 层次结构中获取所提供的元素的父元素、子元素或同级元素。 此代码很简单，并且具有清晰的注释。

## <a name="getexcelelement-internal-method"></a>GetExcelElement 内部方法
 此内部方法使用一个窗口句柄和有关 Excel 元素的信息，并返回所请求的 Excel 元素。

## <a name="see-also"></a>请参阅
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager> <xref:System.NotSupportedException>
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>
 <xref:System.Runtime.InteropServices.ComVisibleAttribute>
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A>
 [扩展编码的 UI 测试和操作录制以支持 Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

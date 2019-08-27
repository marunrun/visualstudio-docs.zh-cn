---
title: 示例 Excel 扩展:ActionFilter 类 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: c69fe3c7-f797-4e90-b21c-f2cc4dddf152
caps.latest.revision: 13
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 26eb001de3a8fed7c6bb1d9d1a547aa618e745e8
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871605"
---
# <a name="sample-excel-extension-actionfilter-class"></a>示例 Excel 扩展:ActionFilter 类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此内部类扩展[microsoft.visualstudio.testtools.uitest.common.uitestactionfilter>](/previous-versions/visualstudio/visual-studio-2012/dd985757(v=vs.110))类, 并表示针对[!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]元素的测试操作的筛选器。

## <a name="simple-properties"></a>简单属性
 通过这些只读属性，开发人员可以指定如何通过编码的 UI 测试框架来执行此测试操作筛选器。 例如，`UITestActionFilter.Name` 属性提供操作筛选器的名称。 其他属性可获取操作筛选器的 `UITestActionFilter.Category`、`UITestActionFilter.FilterType`、由此测试操作筛选器筛选的测试操作的 `UITestActionFilter.Group` 名称。 其他属性指示是否为 `UITestActionFilter.ApplyTimeout` 以及测试操作是否为 `UITestActionFilter.Enabled`。

## <a name="processrule-method"></a>ProcessRule 方法
 此方法由编码的 UI 测试框架调用，并针对提供的 `IUITestActionStack` 执行筛选器。 当堆栈中的下一个操作向单元格发送键击时，此特定重写将移除单元格的选择操作。 然后返回 `false`。

## <a name="private-methods"></a>私有方法
 `IsLeftClick` 方法确定提供的操作是否表示单击鼠标左键。 `AreActionsOnSameExcelCell` 方法确定是否针对 Excel 中同一单元格执行所提供的两个操作。

## <a name="see-also"></a>请参阅

- [扩展编码的 UI 测试和操作录制以支持 Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

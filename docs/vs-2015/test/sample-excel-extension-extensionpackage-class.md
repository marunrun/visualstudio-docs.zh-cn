---
title: 示例 Excel 扩展：ExtensionPackage 类 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 6e45410a-1819-4d54-ac21-7280152f7e3a
caps.latest.revision: 11
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a1c1f4c746fa505b50bab9caa7a516a2abc77f69
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672200"
---
# <a name="sample-excel-extension-extensionpackage-class"></a>示例 Excel 扩展：ExtensionPackage 类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此类扩展 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> 类，并为正在测试 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 工作表的编码的 UI 测试提供入口点。

## <a name="assembly-attribute"></a>程序集属性
 文件以程序集属性开头，此属性将此程序集标识为 UI 测试扩展。

```
[assembly: Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage(
    "ExcelExtensionPackage",
    typeof(
     Microsoft.VisualStudio.Test.Sample.UI.ExtensionPackage))]
```

 此属性声明自定义扩展包类的基类名称、包类的名称和完全限定的类名。

## <a name="simple-properties"></a>简单属性
 此类包含的属性的值供编码的 UI 测试框架用于标识和描述扩展和程序集。 有关详细信息，请参阅代码注释。

## <a name="getservice-method"></a>GetService 方法
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A> 方法是编码的 UI 测试框架使用的单一入口点（由每个对象的基类标识），用于访问技术管理器、属性提供程序和操作筛选器。

## <a name="see-also"></a>请参阅
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>[扩展编码的 UI 测试和操作录制以支持 Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

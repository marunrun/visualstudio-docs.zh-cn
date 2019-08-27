---
title: CA1409:Com 可见类型应该是可创建 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
helpviewer_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
ms.assetid: 9f59569b-de15-4a38-b7cb-cff152972243
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 7bd52ad75c67f9c8faa80e84eb5ae09c22c25280
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65678879"
---
# <a name="ca1409-com-visible-types-should-be-creatable"></a>CA1409:COM 可见类型应该是可创建的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ComVisibleTypesShouldBeCreatable|
|CheckId|CA1409|
|类别|Microsoft.Interoperability|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 专门标记为可见到组件对象模型 (COM) 的引用类型包含公共的参数化构造函数，但不包含公共的默认 （无参数） 构造函数。

## <a name="rule-description"></a>规则说明
 不能由 COM 客户端创建没有公共默认构造函数的类型。 但是，可以仍访问类型的 COM 客户端如果另一种方法可用于创建类型并将其传递给客户端 （例如，通过方法调用的返回值）。

 规则将忽略类型派生自<xref:System.Delegate?displayProperty=fullName>。

 默认情况下，以下是对 COM 可见： 程序集、 公共类型、 公共类型中的公共实例成员和公共值类型的所有成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，将公共默认构造函数添加或删除<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>的类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果提供了其他方法来创建并将该对象传递给 COM 客户端。

## <a name="related-rules"></a>相关的规则
 [CA1017:用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>请参阅
 [为互操作限定.NET 类型](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)[与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)

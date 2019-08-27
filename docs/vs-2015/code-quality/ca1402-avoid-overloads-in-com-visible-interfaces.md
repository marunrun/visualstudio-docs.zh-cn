---
title: CA1402:避免在 COM 可见接口中的重载 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidOverloadsInComVisibleInterfaces
- CA1402
helpviewer_keywords:
- AvoidOverloadsInComVisibleInterfaces
- CA1402
ms.assetid: 2724c1f9-d5d3-4704-b124-21c4d398e5df
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: abf6382dfba8b8d9c3cc0ed6ccf90e929afca589
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694964"
---
# <a name="ca1402-avoid-overloads-in-com-visible-interfaces"></a>CA1402:避免在 COM 可见接口中进行重载
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidOverloadsInComVisibleInterfaces|
|CheckId|CA1402|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
 组件对象模型 (COM) 可见的接口声明重载的方法。

## <a name="rule-description"></a>规则说明
 在向 COM 客户端公开重载的方法时，只有第一个方法重载保留其名称。 对于后续重载将唯一名称，方法名称后面追加的下划线字符 _ 和一个整数，该重载的声明顺序对应。 例如，考虑以下方法。

```
void SomeMethod(int valueOne);
void SomeMethod(int valueOne, int valueTwo, int valueThree);
void SomeMethod(int valueOne, int valueTwo);
```

 向 COM 客户端，如下所示公开这些方法。

```
void SomeMethod(int valueOne);
void SomeMethod_2(int valueOne, int valueTwo, int valueThree);
void SomeMethod_3(int valueOne, int valueTwo);
```

 Visual Basic 6 COM 客户端不能实现接口方法的名称中使用下划线。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请重命名的重载的方法，使名称是唯一的。 或者，使该接口不可见 COM 通过更改到的可访问性`internal`(`Friend`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 或通过应用<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>属性设置为`false`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个违反了此规则的接口和满足该规则的接口。

 [!code-csharp[FxCop.Interoperability.OverloadsInterface#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.OverloadsInterface/cs/FxCop.Interoperability.OverloadsInterface.cs#1)]
 [!code-vb[FxCop.Interoperability.OverloadsInterface#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.OverloadsInterface/vb/FxCop.Interoperability.OverloadsInterface.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1413:避免在 COM 可见值类型中的非公共字段](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

 [CA1407:避免在 COM 可见类型中的静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017:用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>请参阅
 [与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258) [Long 数据类型](https://msdn.microsoft.com/library/b4770c34-1804-4f8c-b512-c10b0893e516)

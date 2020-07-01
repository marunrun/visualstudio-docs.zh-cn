---
title: CA1402：避免在 COM 可见接口中进行重载 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b5c1e3af0e35bf92d72e853948c455893b417998
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534935"
---
# <a name="ca1402-avoid-overloads-in-com-visible-interfaces"></a>CA1402:避免在 COM 可见接口中进行重载
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|AvoidOverloadsInComVisibleInterfaces|
|CheckId|CA1402|
|类别|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 组件对象模型（COM）可见接口声明重载方法。

## <a name="rule-description"></a>规则描述
 在向 COM 客户端公开重载的方法时，只有第一个方法重载保留其名称。 通过在名称后追加下划线字符 "_" 和一个与重载的声明顺序相对应的整数，可对后续重载进行唯一重命名。 例如，请考虑以下方法。

```
void SomeMethod(int valueOne);
void SomeMethod(int valueOne, int valueTwo, int valueThree);
void SomeMethod(int valueOne, int valueTwo);
```

 如下所示，将这些方法公开给 COM 客户端。

```
void SomeMethod(int valueOne);
void SomeMethod_2(int valueOne, int valueTwo, int valueThree);
void SomeMethod_3(int valueOne, int valueTwo);
```

 Visual Basic 6，COM 客户端无法通过在名称中使用下划线来实现接口方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请重命名重载的方法，使名称唯一。 或者，通过将可访问性更改为 `internal` （ `Friend` 在中为 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ）或 <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> 将属性设置为 `false` ，使接口对 COM 不可见。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了违反规则的接口和满足规则的接口。

 [!code-csharp[FxCop.Interoperability.OverloadsInterface#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.OverloadsInterface/cs/FxCop.Interoperability.OverloadsInterface.cs#1)]
 [!code-vb[FxCop.Interoperability.OverloadsInterface#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.OverloadsInterface/vb/FxCop.Interoperability.OverloadsInterface.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1413:避免在 COM 可见值类型中使用非公共字段](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

 [CA1407:避免在 COM 可见类型中使用静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017:用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>另请参阅
 [与非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)[长数据类型](https://msdn.microsoft.com/library/b4770c34-1804-4f8c-b512-c10b0893e516)互操作

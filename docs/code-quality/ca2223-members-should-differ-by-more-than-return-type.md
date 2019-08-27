---
title: CA2223:成员不应只是返回类型不同
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MembersShouldDifferByMoreThanReturnType
- CA2223
helpviewer_keywords:
- CA2223
- MembersShouldDifferByMoreThanReturnType
ms.assetid: eb326d9f-50d9-48cb-84be-d41c84a8fe09
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: de64e0271370a3cdcc6f0963dbf06925621b9b65
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920187"
---
# <a name="ca2223-members-should-differ-by-more-than-return-type"></a>CA2223:成员不应只是返回类型不同

|||
|-|-|
|TypeName|MembersShouldDifferByMoreThanReturnType|
|CheckId|CA2223|
|类别|Microsoft.Usage|
|是否重大更改|重大|

## <a name="cause"></a>原因
两个公共或受保护成员具有相同的签名 (返回类型除外)。

## <a name="rule-description"></a>规则说明
尽管公共语言运行时允许使用返回类型来区分其他完全相同的成员, 但此功能并不属于公共语言规范, 也不是 .NET 编程语言的常见功能。 如果成员的差异仅在于返回类型, 开发人员和开发工具可能无法正确区分它们。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请更改成员的设计, 使其仅基于其名称和参数类型是唯一的, 否则不公开成员。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例 (在 Microsoft 中间语言 (MSIL) 中) 显示了违反此规则的类型。 请注意, 不能使用C#或 Visual Basic 违反此规则。

```
.namespace UsageLibrary
{
  .class public auto ansi beforefieldinit ReturnTypeTest
         extends [mscorlib]System.Object
  {
    .method public hidebysig instance int32
            AMethod(int32 x) cil managed
    {
      // Code size       6 (0x6)
      .maxstack  1
      .locals init (int32 V_0)
      IL_0000:  ldc.i4.0
      IL_0001:  stloc.0
      IL_0002:  br.s       IL_0004

      IL_0004:  ldloc.0
      IL_0005:  ret
    } // end of method ReturnTypeTest::AMethod

    .method public hidebysig instance string
            AMethod(int32 x) cil managed
    {
      // Code size       10 (0xa)
      .maxstack  1
      .locals init (string V_0)
      IL_0000:  ldstr      "test"
      IL_0005:  stloc.0
      IL_0006:  br.s       IL_0008

      IL_0008:  ldloc.0
      IL_0009:  ret
    } // end of method ReturnTypeTest::AMethod

    .method public hidebysig specialname rtspecialname
            instance void  .ctor() cil managed
    {
      // Code size       7 (0x7)
      .maxstack  1
      IL_0000:  ldarg.0
      IL_0001:  call       instance void [mscorlib]System.Object::.ctor()
      IL_0006:  ret
    } // end of method ReturnTypeTest::.ctor

  } // end of class ReturnTypeTest

} // end of namespace UsageLibrary
```
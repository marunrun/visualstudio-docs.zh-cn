---
title: CA2221:终结器应受到保护
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2221
- FinalizersShouldBeProtected
helpviewer_keywords:
- FinalizersShouldBeProtected
- CA2221
ms.assetid: bda03aee-4cce-45d3-907d-17f4ee030acc
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e88f22f25ff0620a88685dee93fd5658c302db74
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920246"
---
# <a name="ca2221-finalizers-should-be-protected"></a>CA2221:终结器应受到保护

|||
|-|-|
|TypeName|FinalizersShouldBeProtected|
|CheckId|CA2221|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
公共类型实现不指定族 (受保护) 访问的终结器。

## <a name="rule-description"></a>规则说明
终结器必须使用族访问修饰符。 此规则由C#、Visual Basic 和 Visual C++编译器强制执行。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将终结器更改为可以进行系列访问。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
任何高级 .NET 语言中都不能违反此规则;如果你正在编写 Microsoft 中间语言, 则可能会违反此方法。

```
// =============== CLASS MEMBERS DECLARATION ===================
//   note that class flags, 'extends' and 'implements' clauses
//          are provided here for information only

.namespace UsageLibrary
{
  .class public auto ansi beforefieldinit FinalizeMethodNotProtected
         extends [mscorlib]System.Object
  {
    .method public hidebysig instance void
            Finalize() cil managed
    {

      // Code size       1 (0x1)
      .maxstack  0
      IL_0000:  ret
    } // end of method FinalizeMethodNotProtected::Finalize

    .method public hidebysig specialname rtspecialname
            instance void  .ctor() cil managed
    {
      // Code size       7 (0x7)
      .maxstack  1
      IL_0000:  ldarg.0
      IL_0001:  call       instance void [mscorlib]System.Object::.ctor()
      IL_0006:  ret
    } // end of method FinalizeMethodNotProtected::.ctor

  } // end of class FinalizeMethodNotProtected
} // end of namespace
```

## <a name="see-also"></a>请参阅

- [释放模式](/dotnet/standard/design-guidelines/dispose-pattern)
---
title: CA2102:在常规处理程序中捕捉非 CLSCompliant 异常 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2102
- CatchNonClsCompliantExceptionsInGeneralHandlers
helpviewer_keywords:
- CA2102
ms.assetid: bf2df68f-d386-4379-ad9e-930a2c2e930d
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3fc0803e4ad73b08e99a05fa62930e039e1b7534
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687431"
---
# <a name="ca2102-catch-non-clscompliant-exceptions-in-general-handlers"></a>CA2102:在常规处理程序中捕捉非 CLSCompliant 异常
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CatchNonClsCompliantExceptionsInGeneralHandlers|
|CheckId|CA2102|
|类别|Microsoft.Security|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 中未标有程序集的成员<xref:System.Runtime.CompilerServices.RuntimeCompatibilityAttribute>，或标记已`RuntimeCompatibility(WrapNonExceptionThrows = false)`包含处理的 catch 块<xref:System.Exception?displayProperty=fullName>，并且不包含紧跟其后的一般 catch 块。 此规则将忽略[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]程序集。

## <a name="rule-description"></a>规则说明
 处理的 catch 块<xref:System.Exception>捕获了所有的公共语言规范 (CLS) 符合异常。 但是，它不捕捉非 CLS 兼容异常。 不符合 CLS 可引发符合异常，从本机代码或从托管代码生成的 Microsoft 中间语言 (MSIL) 组装器。 请注意，C# 和[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]编译器不允许非 CLS 兼容异常引发和[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]不会捕获非 CLS 兼容异常。 如果在 catch 块的目的是处理所有异常，则使用以下常规 catch 块语法。

- C#：`catch {}`

- C++:`catch(...) {}`或 `catch(Object^) {}`

  在 catch 块中删除以前允许的权限时，未处理的非 CLS 兼容异常将成为安全问题。 未捕获非 CLS 兼容异常，因为可以使用提升的权限运行恶意方法引发非 CLS 兼容异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突时的目的是捕获所有异常，替换或添加的常规 catch 块或标记该程序集`RuntimeCompatibility(WrapNonExceptionThrows = true)`。 如果在 catch 块中移除的权限，则重复的功能在常规 catch 块。 如果它不是处理所有异常的意图，替换处理 catch 块<xref:System.Exception>与都处理特定异常类型的 catch 块。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果在 try 块不包含任何可能会产生非 CLS 兼容异常的语句。 因为任何本机或托管代码可能会引发非 CLS 兼容异常，这需要了解的所有代码都可以在 try 块内的所有代码路径中执行。 请注意，公共语言运行时不引发非 CLS 兼容异常。

## <a name="example"></a>示例
 下面的示例演示一个 MSIL 类引发非 CLS 兼容异常。

```
.assembly ThrowNonClsCompliantException {}
.class public auto ansi beforefieldinit ThrowsExceptions
{
   .method public hidebysig static void
         ThrowNonClsException() cil managed
   {
      .maxstack  1
      IL_0000:  newobj     instance void [mscorlib]System.Object::.ctor()
      IL_0005:  throw
   }
}
```

## <a name="example"></a>示例
 下面的示例显示了包含满足该规则的常规 catch 块的方法。

 [!code-csharp[FxCop.Security.CatchNonClsCompliantException#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.CatchNonClsCompliantException/cs/FxCop.Security.CatchNonClsCompliantException.cs#1)]

 编译前面的示例，如下所示。

```
ilasm /dll ThrowNonClsCompliantException.il
csc /r:ThrowNonClsCompliantException.dll CatchNonClsCompliantException.cs
```

## <a name="related-rules"></a>相关的规则
 [CA1031:不要捕捉一般异常类型](../code-quality/ca1031-do-not-catch-general-exception-types.md)

## <a name="see-also"></a>请参阅
 [异常和异常处理](https://msdn.microsoft.com/library/0001887f-4fa2-47e2-8034-2819477e2344) [Ilasm.exe （IL 汇编程序）](https://msdn.microsoft.com/library/4ca3a4f0-4400-47ce-8936-8e219961c76f) [重写安全检查](https://msdn.microsoft.com/4acdeff5-fc05-41bf-8505-7387cdbfca28)[语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)

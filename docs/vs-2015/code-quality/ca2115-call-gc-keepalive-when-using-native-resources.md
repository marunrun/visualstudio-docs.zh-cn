---
title: CA2115：调用 GC。使用本机资源时 KeepAlive |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CallGCKeepAliveWhenUsingNativeResources
- CA2115
helpviewer_keywords:
- CA2115
- CallGCKeepAliveWhenUsingNativeResources
ms.assetid: f00a59a7-2c6a-4bbe-a1b3-7bf77d366f34
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c668172ca318000068fb4e90f4848e456c32208d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543619"
---
# <a name="ca2115-call-gckeepalive-when-using-native-resources"></a>CA2115:使用本机资源时调用 GC.KeepAlive
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|CallGCKeepAliveWhenUsingNativeResources|
|CheckId|CA2115|
|Category|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 具有终结器的类型中声明的方法引用 <xref:System.IntPtr?displayProperty=fullName> 或 <xref:System.UIntPtr?displayProperty=fullName> 字段，但不调用 <xref:System.GC.KeepAlive%2A?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 如果在托管代码中没有更多的引用，则垃圾回收将回收对象。 对对象的非托管引用不会阻止垃圾回收。 该规则检测由于在非托管代码仍在使用非托管资源时终止该非托管资源而可能发生的错误。

 此规则假定 <xref:System.IntPtr> 和 <xref:System.UIntPtr> 字段存储指向非托管资源的指针。 由于终结器的用途是释放非托管资源，因此该规则假定终结器将释放指针字段指向的非托管资源。 此规则还假定方法正在引用指针字段，以将非托管资源传递到非托管代码。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将对的调用添加到 <xref:System.GC.KeepAlive%2A> 方法，同时将当前实例（ `this` 在 c # 和 c + + 中）作为参数传递。 将调用定位在必须保护对象不被垃圾回收的代码的最后一行之后。 调用后 <xref:System.GC.KeepAlive%2A> ，该对象再次被视为已准备好进行垃圾回收，假设没有对它的托管引用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 此规则做出一些可能导致误报的假设。 如果出现以下情况，则可以安全地禁止显示此规则的警告：

- 终结器不释放该 <xref:System.IntPtr> 方法引用的或字段的内容 <xref:System.UIntPtr> 。

- 方法不会将 <xref:System.IntPtr> 或字段传递 <xref:System.UIntPtr> 到非托管代码。

  在排除其他消息之前，请仔细查看这些消息。 此规则检测难以重现和调试的错误。

## <a name="example"></a>示例
 在下面的示例中，`BadMethod` 不包含对 `GC.KeepAlive` 的调用，因此违反了此规则。 `GoodMethod`包含更正后的代码。

> [!NOTE]
> 尽管代码可以编译运行，但本示例是伪代码，之所以不引发警告是因为未创建或释放非托管资源。

 [!code-csharp[FxCop.Security.IntptrAndFinalize#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.IntptrAndFinalize/cs/FxCop.Security.IntptrAndFinalize.cs#1)]

## <a name="see-also"></a>另请参阅
 <xref:System.GC.KeepAlive%2A?displayProperty=fullName> <xref:System.IntPtr?displayProperty=fullName>
 <xref:System.Object.Finalize%2A?displayProperty=fullName>
 <xref:System.UIntPtr?displayProperty=fullName>
 [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)

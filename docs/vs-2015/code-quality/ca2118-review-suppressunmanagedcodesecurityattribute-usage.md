---
title: CA2118：查看 SuppressUnmanagedCodeSecurityAttribute 用法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2118
- ReviewSuppressUnmanagedCodeSecurityUsage
helpviewer_keywords:
- ReviewSuppressUnmanagedCodeSecurityUsage
- CA2118
ms.assetid: 4cb8d2fc-4e44-4dc3-9b74-7f5838827d41
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bb7404d9add159f182ae44b22444dded1aafca20
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658639"
---
# <a name="ca2118-review-suppressunmanagedcodesecurityattribute-usage"></a>CA2118：检查 SuppressUnmanagedCodeSecurityAttribute 用法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ReviewSuppressUnmanagedCodeSecurityUsage|
|CheckId|CA2118|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护的类型或成员具有 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> 特性。

## <a name="rule-description"></a>规则说明
 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 使用 COM 互操作或平台调用为执行非托管代码的成员更改默认的安全系统行为。 通常，系统为非托管代码权限进行[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)。 此要求在运行时针对每个成员调用发生，并检查调用堆栈中的每个调用方是否有权限。 当存在属性时，系统会对权限进行[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)：调用调用程序时，将检查直接调用方的权限。

 该特性主要用于提高性能；不过，提高性能的同时会显著增加安全风险。 如果将属性放置在调用本机方法的公共成员上，调用堆栈中的调用方（而不是直接调用方）不需要非托管代码权限即可执行非托管代码。 根据公共成员的操作和输入处理，它可能会允许不受信任的调用方访问通常限制为可信代码的功能。

 @No__t_0 依赖安全检查来防止调用方获取对当前进程的地址空间的直接访问。 由于此属性会跳过正常的安全性，因此，如果代码可用于读取或写入进程的内存，则代码会带来严重的威胁。 请注意，此风险并不局限于有意提供对处理内存的访问的方法;在任何情况下，恶意代码都可以通过任何方式获取访问权限，例如，提供令人吃惊、格式不正确或无效的输入。

 默认安全策略不向程序集授予非托管代码权限，除非它是从本地计算机执行或是下列组之一的成员：

- 我的电脑区域代码组

- Microsoft 强名称代码组

- ECMA 强名称代码组

## <a name="how-to-fix-violations"></a>如何解决冲突
 仔细检查代码以确保此属性是绝对必要的。 如果你不熟悉托管代码安全性，或者不了解使用此属性的安全影响，请将其从代码中删除。 如果该属性是必需的，则必须确保调用方不能恶意使用您的代码。 如果你的代码没有执行非托管代码的权限，则此属性不起作用，因此应将其删除。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 若要安全地禁止显示此规则发出的警告，您必须确保您的代码不会向调用方提供对可通过破坏性方式使用的本机操作或资源的访问权限。

## <a name="example"></a>示例
 下面的示例与此规则冲突。

 [!code-csharp[FxCop.Security.TypesDoNotSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesDoNotSuppress/cs/FxCop.Security.TypesDoNotSuppress.cs#1)]

## <a name="example"></a>示例
 在下面的示例中，`DoWork` 方法为平台调用方法提供了一个可公开访问的代码路径 `FormatHardDisk`。

 [!code-csharp[FxCop.Security.PInvokeAndSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PInvokeAndSuppress/cs/FxCop.Security.PInvokeAndSuppress.cs#1)]

## <a name="example"></a>示例
 在下面的示例中，公共方法 `DoDangerousThing` 会导致冲突。 若要解决此冲突，应将 `DoDangerousThing` 设为私有，并应通过安全要求所保护的公共方法（如 `DoWork` 方法所示）来访问它。

 [!code-csharp[FxCop.Security.TypeInvokeAndSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypeInvokeAndSuppress/cs/FxCop.Security.TypeInvokeAndSuppress.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> 安全的[编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[安全优化](https://msdn.microsoft.com/cf255069-d85d-4de3-914a-e4625215a7c0)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)[链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)

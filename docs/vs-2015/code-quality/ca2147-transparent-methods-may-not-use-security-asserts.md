---
title: CA2147:透明方法不得使用安全断言 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SecurityTransparentCodeShouldNotAssert
- CA2147
- CA2128
helpviewer_keywords:
- CA2128
- SecurityTransparentCodeShouldNotAssert
ms.assetid: 5d31e940-e599-4b23-9b28-1c336f8d910e
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3e8ac2e907e3c13a019e5f534faf86ae425ae30a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142645"
---
# <a name="ca2147-transparent-methods-may-not-use-security-asserts"></a>CA2147:透明方法不得使用安全断言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SecurityTransparentCodeShouldNotAssert|
|CheckId|CA2147|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 标记为代码<xref:System.Security.SecurityTransparentAttribute>未授予足够的权限进行断言。

## <a name="rule-description"></a>规则说明
 此规则分析所有方法和类型的程序集中的 100%透明或混合透明/关键，并标记的任何声明性或命令性用法<xref:System.Security.CodeAccessPermission.Assert%2A>。

 在运行时，对任何调用<xref:System.Security.CodeAccessPermission.Assert%2A>从透明代码将导致<xref:System.InvalidOperationException>引发。 这可能在两个 100%透明程序集，以及程序集中混合透明/关键方法或类型被声明为透明，但包括声明性或命令性断言。

 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 2.0 引入了一个名为功能*透明度*。 单个方法、 字段、 接口、 类和类型可以是透明或关键。

 透明代码不能提升的安全特权。 因此，授予或其请求的任何权限都会自动通过代码传递给调用方或主机应用程序域。 提升的示例包括 assert 语句、 Linkdemand、 SuppressUnmanagedCode，和`unsafe`代码。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此问题，或者标记的代码调用使用 Assert <xref:System.Security.SecurityCriticalAttribute>，或删除该断言。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不要禁止显示此规则的消息。

## <a name="example"></a>示例
 如果此代码将失败`SecurityTestClass`是透明的当`Assert`方法会抛出<xref:System.InvalidOperationException>。

 [!code-csharp[FxCop.Security.CA2147.TransparentMethodsMustNotUseSecurityAsserts#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2147.transparentmethodsmustnotusesecurityasserts/cs/ca2147 - transparentmethodsmustnotusesecurityasserts.cs#1)]

## <a name="example"></a>示例
 一种方法是代码评审的 SecurityTransparentMethod 方法在以下示例中，而且如果此方法被认为安全的提升，将标记 SecurityTransparentMethod 与安全关键这就要求详细、 完整和无错误的安全审核必须上以及在 Assert 的方法中出现的任何调用出方法执行：

 [!code-csharp[FxCop.Security.SecurityTransparentCode2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SecurityTransparentCode2/cs/FxCop.Security.SecurityTransparentCode2.cs#1)]

 另一个选项是从代码中删除该断言，并允许任何后续文件 I/O 权限需求流超出 SecurityTransparentMethod 给调用方。 这使安全检查。 在这种情况下，通常需要无任何安全审核，因为权限要求将流向调用方和/或应用程序域。 通过安全策略、 宿主环境中，并相应地代码源的权限授予密切控制权限请求。

## <a name="see-also"></a>请参阅
 [安全警告](../code-quality/security-warnings.md)

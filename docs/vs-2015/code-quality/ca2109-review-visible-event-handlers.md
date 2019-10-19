---
title: CA2109：检查可见的事件处理程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2109
- ReviewVisibleEventHandlers
helpviewer_keywords:
- ReviewVisibleEventHandlers
- CA2109
ms.assetid: 8f8fa0ee-e94e-400e-b516-24d8727725d7
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 38a1b7c00c79c7a2e89ef64598b8c409709561ef
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658709"
---
# <a name="ca2109-review-visible-event-handlers"></a>CA2109：检查可见的事件处理程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ReviewVisibleEventHandlers|
|CheckId|CA2109|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 检测到公共事件处理方法或受保护事件处理方法。

## <a name="rule-description"></a>规则说明
 外部可见的事件处理方法显示了需要查看的安全问题。

 除非绝对必要，否则不应公开事件处理方法。 只要处理程序和事件签名匹配，就可以将调用公开方法的事件处理程序（委托类型）添加到任何事件。 事件可能由任何代码引发，并经常由高度可信的系统代码引发，以响应用户操作（例如单击某个按钮）。 向事件处理方法添加安全检查不会阻止代码注册调用方法的事件处理程序。

 请求无法可靠地保护由事件处理程序调用的方法。 安全要求通过检查调用堆栈上的调用方来帮助保护来自不受信任的调用方的代码。 向事件添加事件处理程序的代码在事件处理程序的方法运行时不一定存在于调用堆栈上。 因此，调用堆栈在调用事件处理程序方法时可能只有高度受信任的调用方。 这将导致事件处理程序方法所做的请求成功。 此外，当调用方法时，可能会断言请求的权限。 由于这些原因，在查看事件处理方法后，只能评估不能解决此规则冲突的风险。 检查代码时，请考虑以下问题：

- 你的事件处理程序是否执行任何危险或可利用的操作，如断言权限或禁止非托管代码权限？

- 与代码之间的安全威胁是什么，因为它可以随时在堆栈上只有高度受信任的调用方运行？

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请查看方法并评估以下各项：

- 是否可以使事件处理方法成为非公共的？

- 是否可以将所有危险功能移出事件处理程序？

- 如果实施了安全要求，是否可以通过其他方式实现此目的？

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅在仔细检查安全检查后，禁止显示此规则发出的警告，以确保你的代码不会带来安全威胁。

## <a name="example"></a>示例
 下面的代码演示了一个可能被恶意代码误用的事件处理方法。

 [!code-csharp[FxCop.Security.EventSecLib#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.EventSecLib/cs/FxCop.Security.EventSecLib.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Security.CodeAccessPermission.Demand%2A?displayProperty=fullName> <xref:System.EventArgs?displayProperty=fullName>
 [安全要求](https://msdn.microsoft.com/324c14f8-54ff-494d-9fd1-bfd20962c8ba)

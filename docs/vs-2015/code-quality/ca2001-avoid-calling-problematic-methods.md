---
title: CA2001:避免调用有问题的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2001
- AvoidCallingProblematicMethods
helpviewer_keywords:
- CA2001
- AvoidCallingProblematicMethods
ms.assetid: 19db8edb-31ce-441c-b0de-a0f2746155b7
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 26f50580c8d29e24b25a9dad520a81d22a3dfc0c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189068"
---
# <a name="ca2001-avoid-calling-problematic-methods"></a>CA2001:避免调用有问题的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidCallingProblematicMethods|
|CheckId|CA2001|
|类别|Microsoft.Reliability|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 某个成员调用可能存在危险或有问题的方法。

## <a name="rule-description"></a>规则说明
 避免进行不必要和具有潜在危险的方法调用。

 成员调用以下方法之一，就会发生此规则冲突。

|方法|描述|
|------------|-----------------|
|<xref:System.GC.Collect%2A?displayProperty=fullName>|调用 GC。收集会严重影响应用程序性能和很少需要。 有关详细信息，请参阅[Rico Mariani 性能问题的见解](http://go.microsoft.com/fwlink/?LinkId=169256)MSDN 上的博客文章。|
|<xref:System.Threading.Thread.Resume%2A?displayProperty=fullName><br /><br /> <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>|已弃用 Thread.Suspend 和 Thread.Resume 由于其不可预知的行为。  使用中的其他类<xref:System.Threading>命名空间，如<xref:System.Threading.Monitor>， <xref:System.Threading.Mutex>，和<xref:System.Threading.Semaphore>以同步线程或保护资源。|
|<xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A?displayProperty=fullName>|DangerousGetHandle 方法会带来安全风险，因为它可以返回不是有效的句柄。 请参阅<xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A>和<xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A>详细了解如何安全地使用 DangerousGetHandle 方法的方法。|
|<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>|这些方法可以从意外的位置加载的程序集。 有关示例，请参阅 Suzanne Cook 的.NET CLR 笔记博客文章[LoadFile vs。LoadFrom](http://go.microsoft.com/fwlink/?LinkId=164450)并[选择绑定上下文](http://go.microsoft.com/fwlink/?LinkId=164451)方法加载程序集的信息的 MSDN 网站上。|
|[CoSetProxyBlanket](http://go.microsoft.com/fwlink/?LinkID=169250) (Ole32)<br /><br /> [CoInitializeSecurity](http://go.microsoft.com/fwlink/?LinkId=169255) (Ole32)|用户代码启动托管进程中执行时，它是太迟可靠地调用 CoSetProxyBlanket。 公共语言运行时 (CLR) 执行可能会阻止用户 P/Invoke 之后的初始化操作。<br /><br /> 如果你确实必须 CoSetProxyBlanket 调用托管应用程序，我们建议使用本机代码启动过程 (C++) 可执行文件，在本机代码中，调用 CoSetProxyBlanket，然后在进程中启动托管的代码应用程序。 （请务必指定运行时的版本号。）|

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请删除或替换对危险或有问题的方法的调用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当有问题的方法的任何其他方法时，则应该禁止显示此规则的消息。

## <a name="see-also"></a>请参阅
 [可靠性警告](../code-quality/reliability-warnings.md)

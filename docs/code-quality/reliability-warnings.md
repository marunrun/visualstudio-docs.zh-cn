---
title: 可靠性警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- warnings, reliability
- reliability warnings
- managed code analysis warnings, reliability warnings
ms.assetid: 77886846-10a2-4585-968a-7eb60ebe07e8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cb39bb5f59373f52d77c7cc5d13d12544d4c0314
ms.sourcegitcommit: 3e94d9fb6dc56fa8b23fbacd5d11cf8d6e7e18f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252583"
---
# <a name="reliability-warnings"></a>可靠性警告

可靠性警告支持库和应用程序的可靠性，如正确的内存和线程使用。 可靠性规则包括：

|规则|描述|
|----------|-----------------|
|[CA2000：在丢失范围 @ no__t 之前释放对象-0|由于可能发生异常事件，导致对象的终结器无法运行，因此，应显式释放对象，以避免对该对象的所有引用超出范围。|
|[CA2001：避免调用有问题的方法 @ no__t|某个成员调用可能存在危险或有问题的方法。|
|[CA2002：请勿锁定具有弱标识 @ no__t 的对象|当可以跨应用程序域边界直接进行访问对象时，则认为该对象具有弱标识。 对于尝试获取对具有弱标识的对象的锁的线程，该线程可能会被其他应用程序域中持有对同一对象的锁的另一线程所阻止。|
|[CA2003：不要将纤程视为线程 @ no__t-0|托管线程被视为 Win32 线程。|
|[CA2004：删除对 GC 的调用。KeepAlive @ no__t-0|如果要转换到 SafeHandle 使用情况，请删除对 GC 的所有调用。KeepAlive （object）。 在这种情况下，类不必调用 GC。KeepAlive，假设它们没有终结器，但依赖于 SafeHandle 来完成它们的操作系统句柄。|
|[CA2006：使用 SafeHandle 封装本机资源 @ no__t-0|在托管代码中使用 IntPtr 可能意味着潜在的安全性和可靠性方面的问题。 必须检查所有使用 IntPtr 之处，以确定是否需要在该处使用 SafeHandle 或类似的技术。|
|[CA2007：不要直接等待任务 @ no__t-0|异步方法会 直接[等待](/dotnet/csharp/language-reference/keywords/await) <xref:System.Threading.Tasks.Task>。|

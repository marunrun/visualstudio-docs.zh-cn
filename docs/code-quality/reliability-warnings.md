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
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 602f372e11c4a9a8506186535958fc4f22da7806
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72649120"
---
# <a name="reliability-warnings"></a>可靠性警告

可靠性警告支持库和应用程序的可靠性，如正确的内存和线程使用。 可靠性规则包括：

|规则|描述|
|----------|-----------------|
|[CA2000：超出范围前释放对象](../code-quality/ca2000.md)|由于可能发生异常事件，导致对象的终结器无法运行，因此，应显式释放对象，以避免对该对象的所有引用超出范围。|
|[CA2001：避免调用有问题的方法](../code-quality/ca2001.md)|某个成员调用可能存在危险或有问题的方法。|
|[CA2002：不要锁定具有弱标识的对象](../code-quality/ca2002.md)|当可以跨应用程序域边界直接进行访问对象时，则认为该对象具有弱标识。 对于尝试获取对具有弱标识的对象的锁的线程，该线程可能会被其他应用程序域中持有对同一对象的锁的另一线程所阻止。|
|[CA2003：不要将纤程视为线程](../code-quality/ca2003.md)|托管线程被视为 Win32 线程。|
|[CA2004：移除对 GC.KeepAlive 的调用](../code-quality/ca2004.md)|如果要转换到 SafeHandle 使用情况，请删除对 GC 的所有调用。KeepAlive （object）。 在这种情况下，类不必调用 GC。KeepAlive，假设它们没有终结器，但依赖于 SafeHandle 来完成它们的操作系统句柄。|
|[CA2006：使用 SafeHandle 封装本机资源](../code-quality/ca2006.md)|在托管代码中使用 IntPtr 可能意味着潜在的安全性和可靠性方面的问题。 必须检查所有使用 IntPtr 之处，以确定是否需要在该处使用 SafeHandle 或类似的技术。|
|[CA2007：不直接等待任务](../code-quality/ca2007.md)|异步方法会直接[等待](/dotnet/csharp/language-reference/keywords/await)<xref:System.Threading.Tasks.Task>。|

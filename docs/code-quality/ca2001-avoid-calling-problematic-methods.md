---
title: CA2001:避免调用有问题的方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2001
- AvoidCallingProblematicMethods
helpviewer_keywords:
- CA2001
- AvoidCallingProblematicMethods
ms.assetid: 19db8edb-31ce-441c-b0de-a0f2746155b7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 95209067f3821b6446b64dc7990e189720d20cea
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233197"
---
# <a name="ca2001-avoid-calling-problematic-methods"></a>CA2001:避免调用有问题的方法

|||
|-|-|
|TypeName|AvoidCallingProblematicMethods|
|CheckId|CA2001|
|类别|Microsoft.Reliability|
|重大更改|不间断|

## <a name="cause"></a>原因

某个成员调用可能存在危险或有问题的方法。

## <a name="rule-description"></a>规则说明

避免进行不必要的、有风险的方法调用。 当成员调用以下方法之一时，将发生与此规则的冲突：

|方法|描述|
|------------|-----------------|
|<xref:System.GC.Collect%2A?displayProperty=fullName>|调用 GC。收集可能会显著影响应用程序性能，而且很少需要。 有关详细信息，请参阅 MSDN 上[的多 Mariani 的性能 mariani 关于](http://go.microsoft.com/fwlink/?LinkId=169256)博客条目。|
|<xref:System.Threading.Thread.Resume%2A?displayProperty=fullName><br /><br /> <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>|由于无法预测的行为，因此无法使用 Resume。  使用命名空间中的<xref:System.Threading>其他类， <xref:System.Threading.Monitor>如、 <xref:System.Threading.Mutex>和<xref:System.Threading.Semaphore>，以同步线程或保护资源。|
|<xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A?displayProperty=fullName>|Safehandle.dangerousgethandle 方法会带来安全风险，因为它可能返回无效的句柄。 有关如何安全使用<xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A> safehandle.dangerousgethandle 方法的详细信息，请参阅和方法。<xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A>|
|<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>|这些方法可以从意外的位置加载程序集。 例如，请参阅 Suzanne 库的 .net CLR 说明博客文章[assembly.loadfile 与LoadFrom](http://go.microsoft.com/fwlink/?LinkId=164450)和[选择绑定上下文](http://go.microsoft.com/fwlink/?LinkId=164451)以获取有关加载程序集的方法的信息。|
|[CoSetProxyBlanket](http://go.microsoft.com/fwlink/?LinkID=169250)Ole32.lib<br /><br /> [CoInitializeSecurity](http://go.microsoft.com/fwlink/?LinkId=169255)Ole32.lib|在托管进程中，用户代码开始执行的时间太晚，无法可靠地调用 CoSetProxyBlanket。 公共语言运行时（CLR）会进行初始化操作，这些操作可能会阻止用户进行 P/Invoke。<br /><br /> 如果你确实需要为托管应用程序调用 CoSetProxyBlanket，则建议你通过使用本机代码（C++）可执行文件，在本机代码中调用 CoSetProxyBlanket，然后在进程中启动托管代码应用程序来启动该过程。 （请确保指定运行时版本号。）|

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请删除或替换对危险或有问题的方法的调用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

仅当没有任何有问题的方法可替代时，才应禁止显示此规则的消息。

## <a name="see-also"></a>请参阅

- [可靠性警告](../code-quality/reliability-warnings.md)
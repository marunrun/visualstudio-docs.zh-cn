---
title: CA2006:使用 SafeHandle 封装本机资源
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2006
- UseSafeHandleToEncapsulateNativeResources
helpviewer_keywords:
- UseSafeHandleToEncapsulateNativeResources
- CA2006
ms.assetid: a71950bd-bcc1-463d-b1f2-5233bc451456
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 0e671deab060346bb998932495e5590f19945eaa
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233100"
---
# <a name="ca2006-use-safehandle-to-encapsulate-native-resources"></a>CA2006:使用 SafeHandle 封装本机资源

|||
|-|-|
|TypeName|UseSafeHandleToEncapsulateNativeResources|
|CheckId|CA2006|
|类别|Microsoft.Reliability|
|重大更改|不间断|

## <a name="cause"></a>原因

托管代码使用<xref:System.IntPtr>来访问本机资源。

## <a name="rule-description"></a>规则说明

`IntPtr`在托管代码中使用可能表示存在潜在的安全性和可靠性问题。 必须检查的`IntPtr`所有使用<xref:System.Runtime.InteropServices.SafeHandle> ，以确定是否需要在其位置使用或类似的技术。 如果`IntPtr`表示某些本机资源，如内存、文件句柄或套接字，托管代码被视为拥有，则会出现问题。 如果托管代码拥有资源，则它还必须释放与之关联的本机资源，因为这样做可能会导致资源泄露。

在这种情况下，如果允许多线程访问， `IntPtr`并提供一种方法来释放由表示`IntPtr`的资源，则也会存在安全或可靠性问题。 这些问题涉及到在资源`IntPtr`释放时回收值，同时在另一个线程上使用资源。 这可能导致争用条件，其中一个线程可以读取或写入与错误资源关联的数据。 例如，如果你的类型将 OS 句柄存储为`IntPtr` ，同时允许用户同时调用**Close**和使用该句柄的任何其他方法，而不需要进行某种同步，则你的代码将有一个句柄回收问题。

此句柄回收问题可能会导致数据损坏，并经常导致安全漏洞。 `SafeHandle`及其同级类<xref:System.Runtime.InteropServices.CriticalHandle>提供一种机制，用于封装资源的本机句柄，以便避免此类线程处理问题。 此外，还可以使用`SafeHandle`及其同级类`CriticalHandle`来处理其他线程问题，例如，通过调用本机方法来小心控制包含本机句柄副本的托管对象的生存期。 在这种情况下，您通常可以删除`GC.KeepAlive`对的调用。 当你使用`SafeHandle`和`CriticalHandle`时，所产生的性能开销将经常通过仔细设计来减少。

## <a name="how-to-fix-violations"></a>如何解决冲突

`IntPtr` 将`SafeHandle`使用情况转换为，以安全地管理对本机资源的访问。 有关示例，请参阅参考文章。<xref:System.Runtime.InteropServices.SafeHandle>

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

请勿禁止显示此警告。

## <a name="see-also"></a>请参阅

- <xref:System.IDisposable>
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
ms.openlocfilehash: 6d29eb9475d48e634766df65836162d6a79fed77
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808405"
---
# <a name="ca2006-use-safehandle-to-encapsulate-native-resources"></a>CA2006:使用 SafeHandle 封装本机资源

|||
|-|-|
|TypeName|UseSafeHandleToEncapsulateNativeResources|
|CheckId|CA2006|
|类别|Microsoft.Reliability|
|是否重大更改|非换行|

## <a name="cause"></a>原因

托管代码使用<xref:System.IntPtr>访问本机资源。

## <a name="rule-description"></a>规则说明

使用`IntPtr`在托管代码中可能表示潜在的安全性和可靠性问题。 使用的所有`IntPtr`必须检查以确定是否使用<xref:System.Runtime.InteropServices.SafeHandle>，或类似的技术，需要在其原位置。 如果不会发生问题`IntPtr`表示某些本机资源，例如内存、 文件句柄或套接字时，托管的代码被视为拥有。 如果托管的代码拥有的资源，它还必须释放与其关联的本机资源，因为无法执行此操作会导致资源泄漏。

在这种情况下，安全性或可靠性问题还会存在如果允许多线程的访问`IntPtr`和释放资源所表示的一种方法`IntPtr`提供。 这些问题涉及的回收`IntPtr`在资源释放时同时使用的资源进行了另一个线程上的值。 这会导致争用条件，其中一个线程可以读取或写入错误的资源与相关联的数据。 例如，如果您的类型存储为某个操作系统句柄`IntPtr`，使用户可以同时调用**关闭**和任何其他方法使用该句柄，同时并不使用同步，你的代码存在句柄回收出现问题。

此句柄回收问题可能导致数据损坏和通常情况下，安全漏洞。 `SafeHandle` 和其同级类<xref:System.Runtime.InteropServices.CriticalHandle>提供一种机制来封装本机资源的句柄，以便可以避免此类线程处理问题。 此外，还可以使用`SafeHandle`及其同级类`CriticalHandle`其他线程处理问题，例如，若要仔细控制对本机方法的调用包含的本机句柄的副本的托管对象的生存期。 在此情况下，通常可以消除对调用`GC.KeepAlive`。 你使用时，需要支付的性能开销`SafeHandle`和一定程度上， `CriticalHandle`，通常可以通过仔细设计减少。

## <a name="how-to-fix-violations"></a>如何解决冲突

将转换`IntPtr`使用情况与`SafeHandle`以便安全地管理对本机资源的访问。 请参阅<xref:System.Runtime.InteropServices.SafeHandle>示例的参考文章。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不要禁止显示此警告。

## <a name="see-also"></a>请参阅

- <xref:System.IDisposable>
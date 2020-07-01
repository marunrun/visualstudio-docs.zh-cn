---
title: CA2006：使用 SafeHandle 封装本机资源 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2006
- UseSafeHandleToEncapsulateNativeResources
helpviewer_keywords:
- UseSafeHandleToEncapsulateNativeResources
- CA2006
ms.assetid: a71950bd-bcc1-463d-b1f2-5233bc451456
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fdf3ff02c86a878e9c955d2b3b92879870700efa
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521142"
---
# <a name="ca2006-use-safehandle-to-encapsulate-native-resources"></a>CA2006:使用 SafeHandle 封装本机资源
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|UseSafeHandleToEncapsulateNativeResources|
|CheckId|CA2006|
|类别|Microsoft 可靠性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 托管代码使用 <xref:System.IntPtr> 来访问本机资源。

## <a name="rule-description"></a>规则描述
 `IntPtr`在托管代码中使用可能表示存在潜在的安全性和可靠性问题。 必须检查的所有使用 `IntPtr` ，以确定是否 <xref:System.Runtime.InteropServices.SafeHandle> 需要在其位置使用或类似的技术。 如果 `IntPtr` 表示某些本机资源，如内存、文件句柄或套接字，托管代码被视为拥有，则会出现问题。 如果托管代码拥有资源，则它还必须释放与之关联的本机资源，因为这样做可能会导致资源泄露。

 在这种情况下，如果允许多线程访问， `IntPtr` 并提供一种方法来释放由表示的资源，则也会存在安全或可靠性问题 `IntPtr` 。 这些问题涉及到在 `IntPtr` 资源释放时回收值，同时在另一个线程上使用资源。 这可能导致争用条件，其中一个线程可以读取或写入与错误资源关联的数据。 例如，如果你的类型将 OS 句柄存储为 `IntPtr` ，同时允许用户同时调用**Close**和使用该句柄的任何其他方法，而不需要进行某种同步，则你的代码将有一个句柄回收问题。

 此句柄回收问题可能会导致数据损坏，并经常导致安全漏洞。 `SafeHandle`及其同级类 <xref:System.Runtime.InteropServices.CriticalHandle> 提供一种机制，用于封装资源的本机句柄，以便避免此类线程处理问题。 此外，还可以使用 `SafeHandle` 及其同级类 `CriticalHandle` 来处理其他线程问题，例如，通过调用本机方法来小心控制包含本机句柄副本的托管对象的生存期。 在这种情况下，您通常可以删除对的调用 `GC.KeepAlive` 。 当你使用和时，所产生的性能开销分行 `SafeHandle` `CriticalHandle` 通常可以通过仔细的设计来减少。

## <a name="how-to-fix-violations"></a>如何解决冲突
 将 `IntPtr` 使用情况转换为 `SafeHandle` ，以安全地管理对本机资源的访问。 有关示例，请参阅 <xref:System.Runtime.InteropServices.SafeHandle> 参考主题。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不应禁止显示此警告。

## <a name="see-also"></a>另请参阅
 <xref:System.IDisposable>

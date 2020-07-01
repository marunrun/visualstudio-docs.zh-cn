---
title: 自动功能挂起
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 236a95cd8d4af8da91199bf79e7c9fe3aa0d49af
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769477"
---
# <a name="automatic-feature-suspension"></a>自动功能挂起

如果可用系统内存为 200 MB 或更小，则 Visual Studio 会在代码编辑器中显示以下消息：

![暂停完整解决方案分析的警报文本](../code-quality/media/fsa_alert.png)

当 Visual Studio 检测到内存不足的情况时，它会自动挂起某些高级功能，以帮助其保持稳定。 Visual Studio 继续像以前一样工作，但其性能会下降。

在内存不足的情况下，将执行以下操作：

- Visual c # 和 Visual Basic 的实时代码分析降低到最小范围。

- 针对 Visual c # 和 Visual Basic 的[垃圾回收](/dotnet/standard/garbage-collection/index)（GC）低延迟模式处于禁用状态。

- Visual Studio 缓存已刷新。

## <a name="improve-visual-studio-performance"></a>提高 Visual Studio 性能

有关在处理大型解决方案或内存不足的情况时如何提高 Visual Studio 性能的提示和技巧，请参阅[大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)。

## <a name="live-code-analysis-is-reduced-to-minimal-scope"></a>实时代码分析降低到最小范围

默认情况下，对打开的文档和项目执行实时代码分析。 你可以自定义此分析范围以减小到当前文档或增加到整个解决方案。 有关详细信息，请参阅[如何：配置托管代码的实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。 在内存不足的情况下，Visual Studio 会强制将实时分析范围缩减为当前文档。 但是，你可以通过在信息栏中选择 "**重新启用**" 按钮或重新启动 Visual Studio 来重新启用首选的分析作用域。 "选项" 对话框始终显示当前的实时代码分析范围设置。

## <a name="gc-low-latency-disabled"></a>GC 低延迟已禁用

若要重新启用 GC 低延迟模式，请重启 Visual Studio。 默认情况下，每次键入时，Visual Studio 都会启用 GC 低延迟模式，以确保键入内容不会阻止任何 GC 操作。 但是，如果内存不足的情况导致 Visual Studio 显示自动挂起警告，则会为该会话禁用 GC 低延迟模式。 重新启动 Visual Studio 将重新启用默认的 GC 行为。 有关详细信息，请参阅 <xref:System.Runtime.GCLatencyMode>。

## <a name="visual-studio-caches-flushed"></a>Visual Studio 缓存已刷新

如果继续当前的开发会话或重启 Visual Studio，则会立即清空所有 Visual Studio 缓存，但会开始重新填充。 刷新缓存包括以下功能的缓存：

- 查找所有引用

- 定位到

- 添加使用

此外，还会清除用于内部 Visual Studio 操作的缓存。

> [!NOTE]
> 自动功能暂停警告只会针对每个解决方案出现一次，而不会在每个会话的基础上出现一次。 这意味着，如果从 Visual Basic 切换到 Visual c # （反之亦然），并遇到另一个内存不足的情况，则可能会出现另一个自动功能暂停警告。

## <a name="see-also"></a>另请参阅

- [如何：配置托管代码的实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)
- [垃圾回收基础](/dotnet/standard/garbage-collection/fundamentals)
- [大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)

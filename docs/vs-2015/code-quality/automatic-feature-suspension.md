---
title: 自动功能暂停 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b9c80ba76ba2da978c9cb475299ba0fc9e614120
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655148"
---
# <a name="automatic-feature-suspension"></a>自动功能挂起
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
如果可用系统内存降到200MB 或更低，则 Visual Studio 会在代码编辑器中显示以下消息。

 ![暂停完整解决方案分析的警报文本](../code-quality/media/fsa-alert.png "FSA_Alert")

 当 Visual Studio 检测到内存不足的情况时，它会自动挂起某些高级功能，以帮助其保持稳定。 出现这种高级功能挂起警告时，Visual Studio 将继续像以前一样工作，但其性能会略微下降。

 在内存不足的情况下，将发生以下情况：

- 已禁用视觉对象C#和 Visual Basic 的完整解决方案分析。

- 为视觉对象C#和 Visual Basic 禁用了[垃圾回收](https://msdn.microsoft.com/library/22b6cb97-0c80-4eeb-a2cf-5ed7655e37f9)（GC）低延迟模式。

- Visual Studio 缓存已刷新。

## <a name="improve-visual-studio-performance"></a>提高 Visual Studio 性能
 有关在处理大型解决方案或内存不足的情况时如何提高 Visual Studio 性能的提示和技巧，请参阅[大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)。

## <a name="full-solution-analysis-suspended"></a>已挂起完整解决方案分析
 默认情况下，将对 Visual Basic 启用完整解决方案分析，并对C#视觉对象禁用完整解决方案分析。 但是，在内存不足的情况下，无论 "选项" 对话框中的设置如何， C#都将自动为 Visual Basic 和视觉对象禁用完整的解决方案分析。 但是，你可以通过在 "选项" 对话框中**选择 "** **启用完整解决方案分析**" 复选框或通过重新启动 Visual Studio 来重新启用完整解决方案分析。 "选项" 对话框始终显示当前的完整解决方案分析设置。 有关详细信息，请参阅[如何：启用和禁用完整解决方案分析](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)。

## <a name="gc-low-latency-disabled"></a>GC 低延迟已禁用
 若要重新启用 GC 低延迟模式，请重启 Visual Studio。  默认情况下，每次键入时，Visual Studio 都会启用 GC 低延迟模式，以确保键入内容不会阻止任何 GC 操作。 但是，如果内存不足的情况导致 Visual Studio 显示自动挂起警告，则会为该会话禁用 GC 低延迟模式。 重新启动 Visual Studio 将重新启用默认的 GC 行为。 有关更多信息，请参见<xref:System.Runtime.GCLatencyMode>。

## <a name="visual-studio-caches-flushed"></a>Visual Studio 缓存已刷新

所有 Visual Studio 缓存会立即清空，但如果继续当前的开发会话或重启 Visual Studio，将开始重新填充。 刷新缓存包括以下功能的缓存。

- 查找所有引用

- 定位到

- 添加使用

此外，还会清除用于内部 Visual Studio 操作的缓存。

> [!NOTE]
> 自动功能暂停警告只会针对每个解决方案出现一次，而不会在每个会话的基础上出现一次。 这意味着，如果从 Visual Basic 切换到 Visual C# （或反之）并运行到另一个内存不足的情况，则可能会出现另一个自动功能暂停警告。

## <a name="see-also"></a>请参阅

- [如何：启用和禁用完整解决方案分析](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)
- [垃圾回收的基础知识](https://msdn.microsoft.com/library/67c5a20d-1be1-4ea7-8a9a-92b0b08658d2)
- [大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)
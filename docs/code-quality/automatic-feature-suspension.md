---
title: 自动功能挂起
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d6910bae3d924202fad8995d6ccd53efe848ba50
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75573295"
---
# <a name="automatic-feature-suspension"></a>自动功能挂起

如果你可用系统内存降至 200 MB 或更少，Visual Studio 代码编辑器中显示以下消息：

![警报文本中挂起完整解决方案分析](../code-quality/media/fsa_alert.png)

当 Visual Studio 检测到内存不足的情况时，它会自动挂起某些高级的功能，以帮助其保持不变。 Visual Studio 会继续像以前那样工作，但其性能会降低。

在内存不足的情况，会发生下列操作：

- 对于 Visual C# 和 Visual Basic 的完整解决方案分析处于禁用状态。

- [垃圾回收](/dotnet/standard/garbage-collection/index)视觉对象 (GC) 的低延迟模式C#和 Visual Basic 已禁用。

- Visual Studio 将缓存刷新。

## <a name="improve-visual-studio-performance"></a>提高 Visual Studio 性能

提示和技巧如何改进 Visual Studio 性能，处理大型解决方案或内存不足情况时，请参阅[大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)。

## <a name="full-solution-analysis-suspended"></a>挂起的完整解决方案分析

默认情况下，完整解决方案分析适用于 Visual Basic 启用和禁用对于 Visual C#。 但是，内存不足的情况，在完整解决方案分析会自动禁用 Visual Basic 和 Visual C#，而不考虑其设置选项对话框中。 但是，您可以重新启用完整解决方案分析通过选择**重新启用**中的信息栏出现时，通过选择按钮**启用完整解决方案分析**复选框，在选项对话框中，或通过重新启动 Visual Studio。 选项对话框始终显示当前的完整解决方案分析设置。 有关详细信息，请参阅[如何： 启用和禁用完整解决方案分析](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)。

## <a name="gc-low-latency-disabled"></a>禁用 GC 低延迟

若要重新启用 GC 低延迟模式，请重新启动 Visual Studio。 默认情况下，Visual Studio 使 GC 低延迟模式，只要键入以确保您键入的内容不会阻止任何 GC 操作。 但是，如果内存不足的情况导致 Visual Studio 显示自动暂停警告，为该会话禁用 GC 低延迟模式。 重新启动 Visual Studio 将重新启用默认 GC 行为。 有关更多信息，请参见<xref:System.Runtime.GCLatencyMode>。

## <a name="visual-studio-caches-flushed"></a>Visual Studio 缓存刷新

如果您继续您当前的开发会话或重新启动 Visual Studio，立即将清空所有 Visual Studio 缓存，但开始重新填充。 刷新的缓存包括以下功能的缓存：

- 查找所有引用

- 定位到

- 添加 Using

此外，用于内部 Visual Studio 操作的缓存也会被清除。

> [!NOTE]
> 在每个会话的基础的每个解决方案基础上一次出现自动功能挂起警告。 这意味着，如果您在 Visual Basic 中切换到 Visual C# （或反之亦然），并运行到另一个内存不足的情况，可能就可以自动功能挂起的警告。

## <a name="see-also"></a>另请参阅

- [如何：启用和禁用完整解决方案分析](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)
- [垃圾回收的基础知识](/dotnet/standard/garbage-collection/fundamentals)
- [针对大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)

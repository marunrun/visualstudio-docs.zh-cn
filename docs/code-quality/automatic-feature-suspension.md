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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e8480eb57a08905c2a593adbab519ae793638888
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431236"
---
# <a name="automatic-feature-suspension"></a>自动功能挂起

如果可用的系统内存降至 200 MB 或更少，Visual Studio 会在代码编辑器中显示以下消息：

![警报文本暂停完整的解决方案分析](../code-quality/media/fsa_alert.png)

当 Visual Studio 检测到内存不足时，它会自动挂起某些高级功能，以帮助其保持稳定。 Visual Studio 继续像以前那样工作，但其性能下降。

在内存不足的情况下，将执行以下操作：

- Visual C++ 和可视化基本的实时代码分析被缩小到最小范围。

- 禁用了 Visual C++ 和可视化基本版的[垃圾回收](/dotnet/standard/garbage-collection/index)（GC） 低延迟模式。

- 可视化工作室缓存被刷新。

## <a name="improve-visual-studio-performance"></a>提高视觉工作室性能

有关在处理大型解决方案或内存不足条件时如何提高 Visual Studio 性能的提示和技巧，请参阅[大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)。

## <a name="live-code-analysis-is-reduced-to-minimal-scope"></a>实时代码分析减少到最小范围

默认情况下，对打开的文档和项目执行实时代码分析。 您可以自定义此分析范围以简化为当前文档或增加到整个解决方案。 有关详细信息，请参阅[如何：为托管代码配置实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。 在内存不足的情况下，Visual Studio 强制将实时分析范围缩减为当前文档。 但是，您可以通过在信息栏中选择"在信息栏中**重新启用**"按钮时重新启用该按钮或重新启动 Visual Studio 来重新启用首选分析范围。 "选项"对话框始终显示当前实时代码分析范围设置。

## <a name="gc-low-latency-disabled"></a>禁用 GC 低延迟

要重新启用 GC 低延迟模式，请重新启动 Visual Studio。 默认情况下，可视化工作室在键入时启用 GC 低延迟模式，以确保键入不会阻止任何 GC 操作。 但是，如果内存不足导致 Visual Studio 显示自动挂起警告，则该会话将禁用 GC 低延迟模式。 重新启动可视化工作室可重新启用默认 GC 行为。 有关详细信息，请参阅 <xref:System.Runtime.GCLatencyMode>。

## <a name="visual-studio-caches-flushed"></a>可视化工作室缓存已刷新

如果继续当前开发会话或重新启动 Visual Studio，则所有 Visual Studio 缓存将立即清空，但开始重新填充。 刷新的缓存包括以下功能的缓存：

- 查找所有引用

- 定位到

- 使用添加

此外，还清除了用于内部可视化工作室操作的缓存。

> [!NOTE]
> 自动功能挂起警告仅按每个解决方案发生一次，而不是基于每个会话。 这意味着，如果您从 Visual Basic 切换到 Visual C++（反之亦然），并遇到另一个内存不足的情况，则可能会收到另一个自动功能挂起警告。

## <a name="see-also"></a>另请参阅

- [如何：为托管代码配置实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)
- [垃圾回收基础](/dotnet/standard/garbage-collection/fundamentals)
- [大型解决方案的性能注意事项](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)

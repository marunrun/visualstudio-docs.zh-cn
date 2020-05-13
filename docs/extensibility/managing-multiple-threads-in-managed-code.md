---
title: 如何：在托管代码中管理多个线程 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 59730063-cc29-4dae-baff-2234ad8d0c8f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ceaa0af4f57fe374cf9cf4b2dd8b4f40af74a852
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702784"
---
# <a name="how-to-manage-multiple-threads-in-managed-code"></a>如何：在托管代码中管理多个线程
如果您有一个托管 VSPackage 扩展调用异步方法，或者具有在 Visual Studio UI 线程以外的线程上执行的操作，则应遵循下面给出的准则。 您可以保持 UI 线程的响应速度，因为它不需要等待另一个线程的工作完成。 您可以提高代码的效率，因为您没有占用堆栈空间的额外线程，并且您可以使其更可靠且更易于调试，因为可以避免死锁和挂起。

 通常，可以从 UI 线程切换到其他线程，反之亦然。 当方法返回时，当前线程是最初调用它的线程。

> [!IMPORTANT]
> 以下准则在<xref:Microsoft.VisualStudio.Threading>命名空间中使用 API，特别是<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>类。 此命名空间中的 API 在 中[!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)]是新的。 可以从<xref:Microsoft.VisualStudio.Shell.ThreadHelper>属性`ThreadHelper.JoinableTaskFactory`获取 的<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>实例。

## <a name="switch-from-the-ui-thread-to-a-background-thread"></a>从 UI 线程切换到后台线程

1. 如果位于 UI 线程上，并且想要在后台线程上执行异步工作，请使用`Task.Run()`：

    ```csharp
    await Task.Run(async delegate{
        // Now you're on a separate thread.
    });
    // Now you're back on the UI thread.

    ```

2. 如果位于 UI 线程上，并且希望在对后台线程执行工作时同步阻止，请使用<xref:System.Threading.Tasks.TaskScheduler>`TaskScheduler.Default`<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A>

    ```csharp
    // using Microsoft.VisualStudio.Threading;
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        await TaskScheduler.Default;
        // You're now on a separate thread.
        DoSomethingSynchronous();
        await OrSomethingAsynchronous();
    });
    ```

## <a name="switch-from-a-background-thread-to-the-ui-thread"></a>从后台线程切换到 UI 线程

1. 如果您位于后台线程上，并且想在 UI 线程上执行某些操作，请使用 ： <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>

    ```csharp
    // Switch to main thread
    await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
    ```

     可以使用 方法<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>切换到 UI 线程。 此方法将消息发布到 UI 线程，并延续当前异步方法，并与线程框架的其余部分通信，以设置正确的优先级并避免死锁。

     如果后台线程方法不是异步的，并且无法使其成为异步，则仍可以使用`await`语法通过用<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A>包装工作切换到 UI 线程，如以下示例所示：

    ```csharp
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        // Switch to main thread
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
        // Do your work on the main thread here.
    });
    ```

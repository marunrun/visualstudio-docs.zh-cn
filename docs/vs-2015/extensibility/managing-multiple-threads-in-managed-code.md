---
title: 在托管代码中管理多个线程 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 59730063-cc29-4dae-baff-2234ad8d0c8f
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 296ef23bc512a86917920b3c3d5fbb5ec203a21e
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387013"
---
# <a name="managing-multiple-threads-in-managed-code"></a>在托管代码中管理多个线程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你有一个托管的 VSPackage 扩展，该扩展调用异步方法，或者具有在 Visual Studio UI 线程之外的其他线程上执行的操作，则应遵循下面提供的指导原则。 您可以保持 UI 线程的响应能力，因为无需等待其他线程上的工作完成。 您可以使您的代码更高效，因为您没有占用堆栈空间的额外线程，并且可以使其更可靠、更易于调试，因为这样可以避免死锁和无响应。  
  
 通常，您可以从 UI 线程切换到另一个线程，反之亦然。 当方法返回时，当前线程是最初从中调用它的线程。  
  
> [!IMPORTANT]
> 以下准则使用命名空间中的 Api， <xref:Microsoft.VisualStudio.Threading> 特别是 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> 类。 此命名空间中的 Api 是中的新 Api [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] 。 可以从属性获取的实例 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> <xref:Microsoft.VisualStudio.Shell.ThreadHelper> `ThreadHelper.JoinableTaskFactory` 。  
  
## <a name="switching-from-the-ui-thread-to-a-background-thread"></a>从 UI 线程切换到后台线程  
  
1. 如果在 UI 线程上，并且想要在后台线程上执行异步工作，请使用 "运行" （）：  
  
    ```csharp  
    await Task.Run(async delegate{  
        // Now you’re on a separate thread.  
    });  
    // Now you’re back on the UI thread.  
  
    ```  
  
2. 如果你在 UI 线程上，并且想要在后台线程上执行工作时同步阻止，请使用 <xref:System.Threading.Tasks.TaskScheduler> 中的属性 `TaskScheduler.Default` <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> ：  
  
    ```csharp  
    // using Microsoft.VisualStudio.Threading;  
    ThreadHelper.JoinableTaskFactory.Run(async delegate {  
        await TaskScheduler.Default;  
        // You're now on a separate thread.  
        DoSomethingSynchronous();  
        await OrSomethingAsynchronous();  
    });  
    ```  
  
## <a name="switching-from-a-background-thread-to-the-ui-thread"></a>从后台线程切换到 UI 线程  
  
1. 如果你使用的是后台线程，并且想要在 UI 线程上执行某些操作，请使用 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> ：  
  
    ```csharp  
    // Switch to main thread  
    await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();  
    ```  
  
     可以使用 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> 方法切换到 UI 线程。 此方法会将消息发送到 UI 线程，同时继续使用当前的异步方法，并与线程框架的其余部分通信，以设置正确的优先级并避免死锁。  
  
     如果后台线程方法不是异步的，并且不能使其异步，则仍可使用 `await` 语法通过包装你的工作来切换到 UI 线程 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> ，如以下示例中所示：  
  
    ```csharp  
    ThreadHelper.JoinableTaskFactory.Run(async delegate {  
        // Switch to main thread  
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();  
        // Do your work on the main thread here.  
    });  
    ```

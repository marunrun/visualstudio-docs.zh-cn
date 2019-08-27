---
title: 管理多个线程在托管代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 59730063-cc29-4dae-baff-2234ad8d0c8f
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4e7198623283fa3ef9c82d6a39a1f7c1db6c760c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433034"
---
# <a name="managing-multiple-threads-in-managed-code"></a>在托管代码中管理多个线程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你有托管的 VSPackage 扩展的调用异步方法或已在 Visual Studio UI 线程以外的线程执行的操作，应遵循下面给出的准则。 因为它不需要等待上另一个线程完成的工作，可以使 UI 线程保持响应状态。 您可以使代码更加有效，因为您不需要额外的线程占用的堆栈空间，并且您可以使其更可靠、 更易于调试，因为避免死锁和挂起。  
  
 一般情况下，可以从 UI 线程切换到不同的线程，反之亦然。 方法返回时，当前线程是从其它最初调用的线程。  
  
> [!IMPORTANT]
> 以下指导原则使用中的 Api<xref:Microsoft.VisualStudio.Threading>命名空间，具体而言，<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>类。 此命名空间中的 Api 是中的新增功能[!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)]。 可以获取的实例<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>从<xref:Microsoft.VisualStudio.Shell.ThreadHelper>属性`ThreadHelper.JoinableTaskFactory`。  
  
## <a name="switching-from-the-ui-thread-to-a-background-thread"></a>从 UI 线程切换到后台线程  
  
1. 如果要在 UI 线程上，你想要执行后台线程上的异步工作，使用 Task.Run():  
  
    ```csharp  
    await Task.Run(async delegate{  
        // Now you’re on a separate thread.  
    });  
    // Now you’re back on the UI thread.  
  
    ```  
  
2. 如果您是在 UI 线程上，并且你想要以同步方式阻止后台线程，使用上执行工作时<xref:System.Threading.Tasks.TaskScheduler>属性`TaskScheduler.Default`内<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A>:  
  
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
  
1. 如果你是在后台线程上和你想要在 UI 线程，使用上实现某些<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>:  
  
    ```csharp  
    // Switch to main thread  
    await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();  
    ```  
  
     可以使用<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>方法才能切换到 UI 线程。 此方法将消息发布到与当前的异步方法，继续符的 UI 线程，并且还可与设置正确的优先级并避免死锁的线程框架的其余部分通信。  
  
     如果您不能进行异步后台线程方法不是异步，仍可以使用`await`语法来包装你的工作与通过切换到 UI 线程<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A>，如下例所示：  
  
    ```csharp  
    ThreadHelper.JoinableTaskFactory.Run(async delegate {  
        // Switch to main thread  
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();  
        // Do your work on the main thread here.  
    });  
    ```

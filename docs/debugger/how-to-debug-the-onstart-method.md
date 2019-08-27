---
title: 如何：调试 OnStart 方法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- OnStart method
- debugging [Visual Studio], Windows services
- debugging managed code, OnStart method
- debugging Windows Services applications, OnStart method
- Windows Service applications, debugging
ms.assetid: b06b5d65-424b-490f-bf58-97583cd7006a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2fc5e8a7e0bbc80fd7fa0aa2d242239a9be6a219
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62894412"
---
# <a name="how-to-debug-the-onstart-method"></a>如何：调试 OnStart 方法
通过启动 Windows 服务并将调试器附加到服务进程，可以调试 Windows 服务。 有关详细信息，请参阅[如何：调试 Windows 服务应用程序](/dotnet/framework/windows-services/how-to-debug-windows-service-applications)。 但是，若要调试 Windows 服务的 <xref:System.ServiceProcess.ServiceBase.OnStart%2A?displayProperty=fullName> 方法，必须从该方法内部启动调试器。

1. 将对 <xref:System.Diagnostics.Debugger.Launch%2A> 的调用添加到 `OnStart()`方法的开头。

    ```csharp
    protected override void OnStart(string[] args)
    {
        System.Diagnostics.Debugger.Launch();
    }
    ```

2. 启动服务（可以使用 `net start`，或在“服务”  窗口中启动）。

    将显示一个对话框，如下所示：

    ![OnStartDebug](../debugger/media/onstartdebug.png "OnStartDebug")

3. 选择“是，调试 \<服务名>。”

4. 在“实时调试器”窗口中，选择你想要用于调试的 Visual Studio 版本。

    ![JustInTimeDebugger](../debugger/media/justintimedebugger.png "JustInTimeDebugger")

5. 将启动 Visual Studio 新实例，并在 `Debugger.Launch()` 方法处停止执行。

## <a name="see-also"></a>请参阅
- [调试器安全](../debugger/debugger-security.md)
- [调试托管代码](../debugger/debugging-managed-code.md)

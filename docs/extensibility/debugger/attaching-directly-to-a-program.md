---
title: 直接附加到程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: ad2b7db8-821c-440c-ba07-c55c6a395e0f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a9a5699ee81b8c8ae36bcf492e93467615a9e89
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739259"
---
# <a name="attach-directly-to-a-program"></a>直接附加到程序
希望在已运行的进程中调试程序的用户通常遵循此过程：

1. 在 IDE 中，从 **"工具**"菜单中选择 **"调试过程"** 命令。

    这将显示“进程”**** 对话框。

2. 选择一个进程，然后单击"**附加"** 按钮。

    将显示 **"附加到进程**"对话框，列出计算机上安装的所有调试引擎 （DEs）。

3. 指定用于调试所选进程的 D，然后单击 **"确定**"。

   调试包启动调试会话并将 D 列表传递给它。 调试会话反过来将此列表以及回调函数传递到所选进程，然后要求进程枚举其正在运行的程序。

   在编程上，为了响应用户请求，调试包实例化会话调试管理器 （SDM），并将所选 D 的列表传递给它。 与列表一起，调试包传递 SDM [IDebugEvent 回调2](../../extensibility/debugger/reference/idebugeventcallback2.md)接口。 调试包通过调用[IDebugProcess2：：附加](../../extensibility/debugger/reference/idebugprocess2-attach.md)将 D 选项列表传递给所选进程。 然后，SDM 调用端口上的[IDebugProcess2：：enum程序](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)来枚举进程中运行的程序。

   从此时开始，每个调试引擎都附加到一个程序，完全如[启动后的附加](../../extensibility/debugger/attaching-after-a-launch.md)中详细一样，但有两个例外。

   为提高效率，为与 SDM 共享地址空间而实现的 DE 进行了分组，以便每个 DE 都有一组要附加到的程序。 在这种情况下[，IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)调用[IDebugEngine2：：附加](../../extensibility/debugger/reference/idebugengine2-attach.md)并传递要附加到的程序数组。

   第二个异常是，DE 发送到已运行的程序的启动事件通常不包括入口点事件。

## <a name="see-also"></a>请参阅
- [启动后发送启动事件](../../extensibility/debugger/sending-startup-events-after-a-launch.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)

---
title: 直接附加到程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: ad2b7db8-821c-440c-ba07-c55c6a395e0f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ab49163fc1474b541df3bc1b54d336574761baa3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147994"
---
# <a name="attaching-directly-to-a-program"></a>直接附加到程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

想要调试程序通常已在运行的进程中的用户使用以下过程：  
  
1. 在 IDE 中，选择**调试进程**命令**工具**菜单。  
  
    这将显示“进程”  对话框。  
  
2. 选择一个进程，然后单击**附加**按钮。  
  
    **附加到进程**会显示对话框，列出所有的调试引擎 (DEs) 在计算机上安装。  
  
3. 指定要用于调试所选的进程，然后依次对 DEs**确定**。  
  
   调试包启动调试会话，并向其传递的 DEs 列表。 调试会话反过来传递此列表，以及一个回调函数，为所选的进程，并询问枚举其正在运行的程序的过程。  
  
   以编程方式，以响应用户请求，调试包实例化会话调试管理器 (SDM)，并将所选 DEs 的列表传递给它。 列表中，以及调试程序包传递 SDM [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)接口。 调试包传递到所选的进程的 DEs 列表通过调用[IDebugProcess2::Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)。 然后调用 SDM [IDebugProcess2::EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)上要枚举的进程中运行的程序的端口。  
  
   从现在开始，每个调试引擎附加到程序完全按照中的详述[附加后启动](../../extensibility/debugger/attaching-after-a-launch.md)，有两个例外。  
  
   为提高效率，实现与 SDM 共享一个地址空间的 DEs 进行分组，以便每个 DE 有一组会将连接到的程序。 在这种情况下， [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)调用[IDebugEngine2::Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)并将其传递的程序附加到数组。  
  
   第二个例外情况是，发送 DE 附加到已在运行的程序的启动事件一般都不包含入口点事件。  
  
## <a name="see-also"></a>请参阅  
 [启动后发送启动事件](../../extensibility/debugger/sending-startup-events-after-a-launch.md)   
 [调试任务](../../extensibility/debugger/debugging-tasks.md)

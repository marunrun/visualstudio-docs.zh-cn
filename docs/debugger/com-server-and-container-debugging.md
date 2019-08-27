---
title: 调试 COM 服务器和容器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.com
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- ActiveX control container debugging [Visual Studio]
- debugging ActiveX controls
- COM servers, debugging
- ActiveX controls, debugging
- COM [Visual Studio], debugging
ms.assetid: b7ce8696-ebb8-4354-a767-f76b8ada4ac1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40edce29e8d40310f6eab37309c4c2ca7eb8a85a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62563990"
---
# <a name="com-server-and-container-debugging"></a>调试 COM 服务器和容器
COM 应用程序可执行许多不直接受程序员控制的任务。 DLL 间的通信、对象的使用计数和剪贴板操作只是可能遇到意外行为的少数几种情况。 发生这种情况时，首先应查明问题的根源。

 Visual Studio 调试器支持跨容器和服务器以及在容器和服务器中进行单步调试。 其中包括跨远程过程调用 (RPC) 进行单步调试的功能。

## <a name="BKMK_COMServerandContainerintheSameSolution"></a> 使用同一解决方案调试 COM 服务器和容器
 可以使用同一解决方案中的两个项目来调试 COM 服务器和容器。 在每个项目和调试中设置适当的断点。 当容器对服务器进行调用而遇到断点时，容器将一直等到服务器代码返回（即等到完成调试）。

 调试 COM 容器类似于调试标准程序。 但在调试一个产生回调的事件（比如将数据拖放到容器应用程序上）时有所不同。 在这种情况下，必须在回调函数中设置断点。

## <a name="BKMK_ServerApplicationWithoutContainerInformation"></a> 在没有容器信息的情况下调试服务器应用程序
 如果没有或不想使用容器应用程序的调试信息，开始调试服务器应用程序可分三步进行：

1. 像对待普通的应用程序一样开始调试服务器。

2. 按需要设置断点。

3. 启动容器应用程序。

## <a name="BKMK_DebuggingaServerandDomainIsolationSDIApplication"></a> 调试服务器和域隔离 (SDI) 应用程序
 如果调试的是 SDI 服务器应用程序，对于 C/C++、C# 或 Visual Basic 项目，必须在“项目属性页”对话框中的“命令行参数”属性中指定 `/Embedding` 或 `/Automation`。

 使用这些命令行参数，调试器可以像从容器中启动服务器应用程序一样启动它。 从程序管理器或文件管理器启动容器将导致容器使用在调试器中启动的服务器实例。

 若要访问“项目属性页”对话框，请在解决方案资源管理器中右键单击项目，然后从快捷菜单中选择“属性”。 若要找到“命令行参数”属性，请展开“配置属性”类别并单击“调试”页。

## <a name="see-also"></a>请参阅

- [调试 COM 和 ActiveX](../debugger/com-and-activex-debugging.md)
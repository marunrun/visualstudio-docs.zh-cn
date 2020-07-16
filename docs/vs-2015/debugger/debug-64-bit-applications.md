---
title: 调试 64 位应用程序 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], 64-bit
- 64-bit debugging
ms.assetid: db648e5f-6375-4e2d-aa98-eb7261958927
caps.latest.revision: 38
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c0eaa719bb3eeca2eb3dfe558184699ccca42819
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387195"
---
# <a name="debug-64-bit-applications"></a>调试 64 位应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本可在[调试64位应用程序](/visualstudio/debugger/debug-64-bit-applications)上找到。  
  
您可以调试运行于本地计算机或远程计算机上的 64 位应用程序。  
  
 若要调试在远程计算机上运行的 64 位应用程序，请参阅[远程调试](../debugger/remote-debugging.md)。  
  
 若要在本地调试 64 位应用程序，Visual Studio 将使用 64 位辅助进程 (msvsmon.exe) 执行不能在 32 位 Visual Studio 进程内执行的低级别操作。  
  
 使用 .NET Framework 3.5 或更早版本的 64 位进程不支持混合模式调试。  
  
## <a name="debug-a-64-bit-application"></a>调试 64 位应用程序  
 若要尝试调试 64 位应用程序：  
  
1. 创建一个 Visual Studio 解决方案，例如 C# 控制台应用程序。  
  
2. 使用配置管理器将配置设置为 64 位。 有关详细信息，请参阅[如何：将项目配置为面向平台](../ide/how-to-configure-projects-to-target-platforms.md)。  
  
3. 此时将启动 64 位版本的远程调试器 (msvsmon.exe)。 只要具有 64 位配置的解决方案处于启用状态，它就会运行。  
  
4. 开始调试。 此体验应该与调试 32 位配置的应用程序的体验相同。 如果出现错误，请参阅下面的“疑难解答”一节。  
  
## <a name="troubleshooting-64-bit-debugging"></a>64 位调试疑难解答  
 可能会出现一条错误信息：“64 位调试操作所花费的时间超出了预期。” 在这种情况下，则说明 Visual Studio 已向 64 位版本的 msvsmon.exe 发送请求，返回该请求的结果花费了较长的时间。  
  
 出现此错误的主要原因有两个：  
  
- 你的计算机上所安装的网络安全软件导致网络堆栈不可靠，并且该网络安全软件已删除通过 localhost 的数据包。 请尝试禁用全部的网络安全软件，然后查看该问题是否解决。 如果问题解决，那么请发送报告给你的网络安全软件供应商，说明该软件正在干扰 localhost 通信。  
  
- 遇到 Visual Studio 停止响应或其他性能问题的问题。 如果该问题定期发生，你可收集 Visual Studio (devenv.exe) 和辅助进程 (msvsmon.exe) 的转储并将其发送给 Microsoft。 
  
## <a name="see-also"></a>另请参阅  
 [64位应用程序](https://msdn.microsoft.com/library/fd4026bc-2c3d-4b27-86dc-ec5e96018181)   
 [配置适用于64位的程序](https://msdn.microsoft.com/library/cb99f72b-8c74-48f4-846a-8921b37b97e9)   
 [Visual Studio IDE 64 位支持](../ide/visual-studio-ide-64-bit-support.md)   
 [使用转储文件](../debugger/using-dump-files.md)   
 [远程调试](../debugger/remote-debugging.md)

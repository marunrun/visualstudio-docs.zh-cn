---
title: 如何：启动 Spy++ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Spy++, starting
ms.assetid: 1d36813a-dc2a-4fda-9b3d-a38928a62ced
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 36555d9b00c9aff3f594ae2217afe8434bb41542
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840696"
---
# <a name="how-to-start-spy"></a>如何：启动 Spy++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以从 Visual Studio 或在命令提示符处启动 Spy++。  
  
 当你启动 Spy + + 时，如果显示一条消息以请求对计算机进行更改，请单击 **"是"**。  
  
> [!NOTE]
> 只能运行 Spy++ 的一个实例。 如果尝试运行另一个实例，则只会导致当前正在运行的实例获得焦点。  
  
### <a name="to-start-spy-from-visual-studio"></a>从 Visual Studio 中启动 Spy + +  
  
- 在 " **工具** " 菜单上，单击 " **Spy + +**"。  
  
     由于 Spy + + 独立运行，因此在启动它后，可以关闭 Visual Studio。  
  
    > [!NOTE]
    > 使用 Spy++ 记录消息时，它可能会导致操作系统的执行速度变慢。  
  
### <a name="to-start-spy-at-a-command-prompt"></a>在命令提示符下启动 Spy + +  
  
1. 在命令提示符窗口中，将目录更改为包含 spyxx.exe 的文件夹。 通常，此文件夹的路径是。 \\*Visual Studio 安装文件夹*\Common7\Tools \\ 。  
  
2. 键入 **spyxx.exe** ，然后按 enter。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Spy + +](../debugger/using-spy-increment.md)   
 [Spy + + 视图](../debugger/spy-increment-views.md)   
 [Spy++ 参考](../debugger/spy-increment-reference.md)

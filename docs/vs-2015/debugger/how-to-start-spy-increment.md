---
title: 如何：启动 Spy + + |Microsoft Docs
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442753"
---
# <a name="how-to-start-spy"></a>如何：启动 Spy++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以启动 Spy + + 通过 Visual Studio 或命令提示符处。  
  
 当你启动 Spy + +，如果显示一条消息询问权限对计算机进行更改，请单击**是**。  
  
> [!NOTE]
> 可以运行 Spy + + 的一个实例。 如果你尝试运行另一个实例，它只会导致当前正在运行的实例，若要获取焦点。  
  
### <a name="to-start-spy-from-visual-studio"></a>若要从 Visual Studio 启动 Spy + +  
  
- 上**工具**菜单上，单击**Spy + +**。  
  
     因为 Spy + + 独立运行，在启动后，你可以关闭 Visual Studio。  
  
    > [!NOTE]
    > 当使用 Spy + + 中记录消息时，它可能会导致操作系统执行得更慢。  
  
### <a name="to-start-spy-at-a-command-prompt"></a>若要在命令提示符处启动 Spy + +  
  
1. 在命令提示符窗口中，将目录更改到包含 spyxx.exe 的文件夹。 通常情况下，此文件夹的路径是...\\ *Visual Studio 安装文件夹*\Common7\Tools\\。  
  
2. 类型**spyxx.exe** ，然后按 ENTER。  
  
## <a name="see-also"></a>请参阅  
 [使用 Spy++](../debugger/using-spy-increment.md)   
 [Spy++ 视图](../debugger/spy-increment-views.md)   
 [Spy++ 参考](../debugger/spy-increment-reference.md)

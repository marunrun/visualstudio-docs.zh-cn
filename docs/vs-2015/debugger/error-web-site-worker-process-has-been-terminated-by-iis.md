---
title: 错误：网站辅助进程已被 IIS 终止 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.web_server_process_terminated
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 5707b972-71a6-4cc6-ab99-c7c00ca8628c
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 787785909cd980176fd9220f58198ae6cc272ea8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68185465"
---
# <a name="error-web-site-worker-process-has-been-terminated-by-iis"></a>错误：网站工作进程已被 IIS 终止
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

调试器已停止对网站执行代码。 这导致 Internet Information Services (IIS) 认为辅助进程已停止响应。 因此，IIS 终止了辅助进程。  
  
 若要继续调试，必须配置 IIS 以使辅助进程继续运行。 在低于 IIS 7 的 IIS 版本中，不会显示此错误消息。  
  
### <a name="to-configure-iis-7-to-allow-the-worker-process-to-continue"></a>配置 IIS 7 以使辅助进程继续运行  
  
1. 打开“管理工具”窗口  。  
  
   1. 单击“开始”，然后选择“控制面板”   。  
  
   2. 在**控制面板**中，选择**切换到经典视图**（如有必要），然后双击**管理工具**。  
  
2. 在**管理工具**窗口中，双击**Internet Information Services (IIS) Manager**。  
  
    IIS 管理器随即打开。  
  
3. 在**连接**窗格中，展开\<计算机名称 > 节点（如有必要）。  
  
4. 在\<计算机名称 > 节点下，单击**应用程序池**。  
  
5. 在**应用程序池**列表中，右键单击你的应用程序运行所在的池的名称，然后单击**高级设置**。  
  
6. 在**高级设置**对话框中，找到**进程模型**部分，然后执行以下操作之一：  
  
   - 将“启用 Ping”设置为“False”   。  
  
   - 将“Ping 最大响应时间”设置为一个大于 90 秒的值  。  
  
     将“启用 Ping”设置为“False”可使 IIS 停止检查辅助进程是否仍在运行，并在停止被调试进程前让辅助进程一直运行   。 将“Ping 最大响应时间”设置为较大的值可使 IIS 继续监视辅助进程  。  
  
7. 单击“确定”，关闭“高级设置”对话框   。  
  
8. 关闭 IIS 管理器和“管理工具”窗口  。  
  
## <a name="see-also"></a>请参阅  
 [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)

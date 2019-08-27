---
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: 2e5782c49f26925d9eda81f04653b1a20666c6b1
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149182"
---
1. 在远程计算机上查找和启动**远程调试器**从**启动**菜单。 
   
   如果在远程计算机上没有管理权限，请右击**远程调试器**应用，然后选择**以管理员身份运行**。 否则，只是它正常启动。

   如果想要附加到正在运行以管理员身份，或不同的用户下运行的进程帐户 （如 IIS) 中，右键单击**远程调试器**应用，然后选择**以管理员身份运行**. 有关详细信息，请参阅[以管理员身份运行远程调试器](../remote-debugging-errors-and-troubleshooting.md#run-the-remote-debugger-as-an-administrator)。
   
1. 第一次启动远程调试器 （或之前已配置），**远程调试配置**对话框随即出现。  
  
    ![远程调试器配置](../media/remotedebuggerconfwizardpage.png "远程调试器配置")  
  
1. 如果 Windows Web 服务 API 未安装，这种情况发生，仅在 Windows Server 2008 R2 上，选择**安装**按钮。  
  
1. 选择你想要在使用远程工具的至少一个网络类型。 如果这些计算机通过域连接，则必须选择第一项。 如果这些计算机通过工作组或家庭组连接，选择相应的第二个或第三个项。  
  
1. 选择**配置远程调试**，配置防火墙并启动远程调试器。  
  
1. 配置完成后，**远程调试器**窗口会显示。
  
    ![远程调试器窗口](../media/remotedebuggerwindow.png "远程调试器窗口")
  
    远程调试器现在正在等待连接。 使用服务器名称和端口号显示在 Visual Studio 中设置的远程连接配置。  
  
若要停止远程调试器，请选择**文件** > **退出**。 您可以重新启动它从**启动**菜单中，或从命令行：  
  
```cmd
<Remote debugger installation directory>\msvsmon.exe
```

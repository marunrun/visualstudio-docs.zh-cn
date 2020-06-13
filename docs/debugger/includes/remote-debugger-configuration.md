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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149182"
---
1. 在远程计算机上，从“开始”菜单中查找并启动“远程调试器” 。 
   
   如果你没有远程计算机的管理权限，请右键单击“远程调试器”应用，然后选择“以管理员身份运行” 。 否则，正常启动即可。

   如果打算附加到以管理员身份运行或在其他用户帐户（如 IIS）下运行的进程，请右键单击“远程调试器”应用，然后选择“以管理员身份运行” 。 有关详细信息，请参阅[以管理员身份运行远程调试器](../remote-debugging-errors-and-troubleshooting.md#run-the-remote-debugger-as-an-administrator)。
   
1. 当第一次（或在配置它之前）启动远程调试器时，将显示“远程调试配置”对话框。  
  
    ![远程调试器配置](../media/remotedebuggerconfwizardpage.png "远程调试器配置")  
  
1. 如果未安装 Windows Web 服务 API（仅会在 Windows Server 2008 R2 上发生这种情况），请选择“安装”按钮。  
  
1. 请至少选择一种要对其使用远程工具的网络类型。 如果这些计算机通过域连接，则必须选择第一项。 如果这些计算机通过工作组或家庭组连接，请根据需要选择第二或第三项。  
  
1. 选择“配置远程调试”，配置防火墙并启动远程调试器。  
  
1. 配置完成后，将显示“远程调试器”窗口。
  
    ![远程调试器窗口](../media/remotedebuggerwindow.png "远程调试器窗口")
  
    远程调试器正在等待连接。 使用显示的服务器名称和端口号在 Visual Studio 中设置远程连接配置。  
  
若要停止远程调试器，请选择“文件” > “退出” 。 你可以从“开始”菜单或通过以下命令行重新启动它：  
  
```cmd
<Remote debugger installation directory>\msvsmon.exe
```

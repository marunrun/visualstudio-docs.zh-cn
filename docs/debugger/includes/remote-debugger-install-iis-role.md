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
ms.openlocfilehash: 13ca035b01ec8af1277d70b3c792293a1af4687a
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149229"
---
以下步骤仅显示 IIS 的基本配置。 有关更深入的信息或要安装到 Windows 桌面计算机，请参阅[发布到 IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration) 或[使用 ASP.NET 3.5 和 ASP.NET 4.5 的 IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)。

对于 Windows Server 操作系统，通过“管理”链接或“服务器管理器”中的“仪表板”链接使用“添加角色和功能”向导     。 在“服务器角色”步骤中，选中“Web 服务器(IIS)”框   。

![在选择服务器角色步骤中选择了“Web 服务器 IIS”角色。](../media/remotedbg-server-roles-ws2012.png)

在“角色服务”步骤中，选择所需 IIS 角色服务，或接受提供的默认角色服务  。 如果要使用发布设置和 Web 部署启用部署，请确保选中“IIS 管理脚本和工具”  。

继续执行确认步骤，安装 Web 服务器角色和服务。 安装 Web 服务器 (IIS) 角色后无需重启服务器/IIS。
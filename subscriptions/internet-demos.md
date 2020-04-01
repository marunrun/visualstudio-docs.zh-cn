---
title: 使用产品密钥通过终端服务支持 Internet 演示 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 1c5ede60-cb5a-4d5f-a6a2-a1f536f6c4ad
ms.date: 03/09/2020
ms.topic: conceptual
description: 了解如何使用产品密钥通过终端服务支持 Internet 演示并启用 RDS 访问
ms.openlocfilehash: 2d5f23f0d161ee9f50569e0ff7f8ce585c8c49ff
ms.sourcegitcommit: eeff6f675e7850e718911647343c5df642063d5e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2020
ms.locfileid: "80232431"
---
# <a name="internet-demonstrations-via-terminal-services"></a>通过终端服务访问 Internet 演示
凭借 Visual Studio 订阅，可允许最终用户使用终端服务（Windows Server 2003 或 Windows Server 2008）或远程桌面服务（Windows Server 2008 R2 或更高版本）访问你的程序的 Internet 演示。 使用这种方式，多达 200 位匿名用户可同时访问你的演示。 你的演示不得使用生产数据。 Visual Studio 订阅者可以向最终用户演示其应用程序。 在软件是通过 Visual Studio 订阅授权的情况下，未购买 Visual Studio 订阅的最终用户只能通过使用终端服务 (TS) 或远程桌面服务 (RDS) 的此 Internet 与演示应用程序交互。

除了开发/测试权限，Visual Studio 订阅者可以根据需要使用许多 RDS 或 TS 连接。

## <a name="enabling-rds-access"></a>启用 RDS 访问
Visual Studio 订阅者可以输入[订阅门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)的“[产品密钥](https://my.visualstudio.com/productkeys?wt.mc_id=o~msft~docs)”选项卡中的产品密钥，增加可通过 RDS 访问 Windows Server 的用户数量。 若要获得产品密钥，请连接到“产品密钥”页，然后向下滚动到正在运行的 Windows Server 版本。 找到“Windows Server <版本> R2 远程桌面服务 <用户或设备> 连接”，然后单击“索取密钥”链接  。 例如，如果是在 Windows Server 2012 R2 上使用 RDS，且部署使用用户 CAL，请选择“Windows Server 2012 远程桌面服务用户连接(50)”。
每种类型的 5 个密钥都支持 Windows Server 2008 R2，每个密钥支持 20 个连接。 对于 Windows Server 2012 R2，每种类型提供 4 个密钥，每个密钥支持 50 个连接。

## <a name="to-enable-additional-connections-in-windows-server"></a>在 Windows Server 中启用其他连接：
1. 打开服务器管理器。
2. 打开左侧导航窗格中的“服务器”列表。
3. 右键单击你的许可证服务器，然后选择“安装许可证”。
4. 完成向导中的步骤。  如果选择的是协议类型，请选择“许可证包(零售购买)”，然后输入从我的门户获得的产品密钥。

如果满足以下条件，最终用户可以通过 RDS 进行连接以访问应用程序：
- 用户必须为匿名（处于未经身份验证状态）。
- 必须使用 Internet 连接。
- 若要进行应用程序演示，最多可以使用 200 个并发用户连接。
- Visual Studio 订阅者必须获得启用用户连接所需的产品密钥。

## <a name="see-also"></a>请参阅
- [Windows Server 文档](https://docs.microsoft.com/windows-server/)
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
如果需要有关部署 RDS 的指南，请查看位于 https://techcommunity.microsoft.com/t5/Ask-The-Performance-Team/bg-p/AskPerf 的远程桌面服务 (RDS) 2012 会话部署的多部分博客系列  。 

如果存在任何疑问，请访问 [Microsoft 远程桌面服务论坛](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverTS)。

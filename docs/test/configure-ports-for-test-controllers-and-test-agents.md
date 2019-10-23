---
title: 为测试控制器和测试代理配置端口
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- firewalls, configuring for test agents
- firewalls, configuring for test controllers
- test agents, firewalls
- test controllers, firewalls
- agents, firewalls
- controllers, firewalls
ms.assetid: 211edbd7-9fe4-4251-ba85-8bec4363261b
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f29edf1582b709931e393faa0de5a1542a0ee662
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665190"
---
# <a name="configure-ports-for-test-controllers-and-test-agents"></a>为测试控制器和测试代理配置端口

可以更改测试控制器、测试代理和客户端使用的默认传入端口。 这在您尝试将测试控制器、测试代理或客户端与其他一些软件（这些软件与端口设置发生冲突）一起使用时可能会很有用。 更改端口的另一个原因是，测试控制器和客户端之间的防火墙限制。 在此情况下，您可能需要手动配置端口以便为防火墙启用它，这样测试控制器便能向客户端发送结果。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

下图演示测试控制器、测试代理和客户端之间的连接点。 它概述了用于传入和传出连接的端口以及在这些端口上使用的安全限制。

![测试控制器和测试代理的端口和安全性](../test/media/test-controller-agent-firewall.png)

## <a name="incoming-connections"></a>传入连接

测试控制器使用的默认端口为 6901，而测试代理的默认端口为 6910。 默认情况下，客户端将使用一个随机端口，该端口用于接收来自测试控制器的测试结果。 对于所有传入连接，测试控制器会对调用方进行身份验证，并验证它是否属于特定安全组。

- **测试控制器** 传入连接位于 TCP 端口 6901。 如果需要，您可以配置传入端口。 有关详细信息，请参阅[配置传入端口](#configure-the-incoming-ports)。

    测试控制器需要能够建立与测试代理和客户端的传出连接。

    > [!NOTE]
    > 测试控制器需要打开传入“文件和打印机共享”连接  。

- **测试代理** 传入连接位于 TCP 端口 6910 上。 如果需要，您可以配置传入端口。 有关详细信息，请参阅[配置传入端口](#configure-the-incoming-ports)。

   测试代理需要能够建立与测试控制器的传出连接。

- **客户端** 默认情况下，随机 TCP 端口用于传入连接。 如果需要，您可以配置传入端口。 有关详细信息，请参阅[配置传入端口](#configure-the-incoming-ports)。

   当测试控制器首次尝试连接到客户端时，您可能会收到防火墙通知。

   Windows Server 2008 默认禁用防火墙通知，必须为客户端程序（devenv.exe  、mstest.exe  、mlm.exe  ）手动添加防火墙例外，这样它才能接受传入连接。

## <a name="outgoing-connections"></a>传出连接

随机 TCP 端口用于所有传出连接。

- **测试控制器** 测试控制器需要能够建立与代理和客户端的传出连接。

- **测试代理** 测试代理需要能够建立与控制器的传出连接。

- **客户端** 客户端需要能够建立与控制器的传出连接。

## <a name="configure-the-incoming-ports"></a>配置传入端口

按照以下指示配置测试控制器和测试代理的端口。

- **控制器服务**：通过编辑 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\QTCcontroller.exe.config  文件来修改端口值：

    ```xml
    <appSettings>
      <add key="ControllerServicePort" value="6901"/>
    </appSettings>
    ```

- **代理服务**：通过编辑 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\QTAgentService.exe.config  文件来修改端口：

    ```xml
    <appSettings>
      <add key="AgentServicePort" value="6910"/>
    </appSettings>
    ```

- **客户端**：使用注册表编辑器来添加以下注册表 (DWORD  ) 值。 客户端将使用指定范围内的某个端口来接收来自测试控制器的数据：

     **HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\VisualStudio\12.0\EnterpriseTools\QualityTools\ListenPortRange\PortRangeStart**

     **HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\VisualStudio\12.0\EnterpriseTools\QualityTools\ListenPortRange\PortRangeEnd**

## <a name="see-also"></a>请参阅

- [安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)
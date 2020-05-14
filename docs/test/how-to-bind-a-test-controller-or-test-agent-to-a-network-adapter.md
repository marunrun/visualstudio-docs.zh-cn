---
title: 将测试控制器或测试代理绑定到网络适配器
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- controllers, netwrok adapter
- agents, configuring
- agents, network adapter
- controllers, configuring
ms.assetid: 7eb9290a-f9f6-4e41-9caa-796fcfaf0610
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6383d7a16839ba8934bb7f91664379e99da17a36
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75594781"
---
# <a name="how-to-bind-a-test-controller-or-test-agent-to-a-network-adapter"></a>如何：将测试控制器或测试代理绑定到网络适配器

如果安装有测试控制器或测试代理软件的计算机上有多个网络适配器，则必须指定计算机的 IP 地址而不是名称来标识该测试控制器或测试代理。

> [!WARNING]
> 尝试设置测试代理时，可能会收到以下错误：
>
> **错误 8110。无法连接到指定的控制器计算机或访问控制器对象**
>
> 在包含多个网络适配器的计算机上安装测试控制器可引起此错误。 还是可以成功安装代理，并且在尝试运行测试之前不会出现此问题。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="bind-a-test-controller-to-a-specific-network-adapter"></a>将测试控制器绑定到特定网络适配器

### <a name="to-obtain-the-ip-addresses-of-the-network-adapters"></a>获取网络适配器的 IP 地址

1. 在 Microsoft Windows 中，选择“开始”，在“开始搜索”框中选择，键入 cmd，然后选择“输入”。    

2. 键入 ipconfig /all。 

     将显示网络适配器的 IP 地址。 记录要将控制器绑定到的网络适配器的 IP 地址。

### <a name="to-bind-a-network-adapter-to-a-test-controller"></a>将网络适配器绑定到测试控制器

1. 在 Microsoft Windows 中，选择“开始”，在“开始搜索”框中选择，键入 services.msc，然后选择“输入”。    

     将显示“服务”对话框。 

2. 在结果窗格中的“名称”列中，右键单击“Visual Studio Test Controller”服务，然后选择“停止”。   

     \- 或 -

     使用提升的权限打开命令提示符，并在命令行执行以下命令：

     `net stop vsttcontroller`

3. 打开位于 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\\\<edition>\Common7\IDE 中的 QTCcontroller.exe.config XML 配置文件   。

4. 找到 `<appSettings>` 标记。

    ```xml
    <appSettings>
      <add key="LogSizeLimitInMegs" value="20"/>
      <add key="AgentConnectionTimeoutInSeconds" value="120"/>
      <add key="AgentSyncTimeoutInSeconds" value="300"/>
      <add key="ControllerServicePort" value="6901"/>
      <add key="ControllerUsersGroup" value="TeamTestControllerUsers"/>
      <add key="ControllerAdminsGroup" value="TeamTestControllerAdmins"/>
      <add key="CreateTraceListener" value="no"/>
    </appSettings>
    ```

5. 添加 `BindTo` 键以指定要在 `<appSettings>` 节中使用的网络适配器。

    ```xml
            <add key="BindTo" value="<YOUR IP ADDRESS>"/>
    </appSettings>
    ```

6. 启动测试控制器服务。 为此，请在命令提示符处运行以下命令：

    `net start vsttcontroller`

    > [!WARNING]
    > 若要将测试代理连接到控制器，必须再次运行测试代理安装。 这时，需指定控制器的 IP 地址，而不是指定控制器名称。

     这适用于控制器、代理服务和代理进程。 对于每个在包含多个网络适配器的计算机上运行的进程，都必须设置 `BindTo` 属性。 对于所有三个进程，设置 `BindTo` 属性的过程是相同的，如本主题前面有关测试控制器的内容所述。

### <a name="to-bind-a-network-interface-card-to-a-test-agent"></a>将网络接口卡绑定到测试代理

1. 在 Microsoft Windows 中，选择“开始”，在“开始搜索”框中选择，键入 services.msc，然后选择“输入”。    

    将显示“服务”对话框。 

2. 在结果窗格中的“名称”列中，右键单击“Visual Studio Test Agent”服务，然后选择“停止”。   

     \- 或 -

     使用提升的权限打开命令提示符，并在命令行执行以下命令：

     net stop vsttagent 

3. 打开位于 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\\\<edition>\Common7\IDE 中的 QTAgentService.exe.config XML 配置文件   。

4. 找到 `<appSettings>` 标记。

    ```xml
    <appSettings>
      <appSettings>
      <add key="LogSizeLimitInMegs" value="20"/>
      <add key="AgentServicePort" value="6910"/>
      <add key="ControllerConnectionPeriodInSeconds" value="30"/>
      <add key="StopTestRunCallTimeoutInSeconds" value="120"/>
      <add key="CreateTraceListener" value="no"/>
      <add key="GetCollectorDataTimeout" value="300"/>
    </appSettings>  </appSettings>
    ```

5. 添加 `BindTo` 键以指定要在 `<appSettings>` 节中使用的网络适配器。

    ```xml
            <add key="BindTo" value="<YOUR IP ADDRESS>"/>
    </appSettings>
    ```

6. 启动测试代理服务。 为此，请在命令提示符处运行以下命令：

    `net start vsttagent`

## <a name="see-also"></a>请参阅

- [安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)
- [修改负载测试记录设置](../test/modify-load-test-logging-settings.md)
- [为测试控制器和测试代理配置端口](../test/configure-ports-for-test-controllers-and-test-agents.md)
- [如何：为测试控制器和测试代理指定超时周期](../test/how-to-specify-timeout-periods-for-test-controllers-and-test-agents.md)

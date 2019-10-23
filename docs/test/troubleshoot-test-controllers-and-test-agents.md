---
title: 测试控制器和测试代理的故障排除
ms.date: 10/20/2016
ms.topic: troubleshooting
helpviewer_keywords:
- load tests, test controllers
- load tests, troubleshooting
- load tests, test agents
- troubleshooting, test controllers and agents in load tests
ms.assetid: 77329348-3a5d-43de-b6cb-90f93296a081
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 716bc28626e6b408fd618a8ed6c623c5118d7782
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659912"
---
# <a name="strategies-for-troubleshooting-test-controllers-and-test-agents-in-load-tests"></a>负载测试中测试控制器和测试代理的故障排除策略

本文介绍在 Visual Studio 中使用测试控制器和测试代理时可能遇到的一些常见问题。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="unable-to-collect-performance-counters-on-test-agent-computer"></a>无法在测试代理计算机上收集性能计数器

运行负载测试时，如果尝试连接到测试代理计算机并收集性能计数器，则可能会收到错误。 远程注册表服务是负责为远程计算机提供性能计数器数据的服务。 远程注册表服务在某些操作系统上不会自动启动。 若要解决此问题，请手动启动远程注册表服务。

> [!NOTE]
> 可以在“控制面板”访问远程注册表服务  。 选择“管理工具”，然后选择“服务”   。

导致此问题的另一个原因是没有足够的读取性能计数器权限。 对于本地测试运行，运行测试的用户的帐户必须是 Power Users 组（或更高）或 Performance Monitor Users 组的成员。 对于远程测试运行，配置控制器运行时所用的帐户必须是 Power Users 组（或更高）或 Performance Monitor Users 组的成员。

## <a name="set-the-logging-level-on-a-test-controller-computer"></a>设置测试控制器计算机上的日志记录级别

可以控制测试控制器计算机上的日志记录级别。 当你尝试诊断在某个环境上运行负载测试所出现的问题时，这很有用。

### <a name="to-set-the-logging-level-on-a-test-controller-computer"></a>设置测试控制器计算机上的日志记录级别

1. 停止测试控制器服务。 在命令提示符处键入 `net stop vsttcontroller`。

2. 打开 QTController.exe.config 文件  。此文件位于控制器安装目录中。

3. 在该文件的系统诊断部分中编辑 `EqtTraceLevel` 开关的项。 你的代码应该与下面的内容类似：

    ```xml
    <system.diagnostics>
        <trace autoflush="true" indentsize="4">
            <listeners>
                <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="d:\VSTestHost.log" />
            </listeners>
        </trace>
        <switches>
            <!-- You must use integral values for "value":
                    0 = off,
                    1 = error,
                    2 = warn,
                    3 = info,
                    4 = verbose. -->
            <add name="EqtTraceLevel" value="4" />
        </switches>
    </system.diagnostics>
    ```

4. 保存该文件。

5. 启动控制器服务。 在命令提示符处键入 `net start vsttcontroller`。

这适用于测试控制器、测试代理服务和测试代理进程。 诊断问题时，对所有三个进程都启用日志记录很有用。 对于所有三个进程，设置日志记录级别的过程是相同的，同上面对测试控制器所指定的过程。 若要设置测试代理服务和代理进程的日志记录级别，请使用以下配置文件：

- QTController.exe.config 控制器服务 

- QTAgentService.exe.config 代理服务 

- 用于 32 位体系结构的 QTDCAgent(32).exe.config 代理数据适配器进程  。

- 用于 64 位体系结构的 QTDCAgent(64).exe.config 代理数据适配器进程  。

- 用于 32 位体系结构的 QTAgent(32).exe.config 代理测试进程  。

- 用于 64 位体系结构的 QTAgent(64).exe.config 代理测试进程  。

## <a name="bind-a-test-controller-to-a-network-adapter"></a>将测试控制器绑定到网络适配器

尝试设置测试代理时，可能会收到以下错误：

**错误 8110。无法连接到指定的控制器计算机或访问控制器对象。**

在包含多个网络适配器的计算机上安装测试控制器可引起此错误。

> [!NOTE]
> 成功安装测试代理还是可能的，并且在尝试运行测试之前不会出现此问题。

若要修复此错误，必须将测试控制器绑定到其中一个网络适配器。 必须对测试控制器设置 `BindTo` 属性，然后将测试代理改为通过 IP 地址（而不是通过名称）来引用该测试控制器。 下面的过程中提供了步骤。

### <a name="to-obtain-the-ip-address-of-the-network-adapter"></a>获取网络适配器的 IP 地址

1. 选择“开始”  ，然后选择“运行”  。

     将显示“运行”对话框  。

2. 键入 `cmd`，然后选择“确定”  。

     命令提示将打开。

3. 键入 `ipconfig /all`。

     将显示网络适配器的 IP 地址。 记录要将控制器绑定到的网络适配器的 IP 地址。

### <a name="to-bind-a-test-controller-to-a-network-adapter"></a>将测试控制器绑定到网络适配器

1. 停止测试控制器服务。 在命令提示符处键入 `net stop vsttcontroller`。

2. 打开 QTController.exe.config 文件  。此文件位于 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE 中  。

3. 将 `BindTo` 属性的项添加到应用程序设置中。 指定要将控制器绑定到的网络适配器的 IP 地址。 你的代码应该与下面的内容类似：

    ```xml
    <appSettings>
        <add key="LogSizeLimitInMegs" value="20" />
        <add key="AgentSyncTimeoutInSeconds" value="120" />
        <add key="ControllerServicePort" value="6901" />
        <add key="ControllerUsersGroup" value="TeamTestControllerUsers" />
        <add key="ControllerAdminsGroup" value="TeamTestControllerAdmins" />
        <add key="CreateTraceListener" value="no" />
        <add key="BindTo" value="<YOUR IP ADDRESS>" />
    </appSettings>
    ```

4. 保存该文件。

5. 启动测试控制器服务。 在命令提示符处键入 `net start vsttcontroller`。

### <a name="to-connect-a-test-agent-to-a-bound-controller"></a>将测试代理连接到绑定的控制器

- 再次运行测试代理安装。 这一次，指定测试控制器的 IP 地址，而不是指定测试控制器的名称。

这适用于测试控制器、测试代理服务和测试代理进程。 对于每个在包含多个网络适配器的计算机上运行的进程，都必须设置 `BindTo` 属性。 对于所有三个进程，设置 `BindTo` 属性的过程是相同的，同上面对测试控制器所指定的过程。 要设置测试代理服务和测试代理进程的日志记录级别，请使用[设置测试控制器计算机上日志记录级别](#set-the-logging-level-on-a-test-controller-computer)中列出的配置文件。

## <a name="see-also"></a>请参阅

- [测试控制器和测试代理](../test/configure-test-agents-and-controllers-for-load-tests.md)

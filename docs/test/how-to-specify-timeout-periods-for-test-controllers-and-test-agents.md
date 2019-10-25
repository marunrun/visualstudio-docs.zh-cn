---
title: 测试控制器和测试代理的超时周期
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- agents, configuring
- agetns, timeouts
- controllers, configuring
- controllers, timeouts
ms.assetid: 777d0db5-0073-458a-a2a3-58b1c1f24c60
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2f4e82261b9b36ced471dfa3e93be085e22c4d64
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653326"
---
# <a name="how-to-specify-timeout-periods-for-test-controllers-and-test-agents"></a>如何：为测试控制器和测试代理指定超时周期

测试控制器和测试代理都有多个超时设置，可以指定失败并显示错误之前等待彼此或数据源响应的时间。 在某些情况下，可能需要编辑超时值以满足拓扑需要或其他环境问题的需要。 若要编辑超时值，请按照下面过程中的说明来编辑与测试控制器或测试代理关联的 XML 配置文件。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

若要编辑测试控制器或测试代理的各种超时设置，请使用表中的键名和值来修改以下配置文件：

- 测试控制器：*QTController.exe.config*

    |项名称|说明|值|
    |-|-----------------|-|
    |AgentConnectionTimeoutInSeconds|认为连接丢失前等待代理 ping 请求的秒数。|“n”秒。|
    |AgentSyncTimeoutInSeconds|开始同步测试运行时，中止运行前等待所有代理同步的秒数。|“n”秒。|
    |AgentInitializeTimeout|中止测试运行前，在测试运行开始时等待所有代理及其数据收集器进行初始化的秒数。 如果使用数据收集器，则此值应相当大。|“n”秒。 默认：“120”（2 分钟）。|
    |AgentCleanupTimeout|完成测试运行前，等待所有代理及其数据收集器进行清理的秒数。 如果使用数据收集器，则此值应相当大。|“n”秒。 默认：“120”（2 分钟）。|

- 测试代理：*QTAgentService.exe.config*

    |项名称|说明|值|
    |-|-----------------|-|
    |ControllerConnectionPeriodInSeconds|连接控制器尝试之间的秒数。|“n”秒。 默认：“30”（三十秒）。|
    |RemotingTimeoutSeconds|远程处理调用可以持续的最长时间（以秒为单位）。|“n”秒。 默认：“600”（10 分钟）。|
    |StopTestRunCallTimeoutInSeconds|等待用于停止测试运行的调用的秒数。|“n”秒。 默认：“120”（2 分钟）。|
    |GetCollectorDataTimeout|等待数据收集器的秒数。|“n”秒。 默认：“300”（5 分钟）。|

## <a name="to-specify-agent-timeout-options-for-a-test-controller"></a>指定测试控制器的代理超时选项

1. 打开位于 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE 中的 QTCcontroller.exe.config XML 配置文件   。

2. 找到 `<appSettings>` 标记。

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

3. 编辑测试控制器的一个超时键的现有值。 例如，可以将键 `AgentConnectionTimeoutInSeconds` 的默认值从两分钟更改为三分钟：

    ```xml
    <add key="AgentConnectionTimeoutInSeconds" value="180"/>
    ```

    -或-

    添加其他键并指定超时值。 例如，可以在 `AgentInitializeTimeout` 节中添加 `<appSettings>` 键并指定五分钟的值：

    ```xml
    <appSettings>
            <add key="AgentInitializeTimeout" value="300"/>
    </appSettings>
    ```

## <a name="to-specify-agent-timeout-options-for-a-test-agent"></a>指定测试控代理的代理超时选项

1. 打开位于 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE 中的 QTAgentService.exe.config XML 配置文件   。

2. 找到 `<appSettings>` 标记。

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

3. 编辑测试代理的一个超时键的现有值。 例如，可以将键 `ControllerConnectionPeriodInSeconds` 的默认值从三十秒更改为一分钟：

    ```xml
    <add key="ControllerConnectionPeriodInSeconds" value="60"/>
    ```

    -或-

    添加其他键并指定超时值。 例如，可以在 `RemotingTimeoutSeconds` 节中添加 `<appSettings>` 键并指定十五分钟的值：

    ```xml
    <appSettings>
            <add key=" RemotingTimeoutSeconds " value="900"/>
    </appSettings>
    ```

## <a name="see-also"></a>请参阅

- [安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)
- [修改负载测试记录设置](../test/modify-load-test-logging-settings.md)
- [为测试控制器和测试代理配置端口](../test/configure-ports-for-test-controllers-and-test-agents.md)
- [如何：将测试控制器或测试代理绑定到网络适配器](../test/how-to-bind-a-test-controller-or-test-agent-to-a-network-adapter.md)
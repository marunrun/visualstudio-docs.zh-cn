---
title: 向负载测试运行设置中添加上下文参数
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, run settings, context parameters
- load tests, context parameters
ms.assetid: a8a0b97e-8040-4711-85ab-36548b130ed2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 10a410b18391b3fbaee98f10be56cdc70c0f3562
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288411"
---
# <a name="how-to-add-context-parameters-to-a-load-test-run-setting"></a>如何：向负载测试运行设置中添加上下文参数

在使用“新建负载测试向导”创建负载测试后，可以使用“负载测试编辑器”更改方案属性，以满足你的测试需求和目标。  

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> 有关运行设置属性及其说明的完整列表，请参阅[负载测试运行设置属性](../test/load-test-run-settings-properties.md)。

可以使用负载测试编辑器创建要在负载测试运行设置中使用的上下文参数。 上下文参数允许你将字符串参数化。

假定负载测试包含的 Web 性能测试已经通过上下文参数使用参数化的 Web 服务器 URL。 你可以将上下文参数添加到负载测试运行设置，该参数与在 Web 性能测试中使用的上下文参数使用相同名称值。 这将在运行负载测试时将 Web 性能测试映射到其他服务器。 例如，如果负载测试包含的 Web 性能测试对 URL 中的 Web 服务器名称使用名为 WebServer1 的上下文参数。 如果然后在负载测试运行设置中指定也名为 WebServer1 的上下文参数，则负载测试将使用在负载测试运行设置中指定的上下文参数。 为了不产生混淆，如果负载测试中的 Web 性能测试使用与负载测试中的上下文参数相同的上下文参数名称，则负载测试中的上下文参数将覆盖在 Web 性能测试中使用的上下文参数。

> [!WARNING]
> 在运行设置中使用上下文参数时，注意不要意外重写 Web 性能测试的上下文参数。 避免使用相同的上下文参数名称，除非有意这样做。

如果将 Webserver1 上下文参数的值分配给 `http://CorporateStagingWebServer`，则可以在负载测试中使用 `WebServer1`，因此可以随时轻松地将值更改为其他 Web 服务器。

此外，通过在不同的负载测试运行设置中使用相同的名称对一个上下文参数分配不同的值，可以使用不同的环境运行负载测试：

- 公司临时 Web 服务器运行设置：名为 `WebServer1=http://CorporateStagingWebServer` 的上下文参数

- 公司生产 Web 服务器运行设置：名为 `WebServer1=http://CorporateProductionWebServer` 的上下文参数

  **从命令行更改运行设置**

  如果要从命令行使用不同的运行设置来利用上下文参数策略，请使用以下命令：

  **设置 Test.UseRunSetting= CorporateStagingWebServer**

  －和－

  **mstest /testcontainer:loadtest1.loadtest**

## <a name="to-add-a-context-parameter-to-a-run-setting"></a>向运行设置中添加上下文参数

1. 打开一个负载测试。

2. 在负载测试编辑器中，展开负载测试树中的“运行设置”文件夹  。

3. 右键单击要在其中添加上下文参数的特定运行设置，然后选择“添加上下文参数”  。

     一个新上下文参数将添加到负载测试树中“运行设置”文件夹的“上下文参数”文件夹   。

     或

     如果运行设置已经包含“上下文参数”文件夹，则可以右键单击该文件夹，然后选择“添加上下文参数”   。

4. 在“属性”窗口中，根据需要更改“名称”的值（例如，WebServer1）   。 在“属性”窗口中，将“值”更改为要使用的参数（例如 `http://CorporateStagingWebServer`）。

5. （可选）重复步骤 3 至 5，并对“值”属性使用其他字符串（例如 `http://CorporateProductionWebServer`）。

6. 选择你希望哪些运行设置处于活动状态。 打开运行设置上的快捷菜单并选择“设置为活动的”  。

## <a name="see-also"></a>另请参阅

- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)

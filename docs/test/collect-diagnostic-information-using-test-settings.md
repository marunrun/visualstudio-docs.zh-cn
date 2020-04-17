---
title: 使用测试设置收集诊断信息
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, configuring run settings
ms.assetid: 0c86918b-cd63-4468-8f49-6d547a1276dc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2e853e0ec54179178eba0f1566c34d7cfd63cee5
ms.sourcegitcommit: 5d1b2895d3a249c6bea30eb12b0ad7c0f0862d85
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80880281"
---
# <a name="collect-diagnostic-information-using-test-settings"></a>使用测试设置收集诊断信息

在运行测试时，可使用 Visual Studio 中的测试设置来收集额外的数据  。 例如，你可能想在运行测试时录制视频。 可通过诊断数据适配器执行以下操作：

- 以文本格式收集每个 UI 操作步骤

- 记录每个 UI 操作以便播放

- 收集系统信息

- 收集事件日志数据

- 收集 IntelliTrace 数据来帮助隔离不可重现的 Bug

诊断数据适配器还可用于更改测试计算机的行为。 例如，利用 Visual Studio 中的测试设置，可以模拟各种网络拓扑瓶颈以评估团队应用程序的性能。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="use-test-settings-with-visual-studio"></a>通过 Visual Studio 使用测试设置

若要使用 Visual Studio 运行单元测试、编码的 UI 测试、Web 性能测试或负载测试，可以添加、配置和选择在运行测试时要使用的测试设置。 若要远程运行测试、收集数据或影响测试计算机，则必须指定要在测试设置中使用的测试控制器。 测试控制器拥有可用于测试设置中的每个角色的代理。

## <a name="diagnostic-data-adapter-details"></a>诊断数据适配器详细信息

下表概述了将诊断数据适配器配置为用于本地或远程计算机角色的各种方法。

|测试设置中使用的诊断数据适配器|本地计算机上的手动测试|自动测试|手动测试：使用角色集和环境收集数据|说明|
|-|-|-|-|-|
|**用于 IntelliTrace 和测试影响的 ASP.NET 客户端代理：** 通过此代理可收集有关从客户端到 IntelliTrace 和 Test Impact 诊断数据适配器的 Web 服务器的 http 调用的信息。|是|是|是|-   只有在为客户端角色选择了 IntelliTrace 或测试影响诊断数据适配器的情况下，才使用此设置。|
|**ASP.NET 探查器：** 可以创建包含 ASP.NET 分析的测试设置，该分析收集 ASP.NET Web 应用程序的性能数据。|否|是（请参见“注释”）|否|-   仅当在 Visual Studio 中运行负载测试时，才支持诊断数据适配器。|
|**代码覆盖率：** 可以创建包含代码覆盖率信息的测试设置，该信息用于调查测试覆盖的代码范围。|否|是（请参见“注释”）|否|-   仅当在运行自动测试的计算机上通过 Visual Studio 或 mstest.exe 运行该测试时，才能使用代码覆盖率  。 不支持远程收集。<br />-   如果还将测试设置配置为收集 IntelliTrace 信息，则收集代码覆盖率数据不起作用。 **注意：** 此诊断数据适配器仅适用于 Visual Studio 测试设置。 不适用于 Microsoft 测试管理器（在 Visual Studio 2017 中已弃用）中的测试设置。 此外，此适配器用于与 Visual Studio 2010 测试项目的兼容性。 **注意：** 为了实现兼容，当自动测试从 Microsoft 测试管理器运行或在 Visual Studio 中的远程测试代理（使用旧的 MSTest 运行程序）上运行时，将应用代码覆盖率。|
|**事件日志：** 可以将测试设置配置为包含事件日志收集，该事件日志包含在测试结果中。|是|是|是||
|**IntelliTrace：** 可以为 IntelliTrace配置诊断数据适配器，使其收集特定诊断跟踪信息，从而帮助隔离难以重现的 Bug  。 这将创建包含此信息的 IntelliTrace 文件。 IntelliTrace 文件的扩展名为 .iTrace  。 测试失败时，可以创建 Bug。 随测试结果一起保存的 IntelliTrace 文件会自动链接到此 Bug。 IntelliTrace 文件中收集的数据可减少重现和诊断代码中的错误所需的时间，从而提高调试效率。 可以基于此 IntelliTrace 文件在另一台计算机上模拟本地会话。 这会降低无法重现 Bug 的风险。|是|是|是|-   如果启用收集 IntelliTrace 数据，则收集代码覆盖率数据不起作用。<br />-   如果将 IntelliTrace 用于 Web 客户端角色，还必须选择用于 IntelliTrace 和测试影响诊断数据适配器的 ASP.NET 客户端代理。<br />-   仅支持以下版本的 IIS：IIS 7.0、IIS 7.5 和 IIS 8.0。|
|**网络仿真：** 可以使用测试设置指定你希望在测试中放置的人工网络负载。 网络仿真将仿真特定网络连接（如拨号连接）的速度，从而影响计算机的往来通信。 |否|是（请参见“注释”）|否|可将网络仿真诊断数据适配器用于客户端或服务器角色。 不必对彼此通信的这两个角色都使用适配器。 **注意：** 此诊断数据适配器仅适用于 Visual Studio 测试设置。 不适用于 Microsoft 测试管理器（在 Visual Studio 2017 中已弃用）中的测试设置。 **注意：** 网络仿真不能用于提高网络连接速度。 **警告：** 如果测试设置中包括网络仿真诊断数据适配器并且打算在本地计算机中使用它，那么还必须将网络仿真驱动程序绑定到计算机的网络适配器之一。 必须具有网络仿真驱动程序，网络仿真诊断数据适配器才能起作用。 网络仿真驱动程序以两种方式安装和绑定到适配器： <ul><li>**与 Microsoft Visual Studio 测试代理一起安装的网络仿真驱动程序：** Visual Studio 测试代理可用于远程计算机和本地计算机。 安装 Visual Studio Test Agent 时，安装过程包含一个将网络仿真驱动程序绑定到网卡的配置步骤。 有关详细信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。</li><li>**与 Microsoft Visual Studio Test Professional 一起安装的网络仿真驱动程序：** 第一次使用网络仿真时，系统会提示将网络仿真驱动程序绑定到网卡上。</li></ul> 也可以使用以下命令在不安装 Visual Studio 测试代理的情况下从本地计算机上的命令行中安装网络仿真驱动程序：VSTestConfig NETWORKEMULATION /install  警告：  负载测试会忽略网络仿真适配器。 实际上，负载测试使用在负载测试方案的网络组合中指定的设置。|
|**系统信息：** 可以设置测试设置来包含有关在其上运行测试的计算机的系统信息。|是|是|是||
|**测试影响：** 可以收集在运行某个测试用例时使用了哪些应用程序代码方法的相关信息。 可将它与开发人员进行的应用程序代码更改结合使用，以确定这些开发更改影响了哪些测试。|是|是|是|-   如果为 Web 客户端角色收集测试影响数据，还必须选择用于 IntelliTrace 和测试影响诊断数据适配器的 ASP.NET 客户端代理。<br />-   仅支持以下版本的 IIS：IIS 7.0、IIS 7.5 和 IIS 8.0。|
|**视频录制器：** 可以在运行测试时创建桌面会话的视频录制。 该视频可帮助其他团队成员隔离难以重现的应用程序问题。|是|是（请参见“注释”）|是|-   如果使测试代理软件作为进程（而不是服务）运行，则可以在运行自动测试时创建视频录制。|

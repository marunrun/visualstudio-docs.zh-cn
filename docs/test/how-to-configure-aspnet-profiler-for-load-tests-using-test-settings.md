---
title: 为负载测试配置 ASP.NET 探查器
ms.date: 10/13/2016
ms.topic: conceptual
helpviewer_keywords:
- test settings, ASP.NET
ms.assetid: 6832fe39-04d5-4d94-8a18-3e2730bad423
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: fc0e9c9a8983d58b7b672be6c1cafb7360e25d28
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979297"
---
# <a name="how-to-configure-aspnet-profiler-for-load-tests-using-test-settings-in-visual-studio"></a>如何：在 Visual Studio 中使用测试设置为负载测试配置 ASP.NET 探查器

可以使用 ASP.NET 探查器诊断数据适配器来收集 ASP.NET 探查器信息。 此诊断数据适配器收集 ASP.NET 应用程序的性能数据。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> 此诊断数据适配器不能用于通过 Microsoft 测试管理器运行的测试。 可对仅使用网站的负载测试使用 ASP.NET 探查器诊断适配器，这需要 Visual Studio Enterprise。

使用 ASP.NET 探查器诊断数据适配器，可以在运行负载测试时从应用层收集 ASP.NET 探查器数据。 不能对较长的负载测试（例如，运行时间超过一小时的负载测试）运行探查器。 这是因为探查器文件可能会变得很大，或许可达数百 MB。 应使用 ASP.NET 探查器运行较短的负载测试，从而仍具有深入诊断性能问题的优点。

> [!NOTE]
> ASP.NET 探查器诊断数据适配器将分析 Internet Information Services (IIS) 进程。 因此，它对开发 Web 服务器不起作用。 若要在负载测试中分析网站，必须在运行 IIS 的计算机上安装测试代理。 测试代理不会生成负载，而仅是作为收集代理。 有关详细信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。

有关详细信息，请参阅[如何：为分发的负载测试创建测试设置](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md)。

## <a name="configure-the-aspnet-profiler-for-your-test-settings"></a>为测试设置配置 ASP.NET 探查器

在执行本过程中的步骤之前，必须从 Visual Studio 中打开测试设置，然后选择“数据和诊断”页。

1. 选择用于收集 ASP.NET 探查器数据的角色。

    > [!WARNING]
    > 此角色必须为 Web 服务器。

2. 选择“ASP.NET 探查器”以启用收集 ASP.NET 分析数据，然后选择“配置”。

     此时将显示配置 ASP.NET 分析数据收集的对话框。

3. 在“探查器采样间隔”中键入一个值，该值指示在获取 ASP.NET 分析样本之间要等待的非暂停 CPU 时钟周期数。

4. 若要启用层交互分析，请选择“启用层交互分析”。

     层交互分析对发送给每个项目（例如 MyPage.aspx 或 CompanyLogo.gif）的 Web 服务器的请求数以及处理每个请求所需的时间进行计数。 此外，层交互分析还将收集在页请求期间使用了哪些 ADO.NET 连接，以及在处理该请求期间执行了多少查询和存储过程调用。

     将收集两个不同的计时信息集：

    - 用于处理每个 Web 请求的计时信息（最小值、最大值、平均值和总计值）。

    - 执行每个查询的计时信息（最小值、最大值、平均值和总计值）。

在测试设置中配置了 ASP.NET 探查器诊断数据适配器之后，现在可以收集有关 ASP.NET Web 应用程序的 ASP.NET 分析数据。

## <a name="see-also"></a>请参阅

- [使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)
- [如何：为分发的负载测试创建测试设置](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md)
- [测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)
---
title: IntelliTrace 数据
ms.date: 10/13/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliTrace, configuring test settings
- Diagnostic Data Adapter, InteliTrace
- debugging [Visual Studio ALM], difficult issues using IntelliTrace
- Test Runner, InteliTrace
ms.assetid: 02b6716f-569e-4961-938a-e790a0c74b5c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: adc77ee87bbbf07d04fd7c01a554c7c074e5bf7f
ms.sourcegitcommit: 5d1b2895d3a249c6bea30eb12b0ad7c0f0862d85
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80880216"
---
# <a name="how-to-collect-intellitrace-data-to-help-debug-difficult-issues"></a>如何：收集 IntelliTrace 数据以帮助调试难题

可在 Visual Stdio 中为 IntelliTrace 配置诊断数据适配器以收集特定诊断跟踪信息。 测试可使用此适配器，测试可以收集应用程序的重要诊断事件，开发人员稍后可使用这些事件通过代码进行跟踪以查找导致出现 Bug 的原因。 IntelliTrace 的诊断数据适配器既可用于手动测试，也可用于自动测试。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> IntelliTrace 只可用于使用托管代码编写的应用程序。 如果你正在测试将浏览器用作客户端的 Web 应用程序，则不应该在测试设置中为客户端启用 IntelliTrace，因为没有可用于跟踪的托管代码。 在此情况下，可能需要设置环境并在你的 Web 服务器上远程收集 IntelliTrace 数据。

IntelliTrace 数据存储在扩展名为“.iTrace”  的文件中。 运行测试时如果某个测试步骤未通过，则可以创建一个 Bug。 包含诊断信息的 IntelliTrace 文件会自动附加到此 Bug 中。

> [!NOTE]
> IntelliTrace 的诊断数据适配器在成功通过测试时未创建 IntelliTrace 文件。 它只对未通过的测试用例保存文件，或者只有当您提交 Bug 时，它才会保存文件。

IntelliTrace 文件中收集的数据可减少重现和诊断代码中的错误所需的时间，从而提高调试效率。 此外，由于您可与能在其计算机上复制您的本地会话的其他人共享 IntelliTrace 文件，因此它减少了 Bug 将不可重现的可能性。

> [!NOTE]
> 如果在测试设置中启用 IntelliTrace，则收集代码覆盖率数据将不起作用。

> [!WARNING]
> IntelliTrace 的诊断数据适配器的工作方式是检测托管进程，这项操作必须在测试运行的测试加载后执行。 如果要监视的进程已启动，则不会收集任何 IntelliTrace 文件，因为该进程已在运行。 为了避免这种情况，请确保加载测试之前该进程已停止。 然后在加载测试后或启动第一个测试后启动该进程。

::: moniker range="vs-2017"
下面的过程介绍如何配置您想要收集的 IntelliTrace 数据。 这些步骤适用于 Microsoft 测试管理器中的配置编辑器和 Visual Studio 中的“测试设置”对话框。
::: moniker-end
::: moniker range=">=vs-2019"
下面的过程介绍如何配置您想要收集的 IntelliTrace 数据。 这些步骤适用于 Visual Studio 中的“测试设置”对话框。
::: moniker-end

> [!NOTE]
> 用于收集 IntelliTrace 数据的测试代理的用户帐户必须是管理员组的成员。 有关详细信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。

## <a name="configure-the-data-to-collect-with-the-intellitrace-diagnostic-data-adapter"></a>将数据配置为通过 IntelliTrace 诊断数据适配器进行收集

::: moniker range="vs-2017"
在执行本过程中的步骤之前，必须从 Microsoft 测试管理器或 Visual Studio 中打开测试设置，然后选择“数据和诊断”页  。
::: moniker-end
::: moniker range=">=vs-2019"
在执行本过程中的步骤之前，必须从 Visual Studio 中打开测试设置，然后选择“数据和诊断”页  。
::: moniker-end

### <a name="to-configure-the-data-to-collect-with-the-intellitrace-diagnostic-data-adapter"></a>将数据配置为通过 IntelliTrace 诊断数据适配器进行收集

1. 选择用于收集 IntelliTrace 数据的角色。

2. 选择“IntelliTrace”  。

3. 若要为 Web 客户端角色或 ASP.NET Web 应用程序添加 IntelliTrace，还必须选择“用于 IntelliTrace 和测试影响的 ASP.NET 客户端代理”  。

     此代理允许你为 IntelliTrace 和测试影响诊断数据适配器收集有关从客户端到 Web 服务器的 http 调用的信息。

    > [!WARNING]
    > 如果决定对正用于 Internet Information Server (IIS) 上应用程序池（打算在其中收集 IntelliTrace 数据）的标识使用自定义帐户，必须在 IIS 计算机上为正在使用的自定义帐户创建本地用户配置文件。 您可以为自定义帐户创建本地配置文件，方法是本地登录到 IIS 计算机一次，或使用自定义帐户凭据运行以下命令行：
    >
    > runas /user:domain\name /profile cmd.exe 

4. 对“IntelliTrace”选择“配置”可修改默认的 IntelliTrace 设置   。

     此时将显示用于配置将要收集的数据的对话框。

    > [!WARNING]
    > 如果启用收集 IntelliTrace 数据，则收集代码覆盖率数据将不起作用。

5. 选择“常规”选项卡  。选择“仅 IntelliTrace 事件”以记录测试时对性能影响最小的重要诊断事件  。

     \- 或 -

     选择“IntelliTrace 事件和调用信息”以记录诊断事件以及用于显示调用信息的方法级别跟踪  。 在运行测试时，此跟踪级别可能对性能有影响。

6. 若要从正在 Internet Information Services 上运行的 ASP.NET 应用程序中收集数据，请选择“从 Internet Information Services 上运行的 ASP.NET 应用程序中收集数据”  。 在 Web 服务器角色上安装并配置你的测试代理。 请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。

7. 选择“模块”选项卡  。选择“从以下模块以外的所有模块收集数据”并使用“添加”可添加到模块列表中，单击“移除”可移除模块    。 通过使用此选项，您可以包含除指定的模块之外的系统上运行的所有模块。

     \- 或 -

     选择“仅从以下模块中收集数据”并使用“添加”以添加到模块列表中，使用“移除”以移除模块    。 通过使用此选项，您可以确切地指定所需的模块。

    > [!NOTE]
    > 如果可能，请选择要监视的特定进程。 建议这样做以便优化性能。

8. 选择“进程”选项卡  。选择“从以下进程之外的所有进程收集数据”，然后使用“添加”以添加到进程列表中，使用“移除”以移除进程    。 通过使用此选项，您可以包含除指定的进程之外的系统上运行的所有进程。

     \- 或 -

     选择“仅从指定的进程收集数据”并使用“添加”以添加到进程列表中，使用“移除”以移除进程    。 通过使用此选项，您可以确切地指定所需的进程。

9. （可选）选择“IntelliTrace 事件”选项卡  。选择或清除您想在收集诊断事件时包含或排除的每个 IntelliTrace 事件类别。

10. （可选）展开每个 IntelliTrace 事件类别，然后选择或清除您想在 IntelliTrace 事件中包含或排除的每个特定事件。

11. （可选）选择“高级”选项卡  。接着，选择“用于记录的最大磁盘空间”旁边的箭头，并选择想要留给 IntelliTrace 文件使用的磁盘空间的最大大小  。

    > [!NOTE]
    > 如果增大记录的大小，则可能会在您将此记录与测试结果一起保存时出现超时问题。

12. 如果使用 Microsoft 测试管理器（在 Visual Studio 2017 中已弃用），请选择“保存”  。 如果使用的是 Visual Studio，请选择“确定”  。 现在已为测试设置配置并保存了 IntelliTrace 设置。

    ::: moniker range="vs-2017"
    > [!NOTE]
    > 若要重置此诊断数据适配器的配置，请为 Visual Studio 选择“重置为默认配置”，或为 Microsoft 测试管理器选择“重置为默认值”   。
    ::: moniker-end
    ::: moniker range=">=vs-2019"
    > [!NOTE]
    > 要重置此诊断数据适配器的配置，请在 Visual Studio 中选择“重置为默认配置”  。
    ::: moniker-end

## <a name="see-also"></a>请参阅

- [在测试时收集诊断数据 (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)
- [在手动测试中收集诊断数据 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)
- [使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)
- [收集 IntelliTrace 数据](../test/how-to-collect-intellitrace-data-to-help-debug-difficult-issues.md)

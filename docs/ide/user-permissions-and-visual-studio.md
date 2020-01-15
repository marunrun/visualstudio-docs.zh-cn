---
title: 以管理员身份运行
ms.date: 01/06/2020
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, user permissions
- user permissions
- administrative privileges
- permissions
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 927031b4755644aeac553367a4f8a08faa0c0992
ms.sourcegitcommit: 5421999c9ff05b3242d33e4b0465f8bc29c7c643
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75718631"
---
# <a name="user-permissions-and-visual-studio"></a>用户权限与 Visual Studio

出于安全目的，你应尽可能以典型用户的身份来运行 Visual Studio。

> [!WARNING]
> 你还应确保不要编译、启动或调试任何来自不受信任用户或地址的 Visual Studio 解决方案。

可以以典型用户身份在 Visual Studio IDE 中执行几乎任何操作。 需要管理员权限才能完成以下任务：

|区域|任务|更多相关信息|
|----------|----------| - |
|安装|安装或修改 Visual Studio。|[安装 Visual Studio](../install/install-visual-studio.md)，[修改 Visual Studio](../install/modify-visual-studio.md)|
||安装、更新或删除本地帮助内容。|[安装和管理本地帮助内容](../help-viewer/install-manage-local-content.md)|
|工具箱|将经典 COM 控件添加到“工具箱”  。|[工具箱](../ide/reference/toolbox.md)|
|生成|使用注册组件的生成后事件。|[了解自定义生成步骤和生成事件](/cpp/build/understanding-custom-build-steps-and-build-events)|
||在生成 C++ 项目时包括一个注册步骤。||
|调试|调试使用提升的权限运行的应用程序。|[调试器设置和准备](../debugger/debugger-settings-and-preparation.md)|
||调试在其他用户帐户下运行的应用程序，例如 ASP.NET 网站。|[调试 ASP.NET 和 AJAX 应用程序](../debugger/how-to-enable-debugging-for-aspnet-applications.md)|
||在区域中调试 XAML 浏览器应用程序 (XBAP)。|[WPF 主机 (PresentationHost.exe)](/dotnet/framework/wpf/app-development/wpf-host-presentationhost-exe)|
||使用模拟器可以调试 Microsoft Azure 的云服务项目。|[在 Visual Studio 中调试云服务](/azure/vs-azure-tools-debug-cloud-services-virtual-machines)|
||为远程调试配置防火墙。|[远程调试](../debugger/remote-debugging.md)|
|性能工具|附加到提升的应用程序。|[性能分析初学者指南](../profiling/beginners-guide-to-performance-profiling.md)|
||使用 GPU 探查器。|[GPU 分析](../profiling/gpu-usage.md)|
|部署|在本地计算机上将 Web 应用程序部署到 Internet Information Services (IIS)。|[使用 Visual Studio 部署 ASP.NET Web 应用](/aspnet/web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/)|

## <a name="run-visual-studio-as-an-administrator"></a>以管理员身份运行 Visual Studio

如果需要以管理员身份运行 Visual Studio，请执行以下步骤打开 IDE：

> [!NOTE]
> 这些说明适用于Windows 10。 它们与其他版本的 Windows 类似。

::: moniker range="vs-2017"

1. 打开“开始”  菜单，并滚动到 Visual Studio 2017。

1. 从右键单击或 Visual Studio 2017  的上下文菜单中，依次选择“更多”  >“以管理员身份运行”  。

   Visual Studio 启动时，标题栏的产品名后显示“(管理员)”  。

::: moniker-end

::: moniker range=">=vs-2019"

1. 打开“开始”菜单，并滚动到 Visual Studio 2019  。

1. 从右键单击或 Visual Studio 2019  的上下文菜单中，依次选择“更多”  >“以管理员身份运行”  。

   Visual Studio 启动时，标题栏的产品名后显示“(管理员)”  。

::: moniker-end

此外可以修改应用程序快捷方式，以便始终利用管理权限运行。

## <a name="see-also"></a>请参阅

- [移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
- [安装 Visual Studio](../install/install-visual-studio.md)

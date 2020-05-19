---
title: 启用 ASP.NET 应用调试 | Microsoft Docs
ms.custom: ''
ms.date: 09/21/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging ASP.NET Web applications
- Web.config configuration file, debug mode
- debugging [Visual Studio], ASP.NET
ms.assetid: 3beed819-cece-4864-8184-bd410000973a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: a6f20a2272214a525b00ebf07ebc6e5e803b138c
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911353"
---
# <a name="debug-aspnet-or-aspnet-core-apps-in-visual-studio"></a>在 Visual Studio 中调试 ASP.NET 或 ASP.NET Core 应用

可以在 Visual Studio 中调试 ASP.NET 和 ASP.NET Core 应用。 无论是在 IIS Express 还是在本地 IIS 服务器上运行，ASP.NET 和 ASP.NET Core 的调试过程都不同。

>[!NOTE]
>以下步骤和设置仅适用于在本地服务器上调试应用。 在远程 IIS 服务器上调试应用使用“附加到进程”，并忽略这些设置。 有关在 IIS 上远程调试 ASP.NET 应用的详细信息和说明，请参阅[在 IIS 计算机上远程调试 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) 或[在远程 IIS 计算机上远程调试 ASP.NET Core](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)。

Visual Studio 中内置了 IIS Express 服务器。 IIS Express 是 ASP.NET 和 ASP.NET Core 项目的默认调试服务器，并且是预先配置的。 这是最简单的调试方法，也是初始调试和测试的理想选择。

你还可以在配置为运行该应用的本地 IIS 服务器（8.0 或更高版本）上调试 ASP.NET 或 ASP.NET Core 应用。 要在本地 IIS 上调试，必须满足以下要求：

<a name="iis"></a>
- 安装 Visual Studio 时，请选择“开发时 IIS 支持”。 （如有必要，请重新运行 Visual Studio 安装程序，选择“修改”，然后添加此组件。）
- 以管理员身份运行 Visual Studio。
- 使用适当版本的 ASP.NET 和/或 ASP.NET Core 安装并正确配置 IIS。 有关详细信息和说明，请参阅[使用 ASP.NET 3.5 和 ASP.NET 4.5 的 IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) 或[使用 IIS 在 Windows 上托管 ASP.NET Core](/aspnet/core/host-and-deploy/iis/index)。
- 请确保应用在 IIS 上运行且未出现错误。

## <a name="debug-aspnet-apps"></a>调试 ASP.NET 应用

IIS Express 是默认选择，并且是预先配置的。 如果要在本地 IIS 上调试，请确保满足[本地 IIS 调试的要求](#iis)。

1. 在 Visual Studio“解决方案资源管理器”中选择 ASP.NET 项目，然后单击“属性”图标，按 Alt+Enter，或右键单击并选择“属性”    。

1. 选择 Web 选项卡。

1. 在“属性”窗格中的“服务器”下 ，
   - 对于 IIS Express，请从下拉列表中选择 IIS Express。
   - 对于本地 IIS，
     1. 请从下拉列表中选择“本地 IIS”。
     1. 如果尚未在 IIS 中设置应用，请在“项目 URL”字段旁边选择“创建虚拟目录” 。

1. 在“调试器”下，选择 ASP.NET 。

   ![ASP.NET 调试器设置](media/dbg-aspnet-enable-debugging2.png "ASP.NET 调试器设置")

1. 使用“文件” > “保存选定项”或 Ctrl+S 来保存更改   。

1. 要调试应用，请在项目中的某些代码上设置断点。 在 Visual Studio 工具栏中，确保将配置设置为“调试”，所需的浏览器将出现在模拟器字段中的“IIS Express (\<Browser name>)”或“本地 IIS (\<Browser name>)”中  。

1. 要开始调试，请在工具栏中选择“IIS Express (\<Browser name>)”或“本地 IIS (\<Browser name>)”，从“调试”菜单中选择“启动调试”，或按 F5    。 调试器在断点处暂停。 如果调试器无法命中断点，请参阅[调试疑难解答](#troubleshoot-debugging)。

## <a name="debug-aspnet-core-apps"></a>调试 ASP.NET Core 应用

IIS Express 是默认选择，并且是预先配置的。 如果要在本地 IIS 上调试，请确保满足[本地 IIS 调试的要求](#iis)。

1. 在 Visual Studio“解决方案资源管理器”中选择 ASP.NET Core 项目，然后单击“属性”图标，按 Alt+Enter，或右键单击并选择“属性”    。

1. 选择“调试”选项卡。

1. 在“属性”窗格中的“配置文件”旁边 ，
   - 对于 IIS Express，请从下拉列表中选择 IIS Express。
   - 对于本地 IIS，请从下拉列表中选择应用名称，或选择“新建”，创建新的配置文件名称，然后选择“确定” 。

1. 在“启动”旁边，从下拉列表中选择 IIS Express 或 IIS  。

1. 确保选中“启动浏览器”。

1. 在“环境变量”下，确保 ASPNETCORE_ENVIRONMENT 显示了值“开发”  。 否则，请选择“添加”进行添加。

   ![ASP.NET Core 调试器设置](../debugger/media/dbg-aspnet-enable-debugging3.png "ASP.NET Core 调试器设置")

1. 使用“文件” > “保存选定项”或 Ctrl+S 来保存更改   。

1. 要调试应用，请在项目中的某些代码上设置断点。 在 Visual Studio 工具栏中，确保将配置设置为“调试”，且 IIS Express 或新的 IIS 配置文件名称显示在模拟器字段中 。

1. 要开始调试，请在工具栏中选择 IIS Express 或 \<IIS profile name>，从“调试”菜单中选择“启动调试”，或按 F5    。 调试器在断点处暂停。 如果调试器无法命中断点，请参阅[调试疑难解答](#troubleshoot-debugging)。

## <a name="troubleshoot-debugging"></a>调试疑难解答

如果本地 IIS 调试无法进行到断点，请按照以下步骤进行故障排除。

1. 从 IIS 启动 Web 应用，并确保其正常运行。 使 Web 应用保持运行状态。

2. 在 Visual Studio 中，选择“调试”>“附加到进程”或按 Ctrl+Alt+P，并连接到 ASP.NET 或 ASP.NET Core 进程（通常为 w3wp.exe 或 dotnet.exe     ）。 有关详细信息，请参阅[附加到进程](attach-to-running-processes-with-the-visual-studio-debugger.md)和[如何查找 ASP.NET 进程名称](how-to-find-the-name-of-the-aspnet-process.md)。

如果可以通过使用“附加到进程”来连接和命中断点，但不能通过使用“调试” > “启动调试”或 F5 来连接和命中断点，则项目属性中的设置可能不正确   。 如果使用 HOSTS 文件，请确保其配置正确。

## <a name="configure-debugging-in-the-webconfig-file"></a>在 web.config 文件中配置调试

ASP.NET 项目默认有 web.config 文件，其中包含应用配置、启动信息和调试设置。 必须正确配置 web.config 文件才能进行调试。 可通过前面部分的“属性”设置来更新 web.config 文件，但也可手动配置。

> [!NOTE]
> ASP.NET Core 项目最初没有 web.config 文件，但使用 appsettings.json 和 launchSettings.json 文件来提供应用配置和启动信息  。 部署应用会在项目中创建一个或多个 web.config 文件，但这些文件通常不包含调试信息。

> [!TIP]
> 部署进程可能会更新 web.config 设置，因此，在尝试调试之前，请确保已将 web.config 配置为用于调试 。

**要手动配置 web.config 文件以进行调试，请执行以下操作：** 

1. 在 Visual Studio 中，打开 ASP.NET 项目的 web.config 文件。

2. Web.config 是一个 XML 文件，嵌套部分用标记标识。 找到 `configuration/system.web/compilation` 部分。 （如果 `compilation` 元素不存在，请创建一个。）

3. 确保 `compilation` 元素中的 `debug` 属性设置为 `true`。 （如果 `compilation` 元素不包含 `debug` 属性，请添加该元素并将其设置为 `true`。）

   如果使用本地 IIS 而不是默认 IIS Express 服务器，请确保 `compilation` 元素中的 `targetFramework` 属性值与 IIS 服务器上的框架一致。

   web.config 文件的 `compilation` 元素应类似于下面的示例：

   > [!NOTE]
   > 此示例仅展示部分 web.config 文件。 `configuration` 和 `system.web` 元素中通常还有其他 XML 部分，`compilation` 元素也可能包含其他属性和元素。

   ```xml
   <configuration>
      ...
      <system.web>
          <compilation  debug="true"  targetFramework="4.6.1" ... >
             ...
          </compilation>
      </system.web>
   </configuration>
   ```

[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 会自动检测对 Web.config 文件的任何更改，并应用新的配置设置。 更改立即生效，不必重启计算机或 IIS 服务器。

一个网站可包含多个虚拟目录和子目录，其中每个目录中都有 web.config 文件。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用从 URL 路径中更高级别的 web.config 文件继承配置设置。 分层 web.config 文件设置应用于层次结构中的所有下级 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用。 在层次结构下较低级别的 web.config 文件中设置其他配置将覆盖较高级别文件中的设置。

例如，如果在 www.microsoft.com/aaa/web.config 中指定 `debug="true"`，则 aaa 文件夹或 aaa 任何子文件夹中的任何应用都将继承该设置，除非其中一个应用使用自己的 web.config 文件覆盖设置  。

## <a name="publish-in-debug-mode-using-the-file-system"></a>使用文件系统在调试模式下发布

有几种不同的方法可以将应用发布到 IIS。 以下步骤说明如何使用文件系统创建和部署调试发布配置文件。 要执行此操作，必须以管理员身份运行 Visual Studio。

> [!IMPORTANT]
> 如果更改代码或重新生成，则必须重复这些步骤以重新发布。

1. 在 Visual Studio 中，右键单击项目，选择“发布”。

3. 选择“IIS、FTP 等”并单击“发布” 。

    ![发布到 IIS](media/dbg-aspnet-local-iis.png "发布到 IIS")

4. 在 CustomProfile 对话框中，对于“发布方法”，请选择“文件系统”  。

5. 对于“目标位置”，选择“浏览 (…)”  。

   - 对于 ASP.NET，选择“本地 IIS”，选择为应用创建的网站，然后选择“打开” 。

     ![将 ASP.NET 发布到 IIS](media/dbg-aspnet-local-iis1.png "将 ASP.NET 发布到 IIS")

   - 对于 ASP.NET Core，选择“文件系统”，选择为应用设置的文件夹，然后选择“打开” 。

1. 选择“下一步”。

1. 在“配置”下，从下拉列表中选择“调试” 。

1. 选择“保存”。

1. 在“发布”对话框中，确保显示 CustomProfile（或刚刚创建的配置文件的名称），且 LastUsedBuildConfiguration 设置为“调试”   。

1. 选择“发布”。

    ![发布到 IIS](media/dbg-aspnet-local-iis-select-site.png "发布到 IIS")

> [!IMPORTANT]
> 调试模式会极大地降低应用的性能。 为了获得最佳性能，请在 web.config 文件中设置 `debug="false"`，并在部署生产应用或执行性能度量时指定发布版本。

## <a name="see-also"></a>请参阅
- [ASP.NET 调试：系统要求](aspnet-debugging-system-requirements.md)
- [如何：在用户帐户下运行工作进程](how-to-run-the-worker-process-under-a-user-account.md)
- [如何：查找 ASP.NET 进程的名称](how-to-find-the-name-of-the-aspnet-process.md)
- [调试已部署的 Web 应用程序](debugging-deployed-web-applications.md)
- [演练：调试 Web 窗体](walkthrough-debugging-a-web-form.md)
- [如何：调试 ASP.NET 异常](how-to-debug-aspnet-exceptions.md)
- [调试 Web 应用程序：错误和疑难解答](debugging-web-applications-errors-and-troubleshooting.md)

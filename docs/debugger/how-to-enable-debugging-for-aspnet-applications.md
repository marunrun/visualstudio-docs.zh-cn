---
title: 为 ASP.NET 应用程序启用调试 |Microsoft Docs
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
ms.openlocfilehash: d383c559e605392b01ba2c476fd4ed5ae5d48625
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62848384"
---
# <a name="debug-aspnet-or-aspnet-core-apps-in-visual-studio"></a>调试 Visual Studio 中的 ASP.NET 或 ASP.NET Core 应用

您可以调试在 Visual Studio 中的 ASP.NET 和 ASP.NET Core 应用。 ASP.NET 和 ASP.NET Core 中，流程有所不同和是否在 IIS Express 或本地 IIS 服务器上运行它。

>[!NOTE]
>下面的步骤和设置仅适用于本地服务器上调试应用。 调试远程 IIS 上的应用程序服务器使用**附加到进程**，并忽略这些设置。 有关详细信息和有关在 IIS 上的远程调试 ASP.NET 应用的说明，请参阅[IIS 计算机上的远程调试 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)或[远程调试远程 IIS 计算机上的 ASP.NET Core](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)。

使用 Visual Studio 中包含内置的 IIS Express 服务器。 IIS Express 是 ASP.NET 和 ASP.NET Core 项目的默认调试服务器和预配置。 它是调试，并且非常适合于初始的调试和测试的最简单方法。

此外可以调试在本地 IIS 服务器 （版本 8.0 或更高版本） 上配置为运行应用程序的 ASP.NET 或 ASP.NET Core 应用。 若要在本地 IIS 上进行调试，必须满足以下要求：

<a name="iis"></a>
- 选择**开发时 IIS 支持**安装 Visual Studio 时。 (如果有必要，请重新运行 Visual Studio 安装程序，请选择**修改**，并添加此组件。)
- 以管理员身份运行 Visual Studio。
- 安装并正确配置 IIS 和 ASP.NET 和/或 ASP.NET Core 的适当版本。 有关详细信息和说明，请参阅[IIS 8.0 使用 ASP.NET 3.5 和 ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)或[与 IIS 的 Windows 上托管 ASP.NET Core](https://docs.microsoft.com/aspnet/core/host-and-deploy/iis/index)。
- 请确保应用在 IIS 上运行且未出错。

## <a name="debug-aspnet-apps"></a>调试 ASP.NET 应用

IIS Express 是默认设置，并且预配置。 如果在本地 IIS 上进行调试，请确保你满足[要求对本地 IIS 调试](#iis)。

1. 在 Visual Studio 中选择 ASP.NET 项目**解决方案资源管理器**然后单击**属性**图标中，按**Alt**+**Enter**，或右键单击，然后选择**属性**。

1. 选择**Web**选项卡。

1. 在中**属性**窗格下**服务器**，
   - 对于 IIS Express，请选择**IIS Express**从下拉列表。
   - 本地 IIS
     1. 选择**本地 IIS**从下拉列表。
     1. 下一步**项目 URL**字段中，选择**创建虚拟目录**，如果你尚未设置应用在 IIS 中。

1. 下**调试器**，选择**ASP.NET**。

   ![ASP.NET 调试程序设置](media/dbg-aspnet-enable-debugging2.png "ASP.NET 调试器设置")

1. 使用**文件** > **保存选定项**或**Ctrl**+**S**保存任何更改。

1. 若要调试应用程序，在项目中，一些代码上设置断点。 在 Visual Studio 工具栏中，请确保配置设置为**调试**，并且你想在浏览的器将出现在**IIS Express (\<浏览器名称 >)** 或**本地 IIS (\<浏览器名称 >)** 仿真程序字段中。

1. 若要开始调试，请选择**IIS Express (\<浏览器名称 >)** 或**本地 IIS (\<浏览器名称 >)** 工具栏中，选择**开始调试**从**调试**菜单中或按**F5**。 调试器会在断点处暂停。 如果调试器无法命中断点，请参阅[进行故障排除调试](#troubleshoot-debugging)。

## <a name="debug-aspnet-core-apps"></a>调试 ASP.NET Core 应用

IIS Express 是默认设置，并且预配置。 如果在本地 IIS 上进行调试，请确保你满足[要求对本地 IIS 调试](#iis)。

1. 在 Visual Studio 中选择 ASP.NET Core 项目**解决方案资源管理器**然后单击**属性**图标中，按**Alt**+**Enter**，或右键单击，然后选择**属性**。

1. 选择“调试”选项卡。

1. 在中**属性**窗格中，为下的一步**配置文件**，
   - 对于 IIS Express，请选择**IIS Express**从下拉列表。
   - 本地 iis，从下拉列表中，选择应用名称，或选择**新建**，创建新的配置文件名称，并选择**确定**。

1. 下一步**启动**，选择**IIS Express**或**IIS**从下拉列表。

1. 请确保**启动浏览器**处于选中状态。

1. 下**环境变量**，请确保**ASPNETCORE_ENVIRONMENT**存在且值为**开发**。 如果没有，请选择**添加**并将其添加。

   ![ASP.NET Core 调试器设置](../debugger/media/dbg-aspnet-enable-debugging3.png "ASP.NET Core 调试器设置")

1. 使用**文件** > **保存选定项**或**Ctrl**+**S**保存任何更改。

1. 若要调试应用程序，在项目中，一些代码上设置断点。 在 Visual Studio 工具栏中，请确保配置设置为**调试**，并将**IIS Express**，或者新的 IIS 配置文件名称，将显示在 emulator 字段。

1. 若要开始调试，请选择**IIS Express**或 **\<IIS 配置文件名称 >** 工具栏中，选择**开始调试**从**调试**菜单中或按**F5**。 调试器会在断点处暂停。 如果调试器无法命中断点，请参阅[进行故障排除调试](#troubleshoot-debugging)。

## <a name="troubleshoot-debugging"></a>进行故障排除调试

如果本地 IIS 调试就无法转到断点，请按照这些步骤来解决。

1. 从 IIS 中，启动 web 应用并确保它能够正常运行。 将运行的 web 应用。

2. 从 Visual Studio 中，选择**调试 > 附加到进程**或按**Ctrl**+**Alt**+**P**，和连接到 ASP.NET 或 ASP.NET Core 进程 (通常**w3wp.exe**或**dotnet.exe**)。 有关详细信息，请参阅[附加到进程](attach-to-running-processes-with-the-visual-studio-debugger.md)并[如何查找 ASP.NET 进程的名称](how-to-find-the-name-of-the-aspnet-process.md)。

如果可以连接并使用命中断点**附加到进程**，但不能使用**调试** > **开始调试**或**F5**，设置是在项目属性中可能不正确。 如果使用主机文件，请确保还正确配置。

## <a name="configure-debugging-in-the-webconfig-file"></a>配置在 web.config 文件中进行调试

ASP.NET 项目具有*web.config*文件默认情况下，其中包含这两个应用程序配置和启动信息，包括调试设置。 *Web.config*进行调试，必须正确配置文件。 **属性**之前的部分更新中的设置*web.config*文件，但您还可以配置它们手动。

> [!NOTE]
> ASP.NET Core 项目最初不会出现*web.config*的文件，但使用*appsettings.json*并*launchSettings.json*应用配置和启动文件信息。 部署应用程序会创建*web.config*文件或文件在项目中，但它们通常包含调试信息。

> [!TIP]
> 在部署过程可能会更新*web.config*设置，因此在之前尝试调试，请确保*web.config*配置用于调试。

**若要手动配置*web.config*文件以进行调试：**

1. 在 Visual Studio 中打开 ASP.NET 项目*web.config*文件。

2. *Web.config*是一个 XML 文件，因此包含标记来标记的嵌套的节。 找到 `configuration/system.web/compilation` 部分。 (如果`compilation`元素不存在，请创建它。)

3. 请确保`debug`中的属性`compilation`元素设置为`true`。 (如果`compilation`元素不包含`debug`属性，将其添加并将其设置为`true`。)

   如果使用本地 IIS 而不默认 IIS Express 服务器，请确保`targetFramework`属性中的值`compilation`元素都与匹配的 IIS 服务器上的框架。

   `compilation`的元素*web.config*文件应如以下示例所示：

   > [!NOTE]
   > 此示例是一个分部*web.config*文件。 有中的通常其他 XML 部分`configuration`并`system.web`元素，并`compilation`元素还可能包含其他属性和元素。

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

[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 会自动检测对 Web.config 文件的任何更改，并应用新的配置设置。 您无需重新启动计算机或 IIS 服务器，以使更改生效。

网站可以使用包含多个虚拟目录和子目录*web.config*中每个文件。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用程序继承中的配置设置*web.config*文件 URL 路径中的更高级别。 分层*web.config*文件设置应用于所有[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]下面这些层次结构中的应用。 在中设置不同的配置*web.config*文件层次结构中较低级别重写更高版本的文件中的设置。

例如，如果您指定`debug="true"`中<em>www.microsoft.com/aaa/web.config</em>中的任何应用*aaa*文件夹或任何子文件夹中*aaa*继承该设置，如果这些应用程序的其中一个重写具有其自己的设置除外*web.config*文件。

## <a name="publish-in-debug-mode-using-the-file-system"></a>在调试模式下使用文件系统中发布

有不同的方式来将应用发布到 IIS。 这些步骤演示如何创建并部署调试发布配置文件使用文件系统。 若要执行此操作，您必须运行 Visual Studio 以管理员身份。

> [!IMPORTANT]
> 如果更改代码或重新生成，则必须重复以下步骤来重新发布。

1. 在 Visual Studio 中，右键单击该项目并选择**发布**。

3. 选择**IIS、 FTP 等**然后单击**发布**。

    ![将发布到 IIS](media/dbg-aspnet-local-iis.png "将发布到 IIS")

4. 在中**CustomProfile**对话框中，对于**发布方法**，选择**文件系统**。

5. 有关**目标位置**，选择**浏览**(**...**).

   - 对于 ASP.NET 中，选择**本地 IIS**，选择要为应用程序中，创建的网站，然后选择**打开**。

     ![将发布到 IIS 的 ASP.NET](media/dbg-aspnet-local-iis1.png "发布到 IIS 的 ASP.NET")

   - 对于 ASP.NET Core 中，选择**文件系统**，选择您为应用设置，然后选择该文件夹**打开**。

1. 选择“下一步”。

1. 下**配置**，选择**调试**从下拉列表。

1. 选择“保存”。

1. 中**发布**对话框中，请确保**CustomProfile** （或刚创建的配置文件的名称） 显示，并且**LastUsedBuildConfiguration**设置为**调试**。

1. 选择“发布”。

    ![将发布到 IIS](media/dbg-aspnet-local-iis-select-site.png "将发布到 IIS")

> [!IMPORTANT]
> 调试模式下极大地减少了您的应用程序的性能。 为了获得最佳性能，设置`debug="false"`中*web.config*和部署生产应用程序或进行性能度量时指定的版本生成。

## <a name="see-also"></a>请参阅
- [ASP.NET 调试：系统要求](aspnet-debugging-system-requirements.md)
- [如何：辅助角色下运行进程的用户帐户](how-to-run-the-worker-process-under-a-user-account.md)
- [如何：查找 ASP.NET 进程的名称](how-to-find-the-name-of-the-aspnet-process.md)
- [调试已部署的 Web 应用程序](debugging-deployed-web-applications.md)
- [演练：调试 web 窗体](walkthrough-debugging-a-web-form.md)
- [如何：调试 ASP.NET 异常](how-to-debug-aspnet-exceptions.md)
- [调试 Web 应用程序：错误和疑难解答](debugging-web-applications-errors-and-troubleshooting.md)

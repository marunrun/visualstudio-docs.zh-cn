---
title: 通过命令行生成 ClickOnce 应用程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, from command line
- publishing
- publishing, ClickOnce
ms.assetid: d9bc6212-c584-4f72-88c9-9a4b998c555e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 065eea058ffa78c84428e031832e24837eb81d08
ms.sourcegitcommit: af9bbf9116a63c0631ff2f4f3a878564aa63cd8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74797199"
---
# <a name="build-clickonce-applications-from-the-command-line"></a>从命令行生成 ClickOnce 应用程序
在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]中，可以从命令行生成项目，即使它们是在集成开发环境（IDE）中创建的。 事实上，你可以在仅安装了 .NET Framework 的另一台计算机上重新生成使用 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 创建的项目。 这样一来，您就可以使用自动化进程（例如，在中央生成实验室中）或使用超出生成项目本身范围的高级脚本技术来重现生成。

## <a name="use-msbuild-to-reproduce-clickonce-application-deployments"></a>使用 MSBuild 重现 ClickOnce 应用程序部署
 调用 msbuild/target：在命令行发布时，它会告知 MSBuild 系统生成项目，并在 "发布" 文件夹中创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 这等效于在 IDE 中选择 "**发布**" 命令。

 此命令执行*msbuild.exe*，后者位于 Visual Studio 命令提示符环境的路径中。

 "目标" 是有关如何处理命令的 MSBuild 的指示器。 键目标为 "生成" 目标和 "发布" 目标。 生成目标等效于在 IDE 中选择 "生成" 命令（或按 F5）。 如果只想生成项目，则可以通过键入 `msbuild`来实现。 此命令有效，因为生成目标是 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]生成的所有项目的默认目标。 这意味着你不需要显式指定生成目标。 因此，键入 `msbuild` 与键入 `msbuild /target:build`相同。

 `/target:publish` 命令指示 MSBuild 调用发布目标。 发布目标取决于 build 目标。 这意味着发布操作是生成操作的超集。 例如，如果对某个 Visual Basic 或C#源文件进行了更改，则发布操作将自动重新生成相应的程序集。

 有关使用 Mage.exe 命令行 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 工具生成完整 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署的信息，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

## <a name="create-and-build-a-basic-clickonce-application-with-msbuild"></a>使用 MSBuild 创建并生成基本的 ClickOnce 应用程序

#### <a name="to-create-and-publish-a-clickonce-project"></a>创建和发布 ClickOnce 项目

1. 打开 Visual Studio 并创建一个新项目。

    选择 " **Windows 桌面应用程序**" 项目模板，并将项目命名为 `CmdLineDemo`。

1. 在 "**生成**" 菜单中，单击 "**发布**" 命令。

    此步骤可确保将项目正确配置为生成 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的应用程序部署。

    此时，将显示发布向导。

1. 在发布向导中，单击 "**完成**"。

    Visual Studio 将生成并显示名为*Publish*的默认网页。

1. 保存项目，并记下存储项目的文件夹位置。

   以上步骤创建一个 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 项目，该项目是第一次发布的。 现在，可以在 IDE 外部重现生成。

#### <a name="to-reproduce-the-build-from-the-command-line"></a>从命令行重现生成

1. 退出 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]。

2. 在 Windows 的 "**开始**" 菜单中，依次单击 "**所有程序**"、 **Microsoft Visual Studio**"、" **Visual Studio Tools**"、" **Visual Studio 命令提示**"。 这应该会在当前用户的根文件夹中打开一个命令提示符。

3. 在**Visual Studio 命令提示符下**，将当前目录更改为刚才生成的项目的位置。 例如，键入 `chdir My Documents\Visual Studio\Projects\CmdLineDemo`。

4. 若要删除 "创建并发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 项目" 中生成的现有文件，请键入 `rmdir /s publish`。

    此步骤是可选的，但它可确保新文件都是通过命令行生成生成的。

5. 键入 `msbuild /target:publish`。

   以上步骤会在名为**Publish**的项目的子文件夹中生成完整的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序部署。 *CmdLineDemo*是 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署清单。 文件夹*CmdLineDemo_1*包含 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中的文件*CmdLineDemo*和*CmdLineDemo。* Setup.exe 是引导*程序*，默认情况下配置为安装 .NET Framework。 Dotnetfx.exe 文件夹包含 .NET Framework 的可再发行组件。 这是通过 Web 或 UNC 或 CD/DVD 部署应用程序所需的整个文件集。
   
> [!NOTE]
> MSBuild 系统使用**PublishDir**选项来指定输出的位置，例如 `msbuild /t:publish /p:PublishDir="<specific location>"`。

## <a name="publish-properties"></a>发布属性
 在上述过程中发布应用程序时，发布向导会将以下属性插入项目文件中。 这些属性会直接影响 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的生成方式。

 在*CmdLineDemo. .vbproj* / *CmdLineDemo*：

```xml
<AssemblyOriginatorKeyFile>WindowsApplication3.snk</AssemblyOriginatorKeyFile>
<GenerateManifests>true</GenerateManifests>
<TargetZone>LocalIntranet</TargetZone>
<PublisherName>Microsoft</PublisherName>
<ProductName>CmdLineDemo</ProductName>
<PublishUrl>http://localhost/CmdLineDemo</PublishUrl>
<Install>true</Install>
<ApplicationVersion>1.0.0.*</ApplicationVersion>
<ApplicationRevision>1</ApplicationRevision>
<UpdateEnabled>true</UpdateEnabled>
<UpdateRequired>false</UpdateRequired>
<UpdateMode>Foreground</UpdateMode>
<UpdateInterval>7</UpdateInterval>
<UpdateIntervalUnits>Days</UpdateIntervalUnits>
<UpdateUrlEnabled>false</UpdateUrlEnabled>
<IsWebBootstrapper>true</IsWebBootstrapper>
<BootstrapperEnabled>true</BootstrapperEnabled>
```

 您可以在命令行重写这些属性中的任何属性，而无需更改项目文件本身。 例如，以下内容将生成不带引导程序的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序部署：

```cmd
msbuild /target:publish /property:BootstrapperEnabled=false
```

 发布属性在 "**项目设计器**" 的 "**发布**"、"**安全性**" 和 "**签名**" 属性页 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中进行控制。 下面是发布属性的说明，以及如何在应用程序设计器的各种属性页中设置每个属性的说明：

- `AssemblyOriginatorKeyFile` 确定用于对 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单进行签名的密钥文件。 此相同键还可用于为程序集分配强名称。 此属性在 "**项目设计器**" 的 "**签名**" 页上设置。

  在 "**安全**" 页上设置以下属性：

- **启用 ClickOnce 安全设置**确定是否生成 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单。 最初创建项目时，默认情况下 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单生成。 首次发布时，向导将自动打开此标志。

- **TargetZone**确定要发出到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中的信任级别。 可能的值包括 "Internet"、"LocalIntranet" 和 "Custom"。 Internet 和 LocalIntranet 将导致默认权限集发出到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的应用程序清单中。 LocalIntranet 是默认设置，基本上意味着完全信任。 Custom 指定仅在基本*app.config*文件中显式指定的权限将发送到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中。 *App.config*文件是部分清单文件，只包含信任信息定义。 它是一个隐藏的文件，当你在 "**安全**" 页上配置权限时，会自动将其添加到你的项目。

  以下属性是在 "**发布**" 页上设置的：

- `PublishUrl` 是在 IDE 中将应用程序发布到的位置。 如果 `InstallUrl` 或 `UpdateUrl` 属性均未指定，则会将其插入 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中。

- `ApplicationVersion` 指定 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的版本。 此版本号为四位数。 如果最后一个数字是 "*"，则会将 `ApplicationRevision` 替换为在生成时插入到清单中的值。

- `ApplicationRevision` 指定修订版本。 这是一个整数，每次在 IDE 中发布时都会递增。 请注意，对于在命令行中执行的生成，不会自动递增。

- `Install` 确定应用程序是已安装的应用程序还是从 Web 上运行的应用程序。

- `InstallUrl` （未显示）是用户将从中安装应用程序的位置。 如果已指定，则在启用 `IsWebBootstrapper` 属性时，此值将被刻录到*setup.exe 引导程序*。 如果未指定 `UpdateUrl`，还会将其插入应用程序清单中。

- `SupportUrl` （未显示）是在已安装的应用程序的 "**添加/删除程序**" 对话框中链接的位置。

  以下属性是在 "**应用程序更新**" 对话框中设置的，可从 "**发布**" 页访问。

- `UpdateEnabled` 指示应用程序是否应检查更新。

- `UpdateMode` 指定前台更新或后台更新。

- `UpdateInterval` 指定应用程序检查更新的频率。

- `UpdateIntervalUnits` 指定 `UpdateInterval` 值是否以小时、日或周为单位。

- `UpdateUrl` （未显示）是应用程序将从其接收更新的位置。 如果指定此值，则会将此值插入应用程序清单中。

  以下属性是在 "**发布选项**" 对话框中设置的，可从 "**发布**" 页访问。

- `PublisherName` 指定在安装或运行应用程序时显示的提示中所显示发布服务器的名称。 对于已安装的应用程序，它还用于指定 "**开始**" 菜单上的文件夹名称。

- `ProductName` 指定在安装或运行应用程序时显示的提示中所显示产品的名称。 对于已安装的应用程序，它还用于在 "**开始**" 菜单中指定快捷方式名称。

  以下属性是在 "**系统必备**" 对话框中设置的，可从 "**发布**" 页访问。

- `BootstrapperEnabled` 确定是否生成 setup.exe 引导*程序*。

- `IsWebBootstrapper` 确定 setup.exe 引导*程序*是通过 Web 还是在基于磁盘的模式下工作。

## <a name="installurl-supporturl-publishurl-and-updateurl"></a>InstallURL、SupportUrl、PublishURL 和 UpdateURL
 下表显示了用于 ClickOnce 部署的四个 URL 选项。

|URL 选项|描述|
|----------------|-----------------|
|`PublishURL`|如果要将 ClickOnce 应用程序发布到网站，则需要。|
|`InstallURL`|可选。 如果安装站点与 `PublishURL`不同，请设置此 URL 选项。 例如，可以将 `PublishURL` 设置为 FTP 路径，并将 `InstallURL` 设置为 Web URL。|
|`SupportURL`|可选。 如果支持站点与 `PublishURL`不同，请设置此 URL 选项。 例如，你可以将 `SupportURL` 设置为公司的客户支持网站。|
|`UpdateURL`|可选。 如果更新位置与 `InstallURL`不同，请设置此 URL 选项。 例如，可以将 `PublishURL` 设置为 FTP 路径，并将 `UpdateURL` 设置为 Web URL。|

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.Build.Tasks.GenerateBootstrapper>
- <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>
- <xref:Microsoft.Build.Tasks.GenerateDeploymentManifest>
- [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)

---
title: 安装 Visual Studio 2015 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
f1_keywords:
- vs.about
helpviewer_keywords:
- Visual Studio, installing
- installing Visual Studio
- server installations [Visual Studio]
- Setup [Visual Studio]
- install Visual Studio
- visual studio installer
ms.assetid: da049020-cfda-40d7-8ff4-7492772b620f
caps.latest.revision: 183
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: dc84fc135e59a43a05ce66186c4a44e9e31f8f2c
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851051"
---
# <a name="install-visual-studio-2015"></a>安装 Visual Studio 2015

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此页包含帮助安装“Visual Studio 2015”的详细信息，这是一款由开发人员工作效率工具组成的集成套件。 此外，还介绍了可帮助你快速了解有关 [功能](https://www.visualstudio.com/news/vs2015-vs.aspx)、 [版本](https://visualstudio.microsoft.com/en-US/products/compare-visual-studio-products-vs)、 [系统要求](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs)、 [下载](https://visualstudio.microsoft.com/downloads/)和更多信息的链接。

## <a name="quick-links"></a>快速链接

在我们深入了解详细信息之前，这里是最常用的链接列表。

|||
|------------------|----------------|
|![下载 Visual Studio](../install/media/downloads.png "下载") |**下载**：若要安装 Visual Studio 2015，你可以从 " [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) " 页下载产品可执行文件（需要订阅），或使用盒装产品中的安装媒体。 [了解有关如何下载当前版本或以前版本的 Visual Studio 的详细信息](https://www.visualstudio.com/vs/older-downloads/)。|
|![了解有关功能的详细信息](../install/media/features.png "特征") |**功能**：若要了解有关 Visual Studio 2015 中的功能的详细信息，请参阅[RTM](https://www.visualstudio.com/news/vs2015-vs)、 [update 1](https://www.visualstudio.com/news/vs2015-update1-vs)、 [update 2](https://www.visualstudio.com/news/vs2015-update2-vs)和[update 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs)的发行说明。|
|![了解每个 SKU 中的内容](../install/media/sku.png "SKU") |**SKU**：若要查看 Visual Studio 2015 各个版本中的可用功能，请参阅我们的[比较 Visual Studio 产品](https://visualstudio.microsoft.com/en-US/products/compare-visual-studio-products-vs)页。|
|![查看系统要求](../install/media/system-requirements.png "系统需求") |**系统要求**：若要查看每个版本的 visual studio 2015 的系统要求，请参阅[Visual Studio 2015 兼容性](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs)页。|
|![找到你的产品密钥](../install/media/product-keys.png "产品密钥") |**产品密钥**：若要查找产品密钥，请参阅[如何：查找 Visual Studio 产品密钥](../install/how-to-locate-the-visual-studio-product-key.md)主题。|
|![了解许可](../install/media/licensing.png "许可") |**许可**：若要了解个人或企业客户的许可选项，请参阅[VISUAL Studio 和 MSDN 许可](https://www.microsoft.com/download/details.aspx?id=13350)白皮书。|

## <a name="custom"></a>默认值与自定义设置
 在安装 Visual Studio 2015 时，你可以包括或排除你每天都会使用的组件。 这意味着，默认安装比自定义安装所占用的空间更小，安装速度更快。 这还意味着在以前的版本中，默认安装的许多组件现在被视为必须在此版本中显式选择的自定义组件。

 ![Visual Studio 2015 安装对话框](../ide/media/vs2015-setup-screen.png "VS2015_Setup_screen")

 自定义组件包括 Visual C++、Visual F#、SQL Server Data Tools、跨平台移动工具和 SDK，以及第三方 SDK 和扩展。 如果在初始安装过程中没有选择这些自定义组件，则可以在之后安装任何自定义组件。

> [!NOTE]
> 自定义安装自动包含默认安装中的组件。

 自定义组件的完整列表如下所示：

|功能集|组件数|
|------------------|----------------|
|**更新**|Visual Studio 2015 Update 3|
|**编程语言**|Visual C++<br />Visual F#<br />Python Tools for Visual Studio|
|**Windows 和 Web 开发**|ClickOnce 发布工具<br />LightSwitch<br />Microsoft Office 开发人员工具<br />Microsoft SQL Server Data Tools<br /> Microsoft Web 开发人员工具<br />PowerShell Tools for Visual Studio （第三方）<br />Silverlight 开发工具包<br />通用 Windows 应用开发工具<br />Windows 10 工具和 SDK<br />Windows 8.1 和 Windows Phone 8.0/8.1 工具<br />Windows 8.1 工具和 SDK|
|**跨平台移动开发**|C#/.NET (Xamarin)<br />HTML/JavaScript (Apache Cordova)<br />适用于 iOS/Android 的 Visual C++ 移动开发<br />Clang with Microsoft CodeGen|
|**常用工具和软件开发工具包**|Android 本机开发工具包（第三方）<br /> Android SDK [第三方]<br />Android SDK 安装 Api （第三方）<br />Apache Ant （第三方）<br /> Java SE 开发工具包（第三方）<br /> Joyent node.js （第三方）|
|**常用工具**|Git for Windows （第三方）<br />适用于 Visual Studio 的 GitHub 扩展（第三方）<br /> Visual Studio 扩展性工具|

## <a name="installing"></a>安装 Visual Studio
 你可以通过使用安装媒体（Dvd）、从[My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015)网站下载 web 安装程序、从[visual studio 下载](https://visualstudio.microsoft.com/downloads/)网站下载 web 安装程序或通过创建脱机安装布局（有关详细信息，请参阅[创建 Visual studio 的脱机安装](../install/create-an-offline-installation-of-visual-studio.md)页）安装 visual studio。

> [!IMPORTANT]
> 你必须具有管理员凭据才能安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 但是，在安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 之后，在使用时不需要凭据。

 你的本地管理员帐户必须启用以下权限才能在 Visual Studio 中安装任意内容。

|本地策略对象显示名称|用户权限|
|--------------------------------------|----------------|
|备份文件和目录|SeBackupPrivilege|
|调试程序|SeDebugPrivilege|
|管理审核和安全日志|Sesecurityprivilege|

 有关此本地管理员帐户要求的详细信息，请参阅知识库文章： [如果安装帐户没有某些用户权限，则 SQL Server 安装失败](https://support.microsoft.com/kb/2000257)。

### <a name="BKMK_Media"></a>使用安装媒体
 若要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]安装媒体上的根目录中安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，请运行所需版本的安装文件：

|版本类别|安装文件|
|-------------|-----------------------|
|Visual Studio Enterprise|vs_enterprise.exe|
|Visual Studio Professional|vs_professional.exe|
|Visual Studio Community|vs_community.exe|

### <a name="BKMK_Website"></a>从产品网站下载
 访问[Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页，然后选择所需的 visual studio 版本。

### <a name="downloading-from-your-subscription-service"></a>正在从订阅服务下载
 访问 " [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) " 页，然后选择所需的 Visual Studio 版本。

### <a name="BKMK_Offline"></a>创建脱机安装布局
 如果你没有 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 安装媒体，或者没有 Visual Studio 订阅，或者你不希望使用 web 安装程序安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，则可以通过创建所谓的脱机安装布局来执行 "断开连接" 安装。 有关详细信息，请参阅[创建 Visual Studio 的脱机安装](../install/create-an-offline-installation-of-visual-studio.md)页。

## <a name="enterprise"></a>在企业中部署 Visual Studio
 有关如何通过网络部署 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的信息，请参阅[Visual Studio 管理员指南](../install/visual-studio-administrator-guide.md)。

### <a name="BKMK_Virtualized"></a>在虚拟化环境中安装 Visual Studio
 **有关 HYPER-V 的视频问题**

 如果你运行的 Windows Server 2008 R2 启用了 Hyper-V 并包含加速图形适配器，则你可能会遇到系统速度下降的情况。

 有关详细信息，请参阅 Microsoft 网站上的以下页面： [在基于 Windows Server 2008 或 Windows Server 2008 R2 的计算机启用了 Hyper-V 角色并安装加速显示适配器时，视频性能可能会降低](https://support.microsoft.com/kb/961661)。

 **使用 HYPER-V 模拟设备**

 在不包含虚拟化的真实硬件上安装 Visual Studio 2015 时，你可以选择对使用 Hyper-V 的 Windows 和 Android 设备启用模拟的功能。 安装到 Hyper-V 中时，你将无法模拟 Windows 或 Android 设备。 这是因为仿真程序本身就是虚拟机，并且当前无法将 VM 托管在另一个 VM 内部。 解决方法是拥有能够直接在上面部署和调试应用程序的真正的 Windows 和 Android 设备。

## <a name="optionalComponents"></a>安装可选组件
 如果要安装在初始安装过程中可能未选择的组件，请使用以下过程。

#### <a name="to-install-optional-components"></a>安装可选组件

1. 在“控制面板”上的“程序和功能” 页中，选择要将一个或多个组件添加到的产品版本，然后选择“更改”。

2. 在安装向导中，选择“修改”，然后选择想要安装的组件。

3. 选择“下一步”，然后按照其余说明进行操作。

## <a name="helpContent"></a>安装脱机帮助内容
 安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]之后，为了可脱机使用，可以下载其他帮助内容。

#### <a name="to-install-or-uninstall-help-content"></a>安装或卸载帮助内容

1. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 菜单栏上，选择“帮助”和“添加和移除帮助内容”。

2. 在“Microsoft 帮助查看器” 的“管理内容”选项卡上，选择你的帮助内容对应的安装源。

3. 如果要查找特定的帮助集合，请在“搜索”文本框中输入名称或关键字，然后按 Enter。

4. 在所需帮助集合的名称旁边，选择“添加” 或“移除” 链接。

5. 单击 "**更新**" 按钮。

   有关如何安装或部署脱机帮助的详细信息，请参阅[帮助查看器管理员指南](../ide/help-viewer-administrator-guide.md)。

## <a name="serviceReleases"></a>检查是否有 Service Release 和产品更新
 因为并非所有扩展都兼容，所以从 Visual Studio 早期版本进行升级时，不会自动升级扩展。 您必须从[Visual Studio Marketplace](https://marketplace.visualstudio.com/)或软件发行者重新安装这些扩展。

#### <a name="to-automatically-check-for-service-releases"></a>自动检查是否有 Service Release

1. 在菜单栏上，依次选择“工具”、“选项”。

2. 在“选项” 对话框中，展开“环境”，然后选择“扩展和更新”。 请确保已选中“自动检查更新” 复选框，然后选择“确定”。

## <a name="registering-visual-studio"></a>注册 Visual Studio

1. 在菜单栏上，依次选择“帮助”和“关于”。

     “关于” 对话框显示产品标识号 (PID)。 需使用 PID 和 Windows 帐户凭据（如 Hotmail 或 Outlook.com 电子邮件地址和密码）来注册产品。

2. 在菜单栏上，选择“帮助”和“注册产品”。

## <a name="repair"></a>修复 Visual Studio

#### <a name="to-repair-visual-studio"></a>要修复 Visual Studio

1. 在“控制面板”上的“程序和功能” 页中，选择要修复的产品版本，然后选择“更改”。

2. 在安装向导中，选择“修复”，再选择“下一步”，然后按照其余说明进行操作。

#### <a name="to-repair-visual-studio-in-silent-or-passive-modes-that-is-to-repair-from-source"></a>在无提示或被动模式下（即从源修复）修复 Visual Studio

1. 在安装了 Visual Studio 的计算机上，打开 Windows 命令提示符。

2. 输入以下参数：

     *DVDRoot* \\< 安装文件\> \</quiet&#124;/passive > [/norestart]/Repair

## <a name="troubleshooting"></a>排查安装问题
 使用这些资源来获取关于设置和安装问题的帮助：

- [Visual Studio Setup and Installation（Visual Studio 设置和安装）](https://social.msdn.microsoft.com/Forums/en-US/vssetup/threads) 论坛。 查看 Visual Studio 社区中他人的问题和回答。 如果未找到所需的帮助，可自行提问。

- [Microsoft Support for Visual Studio（针对 Visual Studio 的 Microsoft 支持）](https://support.microsoft.com/ph/1117) 网站。 阅读知识库 (KB) 文章并了解如何联系 Microsoft 支持，以获取有关 Visual Studio 安装问题的信息。

## <a name="relatedTopics"></a>相关主题

|职务|描述|
|-----------|-----------------|
|[创建 Visual Studio 的脱机安装](../install/create-an-offline-installation-of-visual-studio.md)|介绍如何在未连接到 Internet 时安装 Visual Studio。
|[并行安装 Visual Studio 版本](../install/install-visual-studio-versions-side-by-side.md)|提供有关如何在同一台计算机上安装多个 Visual Studio 版本的信息。|
|[使用命令行参数安装 Visual Studio](/visualstudio/install/use-command-line-parameters-to-install-visual-studio)|列出在通过命令提示符安装 Visual Studio 时可以使用的命令行参数。|
|[卸载 Visual Studio](../install/uninstall-visual-studio.md)|介绍如何卸载 Visual Studio。|
|[Visual Studio 管理员指南](../install/visual-studio-administrator-guide.md)|提供有关 Visual Studio 部署选项的信息。|
|[Visual Studio 图像库](../designers/the-visual-studio-image-library.md)|提供有关如何安装可在 Visual Studio 应用程序中使用的图形的信息。|
|[Visual Studio 开发入门](../ide/get-started-developing-with-visual-studio.md)|包括有助于更有效地使用 Visual Studio 的信息和链接。|

## <a name="see-also"></a>请参阅

- [登录 Visual Studio](../ide/signing-in-to-visual-studio.md)

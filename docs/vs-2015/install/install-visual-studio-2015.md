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
ms.openlocfilehash: a31bc328c20aada21b05edeef61886d57e914165
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298051"
---
# <a name="install-visual-studio-2015"></a>安装 Visual Studio 2015

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此页包含帮助安装“Visual Studio 2015”的详细信息，这是一款由开发人员工作效率工具组成的集成套件。 此外，还介绍了可帮助你快速了解有关 [功能](https://www.visualstudio.com/news/vs2015-vs.aspx)、 [版本](https://go.microsoft.com/fwlink/?LinkID=242142)、 [系统要求](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs)、 [下载](https://go.microsoft.com/fwlink/?LinkId=517106)和更多信息的链接。

## <a name="quick-links"></a>快速链接

在我们深入了解详细信息之前，这里是最常用的链接列表。

|||
|------------------|----------------|
|![下载 Visual Studio](../install/media/downloads.png "下载") |**Downloads**: To install Visual Studio 2015, you can download a product executable file from the  [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) page (subscription required), or use the installation media from the boxed product. [Learn more about how to download current or previous versions of Visual Studio](https://www.visualstudio.com/vs/older-downloads/).|
|![Learn more about features](../install/media/features.png "特征") |**Features**: To learn  more about the features in Visual Studio 2015, see the release notes for [RTM](https://www.visualstudio.com/news/vs2015-vs), [Update 1](https://www.visualstudio.com/news/vs2015-update1-vs), [Update 2](https://www.visualstudio.com/news/vs2015-update2-vs), and [Update 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs).|
|![Find out what's in each SKU](../install/media/sku.png "SKU") |**SKU**：若要查看 Visual Studio 2015 各个版本中的可用功能，请参阅我们的[比较 Visual Studio 产品](https://go.microsoft.com/fwlink/?LinkID=242142)页。|
|![View system requirements](../install/media/system-requirements.png "系统要求") |**System Requirements**: To view the system requirements for each edition of Visual Studio 2015, see the [Visual Studio 2015 Compatibility](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs) page.|
|![Locate your Product Key](../install/media/product-keys.png "产品密钥") |**Product Keys**: To locate your product key, see the [How to: Locate the Visual Studio Product Key](../install/how-to-locate-the-visual-studio-product-key.md) topic.|
|![Find out about licensing](../install/media/licensing.png "授权") |**Licensing**: To find out about licensing options for both individuals or enterprise customers, see  the [Visual Studio and MSDN Licensing](https://www.microsoft.com/download/details.aspx?id=13350) white paper.|

## <a name="custom"></a> Default vs. Custom Setup
 在安装 Visual Studio 2015 时，你可以包括或排除你每天都会使用的组件。 这意味着，默认安装比自定义安装所占用的空间更小，安装速度更快。 这还意味着在以前的版本中，默认安装的许多组件现在被视为必须在此版本中显式选择的自定义组件。

 ![Visual Studio 2015 Setup Dialog](../ide/media/vs2015-setup-screen.png "VS2015_Setup_screen")

 自定义组件包括 Visual C++、Visual F#、SQL Server Data Tools、跨平台移动工具和 SDK，以及第三方 SDK 和扩展。 如果在初始安装过程中没有选择这些自定义组件，则可以在之后安装任何自定义组件。

> [!NOTE]
> 自定义安装自动包含默认安装中的组件。

 自定义组件的完整列表如下所示：

|Feature Sets|组件数|
|------------------|----------------|
|**更新**|Visual Studio 2015 Update 3|
|**编程语言**|Visual C++<br />Visual F#<br />Visual Studio 的 Python 工具|
|**Windows 和 Web 开发**|ClickOnce 发布工具<br />LightSwitch<br />Microsoft Office 开发人员工具<br />Microsoft SQL Server Data Tools<br /> Microsoft Web 开发人员工具<br />PowerShell Tools for Visual Studio (3rd Party)<br />Silverlight 开发工具包<br />通用 Windows 应用开发工具<br />Windows 10 工具和 SDK<br />Windows 8.1 和 Windows Phone 8.0/8.1 工具<br />Windows 8.1 工具和 SDK|
|**跨平台移动开发**|C#/.NET (Xamarin)<br />HTML/JavaScript (Apache Cordova)<br />适用于 iOS/Android 的 Visual C++ 移动开发<br />Clang with Microsoft CodeGen|
|**Common Tools and Software Development Kits**|Android Native Development Kit (3rd Party)<br /> Android SDK [3rd Party]<br />Android SDK Setup APIs (3rd Party)<br />Apache Ant (3rd Party)<br /> Java SE Development Kit (3rd Party)<br /> Joyent Node.js (3rd Party)|
|**常用工具**|Git for Windows (3rd Party)<br />GitHub Extension for Visual Studio (3rd Party)<br /> Visual Studio 扩展性工具|

## <a name="installing"></a>安装 Visual Studio
 You can install Visual Studio by using installation media (DVDs), by using your Visual Studio subscription service from the [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) website, by downloading  a web installer from the [Visual Studio Downloads](https://go.microsoft.com/fwlink/?LinkId=517106) website, or by creating an offline installation layout (see the [Create an Offline Installation of Visual Studio](../install/create-an-offline-installation-of-visual-studio.md) page for more details).

> [!IMPORTANT]
> 你必须具有管理员凭据才能安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 但是，在安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 之后，在使用时不需要凭据。

 你的本地管理员帐户必须启用以下权限才能在 Visual Studio 中安装任意内容。

|本地策略对象显示名称|用户权限|
|--------------------------------------|----------------|
|备份文件和目录|SeBackupPrivilege|
|调试程序|SeDebugPrivilege|
|管理审核和安全日志|Sesecurityprivilege|

 有关此本地管理员帐户要求的详细信息，请参阅知识库文章： [如果安装帐户没有某些用户权限，则 SQL Server 安装失败](https://support.microsoft.com/kb/2000257)。

### <a name="BKMK_Media"></a> Using installation media
 若要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]安装媒体上的根目录中安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，请运行所需版本的安装文件：

|版本|安装文件|
|-------------|-----------------------|
|Visual Studio Enterprise|vs_enterprise.exe|
|Visual Studio Professional|vs_professional.exe|
|Visual Studio Community|vs_community.exe|

### <a name="BKMK_Website"></a> Downloading from the product website
 Visit the [Visual Studio Downloads](https://go.microsoft.com/fwlink/?LinkId=517106) page, and select the edition of Visual Studio that you want.

### <a name="downloading-from-your-subscription-service"></a>Downloading from your subscription service
 Visit  the [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) page, and select the edition of Visual Studio that you want.

### <a name="BKMK_Offline"></a> Creating an offline installation layout
 If you do not have the [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] installation media, or you do not have a Visual Studio subscription,  or you do not want to install [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] by using the web installer, you can perform a "disconnected" installation by creating what is known as an offline installation layout. For more information, see the [Create an Offline Installation of Visual Studio](../install/create-an-offline-installation-of-visual-studio.md) page.

## <a name="enterprise"></a> Deploying Visual Studio in an Enterprise
 For information about how to deploy [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] over a network, see the [Visual Studio Administrator Guide](../install/visual-studio-administrator-guide.md).

### <a name="BKMK_Virtualized"></a> Installing Visual Studio in a virtualized environment
 **有关 HYPER-V 的视频问题**

 如果你运行的 Windows Server 2008 R2 启用了 Hyper-V 并包含加速图形适配器，则你可能会遇到系统速度下降的情况。

 有关详细信息，请参阅 Microsoft 网站上的以下页面： [在基于 Windows Server 2008 或 Windows Server 2008 R2 的计算机启用了 Hyper-V 角色并安装加速显示适配器时，视频性能可能会降低](https://go.microsoft.com/fwlink/?LinkID=231084)。

 **使用 HYPER-V 模拟设备**

 在不包含虚拟化的真实硬件上安装 Visual Studio 2015 时，你可以选择对使用 Hyper-V 的 Windows 和 Android 设备启用模拟的功能。 安装到 Hyper-V 中时，你将无法模拟 Windows 或 Android 设备。 这是因为仿真程序本身就是虚拟机，并且当前无法将 VM 托管在另一个 VM 内部。 解决方法是拥有能够直接在上面部署和调试应用程序的真正的 Windows 和 Android 设备。

## <a name="optionalComponents"></a> Installing optional components
 If you want to install components that you might not have selected during your original installation, use the following procedure.

#### <a name="to-install-optional-components"></a>To install optional components

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

5. Click the **Update** button.

   For more information about how to install or deploy offline Help, see the [Help Viewer Administrator Guide](../ide/help-viewer-administrator-guide.md).

## <a name="serviceReleases"></a>检查是否有 Service Release 和产品更新
 因为并非所有扩展都兼容，所以从 Visual Studio 早期版本进行升级时，不会自动升级扩展。 You must reinstall the extensions from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/) or from the software publisher.

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

#### <a name="to-repair-visual-studio-in-silent-or-passive-modes-that-is-to-repair-from-source"></a>To repair Visual Studio in silent or passive modes (that is, to repair from source)

1. 在安装了 Visual Studio 的计算机上，打开 Windows 命令提示符。

2. 输入以下参数：

     *DVDRoot* \\<Installation File\> \</quiet&#124;/passive> [/norestart]/Repair

## <a name="troubleshooting"></a> Troubleshooting an installation
 使用这些资源来获取关于设置和安装问题的帮助：

- [Visual Studio Setup and Installation（Visual Studio 设置和安装）](https://go.microsoft.com/fwlink/?LinkID=151190) 论坛。 查看 Visual Studio 社区中他人的问题和回答。 如果未找到所需的帮助，可自行提问。

- [Microsoft Support for Visual Studio（针对 Visual Studio 的 Microsoft 支持）](https://go.microsoft.com/fwlink/?LinkID=251019) 网站。 阅读知识库 (KB) 文章并了解如何联系 Microsoft 支持，以获取有关 Visual Studio 安装问题的信息。

## <a name="relatedTopics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[创建 Visual Studio 的脱机安装](../install/create-an-offline-installation-of-visual-studio.md)|Describes how to install Visual Studio when you are not connected to the Internet.
|[并行安装 Visual Studio 版本](../install/install-visual-studio-versions-side-by-side.md)|提供有关如何在同一台计算机上安装多个 Visual Studio 版本的信息。|
|[使用命令行参数安装 Visual Studio](/visualstudio/install/use-command-line-parameters-to-install-visual-studio)|Lists the command-line parameters that you can use when you install Visual Studio from a command prompt.|
|[卸载 Visual Studio](../install/uninstall-visual-studio.md)|Describes how to uninstall Visual Studio.|
|[Visual Studio 管理员指南](../install/visual-studio-administrator-guide.md)|提供有关 Visual Studio 部署选项的信息。|
|[Visual Studio 图像库](../designers/the-visual-studio-image-library.md)|提供有关如何安装可在 Visual Studio 应用程序中使用的图形的信息。|
|[Visual Studio 开发入门](../ide/get-started-developing-with-visual-studio.md)|Includes information and links that can help you use Visual Studio more effectively.|

## <a name="see-also"></a>请参阅

- [登录 Visual Studio](../ide/signing-in-to-visual-studio.md)
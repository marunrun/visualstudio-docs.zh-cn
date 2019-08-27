---
title: 使用命令行参数安装 Visual Studio 2015 |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
f1_keywords:
- command-line parameters
- switches
- command prompt
ms.assetid: 480f3cb4-d873-434e-a8bf-82cff7401cf2
caps.latest.revision: 10
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: a3fe0233f08f33535be4b02cc06c29d919d75169
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180249"
---
# <a name="use-command-line-parameters-to-install-visual-studio"></a>使用命令行参数安装 Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[使用命令行参数安装 Visual Studio](/visualstudio/install/use-command-line-parameters-to-install-visual-studio)。

在命令提示符下安装 Visual Studio 2015 时，可以使用以下命令行参数（也称为开关）。

> [!NOTE]
> 请确保使用实际的安装程序而不是引导程序文件。 例如，请确保你使用 **`vs_enterprise.exe`** 而不是 vs_enterprise_*GUID*.exe。 您可以下载的安装程序从[My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015)。

## <a name="list-of-command-line-parameters"></a>命令行参数列表

Visual Studio 命令行参数不区分大小写。

|参数|描述|
|---------------|-----------------|
|**/?**<br /><br /> **/help**<br /><br /> **/h**|显示命令行参数。|
|/AddRemoveFeatures |指定要在安装的产品中添加或移除的功能。|
|/AdminFile AdminDeployment.xml  |使用你为管理安装指定的数据文件安装 Visual Studio。|
|/ ChainingPackage BundleName  |指定此捆绑包链接到的捆绑包。 还可用于指定客户改善体验队列。|
|/ CreateAdminFile\<filename> |指定用于创建可与 /AdminFile 一起使用的控制文件的位置|
|/CustomInstallPath InstallationDirectory  |在你指定的目录中安装所有可重定目标的包。|
|/ForceRestart |安装完成后始终重新启动计算机。|
|**/full**|安装所有产品功能。|
|/InstallSelectableItems \<item name 1>[;\<item name 2>] |要在安装程序向导选择屏幕上检查的选择树项列表。|
|**/l**<br /><br /> /Log Filename  |指定日志文件的位置。|
|/layout Directory  |将安装媒体上的文件复制到你指定的目录。|
|**/NoCacheOnlyMode**|阻止包缓存的预填充。|
|**/NoRefresh**|禁止检查此产品的较新版本是否存在必需或推荐的更新版本。|
|**/norestart**|在安装期间或安装完成后，阻止安装应用程序重新启动计算机。 请参阅 [Visual Studio 管理员指南](../install/visual-studio-administrator-guide.md)的返回代码部分了解查找的返回代码。|
|**/noweb**|阻止从 Internet 中安装。|
|**/ OverrideFeedUri\<馈送文件的路径 >**|本地外部源的路径，它描述软件项|
|**/ProductKey**<br /><br /> *ProductKey*|设置不包含短划线且不超过 25 个字符的自定义产品密钥。|
|**/PromptRestart**|在重新启动计算机之前提示用户。|
|**/q**<br /><br /> **/quiet**<br /><br /> **/s**<br /><br /> **/Silent**|取消安装应用程序的用户界面 (UI)。 如果已安装 Visual Studio，并且你除了这个参数之外未指定任何参数，则在维护模式下运行安装应用程序。|
|**/qb**<br /><br /> **/passive**|显示进度，但不等待用户输入。|
|**/repair**|修复 Visual Studio。|
|**/SuppressRefreshPrompt**|禁止在安装向导中显示更新可用对话框，因此安装向导将自动接受任意必需或推荐更新版本。|
|/u <br /><br /> **/Uninstall**|卸载 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。|
|**/Uninstall /Force**<br /><br /> /u /force |卸载 Visual Studio 以及与其他产品共享的所有功能。 **警告：** 如果使用此参数，则在同一台计算机上安装的其他产品可能会停止正常工作。|

## <a name="see-also"></a>请参阅

- [Visual Studio 管理员指南](../install/visual-studio-administrator-guide.md)
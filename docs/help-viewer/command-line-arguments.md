---
title: Help Content Manager 的命令行参数
ms.date: 11/01/2017
ms.topic: reference
ms.assetid: 3aa9890a-1147-42ba-adea-17935d184038
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d9bead01c6440d5232a91a5e8fe2007b3e30340c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72631968"
---
# <a name="command-line-arguments-for-the-help-content-manager"></a>Help Content Manager 的命令行参数

可以使用 Help Content Manager (HlpCtntMgr.exe) 的命令行参数指定如何部署和管理本地帮助内容。 必须以管理员权限运行此命令行工具的脚本，无法以服务形式运行这些脚本。 可以使用此工具执行以下任务：

- 从磁盘或云添加或更新本地帮助内容。

- 移除本地帮助内容。

- 移动本地帮助内容存储区。

- 以无提示方式添加、更新、移除或移动本地帮助内容。

语法：

```cmd
HlpCtntmgr.exe /operation Value /catalogname CatalogName /locale Locale /sourceuri InstallationPoint
```

例如:

```cmd
hlpctntmgr.exe /operation install /catalogname VisualStudio15 /locale en-us /sourceuri d:\productDocumentation\HelpContentSetup.msha
```

>[!NOTE]
> 对于 Visual Studio 2017 和 Visual Studio 2019，目录名称为 VisualStudio15。 这可能是意外情况，但这是因为这两个 Visual Studio 版本使用的是相同的帮助查看器。

## <a name="switches-and-arguments"></a>开关和参数

下表定义了可以用于 Help Content Manager 的命令行工具的开关和参数：

|开关|是否必需？|自变量|
|------------|---------------|---------------|
|/operation|是|-   **Install** -- 将书籍从指定安装源添加到本地内容存储区。<br />     此开关需要 /booklist 自变量、/sourceURI 自变量或两者。 如果未指定 /sourceURI 参数，则默认 Visual Studio URI 用作安装源。 如果未指定 /booklist 变量，则会安装 /sourceUri 上的所有书籍。<br />-   **Uninstall** -- 从本地内容存储区中删除指定的书籍。<br />     此开关需要 /booklist 自变量或 /sourceURI 自变量。  如果指定 /sourceURI 自变量，则会移除所有书籍，并且会忽略 /booklist 自变量。<br />-   **Move** -- 将本地存储区移动到指定的路径。 默认本地存储区路径设置为 %ProgramData% 下的目录<br />     此开关需要 /locationPath 和 /catalogName 自变量。 如果指定的路径无效或驱动器未包含足够的可用空间来存放内容，则会在事件日志中记录错误消息。<br />-   **Refresh** -- 更新自安装或最近更新以来已更改的主题。<br />     此开关需要 /sourceURI 自变量。|
|/catalogName|是|指定内容目录的名称。 对于 Visual Studio 2017 和 Visual Studio 2019，这是 VisualStudio15。|
|/locale|No|为 Help Viewer 的当前实例指定用于查看和管理内容的产品区域设置。 例如，可为美国英语指定 `EN-US`。<br /><br /> 如果未指定区域设置，则使用操作系统的区域设置。 如果无法确定该区域设置，则使用 `EN-US`。<br /><br /> 如果指定了无效的区域设置，则会在事件日志中记录错误消息。|
|/e|No|如果当前用户具有管理凭据，则会将 Help Content Manager 提升为管理特权。|
|/sourceURI|No|指定从中安装内容的 URL（服务 API）或内容安装文件 (.msha) 的路径。 该 URL 可以指向 Visual Studio 2010 样式终结点中的产品组（顶级节点）或产品书籍（叶级节点）。 无需在 URL 的末尾包含斜杠 (/)。 如果确实要包含尾部斜线，则会对它进行相应处理。<br /><br /> 如果找不到指定的文件、或者该文件无效或无法访问，或是如果与 Internet 的连接不可用或在管理内容时中断，则会在事件日志中记录错误消息。|
|/vendor|No|指定将移除的产品内容的供应商（例如 `Microsoft`）。 此开关的默认参数是 Microsoft。|
|/productName|No|指定将删除的书籍的产品名。 产品名在随内容附带的 helpcontentsetup.msha 或 books.html 文件中标识。 一次只能从一个产品中移除书籍。 若要从多个产品中移除书籍，必须执行多个安装。|
|/booklist|No|指定要管理的书籍的名称（用空格分隔）。 值必须与安装媒体上列出的书籍名匹配。<br /><br /> 如果未指定此参数，则会安装 /sourceURI 中指定产品的所有推荐书籍。<br /><br /> 如果书籍的名称包含一个或多个空格，请在它两边添加双引号 (")，以便正确地分隔列表。<br /><br /> 如果指定的 /sourceURI 无效或无法访问，则会记录错误消息。|
|/skuId|No|指定安装源中的产品的库存单位 (SKU)，并筛选 /SourceURI 开关标识的书籍。|
|/membership|No|-   **Minimum** -- 基于使用 /skuId 开关指定的 SKU 安装最小帮助内容集。 SKU 与内容集之间的映射在服务 API 中进行公开。<br />-   **Recommended** -- 针对使用 /skuId 参数指定的 SKU 安装一组推荐书籍。 安装源是服务 API 或 .MSHA。<br />-   **Full** -- 针对使用 /skuId 参数指定的 SKU 安装整套书籍。 安装源是服务 API 或 .MSHA。|
|/locationpath|No|指定本地帮助内容的默认文件夹。 必须仅使用此开关安装或移动内容。 如果指定此开关，则还必须指定 /silent 开关。|
|/silent|No|安装或移除帮助内容，而不提示用户或显示任何 UI（包括状态通知区域中的图标）。 输出会记录到 %Temp% 目录中的文件。 重要提示：若要以无提示方式安装内容，必须使用数字签名的 .cab 文件，而不能使用 .mshc 文件。|
|/launchingApp|No|当在没有父应用程序的情况下启动帮助查看器时，定义应用程序和目录上下文。 此开关的参数是 CompanyName、ProductName 和 VersionNumber（例如 `/launchingApp Microsoft,VisualStudio,16.0`）。<br /><br /> 使用 /silent 参数安装内容时需要此开关。|
|/wait Seconds|No|暂停安装、卸载和刷新操作。 如果操作已在对目录进行，则进程会等待给定秒数，然后继续。 使用 0 表示无限期等待。|
|/?|No|列出 Help Content Manager 的命令行工具的开关及其说明。|

### <a name="exit-codes"></a>退出代码

在静默模式下运行 Help Content Manager 的命令行工具时，它会返回以下退出代码：

```
Success = 0,

FailureToElevate = 100
InvalidCmdArgs = 101,
FailOnFetchingOnlineContent = 110,
FailOnFetchingContentFromDisk = 120,
FailOnFetchingInstalledBooks = 130,
NoBooksToUninstall = 200,
NoBooksToInstall = 300,
FailOnUninstall = 400,
FailOnInstall = 500,
FailOnMove = 600,
FailOnUpdate = 700,
FailOnRefresh = 800,
Cancelled = 900,
Others = 999,
ContentManagementDisabled = 1200,
OnlineHelpPreferenceDisabled = 1201
UpdateAlreadyRunning = 1300 - (Signals that the update didn't run because another was in progress.)
```

## <a name="see-also"></a>请参阅

- [Help Viewer 管理员指南](../help-viewer/administrator-guide.md)
- [Help Content Manager 重写](../help-viewer/behavior-overrides.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)
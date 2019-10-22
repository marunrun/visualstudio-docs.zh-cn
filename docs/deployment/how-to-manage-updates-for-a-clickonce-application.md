---
title: 如何：管理 ClickOnce 应用程序的更新 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.Update
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, managing applications
- ClickOnce deployment, updates
- updating data, ClickOnce
- application updates
ms.assetid: a3f23f05-e7f1-4620-b23c-2d68f9643684
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ba899e922e98817462b06a1693525ab1ae69e20
ms.sourcegitcommit: a1e899248adaf104697fa7dea32a36e69e9cc119
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2019
ms.locfileid: "71159903"
---
# <a name="how-to-manage-updates-for-a-clickonce-application"></a>如何：管理 ClickOnce 应用程序的更新
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序可以自动或以编程方式检查更新。 作为开发人员，您可以很灵活地指定何时以及如何执行更新检查、是否需要更新以及应用程序应检查更新的位置。

 你可以将应用程序配置为在应用程序启动前自动检查是否有更新，或在应用程序启动后按设置的时间间隔。 此外，还可以指定所需的最低版本;也就是说，如果用户的版本低于所需版本，则会安装更新。

 你可以将应用程序配置为基于事件（例如用户请求）以编程方式检查更新。 本主题中的 "以编程方式检查更新" 过程说明如何编写使用<xref:System.Deployment.Application.ApplicationDeployment>类的代码，以便基于事件检查更新。

 你还可以从一个位置部署你的应用程序，并从另一个位置进行更新。 请参阅过程 "指定其他更新位置"。

 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

 在 "**应用程序更新**" 对话框（可从 "**项目设计器**" 的 "**发布**" 页获得）中管理更新行为。

### <a name="to-check-for-updates-before-the-application-starts"></a>在应用程序启动前检查更新

1. 在“解决方案资源管理器”中选择了项目的情况下，在“项目” 菜单上单击“属性”。

2. 单击“发布”选项卡。

3. 单击 "**更新**" 按钮以打开 "**应用程序更新**" 对话框。

4. 在 "**应用程序更新**" 对话框中，确保选中 "**应用程序应检查更新"** 复选框。

5. 在 "**选择应用程序何时应该检查更新**" 部分中，选择 **"在应用程序启动之前**"。 这可确保连接到网络的用户始终运行包含最新更新的应用程序。

### <a name="to-check-for-updates-in-the-background-after-the-application-starts"></a>在应用程序启动后在后台检查更新

1. 在“解决方案资源管理器”中选择了项目的情况下，在“项目” 菜单上单击“属性”。

2. 单击“发布”选项卡。

3. 单击 "**更新**" 按钮以打开 "**应用程序更新**" 对话框。

4. 在 "**应用程序更新**" 对话框中，确保选中 "**应用程序应该检查更新**" 复选框。

5. 在 "**选择应用程序何时应该检查更新" 部分**中，选择 **"在应用程序启动后**"。 应用程序将以这种方式开始更快速地启动，然后它将在后台检查更新，并且仅在更新可用时通知用户。 安装后，在应用程序重新启动之前，更新将不会生效。

6. 在 "**指定应用程序检查更新的频率**" 部分中，选择 "**每次运行应用程序时检查**" （默认）或 "**检查每个**" 并输入一个数字和时间间隔。

### <a name="to-specify-a-minimum-required-version-for-the-application"></a>指定应用程序所需的最低版本

1. 在“解决方案资源管理器”中选择了项目的情况下，在“项目” 菜单上单击“属性”。

2. 单击“发布”选项卡。

3. 单击 "**更新**" 按钮以打开 "**应用程序更新**" 对话框。

4. 在 "**应用程序更新**" 对话框中，确保选中 "**应用程序应检查更新"** 复选框。

5. 选中 "**指定此应用程序所需的最低版本**" 复选框，然后输入应用程序的**主**版本号、**次**版本号、**内部**版本号和**修订**号。

### <a name="to-specify-a-different-update-location"></a>指定其他更新位置

1. 在“解决方案资源管理器”中选择了项目的情况下，在“项目” 菜单上单击“属性”。

2. 单击“发布”选项卡。

3. 单击 "**更新**" 按钮以打开 "**应用程序更新**" 对话框。

4. 在 "**应用程序更新**" 对话框中，确保选中 "**应用程序应检查更新"** 复选框。

5. 在 "**更新位置**" 字段中，使用 *http://Hostname/ApplicationName*  *\\ \Server\ApplicationName*格式输入完全限定的 URL，使用格式或 UNC 路径输入更新位置，或单击 "**浏览**" 按钮浏览到更新位置。

### <a name="to-check-for-updates-programmatically"></a>以编程方式检查更新

1. 在“解决方案资源管理器”中选择了项目的情况下，在“项目” 菜单上单击“属性”。

2. 单击“发布”选项卡。

3. 单击 "**更新**" 按钮以打开 "**应用程序更新**" 对话框。

4. 在 "**应用程序更新**" 对话框中，确保清除了 **"应用程序应检查更新"** 复选框。 （也可以选择此复选框以编程方式检查更新，也可以让 ClickOnce 运行时自动检查更新。）

5. 在 "**更新位置**" 字段中，使用 *http://Hostname/ApplicationName*  *\\ \Server\ApplicationName*格式输入完全限定的 URL，使用格式或 UNC 路径输入更新位置，或单击 "**浏览**" 按钮浏览到更新位置。 应用程序将在此更新位置查找其自身的更新版本。

6. 在 Windows 窗体上创建一个按钮、菜单项或其他用户界面项，用户将选择这些项来检查更新。 从该项的事件处理程序中，调用方法以检查和安装更新。 你可以在如何执行以下操作中C# [找到此类方法的 Visual Basic 和 Visual 代码的示例：使用 ClickOnce 部署 API](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)以编程方式检查应用程序更新。

7. 构建你的应用程序。

## <a name="see-also"></a>请参阅
- <xref:System.Deployment.Application.ApplicationDeployment>
- [“应用程序更新”对话框](/previous-versions/visualstudio/visual-studio-2010/axw1fa38(v=vs.100))
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [如何：使用 ClickOnce 部署 API 以编程方式检查是否有应用程序更新](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)

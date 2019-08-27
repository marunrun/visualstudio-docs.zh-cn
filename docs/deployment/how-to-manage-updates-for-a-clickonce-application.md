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
ms.openlocfilehash: ed5ae8486ebede9db2ab6b052c1fed789883ceaf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928561"
---
# <a name="how-to-manage-updates-for-a-clickonce-application"></a>如何：管理 ClickOnce 应用程序的更新
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可以自动或以编程方式检查更新。 作为开发人员，您可以自由地指定何时以及如何执行更新检查更新是否强制性的以及应用程序应检查更新。

 可以配置要在应用程序启动后检查更新之前在应用程序启动，自动或在设置的时间间隔的应用程序。 此外可以指定所需的最低版本;也就是说，如果用户的版本低于所需的版本安装更新。

 可以配置应用程序检查更新以编程方式根据用户请求等事件。 "若要以编程方式检查更新"的过程本主题中演示了如何编写使用的代码<xref:System.Deployment.Application.ApplicationDeployment>类，以检查更新的基于事件。

 此外可以部署你的应用程序从一个位置，并从另一个更新。 请参阅"指定不同的更新位置。"过程

 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

 在中管理更新行为**应用程序更新**对话框中，从可用**发布**页**项目设计器。**

### <a name="to-check-for-updates-before-the-application-starts"></a>应用程序启动之前检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“发布”选项卡。

3. 单击**更新**按钮以打开**应用程序更新**对话框。

4. 在中**应用程序更新**对话框框中，请确保**应用程序应检查更新**复选框处于选中状态。

5. 在中**选择应用程序应检查更新时**部分中，选择**应用程序启动前**。 这可确保始终连接到网络的用户使用最新的更新运行应用程序。

### <a name="to-check-for-updates-in-the-background-after-the-application-starts"></a>在应用程序启动后在后台检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“发布”选项卡。

3. 单击**更新**按钮以打开**应用程序更新**对话框。

4. 中**应用程序更新**对话框框中，确保选中该复选框**应用程序应检查更新**处于选中状态。

5. 在中**选择何时该应用程序应该检查更新节**，选择**应用程序启动后**。 将启动更快地这样一来，应用程序，然后它将在后台检查更新并仅在有可用的更新时通知用户。 安装后，更新才会生效，直到重新启动该应用程序。

6. 在中**指定应用程序检查更新的频率**部分中，选择**每次应用程序运行时检查**（默认值） 或**检查每个**然后输入一个数字和时间间隔。

### <a name="to-specify-a-minimum-required-version-for-the-application"></a>若要指定应用程序所需的最低版本

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“发布”选项卡。

3. 单击**更新**按钮以打开**应用程序更新**对话框。

4. 在中**应用程序更新**对话框框中，请确保**应用程序应检查更新**复选框处于选中状态。

5. 选择**指定此应用程序所需的最低版本**复选框，并输入**主要**，**次要**，**生成**，和**修订**应用程序的数字。

### <a name="to-specify-a-different-update-location"></a>若要指定不同的更新位置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“发布”选项卡。

3. 单击**更新**按钮以打开**应用程序更新**对话框。

4. 在中**应用程序更新**对话框框中，请确保**应用程序应检查更新**复选框处于选中状态。

5. 在中**更新位置**字段中，输入完全限定 url，使用以下格式的更新位置*http://Hostname/ApplicationName*，或使用以下格式的 UNC 路径 *\\\Server\ApplicationName*，或单击**浏览**按钮以浏览更新位置。

### <a name="to-check-for-updates-programmatically"></a>若要以编程方式检查更新

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“发布”选项卡。

3. 单击**更新**按钮以打开**应用程序更新**对话框。

4. 在中**应用程序更新**对话框框中，请确保**应用程序应检查更新**清除复选框。 （或者，您可以选中此复选框以检查更新，以编程方式，同时让 ClickOnce 运行时自动检查更新。）

5. 在中**更新位置**字段中，输入完全限定 url，使用以下格式的更新位置*http://Hostname/ApplicationName*，或使用以下格式的 UNC 路径 *\\\Server\ApplicationName*，或单击**浏览**按钮以浏览更新位置。 更新位置为应用程序将寻找其自身的更新版本。

6. 在用户将选择检查更新的 Windows 窗体上创建一个按钮、 菜单项或其他用户界面项。 从该项目的事件处理程序，调用方法来检查并安装更新。 您可以找到示例的 Visual Basic 和 VisualC#中的此类的方法的代码[如何：检查应用程序更新使用 ClickOnce 部署 API 以编程方式](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)。

7. 构建应用程序。

## <a name="see-also"></a>请参阅
- <xref:System.Deployment.Application.ApplicationDeployment>
- [“应用程序更新”对话框](/previous-versions/visualstudio/visual-studio-2010/axw1fa38(v=vs.100))
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [如何：使用 ClickOnce 部署 API 以编程方式检查是否有应用程序更新](../deployment/how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api.md)
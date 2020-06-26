---
title: 调试使用 System.web 的 ClickOnce 应用程序
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, debugging
- debugging, ClickOnce applications
- debugging, System.Deployment
- deploying applications [ClickOnce], debugging
ms.assetid: 86f31948-2ca8-47c0-8e8b-c2b817bbf79f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 203f1edc2e29bbbc34fb39e6aa01c1b56bf20e91
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382648"
---
# <a name="debug-clickonce-applications-that-use-systemdeploymentapplication"></a>调试使用 System.Deployment.Application 的 ClickOnce 应用程序
在中 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] ， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署允许你配置应用程序的更新方式。 但是，如果你需要使用和自定义高级 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署功能，你将需要访问提供的部署对象模型 <xref:System.Deployment.Application> 。 可以将 <xref:System.Deployment.Application> api 用于高级任务，例如：

- 在应用程序中创建 "立即更新" 选项

- 各种应用程序组件的有条件、按需下载

- 直接集成到应用程序中的更新

- 确保客户端应用程序始终是最新的

  由于 <xref:System.Deployment.Application> api 仅在部署应用程序时使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 技术，因此调试它们的唯一方法是使用部署应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，将其附加到该应用程序，然后调试它。 可能很难提前附加调试器，因为此代码通常在应用程序启动时运行，并且在你可以附加调试器之前执行。 解决方法是在更新检查代码或按需代码之前，对 Visual Basic 项目执行中断（或停止）。

  建议的调试技术如下所示：

1. 在开始之前，请确保已存档符号（.pdb）和源文件。

2. 部署应用程序的版本1。

3. 创建新的空白解决方案。 在“文件”菜单中，单击“新建”，然后单击“项目”************。 在 "**新建项目**" 对话框中，打开 "**其他项目类型**" 节点，然后选择 " **Visual Studio 解决方案**" 文件夹。 在 "**模板**" 窗格中选择 "**空白解决方案**"。

4. 将存档的源位置添加到此新解决方案的属性中。 在**解决方案资源管理器**中，右键单击 "解决方案" 节点，然后单击 "**属性**"。 在 "**属性页**" 对话框中，选择 "**调试源文件**"，然后添加存档源代码的目录。 否则，调试器会找到过期的源文件，因为源文件路径记录在 .pdb 文件中。 如果调试器使用过期的源文件，则会看到一条消息，告知您源不匹配。

5. 请确保调试器能够找到 *.pdb*文件。 如果已将这些应用程序与应用程序一起部署，则调试器会自动找到它们。 它始终显示在相关程序集的旁边。 否则，你将需要将存档路径添加到**符号文件（.pdb）位置**（若要访问此选项，请从 "**工具**" 菜单中，单击 "**选项**"，打开 "**调试**" 节点，然后单击 "**符号**"）。

6. 调试 `CheckForUpdate` 和 `Download` / `Update` 方法调用之间发生的情况。

    例如，更新代码可能如下所示：

   ```vb
       Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
           If My.Application.Deployment.IsNetworkDeployed Then

               If (My.Application.Deployment.CheckForUpdate()) Then

                   My.Application.Deployment.Update()
                   Application.Restart()

               End If

           End If
       End Sub
   ```

7. 部署版本2。

8. 在下载版本2的更新时尝试将调试器附加到版本1应用程序。 或者，您也可以使用 `System.Diagnostics.Debugger.Break` 方法或简单地 `Stop` Visual Basic。 当然，您不应在生产代码中保留这些方法调用。

    例如，假设你要开发一个 Windows 窗体应用程序，并且此方法的事件处理程序具有其中的更新逻辑。 若要对此进行调试，只需在按下按钮之前附加，然后设置断点（请确保打开适当的存档文件并在此处设置断点）。

   <xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A> <xref:System.Deployment.Application> 仅在部署应用程序时使用属性来调用 api; 不应在中的调试过程中调用 api [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="see-also"></a>请参阅
- <xref:System.Deployment.Application>
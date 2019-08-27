---
title: 调试使用 System.Deployment.Application 的 ClickOnce 应用程序
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: d70697e3523fcb12384cb51415f73ebd210f45c9
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66261999"
---
# <a name="debug-clickonce-applications-that-use-systemdeploymentapplication"></a>调试使用 System.Deployment.Application 的 ClickOnce 应用程序
在中[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署允许您配置如何更新应用程序。 但是，如果您需要使用和自定义高级[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署功能，您将需要访问提供的部署对象模型<xref:System.Deployment.Application>。 可以使用<xref:System.Deployment.Application>Api，可用于高级任务如：

- 创建应用程序中的"立即更新"选项

- 条件，按需下载的各种应用程序组件

- 直接集成到应用程序的更新

- 保证客户端应用程序始终最新

  因为<xref:System.Deployment.Application>Api 的工作原理仅当应用程序部署与[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]技术，对其进行调试的唯一方法是部署应用程序使用[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]，将附加到它，然后对其进行调试。 它可能很难将调试器附加，足够早，因为应用程序启动和执行之前可以附加调试器时，通常在运行此代码。 一种解决方案是在更新检查代码或按需代码之前将分页符 （或停止，对于 Visual Basic 项目）。

  建议的调试方法是按如下所示：

1. 在开始之前，请确保已存档的符号 (.pdb) 和源文件。

2. 部署应用程序的版本 1。

3. 创建新的空白解决方案。 从**文件**菜单上，单击**新建**，然后**项目**。 在中**新的项目**对话框中，打开**其他项目类型**节点，然后选择**Visual Studio 解决方案**文件夹。 在中**模板**窗格中，选择**空白解决方案**。

4. 将已存档的源位置添加到这个新的解决方案的属性。 在中**解决方案资源管理器**，右键单击解决方案节点，然后单击**属性**。 在中**属性页**对话框中，选择**调试源文件**，然后添加存档的源代码的目录。 否则，调试器将发现过期的源文件，因为源文件路径记录在.pdb 文件。 如果调试器使用过期的源文件，您将看到一个消息，指示源不匹配。

5. 请确保调试器可找到 *.pdb*文件。 如果已与你的应用程序部署它们，调试器会自动找到它们。 它始终会查找旁边程序集有问题第一次。 否则，需要将添加到存档路径**符号文件 (.pdb) 位置**(若要访问此选项，从**工具**菜单中，单击**选项**，然后打开**调试**节点，然后单击**符号**)。

6. 调试之间会发生什么情况`CheckForUpdate`并`Download` / `Update`方法调用。

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

7. 部署第 2 版。

8. 尝试将调试器附加到版本 1 应用程序，如下载版本 2 的更新。 或者可以使用`System.Diagnostics.Debugger.Break`方法或只需`Stop`在 Visual Basic 中。 当然，不应在生产代码中将这些方法调用。

    例如，假设你在开发 Windows 窗体应用程序，并且此方法与更新逻辑的事件处理程序在。 若要调试它，只需之前附加按钮按下时，则设置一个断点 （请确保您打开相应的存档的文件，并设置断点）。

   使用<xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A>属性来调用<xref:System.Deployment.Application>仅当应用程序部署的 Api; Api 不应调用在调试期间[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

## <a name="see-also"></a>请参阅
- <xref:System.Deployment.Application>
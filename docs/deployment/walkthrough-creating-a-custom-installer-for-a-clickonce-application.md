---
title: 创建自定义安装程序的 ClickOnce 应用程序
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, custom installer
- installer [ClickOnce], custom
- deploying applications [ClickOnce], custom installer
- InPlaceHostingManager [ClickOnce], custom installer
- custom installer [ClickOnce]
ms.assetid: fb222cc5-8aeb-4b94-8c49-b93e342f5f69
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e6969490789b4f5747c28f33e91c7d61e97de52e
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263460"
---
# <a name="walkthrough-create-a-custom-installer-for-a-clickonce-application"></a>演练：创建 ClickOnce 应用程序的自定义安装程序
任何 ClickOnce 应用程序基于 *.exe*可以以无提示方式安装和自定义安装程序更新文件。 自定义安装程序可以在安装期间，包括用于安全性和维护操作的自定义对话框实现自定义用户体验。 若要执行安装操作，自定义安装程序使用<xref:System.Deployment.Application.InPlaceHostingManager>类。 本演练演示如何创建一个自定义安装程序，以无提示方式安装 ClickOnce 应用程序。

## <a name="prerequisites"></a>系统必备

### <a name="to-create-a-custom-clickonce-application-installer"></a>若要创建自定义 ClickOnce 应用程序安装程序

1. 在 ClickOnce 应用程序中，添加对 System.Deployment 和 System.Windows.Forms 的引用。

2. 将新类添加到你的应用程序并指定任何名称。 本演练使用名称 `MyInstaller`。

3. 添加以下`Imports`或`using`到您的新类的顶部的语句。

    ```vb
    Imports System.Deployment.Application
    Imports System.Windows.Forms
    ```

    ```csharp
    using System.Deployment.Application;
    using System.Windows.Forms;
    ```

4. 将以下方法添加到您的类。

     这些方法调用<xref:System.Deployment.Application.InPlaceHostingManager>方法下载部署清单中，添加相应的权限，要求用户提供权限来安装，然后下载并安装到 ClickOnce 缓存的应用程序。 自定义安装程序可以指定 ClickOnce 应用程序预受信任，也可以将推迟到信任决定<xref:System.Deployment.Application.InPlaceHostingManager.AssertApplicationRequirements%2A>方法调用。 此代码预信任应用程序。

    > [!NOTE]
    > 通过预先信任分配的权限不能超过的自定义安装程序代码的权限。

     [!code-vb[System.Deployment.Application.InPlaceHostingManager#1](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-installer-for-a-clickonce-application_1.vb)]
     [!code-csharp[System.Deployment.Application.InPlaceHostingManager#1](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-installer-for-a-clickonce-application_1.cs)]

5. 若要尝试在代码中的安装，请调用`InstallApplication`方法。 例如，如果将类命名为`MyInstaller`，可能会调用`InstallApplication`如下所示。

    ```vb
    Dim installer As New MyInstaller()
    installer.InstallApplication("\\myServer\myShare\myApp.application")
    MessageBox.Show("Installer object created.")
    ```

    ```csharp
    MyInstaller installer = new MyInstaller();
    installer.InstallApplication(@"\\myServer\myShare\myApp.application");
    MessageBox.Show("Installer object created.");
    ```

## <a name="next-steps"></a>后续步骤
 ClickOnce 应用程序还可以添加自定义更新逻辑，包括一个自定义用户界面来显示在更新过程。 有关详细信息，请参阅 <xref:System.Deployment.Application.UpdateCheckInfo>。 ClickOnce 应用程序也可以禁止显示标准的开始菜单项、 快捷方式，并添加或删除程序条目使用`<customUX>`元素。 有关详细信息，请参阅[\<入口点 > 元素](../deployment/entrypoint-element-clickonce-application.md)和<xref:System.Deployment.Application.DownloadApplicationCompletedEventArgs.ShortcutAppId%2A>。

## <a name="see-also"></a>请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<入口点 > 元素](../deployment/entrypoint-element-clickonce-application.md)
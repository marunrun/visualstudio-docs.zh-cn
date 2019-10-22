---
title: 为 ClickOnce 应用程序创建自定义安装程序
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
ms.openlocfilehash: b648134b7ad27a8f622ce270dc0f05e0a7e6516c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72637420"
---
# <a name="walkthrough-create-a-custom-installer-for-a-clickonce-application"></a>演练：为 ClickOnce 应用程序创建自定义安装程序
任何基于 *.exe*文件的 ClickOnce 应用程序都可以由自定义安装程序进行静默安装和更新。 自定义安装程序可以在安装过程中实现自定义用户体验，包括安全和维护操作的自定义对话框。 若要执行安装操作，自定义安装程序将使用 <xref:System.Deployment.Application.InPlaceHostingManager> 类。 本演练演示如何创建一个无提示安装 ClickOnce 应用程序的自定义安装程序。

## <a name="prerequisites"></a>Prerequisites

### <a name="to-create-a-custom-clickonce-application-installer"></a>创建自定义 ClickOnce 应用程序安装程序

1. 在 ClickOnce 应用程序中，添加对 System.web 和 System.object 的引用。

2. 向应用程序中添加一个新类并指定任意名称。 本演练使用名称 `MyInstaller`。

3. 将以下 `Imports` 或 `using` 指令添加到新类的顶部。

    ```vb
    Imports System.Deployment.Application
    Imports System.Windows.Forms
    ```

    ```csharp
    using System.Deployment.Application;
    using System.Windows.Forms;
    ```

4. 将以下方法添加到类。

     这些方法调用 <xref:System.Deployment.Application.InPlaceHostingManager> 方法来下载部署清单，断言适当的权限，要求用户提供安装权限，然后将应用程序下载并安装到 ClickOnce 缓存中。 自定义安装程序可以指定 ClickOnce 应用程序是预信任的，也可以将信任决策推迟到 <xref:System.Deployment.Application.InPlaceHostingManager.AssertApplicationRequirements%2A> 方法调用。 此代码预信任应用程序。

    > [!NOTE]
    > 由预信任分配的权限不能超过自定义安装程序代码的权限。

     [!code-vb[System.Deployment.Application.InPlaceHostingManager#1](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-installer-for-a-clickonce-application_1.vb)]
     [!code-csharp[System.Deployment.Application.InPlaceHostingManager#1](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-installer-for-a-clickonce-application_1.cs)]

5. 若要尝试从代码安装，请调用 `InstallApplication` 方法。 例如，如果您将类命名为 `MyInstaller`，则可以通过以下方式调用 `InstallApplication`。

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
 ClickOnce 应用程序还可以添加自定义的更新逻辑，包括要在更新过程中显示的自定义用户界面。 有关更多信息，请参见<xref:System.Deployment.Application.UpdateCheckInfo>。 ClickOnce 应用程序还可以通过使用 `<customUX>` 元素，禁止显示标准的 "开始" 菜单项、快捷方式和 "添加或删除程序" 项。 有关详细信息，请参阅[\<entryPoint > 元素](../deployment/entrypoint-element-clickonce-application.md)和 <xref:System.Deployment.Application.DownloadApplicationCompletedEventArgs.ShortcutAppId%2A>。

## <a name="see-also"></a>请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<entryPoint > 元素](../deployment/entrypoint-element-clickonce-application.md)

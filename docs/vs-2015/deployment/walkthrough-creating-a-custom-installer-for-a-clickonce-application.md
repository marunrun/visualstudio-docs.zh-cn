---
title: 演练：应用程序创建自定义 ClickOnce 应用程序安装 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
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
caps.latest.revision: 36
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9ebde75fdf36c84f40ae660a24d469c36e72ceaf
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386589"
---
# <a name="walkthrough-creating-a-custom-installer-for-a-clickonce-application"></a>演练：创建 ClickOnce 应用程序的自定义安装程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

任何基于.exe 文件的 ClickOnce 应用程序可以以无提示方式安装和自定义安装程序更新。 自定义安装程序可以在安装期间，包括用于安全性和维护操作的自定义对话框实现自定义用户体验。 若要执行安装操作，自定义安装程序使用<xref:System.Deployment.Application.InPlaceHostingManager>类。 本演练演示如何创建一个自定义安装程序，以无提示方式安装 ClickOnce 应用程序。  
  
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
  
     [!code-csharp[System.Deployment.Application.InPlaceHostingManager#1](../snippets/csharp/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/CS/Form1.cs#1)]
     [!code-vb[System.Deployment.Application.InPlaceHostingManager#1](../snippets/visualbasic/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/VB/Form1.vb#1)]  
  
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
 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)   
 [\<entryPoint> 元素](../deployment/entrypoint-element-clickonce-application.md)

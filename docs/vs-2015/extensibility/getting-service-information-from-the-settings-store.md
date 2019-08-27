---
title: 从设置存储中获取服务信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cfe754203ae9b4e951de5beef8cd829f9d7716bb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204312"
---
# <a name="getting-service-information-from-the-settings-store"></a>从设置存储中获取服务信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要查找所有可用的服务，或以确定是否安装了特定服务，可以使用设置存储。 您必须知道服务类的类型。  
  
### <a name="to-list-the-available-services"></a>若要列出可用服务  
  
1. 创建一个名为 FindServicesExtension 的 VSIX 项目，然后添加名为 FindServicesCommand 的自定义命令。 有关如何创建自定义命令的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
2. 在 FindServicesCommand.cs，添加以下 using 语句：  
  
    ```vb  
    using System.Collections.Generic;  
    using Microsoft.VisualStudio.Settings;  
    using Microsoft.VisualStudio.Shell.Settings;  
    using System.Windows.Forms;  
    ```  
  
3. 获取配置设置存储区，然后查找名为服务的子集合。 此集合包括所有可用的服务。 在 MenuItemCommand 方法中，删除现有的代码并使用以下代码替换它：  
  
    ```  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);  
        string message = "Available services:\n";  
        IEnumerable<string> collection = configurationSettingsStore.GetSubCollectionNames("Services");  
        int n = 0;  
        foreach (string service in collection)  
        {  
            message += configurationSettingsStore.GetString("Services\\" + service, "Name", "Unknown") + "\n";  
        }  
  
        MessageBox.Show(message);  
    }  
    ```  
  
4. 生成项目并启动调试。 将显示在实验实例。  
  
5. 在实验实例上**工具**菜单上，单击**调用 FindServicesCommand**。  
  
     您应看到列出的所有服务的消息框。  
  
     若要验证这些设置，可以使用注册表编辑器。  
  
## <a name="finding-a-specific-service"></a>查找特定的服务  
 此外可以使用<xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A>方法，以确定是否安装了特定服务。 您必须知道服务类的类型。  
  
1. 在上一个过程中创建的项目的 MenuItemCallback，搜索的配置设置存储`Services`具有子集合的服务的 GUID 命名的集合。 在这种情况下，我们将寻找帮助服务。  
  
    ```  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);  
        string helpServiceGUID = typeof(SVsHelpService).GUID.ToString("B").ToUpper();  
        bool hasHelpService = configurationSettingsStore.CollectionExists("Services\\" + helpServiceGUID);  
        string message = "Help Service Available: " + hasHelpService;  
  
        MessageBox.Show(message);  
    }  
    ```  
  
2. 生成项目并启动调试。  
  
3. 在实验实例上**工具**菜单上，单击**调用 FindServicesCommand**。  
  
     你应看到一条消息包含文本**帮助服务可用：** 跟**True**或**False**。 若要验证此设置，可以使用注册表编辑器，如在前面的步骤中所示。

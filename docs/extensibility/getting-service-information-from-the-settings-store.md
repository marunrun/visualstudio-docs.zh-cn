---
title: 正在从设置存储获取服务信息 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 51aa0369793fe5dc4b39fe510c069a7ec93d102a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72647981"
---
# <a name="get-service-information-from-the-settings-store"></a>从设置存储获取服务信息
您可以使用 "设置存储" 查找所有可用的服务，或确定是否安装了某个特定的服务。 您必须知道服务类的类型。

## <a name="to-list-the-available-services"></a>列出可用的服务

1. 创建一个名为 `FindServicesExtension` 的 VSIX 项目，然后添加一个名为 `FindServicesCommand` 的自定义命令。 有关如何创建自定义命令的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

2. 在*FindServicesCommand.cs*中，添加以下 using 指令：

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. 获取 "配置设置" 存储，然后查找名为 "子集合" 的服务。 此集合包含所有可用服务。 在 `MenuItemCommand` 方法中，删除现有代码，并将其替换为以下代码：

    ```csharp
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

4. 生成项目并启动调试。 将显示实验实例。

5. 在实验实例中，单击 "**工具**" 菜单上的 "**调用 FindServicesCommand**"。

     应该会看到一个列出所有服务的消息框。

     若要验证这些设置，可以使用注册表编辑器。

## <a name="find-a-specific-service"></a>查找特定服务
 你还可以使用 <xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A> 方法来确定是否安装了某个特定的服务。 您必须知道服务类的类型。

1. 在上一个过程中创建的项目的 MenuItemCallback 中，在 "配置设置" 存储中搜索包含由服务的 GUID 命名的子集合的 `Services` 集合。 在此示例中，我们将查找帮助服务。

    ```csharp
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

3. 在实验实例中，单击 "**工具**" 菜单上的 "**调用 FindServicesCommand**"。

     应该会看到一条消息，其中包含文本**帮助服务可用：** 后跟**True**或**False**。 若要验证此设置，可以使用注册表编辑器，如前面的步骤中所示。

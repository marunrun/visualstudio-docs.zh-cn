---
title: 从设置商店获取服务信息 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b15d5c9f122ca66d21940b9998969b0d39d1a74d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711375"
---
# <a name="get-service-information-from-the-settings-store"></a>从设置存储处获取服务信息
您可以使用设置存储查找所有可用服务或确定是否安装了特定服务。 您必须知道服务类的类型。

## <a name="to-list-the-available-services"></a>列出可用服务

1. 创建名为`FindServicesExtension`的 VSIX 项目，然后添加名为`FindServicesCommand`的自定义命令。 有关如何创建自定义命令的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

2. 在*FindServicesCommand.cs*中，添加以下使用指令：

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. 获取配置设置存储，然后查找名为"服务"的子集合。 此集合包括所有可用的服务。 在`MenuItemCommand`方法中，删除现有代码并将其替换为以下内容：

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

4. 生成项目并启动调试。 出现实验实例。

5. 在实验实例中，在 **"工具"** 菜单上，单击 **"调用查找服务命令**"。

     您应该会看到一个消息框，列出所有服务。

     要验证这些设置，可以使用注册表编辑器。

## <a name="find-a-specific-service"></a>查找特定服务
 您还可以使用 方法<xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A>来确定是否安装了特定服务。 您必须知道服务类的类型。

1. 在上一过程中创建的项目的 MenuItem 回拨中，搜索配置设置存储中具有由服务的`Services`GUID 命名的子集合的集合。 在这种情况下，我们将查找帮助服务。

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

3. 在实验实例中，在 **"工具"** 菜单上，单击 **"调用查找服务命令**"。

     您应该会看到一条消息，其中文本 **"帮助服务可用"：** 后跟 **"真****"或"假**"。 要验证此设置，可以使用注册表编辑器，如前面的步骤所示。

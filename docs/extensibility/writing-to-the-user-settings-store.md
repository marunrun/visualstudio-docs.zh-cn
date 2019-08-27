---
title: 写入用户设置存储 |Microsoft Docs
ms.date: 05/23/2019
ms.topic: conceptual
ms.assetid: efd27f00-7fe5-45f8-9b97-371af732be97
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44380a03b87318be0fdf746c75eff8988ac68267
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318485"
---
# <a name="writing-to-the-user-settings-store"></a>写入用户设置存储
用户设置是可写设置中的一样**工具 / 选项**对话框、 属性窗口和某些其他对话框。 Visual Studio 扩展可能会使用这些存储少量数据。 本演练演示如何将记事本到 Visual Studio 添加为外部工具，通过读取和写入用户设置存储。

## <a name="writing-to-the-user-settings-store"></a>写入用户设置存储

1. 创建一个名为 UserSettingsStoreExtension 的 VSIX 项目，然后添加名为 UserSettingsStoreCommand 的自定义命令。 有关如何创建自定义命令的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

2. 在 UserSettingsStoreCommand.cs，添加以下 using 语句：

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    ```

3. 在 MenuItemCallback，删除方法的主体以及获取的用户设置存储，按如下所示：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);
    }
    ```

4. 现在，了解记事本是否已设置为外部工具。 您需要循环访问所有外部工具，以确定是否 ToolCmd 设置为"记事本"，如下所示：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);

        // Find out whether Notepad is already an External Tool.
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");
        bool hasNotepad = false;
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;
        for (int i = 0; i < toolCount; i++)
        {
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)
            {
                hasNotepad = true;
                break;
            }
        }
    }

    ```

5. 如果记事本未设置为外部工具，请按如下所示进行设置：

    ```vb
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);

        // Find out whether Notepad is already installed.
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");
        bool hasNotepad = false;
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;
        for (int i = 0; i < toolCount; i++)
        {
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)
            {
                hasNotepad = true;
                break;
            }
        }

        string message = (hasNotepad) ? "Notepad already installed" : "Installing Notepad";
         if (!hasNotepad)
        {
            userSettingsStore.SetString("External Tools", "ToolTitle" + toolCount, "&Notepad");
            userSettingsStore.SetString("External Tools", "ToolCmd" + toolCount, "C:\\Windows\\notepad.exe");
            userSettingsStore.SetString("External Tools", "ToolArg" + toolCount, "");
            userSettingsStore.SetString("External Tools", "ToolDir" + toolCount, "$(ProjectDir)");
            userSettingsStore.SetString("External Tools", "ToolSourceKey" + toolCount, "");
            userSettingsStore.SetUInt32("External Tools", "ToolOpt" + toolCount, 0x00000011);

            userSettingsStore.SetInt32("External Tools", "ToolNumKeys", toolCount + 1);
        }
    }
    ```

6. 测试代码。 请记住，它添加了记事本作为外部工具，所以您必须回滚注册表之前第二次运行它。

7. 生成代码并开始调试。

8. 上**工具**菜单上，单击**调用 UserSettingsStoreCommand**。 这将添加到记事本**工具**菜单。

9. 现在，会看到记事本工具 / 选项菜单，并单击**记事本**应打开一个记事本实例。
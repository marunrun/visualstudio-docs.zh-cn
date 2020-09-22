---
title: 正在写入用户设置存储 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: efd27f00-7fe5-45f8-9b97-371af732be97
caps.latest.revision: 4
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 764d9b81297c6bbefd1f5fdf7c77e4d514bb5045
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840685"
---
# <a name="writing-to-the-user-settings-store"></a>写入用户设置存储
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

用户设置是 " **工具/选项** " 对话框、"属性" 窗口和某些其他对话框中的可写设置。 Visual Studio 扩展可以使用这些扩展来存储少量数据。 本演练演示如何通过读取和写入用户设置存储，将记事本作为外部工具添加到 Visual Studio。  
  
### <a name="backing-up-your-user-settings"></a>备份用户设置  
  
1. 您必须能够重置 "外部工具" 设置，以便您可以调试并重复该过程。 为此，必须保存原始设置，以便可以根据需要还原它们。  
  
2. 打开 Regedit.exe。  
  
3. 导航到 HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\14.0Exp\External 工具 " \\ 。  
  
    > [!NOTE]
    > 请确保正在查看包含 \14.0Exp\ 的密钥，而不是 \ 14.0 \\ 。 运行 Visual Studio 的实验实例时，用户设置在注册表配置单元 "14.0 Exp" 中。  
  
4. 右键单击 "\External 工具 \" 子项，然后单击 " **导出**"。 请确保选中 " **选定的分支** "。  
  
5. 保存生成的外部工具 .reg 文件。  
  
6. 稍后，当你想要重置外部工具设置时，选择 HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\14.0Exp\External Tools \ 注册表项，并在上下文菜单上单击 " **删除** "。  
  
7. 出现 " **确认密钥删除** " 对话框时，单击 **"是"**。  
  
8. 右键单击前面保存的 "外部工具 .reg" 文件，单击 " **打开方式**"，然后单击 " **注册表编辑器**"。  
  
## <a name="writing-to-the-user-settings-store"></a>写入用户设置存储  
  
1. 创建名为 UserSettingsStoreExtension 的 VSIX 项目，然后添加名为 UserSettingsStoreCommand 的自定义命令。 有关如何创建自定义命令的详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
2. 在 UserSettingsStoreCommand.cs 中，添加以下 using 语句：  
  
    ```csharp  
    using System.Collections.Generic;  
    using Microsoft.VisualStudio.Settings;  
    using Microsoft.VisualStudio.Shell.Settings;  
    ```  
  
3. 在 MenuItemCallback 中，删除方法的正文并获取用户设置存储，如下所示：  
  
    ```csharp  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);  
    }  
    ```  
  
4. 现在，确定是否已将记事本设置为外部工具。 需要循环访问所有外部工具，以确定 ToolCmd 设置是否为 "Notepad"，如下所示：  
  
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
  
5. 如果记事本尚未设置为外部工具，请按如下所示进行设置：  
  
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
  
6. 测试代码。 请记住，它会将记事本添加为外部工具，因此，在第二次运行它之前，必须先回滚注册表。  
  
7. 生成代码并开始调试。  
  
8. 在 " **工具** " 菜单上，单击 " **调用 UserSettingsStoreCommand**"。 这会将记事本添加到 " **工具** " 菜单。  
  
9. 现在，应会在 "工具"/"选项" 菜单上看到 "记事本"，然后单击 " **记事本** " 以打开记事本的实例。

---
title: 使用设置存储 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Settings Store, using
ms.assetid: 447ec08a-eca5-40b8-89b0-f98fdf3d39a4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b3bbc09586f883e067e32f525a0331c1a9e253f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698520"
---
# <a name="using-the-settings-store"></a>使用设置存储
有两种类型的设置存储：

- 配置设置，它们是只读的可视化工作室和 VSPackage 设置。 可视化工作室将所有已知的 .pkgdef 文件的设置合并到此存储中。

- 用户设置，这些设置是可写入的设置，例如显示在 **"选项"** 对话框、属性页和某些其他对话框中的页面上的设置。 Visual Studio 扩展可能使用这些扩展用于本地存储少量数据。

  本演练演示如何从配置设置存储中读取数据。 有关如何[写入用户设置存储的说明，请参阅写入用户设置存储](../extensibility/writing-to-the-user-settings-store.md)。

## <a name="creating-the-example-project"></a>创建示例项目
 本节演示如何使用菜单命令创建用于演示的简单扩展项目。

1. 每个 Visual Studio 扩展都从包含扩展资产的 VSIX 部署项目开始。 创建[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]名为 的`SettingsStoreExtension`VSIX 项目。 您可以在**Visual C# / 扩展性**下的 **"新项目**"对话框中找到 VSIX 项目模板。

2. 现在添加名为**SettingsStore命令 的**自定义命令项模板。 在"**添加新项目"** 对话框中，转到**可视化 C# / 扩展性**，然后选择 **"自定义命令**"。 在窗口底部的 **"名称"** 字段中，将命令文件名更改为**SettingsStoreCommand.cs**。 有关如何创建自定义命令的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

## <a name="using-the-configuration-settings-store"></a>使用配置设置存储
 本节演示如何检测和显示配置设置。

1. 在SettingsStorageCommand.cs文件中，添加以下使用指令：

   ```
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Settings;
   using Microsoft.VisualStudio.Shell.Settings;
   using System.Windows.Forms;
   ```

2. 在`MenuItemCallback`中，删除方法的主体，并添加这些行获取配置设置存储：

   ```
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
   ```

    是<xref:Microsoft.VisualStudio.Shell.Settings.ShellSettingsManager>服务上的<xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager>托管帮助器类。

3. 现在了解是否安装了 Windows 电话工具。 代码应如下所示：

   ```
   private void MenuItemCallback(object sender, EventArgs e)
   {
       SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
       SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
       bool arePhoneToolsInstalled = configurationSettingsStore.CollectionExists(@"InstalledProducts\Microsoft Windows Phone Developer Tools");
       string message = "Microsoft Windows Phone Developer Tools: " + arePhoneToolsInstalled;
       MessageBox.Show(message);
   }
   ```

4. 测试代码。 生成项目并启动调试。

5. 在实验实例中，在 **"工具"** 菜单上，单击 **"调用设置存储命令**"。

    您应该会看到一个消息框，上面写着**微软 Windows Phone 开发人员工具：** 后跟 **"真****"或"假**"。

   Visual Studio 将设置存储在系统注册表中。

#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>使用注册表编辑器验证配置设置

1. 打开 Regedit.exe。

2. 导航到HKEY_CURRENT_USER\软件\微软_VisualStudio_14.0Exp_Config\已安装\\的产品。

    > [!NOTE]
    > 请确保正在查看包含 [14.0Exp_Config] 的密钥，而不是 [14.0_Config。\\ 运行 Visual Studio 的实验实例时，配置设置位于注册表配置单元"14.0Exp_Config"。

3. 展开 [已安装的产品] 节点。 如果前面的步骤中的消息是微软**Windows Phone 开发人员工具安装：True，** 则 [已安装的产品] 应包含一个 Microsoft Windows Phone 开发人员工具节点。 如果消息是**微软 Windows 手机开发人员工具安装： False**， 则 [已安装的产品] 不应包含 Microsoft Windows Phone 开发人员工具节点。

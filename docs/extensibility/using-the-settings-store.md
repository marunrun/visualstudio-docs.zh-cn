---
title: 使用设置存储 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Settings Store, using
ms.assetid: 447ec08a-eca5-40b8-89b0-f98fdf3d39a4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f9c42835e720fd3c33e53d862192e3e2863a4423
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72632600"
---
# <a name="using-the-settings-store"></a>使用设置存储
有两种类型的设置存储：

- 配置设置，这些设置是只读的 Visual Studio 和 VSPackage 设置。 Visual Studio 将所有已知的 .pkgdef 文件中的设置合并到此存储区中。

- 用户设置，这是可写的设置，例如在 "**选项**" 对话框、属性页和某些其他对话框中的页面上显示的设置。 对于少量数据的本地存储，Visual Studio 扩展可能会使用这些扩展。

  此演练演示如何从配置设置存储中读取数据。 有关如何写入用户设置存储的说明，请参阅[写入用户设置存储](../extensibility/writing-to-the-user-settings-store.md)。

## <a name="creating-the-example-project"></a>创建示例项目
 本部分演示如何使用用于演示的菜单命令创建简单的扩展项目。

1. 每个 Visual Studio 扩展都从包含扩展资产的 VSIX 部署项目开始。 创建一个名为 `SettingsStoreExtension` [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSIX 项目。 可以在 "**可视C# /扩展性**" 下的 "**新建项目**" 对话框中找到 VSIX 项目模板。

2. 现在，添加一个名为**SettingsStoreCommand**的自定义命令项模板。 在 "**添加新项**" 对话框中，中转到 "**视觉对象C# /扩展性**"，然后选择 "**自定义命令**"。 在窗口底部的 "**名称**" 字段中，将命令文件名更改为**SettingsStoreCommand.cs**。 有关如何创建自定义命令的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

## <a name="using-the-configuration-settings-store"></a>使用配置设置存储
 本部分说明如何检测和显示配置设置。

1. 在 SettingsStorageCommand.cs 文件中，添加以下 using 指令：

   ```
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Settings;
   using Microsoft.VisualStudio.Shell.Settings;
   using System.Windows.Forms;
   ```

2. 在 `MenuItemCallback` 中，删除方法的主体，并添加以下行以获取配置设置存储：

   ```
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
   ```

    @No__t_0 是 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> 服务上的托管帮助器类。

3. 现在，确定是否安装了 Windows Phone 工具。 代码应如下所示：

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

5. 在实验实例中，单击 "**工具**" 菜单上的 "**调用 SettingsStoreCommand**"。

    应该会看到一个消息框，指出**Microsoft Windows Phone 开发人员工具：** 后跟**True**或**False**。

   Visual Studio 会将设置存储在系统注册表中。

#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>使用注册表编辑器验证配置设置

1. 打开 Regedit.exe。

2. 导航到 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp_Config\InstalledProducts \\。

    > [!NOTE]
    > 请确保正在查看包含 \14.0Exp_Config\ 的密钥，而不是 \14.0_Config \\。 运行 Visual Studio 的实验实例时，配置设置位于注册表配置单元 "14.0 Exp_Config" 中。

3. 展开 "\Installed Products \" 节点。 如果前面步骤中的消息是 " **microsoft Windows Phone 开发人员工具已安装： True**，则 \Installed Products \ 应包含 microsoft Windows Phone 开发人员工具节点。 如果消息为**Microsoft Windows Phone 开发人员工具已安装： False**，则 \Installed Products \ 不应包含 microsoft Windows Phone 开发人员工具节点。

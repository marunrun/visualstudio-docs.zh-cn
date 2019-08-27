---
title: 使用设置存储 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Settings Store, using
ms.assetid: 447ec08a-eca5-40b8-89b0-f98fdf3d39a4
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4b6c2810a81ada06152faea06e86a27f7907a643
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430097"
---
# <a name="using-the-settings-store"></a>使用设置存储
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有两种类型的设置存储：  
  
- 配置设置是只读的 Visual Studio 和 VSPackage 的设置。 Visual Studio 将合并到此存储区的所有已知的.pkgdef 文件中的设置。  
  
- 用户设置，包括可写设置，如在页面上显示的那些**选项**对话框、 属性页和某些其他对话框。 Visual Studio 扩展可能会使用这些本地存储少量数据。  
  
  本演练演示如何从配置设置存储中读取数据。 请参阅[写入用户设置存储](../extensibility/writing-to-the-user-settings-store.md)有关如何将写入到的用户设置存储中的说明。  
  
## <a name="creating-the-example-project"></a>创建示例项目  
 本部分演示如何使用演示的菜单命令创建一个简单的扩展项目。  
  
1. 每个 Visual Studio 扩展开始于 VSIX 部署项目，它将包含扩展资产。 创建[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]VSIX 项目名为`SettingsStoreExtension`。 可以查找中的 VSIX 项目模板**新的项目**下的对话框**Visual C# / 可扩展性**。  
  
2. 现在，添加名为的自定义命令项模板**SettingsStoreCommand**。 在中**添加新项**对话框中，转到**Visual C# / 可扩展性**，然后选择**自定义命令**。 在中**名称**在窗口底部字段中，将命令文件名称更改为**SettingsStoreCommand.cs**。 有关如何创建自定义命令的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
## <a name="using-the-configuration-settings-store"></a>使用配置设置存储  
 本部分介绍如何检测和显示配置设置。  
  
1. 在 SettingsStorageCommand.cs 文件中，添加以下 using 语句：  
  
   ```  
   using System.Collections.Generic;  
   using Microsoft.VisualStudio.Settings;  
   using Microsoft.VisualStudio.Shell.Settings;  
   using System.Windows.Forms;  
   ```  
  
2. 在`MenuItemCallback`，删除方法的主体，并添加以下行获取配置设置存储区：  
  
   ```  
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);  
   ```  
  
    <xref:Microsoft.VisualStudio.Shell.Settings.ShellSettingsManager>是一个托管帮助器类，通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager>服务。  
  
3. 现在，了解是否安装了 Windows Phone 工具。 代码应如下所示：  
  
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
  
5. 在实验实例上**工具**菜单上，单击**调用 SettingsStoreCommand**。  
  
    应会看到消息框： **Microsoft Windows Phone 开发人员工具：** 跟**True**或**False**。  
  
   Visual Studio 将设置存储在系统注册表中。  
  
#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>若要使用注册表编辑器来验证配置设置  
  
1. 打开 Regedit.exe。  
  
2. 导航到 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp_Config\InstalledProducts\\。  
  
    > [!NOTE]
    > 请确保您查看时包含 \14.0Exp_Config\ 且不 \14.0_Config 密钥\\。 当您运行的 Visual Studio 实验实例时，配置设置是在注册表配置单元"14.0Exp_Config"。  
  
3. 展开 \Installed Products\ 节点。 如果在前面步骤中的消息是**Microsoft Windows Phone 开发人员工具安装：True**，\Installed Products\ 应包含 Microsoft Windows Phone 开发人员工具节点。 如果消息是**Microsoft Windows Phone 开发人员工具安装：False**，然后 \Installed Products\ 不应包含 Microsoft Windows Phone 开发人员工具节点。

---
title: 创建自定义起始页 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 3ac0abfe9eedf1c03a8be3bacddbe06ff5698380
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739641"
---
# <a name="creating-a-custom-start-page"></a>创建自定义起始页

您可以按照本文档中的步骤创建自定义"起始页"。

## <a name="create-a-blank-start-page"></a>创建空白起始页

首先，通过创建具有 Visual Studio 将识别的标记结构的 *.xaml*文件，创建一个空白的起始页。 然后，添加标记和代码后面以生成所需的外观和功能。

1. 创建**WPF 应用程序**类型 **（Visual C#** > **Windows 桌面**） 的新项目。

2. 添加对 `Microsoft.VisualStudio.Shell.14.0` 的引用。

3. 在 XML 编辑器中打开 XAML 文件，并将顶级\<窗口>元素更改为\<UserControl>元素，而无需删除任何命名空间声明。

4. 从顶级`x:Class`元素中删除声明。 这使得 XAML 内容与承载"开始页面"的可视化工作室工具窗口兼容。

5. 将以下命名空间声明添加到顶级\<用户控制>元素。

    ```vb
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
    ```

     这些命名空间允许您访问 Visual Studio 命令、控件和 UI 设置。 有关详细信息，请参阅[将可视化工作室命令添加到"开始页面](../extensibility/adding-visual-studio-commands-to-a-start-page.md)"。

     下面的示例显示空白起始页的 *.xaml*文件中的标记。 任何自定义内容都应位于内部<xref:System.Windows.Controls.Grid>元素中。

    ```vb
    <UserControl
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:MyNamespace="clr-namespace:ManualStartPage;assembly=ManualStartPage"
        xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
                xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
        xmlns:local="clr-namespace:StartPageHost"
        mc:Ignorable="d"
         Height="350" Width="525">
        <Grid>
        <!--Add content here.-->
        </Grid>
    </UserControl>
    ```

6. 将控件添加到空\<用户控制>元素以填充自定义起始页。 有关如何添加特定于可视化工作室的功能的信息，请参阅[将可视化工作室命令添加到"开始页面](../extensibility/adding-visual-studio-commands-to-a-start-page.md)"。

## <a name="test-and-apply-the-custom-start-page"></a>测试并应用自定义起始页

在验证 Visual Studio 不会崩溃 Visual Studio 之前，不要将 Visual Studio 的主实例设置为运行自定义"开始页"。 而是在实验实例中测试它。

### <a name="to-test-a-manually-created-custom-start-page"></a>测试手动创建的自定义开始页

1. 将 XAML 文件以及任何支持的文本文件或标记文件复制到 *%USERPROFILE%*我的文档_Visual Studio 2015_StartPages\\*文件夹。

2. 如果起始页引用 Visual Studio 未安装的程序集中的任何控件或类型，请复制程序集，然后将它们粘贴到 *[Visual Studio 安装文件夹]Common7_IDE_私有\\程序集*中。

3. 在 Visual Studio 命令提示符中，键入**devenv /rootsuffix Exp**以打开 Visual Studio 的实验实例。

4. 在实验实例中，转到 **"工具** > **选项** > **环境** > **启动"** 页，然后从 **"自定义起始页"** 下拉列表中选择 XAML 文件。

5. 在“视图” **** 菜单上，单击“起始页” ****。

     应显示自定义起始页。 如果要更改任何文件，则必须关闭实验实例、进行更改、复制和粘贴已更改的文件，然后重新打开实验实例以查看更改。

### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>在可视化工作室的主实例中应用自定义起始页

- 测试"开始页"并发现其稳定后，请使用 **"选项**"对话框中的 **"自定义起始页"** 选项将其作为 Visual Studio 主实例中的起始页选择

## <a name="see-also"></a>请参阅

- [演练：将自定义 XAML 添加到起始页](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
- [将用户控件添加到"开始页面"](../extensibility/adding-user-control-to-the-start-page.md)
- [将可视化工作室命令添加到"开始"页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
- [演练：在"开始"页上保存用户设置](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)
- [部署自定义起始页](../extensibility/deploying-custom-start-pages.md)

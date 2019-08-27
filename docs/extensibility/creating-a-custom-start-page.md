---
title: 创建自定义起始页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 2b0b8c6fde31f4f4d9573381e511465e60086add
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336670"
---
# <a name="creating-a-custom-start-page"></a>创建自定义起始页

可以按照本文档中的步骤创建一个自定义起始页。

## <a name="create-a-blank-start-page"></a>创建一个空白起始页

首先，请通过创建一个空白起始页 *.xaml*具有 Visual Studio 将识别的标记结构文件。 然后，添加标记和代码隐藏来生成的外观和所需的功能。

1. 创建新的项目类型的**WPF 应用程序**(**Visual C#**  > **Windows 桌面**)。

2. 添加对 `Microsoft.VisualStudio.Shell.14.0` 的引用。

3. 在 XML 编辑器中打开 XAML 文件并将更改的顶级\<窗口 > 元素\<UserControl > 而不删除任何命名空间声明的元素。

4. 删除`x:Class`从顶级元素声明。 这使 XAML 内容兼容使用 Visual Studio 工具窗口承载起始页。

5. 将以下命名空间声明添加到顶级\<UserControl > 元素。

    ```vb
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
    ```

     这些命名空间使你可以访问 Visual Studio 命令、 控件和用户界面设置。 有关详细信息，请参阅[到起始页添加 Visual Studio 命令](../extensibility/adding-visual-studio-commands-to-a-start-page.md)。

     下面的示例演示中的标记 *.xaml*空白起始页的文件。 任何自定义内容应当放在内部<xref:System.Windows.Controls.Grid>元素。

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

6. 将控件添加到空\<UserControl > 元素来填充你的自定义起始页。 有关如何添加特定于 Visual Studio 的功能的信息，请参阅[到起始页添加 Visual Studio 命令](../extensibility/adding-visual-studio-commands-to-a-start-page.md)。

## <a name="test-and-apply-the-custom-start-page"></a>测试并应用自定义起始页

未设置 Visual Studio 运行自定义起始页，直到确认它不会崩溃 Visual Studio 的主实例。 相反，在实验实例中测试它。

### <a name="to-test-a-manually-created-custom-start-page"></a>若要测试手动创建自定义起始页

1. 将你的 XAML 文件，和任何支持的文本文件或标记文件，为复制 *%USERPROFILE%\My Documents\Visual Studio 2015\StartPages\\* 文件夹。

2. 如果你的起始页引用的任何控件或未安装 Visual studio 的程序集中的类型，复制程序集，然后将其粘贴 *{Visual Studio 安装文件夹} \Common7\IDE\PrivateAssemblies\\* .

3. 在 Visual Studio 命令提示符下键入**devenv /rootsuffix Exp**打开 Visual Studio 的实验实例。

4. 在实验实例中，转到**工具** > **选项** > **环境** > **启动**页上，并选择从 XAML 文件**自定义起始页**下拉列表。

5. 在“视图”  菜单上，单击“起始页”  。

     应显示你的自定义起始页。 如果你想要更改的任何文件，必须关闭实验实例，进行更改、 复制和粘贴已更改的文件，以及然后重新打开实验实例，以查看所做的更改。

### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>要应用自定义起始页中的 Visual Studio 主实例

- 已测试你的起始页并发现它是稳定后，使用**自定义起始页**选项**选项**对话框可以选择在 Visual Studio 的主实例中的起始页

## <a name="see-also"></a>请参阅

- [演练：将自定义 XAML 添加到启动页](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
- [将用户控件添加到启动页](../extensibility/adding-user-control-to-the-start-page.md)
- [将 Visual Studio 命令添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
- [演练：起始页上保存用户设置](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)
- [部署自定义起始页](../extensibility/deploying-custom-start-pages.md)
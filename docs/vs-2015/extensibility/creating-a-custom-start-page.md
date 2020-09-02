---
title: 创建自定义起始页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: acb7922658a5dd7db0839051a42a119733c8b1d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184208"
---
# <a name="creating-a-custom-start-page"></a>创建自定义起始页
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果无法通过使用 "起始页" 项目模板创建自定义起始页（如 [起始](../misc/creating-your-own-start-page.md)页中所述），则可以按照本文档中的步骤手动创建一个。  
  
## <a name="creating-a-blank-start-page"></a>创建一个空白起始页  
 首先，创建一个包含 Visual Studio 将识别的标记结构的 .xaml 文件，从而创建一个空白起始页。 然后，添加标记和代码隐藏以生成所需的外观和功能。  
  
#### <a name="to-create-a-blank-start-page"></a>创建空白起始页  
  
1. 在**Visual c #/Windows Desktop** (创建 " **WPF 应用程序**" 类型的新项目。  
  
2. 添加对 `Microsoft.VisualStudio.Shell.14.0` 的引用。  
  
3. 在 XML 编辑器中打开该 XAML 文件，将顶级 \<Window> 元素更改为一个元素， \<UserControl> 而无需删除任何命名空间声明。  
  
4. `x:Class`从顶级元素中删除声明。 这使得 XAML 内容与承载起始页的 Visual Studio 工具窗口兼容。  
  
5. 将以下命名空间声明添加到顶级 \<UserControl> 元素。  
  
    ```  
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"  
    ```  
  
     通过这些命名空间，你可以访问 Visual Studio 命令、控件和 UI 设置。 有关详细信息，请参阅 [将 Visual Studio 命令添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)。  
  
     下面的示例演示了一个空白起始页的 .xaml 文件中的标记。 所有自定义内容应在内部 <xref:System.Windows.Controls.Grid> 元素中。  
  
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
  
6. 向空元素添加控件 \<UserControl> 以填充自定义起始页。 有关如何添加特定于 Visual Studio 的功能的信息，请参阅 [将 Visual Studio 命令添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)。  
  
## <a name="testing-and-applying-the-custom-start-page"></a>测试并应用自定义起始页  
 在验证它不会使 Visual Studio 崩溃之前，不要将 Visual Studio 的主实例设置为运行自定义起始页。 相反，请在实验实例中对其进行测试。  
  
#### <a name="to-test-a-manually-created-custom-start-page"></a>测试手动创建的自定义起始页  
  
1. 将 XAML 文件和任何支持的文本文件或标记文件复制到 **%USERPROFILE%\My Documents\Visual Studio 2015 \ StartPages \\ **文件夹中。  
  
2. 如果起始页引用 Visual Studio 未安装的程序集中的任何控件或类型，请复制这些程序集，然后将其粘贴到_Visual studio 安装文件夹_**\Common7\IDE\PrivateAssemblies \\ **中。  
  
3. 在 Visual Studio 命令提示符处，键入 **devenv/Rootsuffix Exp** 来打开 Visual studio 的实验实例。  
  
4. 在实验实例中，请切换到 " **工具/选项/环境/启动** " 页，然后从 " **自定义起始页** " 下拉列表中选择您的 XAML 文件。  
  
5. 在“视图” **** 菜单上，单击“起始页” ****。  
  
     应显示自定义起始页。 如果要更改任何文件，则必须关闭实验实例，进行更改，复制并粘贴已更改的文件，然后重新打开实验实例以查看更改。  
  
#### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>在 Visual Studio 的主实例中应用自定义起始页  
  
- 在测试起始页并发现它稳定后，使用 "**选项**" 对话框中的 "**自定义起始页**" 选项将其选择为 Visual Studio 主实例中的起始页  
  
## <a name="see-also"></a>另请参阅  
 [演练：将自定义 XAML 添加到起始页](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)   
 [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)   
 [将 Visual Studio 命令添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)   
 [演练：在起始页上保存用户设置](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)   
 [部署自定义起始页](../extensibility/deploying-custom-start-pages.md)

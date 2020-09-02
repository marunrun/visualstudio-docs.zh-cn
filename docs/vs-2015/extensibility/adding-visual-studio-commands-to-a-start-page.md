---
title: 将 Visual Studio 命令添加到起始页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0a2042ef9a96eed99636ea0a2f5f09d99cd35ea2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65699157"
---
# <a name="adding-visual-studio-commands-to-a-start-page"></a>将 Visual Studio 命令添加到起始页
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建自定义起始页时，可以向其添加 Visual Studio 命令。 本文档介绍将 Visual Studio 命令绑定到起始页上 XAML 对象的不同方法。  
  
 有关 XAML 中的命令的详细信息，请参阅命令 [概述](https://msdn.microsoft.com/library/bc208dfe-367d-426a-99de-52b7e7511e81)  
  
## <a name="adding-commands-from-the-command-well"></a>从命令添加命令良好  
 创建 [自定义起始页](../extensibility/creating-a-custom-start-page.md) 时创建的起始页添加了 <xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName> 和 <xref:Microsoft.VisualStudio.Shell?displayProperty=fullName> 命名空间，如下所示。  
  
```  
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"  
```  
  
 从程序集 Microsoft.VisualStudio.Shell.Immutable.11.0.dll 中为 VisualStudio 添加另一个命名空间。  (可能需要在项目中添加对此程序集的引用 )   
  
```xml  
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"  
```  
  
 可以 `vscom:` 通过将控件的属性设置为，使用别名将 Visual Studio 命令绑定到页面上的 XAML 控件 <xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A> `vscom:VSCommands.ExecuteCommand` 。 然后，可以将 <xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A> 属性设置为要执行的命令的名称，如下面的示例中所示。  
  
```xml  
<Button Name="btnNewProj" Content="New Project"   
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
    CommandParameter="File.NewProject" >  
</Button>  
```  
  
> [!NOTE]
> 在 `x:` 所有命令的开头都需要有引用 XAML 架构的别名。  
  
 可以将属性的值设置 `Command` 为可从 " **命令** " 窗口访问的任何命令。 有关可用命令的列表，请参阅 [Visual Studio 命令别名](../ide/reference/visual-studio-command-aliases.md)。  
  
 如果要添加的命令需要其他参数，可以将其添加到属性的值 `CommandParameter` 。 使用空格分隔命令中的参数，如下面的示例中所示。  
  
```xml  
<Button Content="Web Search"   
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
        CommandParameter="View.WebBrowser www.bing.com" />  
```  
  
### <a name="calling-extensions-from-the-command-well"></a>正在从命令中调用扩展  
 可以通过使用用于调用其他 Visual Studio 命令的语法来调用已注册 Vspackage 中的命令。 例如，如果已安装的 VSPackage 将 **主页** 命令添加到 " **视图** " 菜单，则可以通过将设置为来调用该命令 `CommandParameter` `View.HomePage` 。  
  
> [!NOTE]
> 如果调用与 VSPackage 关联的命令，则在调用该命令时必须加载包。  
  
## <a name="adding-commands-from-assemblies"></a>从程序集添加命令  
 若要从程序集调用命令，或若要访问 VSPackage 中与菜单命令无关的代码，则必须为该程序集创建一个别名，然后调用该别名。  
  
#### <a name="to-call-a-command-from-an-assembly"></a>从程序集调用命令  
  
1. 在解决方案中，添加对程序集的引用。  
  
2. 在 StartPage 文件的顶部，为程序集添加命名空间指令，如以下示例中所示。  
  
    ```xml  
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"  
    ```  
  
3. 通过设置 XAML 对象的属性来调用命令 `Command` ，如以下示例中所示。  
  
     Xaml  
  
    ```  
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>  
    ```  
  
> [!NOTE]
> 必须复制程序集，然后将其粘贴到中。 \\*Visual Studio 安装文件夹*\Common7\IDE\PrivateAssemblies\，以确保在调用之前加载它。  
  
## <a name="adding-commands-with-the-dte-object"></a>添加带有 DTE 对象的命令  
 你可以在 "标记" 和 "代码" 中从起始页访问 DTE 对象。  
  
 在标记中，可以通过使用 [绑定标记扩展](https://msdn.microsoft.com/library/83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63) 语法来调用 <xref:EnvDTE.DTE> 对象。 您可以使用此方法绑定到简单的属性（如返回集合的属性），但不能绑定到方法或服务。 下面的示例演示 <xref:System.Windows.Controls.TextBlock> 绑定到属性的控件 <xref:EnvDTE._DTE.Name%2A> ，以及一个 <xref:System.Windows.Controls.ListBox> 枚举 <xref:EnvDTE.Window.Caption%2A> 属性返回的集合的属性的控件 <xref:EnvDTE._DTE.Windows%2A> 。  
  
```xml  
<TextBlock Text="{Binding Path=DTE.Name}" FontSize="12" HorizontalAlignment="Center"/>  
<ListBox ItemsSource="{Binding Path=DTE.Windows}">  
    <ListBox.ItemTemplate>  
        <DataTemplate>  
            <TextBlock Text="{Binding Path=Caption}"/>  
        </DataTemplate>  
    </ListBox.ItemTemplate>  
</ListBox  
```  
  
 有关示例，请参阅 [演练：在起始页上保存用户设置](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)。  
  
## <a name="see-also"></a>另请参阅  
 [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)

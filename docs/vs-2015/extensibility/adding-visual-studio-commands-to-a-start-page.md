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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699157"
---
# <a name="adding-visual-studio-commands-to-a-start-page"></a>将 Visual Studio 命令添加到起始页
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当创建自定义起始页时，可以将 Visual Studio 命令添加到它。 本文档讨论了将 Visual Studio 命令绑定到 XAML 对象起始页上的不同方式。  
  
 有关在 XAML 中的命令的详细信息，请参阅[命令概述](https://msdn.microsoft.com/library/bc208dfe-367d-426a-99de-52b7e7511e81)  
  
## <a name="adding-commands-from-the-command-well"></a>还将命令添加命令  
 开始页中创建[创建自定义起始页](../extensibility/creating-a-custom-start-page.md)添加<xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName>和<xref:Microsoft.VisualStudio.Shell?displayProperty=fullName>命名空间，按如下所示。  
  
```  
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"  
```  
  
 从程序集 Microsoft.VisualStudio.Shell.Immutable.11.0.dll Microsoft.VisualStudio.Shell 添加另一个命名空间。 （您可能需要在项目中添加对此程序集的引用。）  
  
```xml  
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"  
```  
  
 可以使用`vscom:`页上，通过设置控件绑定到 XAML 的 Visual Studio 命令别名<xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A>该控件的属性`vscom:VSCommands.ExecuteCommand`。 然后，可以设置<xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A>属性设置为要执行，如下面的示例中所示的命令的名称。  
  
```xml  
<Button Name="btnNewProj" Content="New Project"   
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
    CommandParameter="File.NewProject" >  
</Button>  
```  
  
> [!NOTE]
> `x:`别名引用的 XAML 架构，是必需的所有命令的开头。  
  
 可以设置的值`Command`属性设置为从可以访问任何命令**命令**窗口。 有关可用命令的列表，请参阅[Visual Studio 命令别名](../ide/reference/visual-studio-command-aliases.md)。  
  
 如果要添加的命令需要一个附加参数，可以将其添加到的值`CommandParameter`属性。 通过使用空格，如下面的示例中所示的命令从单独的参数。  
  
```xml  
<Button Content="Web Search"   
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
        CommandParameter="View.WebBrowser www.bing.com" />  
```  
  
### <a name="calling-extensions-from-the-command-well"></a>从该命令还调用扩展  
 通过使用相同的语法，用于调用其他 Visual Studio 命令，可以从已注册 Vspackage 调用命令。 例如，如果添加了已安装的 VSPackage**主页**命令**视图**菜单中，您可以通过设置调用该命令`CommandParameter`到`View.HomePage`。  
  
> [!NOTE]
> 如果调用 VSPackage 与关联的命令，在调用命令时，必须加载包。  
  
## <a name="adding-commands-from-assemblies"></a>将命令添加从程序集  
 若要从程序集，或访问代码不是与菜单命令相关联的 VSPackage 中调用命令，你必须为程序集创建别名，然后调用该别名。  
  
#### <a name="to-call-a-command-from-an-assembly"></a>若要从程序集调用命令  
  
1. 在解决方案中，添加对程序集的引用。  
  
2. 在 StartPage.xaml 文件的顶部，添加的命名空间指令程序集，如下面的示例中所示。  
  
    ```xml  
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"  
    ```  
  
3. 通过设置调用命令`Command`XAML 对象，如下面的示例中所示的属性。  
  
     Xaml  
  
    ```  
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>  
    ```  
  
> [!NOTE]
> 必须复制您的程序集，然后将其粘贴在...\\ *Visual Studio 安装文件夹*\Common7\IDE\PrivateAssemblies\ 以确保加载之前调用它。  
  
## <a name="adding-commands-with-the-dte-object"></a>将命令添加与 DTE 对象  
 您可以从起始页，在标记和代码中访问 DTE 对象。  
  
 在标记中，你可以通过访问它使用[绑定标记扩展](https://msdn.microsoft.com/library/83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63)语法调用<xref:EnvDTE.DTE>对象。 可以使用此方法将绑定到简单属性，如返回集合，但不能绑定到方法或服务。 下面的示例演示<xref:System.Windows.Controls.TextBlock>绑定到控件<xref:EnvDTE._DTE.Name%2A>属性，和一个<xref:System.Windows.Controls.ListBox>枚举的控件<xref:EnvDTE.Window.Caption%2A>返回的集合的属性<xref:EnvDTE._DTE.Windows%2A>属性。  
  
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
  
 有关示例，请参阅[演练：将用户设置保存在起始页上](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)。  
  
## <a name="see-also"></a>请参阅  
 [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)

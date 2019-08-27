---
title: 将 Visual Studio 命令添加到起始页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 86fe084d2dab10ed7370f5fc5b99931491b096be
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352281"
---
# <a name="add-visual-studio-commands-to-a-start-page"></a>将 Visual Studio 命令添加到起始页

当创建自定义起始页时，可以将 Visual Studio 命令添加到它。 本文档讨论了将 Visual Studio 命令绑定到 XAML 对象在起始页上的不同方式。

有关在 XAML 中的命令的详细信息，请参阅[Commanding 概述](/dotnet/framework/wpf/advanced/commanding-overview)

## <a name="add-commands-from-the-command-well"></a>还将命令添加命令

启动页中创建[创建自定义起始页](../extensibility/creating-a-custom-start-page.md)添加<xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName>和<xref:Microsoft.VisualStudio.Shell?displayProperty=fullName>命名空间，按如下所示。

```xml
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

从程序集的 Microsoft.VisualStudio.Shell 添加另一个命名空间*Microsoft.VisualStudio.Shell.Immutable.11.0.dll*。 （您可能需要在项目中添加对此程序集的引用。）

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

### <a name="call-extensions-from-the-command-well"></a>也从该命令调用扩展
 通过使用相同的语法，用于调用其他 Visual Studio 命令，可以从已注册 Vspackage 调用命令。 例如，如果添加了已安装的 VSPackage**主页**命令**视图**菜单中，您可以通过设置调用该命令`CommandParameter`到`View.HomePage`。

> [!NOTE]
> 如果调用 VSPackage 与关联的命令，在调用命令时，必须加载包。

## <a name="add-commands-from-assemblies"></a>从程序集添加命令
 若要从程序集，或访问代码不是与菜单命令相关联的 VSPackage 中调用命令，你必须为程序集创建别名，然后调用该别名。

### <a name="to-call-a-command-from-an-assembly"></a>若要从程序集调用命令

1. 在解决方案中，添加对程序集的引用。

2. 在顶部*StartPage.xaml*文件，将命名空间指令添加程序集，如下面的示例中所示。

    ```xml
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
    ```

3. 通过设置调用命令`Command`XAML 对象，如下面的示例中所示的属性。

     Xaml

    ```
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>
    ```

> [!NOTE]
> 必须复制您的程序集，然后将其粘贴在 *...\\{Visual Studio 安装文件夹} \Common7\IDE\PrivateAssemblies\*以确保加载之前调用它。

## <a name="add-commands-with-the-dte-object"></a>添加与 DTE 对象的命令
 您可以从起始页，在标记和代码中访问 DTE 对象。

 在标记中，你可以通过访问它使用[绑定标记扩展](/dotnet/framework/wpf/advanced/binding-markup-extension)语法调用<xref:EnvDTE.DTE>对象。 可以使用此方法将绑定到简单属性，如返回集合，但不能绑定到方法或服务。 下面的示例演示<xref:System.Windows.Controls.TextBlock>绑定到控件<xref:EnvDTE._DTE.Name%2A>属性，和一个<xref:System.Windows.Controls.ListBox>枚举的控件<xref:EnvDTE.Window.Caption%2A>返回的集合的属性<xref:EnvDTE._DTE.Windows%2A>属性。

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

- [将用户控件添加到启动页](../extensibility/adding-user-control-to-the-start-page.md)
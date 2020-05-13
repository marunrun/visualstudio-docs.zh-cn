---
title: 将可视化工作室命令添加到"开始"页面 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 13dd40006039209b06cc6a71760fdbaa240db4fe
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740113"
---
# <a name="add-visual-studio-commands-to-a-start-page"></a>将可视化工作室命令添加到"开始"页

创建自定义"开始页"时，可以将 Visual Studio 命令添加到其中。 本文档讨论了将 Visual Studio 命令绑定到"开始"页上的 XAML 对象的不同方法。

有关 XAML 中命令的详细信息，请参阅[命令概述](/dotnet/framework/wpf/advanced/commanding-overview)

## <a name="add-commands-from-the-command-well"></a>从命令井添加命令

在[创建自定义"开始页"](../extensibility/creating-a-custom-start-page.md)中创建的"开始页<xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName>"<xref:Microsoft.VisualStudio.Shell?displayProperty=fullName>添加了 和命名空间，如下所示。

```xml
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

从程序集微软 *.VisualStudio.Shell*添加另一个命名空间。 （您可能需要在项目中添加对此程序集的引用。

```xml
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"
```

通过将控件`vscom:`<xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A>的属性设置为，可以使用别名将 Visual Studio 命令绑定到页面上的 XAML 控件`vscom:VSCommands.ExecuteCommand`。 然后，<xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A>您可以将该属性设置为要执行的命令的名称，如以下示例所示。

```xml
<Button Name="btnNewProj" Content="New Project"
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
    CommandParameter="File.NewProject" >
</Button>
```

> [!NOTE]
> 该`x:`别名（引用 XAML 架构）在所有命令的开头都是必需的。

 您可以将`Command`属性的值设置为可以从**命令**窗口访问的任何命令。 有关可用命令的列表，请参阅[可视化工作室命令别名](../ide/reference/visual-studio-command-aliases.md)。

 如果要添加的命令需要其他参数，则可以将其添加到`CommandParameter`属性的值。 通过使用空格将参数与命令分开，如以下示例所示。

```xml
<Button Content="Web Search"
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"
        CommandParameter="View.WebBrowser www.bing.com" />
```

### <a name="call-extensions-from-the-command-well"></a>从命令井调用分机
 您可以使用用于调用其他 Visual Studio 命令的相同语法从已注册的 VSPackages 调用命令。 例如，如果已安装的 VSPackage 将**主页**命令添加到 **"视图"** 菜单中，则可以通过设置为`CommandParameter`调用该`View.HomePage`命令。

> [!NOTE]
> 如果调用与 VSPackage 关联的命令，则必须在调用该命令时加载包。

## <a name="add-commands-from-assemblies"></a>从程序集添加命令
 要从程序集调用命令，或访问未与菜单命令关联的 VSPackage 中的代码，必须为程序集创建别名，然后调用别名。

### <a name="to-call-a-command-from-an-assembly"></a>从程序集调用命令

1. 在解决方案中，添加对程序集的引用。

2. 在*StartPage.xaml*文件的顶部，为程序集添加命名空间指令，如以下示例所示。

    ```xml
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
    ```

3. 通过设置 XAML`Command`对象的属性来调用命令，如以下示例所示。

     Xaml

    ```
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>
    ```

> [!NOTE]
> 您必须复制程序集，然后将其粘贴到 *中。\\{可视化工作室安装文件夹{通用 7}IDE_私有程序集\*，以确保在调用之前加载它。

## <a name="add-commands-with-the-dte-object"></a>使用 DTE 对象添加命令
 您可以在标记和代码中从起始页访问 DTE 对象。

 在标记中，可以使用[绑定标记扩展语法](/dotnet/framework/wpf/advanced/binding-markup-extension)来调用<xref:EnvDTE.DTE>对象来访问它。 可以使用此方法绑定到简单属性，例如返回集合的属性，但不能绑定到方法或服务。 下面的示例显示<xref:System.Windows.Controls.TextBlock>绑定到 属性的<xref:EnvDTE._DTE.Name%2A>控件，以及枚举属性返回<xref:System.Windows.Controls.ListBox>的集合<xref:EnvDTE.Window.Caption%2A>的属性的<xref:EnvDTE._DTE.Windows%2A>控件。

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

 例如，请参阅[演练：在"开始页"上保存用户设置](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)。

## <a name="see-also"></a>请参阅

- [将用户控件添加到"开始页"](../extensibility/adding-user-control-to-the-start-page.md)

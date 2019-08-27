---
title: 演练：在起始页上保存用户设置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 79a54867044961d972e2ded452958d2463038e7d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318518"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>演练：起始页上保存用户设置

您可以保留用户设置的起始页。 通过完成本演练，您可以创建将设置保存到注册表，当用户单击某个按钮，然后检索该设置，每次加载起始页的控件。 起始页项目模板包括一个可自定义用户控件，并且默认开始页 XAML 将调用该控件，因为您无需修改启动页本身。

在本演练中实例化的设置存储出现的实例<xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore>接口，它读取并写入以下注册表位置时调用它：**HKCU\Software\Microsoft\VisualStudio\14.0\\\<CollectionName>**

当 Visual Studio 的实验实例中运行它时，设置存储读取并写入**HKCU\Software\Microsoft\VisualStudio\14.0Exp\\\<集合名称 >。**

有关如何保存设置的详细信息，请参阅[扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)。

## <a name="prerequisites"></a>系统必备

> [!NOTE]
> 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。
>
> 可以使用下载起始页项目模板**扩展管理器**。

## <a name="set-up-the-project"></a>设置项目

1. 创建起始页项目中所述[创建自定义起始页](creating-a-custom-start-page.md)。 将项目命名**SaveMySettings**。

2. 在中**解决方案资源管理器**，添加对 StartPageControl 项目的以下程序集引用：

    - EnvDTE

    - EnvDTE80

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.Shell.Interop.11.0

3. 打开*MyControl.xaml*。

4. 从 XAML 窗格中的顶级<xref:System.Windows.Controls.UserControl>元素定义，添加以下命名空间声明后的事件声明。

    ```xml
    Loaded="OnLoaded"
    ```

5. 在设计窗格中，单击该控件的主区域，然后按**删除**。

     此步骤中删除<xref:System.Windows.Controls.Border>元素和其中的所有内容，并且将只返回前留级别<xref:System.Windows.Controls.Grid>元素。

6. 从**工具箱**，拖动<xref:System.Windows.Controls.StackPanel>到网格控件。

7. 现在拖动<xref:System.Windows.Controls.TextBlock>、 一个<xref:System.Windows.Controls.TextBox>，和一个按钮<xref:System.Windows.Controls.StackPanel>。

8. 添加**X:name**特性<xref:System.Windows.Controls.TextBox>，和一个`Click`事件<xref:System.Windows.Controls.Button>，如以下示例所示。

    ```xml
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />
        <Button Click="Button_Click" Width="100">Save My Setting</Button>
    </StackPanel>
    ```

## <a name="implement-the-user-control"></a>实现用户控件

1. 在 XAML 窗格中，右键单击`Click`的属性<xref:System.Windows.Controls.Button>元素，并单击**定位到事件处理程序**。

     此步骤将打开*MyControl.xaml.cs*，并创建一个存根 （stub） 处理程序`Button_Click`事件。

2. 以下代码添加到`using`到文件顶部的语句。

     [!code-csharp[StartPageDTE#11](../extensibility/codesnippet/CSharp/walkthrough-saving-user-settings-on-a-start-page_1.cs)]

3. 添加一个私有`SettingsStore`属性，如下面的示例中所示。

    ```csharp
    private IVsWritableSettingsStore _settingsStore = null;
    private IVsWritableSettingsStore SettingsStore
    {
        get
        {
            if (_settingsStore == null)
            {
                // Get a reference to the DTE from the DataContext.
                var typeDescriptor = DataContext as ICustomTypeDescriptor;
                var propertyCollection = typeDescriptor.GetProperties();
                var dte = propertyCollection.Find("DTE", false).GetValue(
                    DataContext) as DTE2;

                // Get the settings manager from the DTE.
                var serviceProvider = new ServiceProvider(
                    (Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);
                var settingsManager = serviceProvider.GetService(
                    typeof(SVsSettingsManager)) as IVsSettingsManager;

                // Write the user settings to _settingsStore.
                settingsManager.GetWritableSettingsStore(
                    (uint)__VsSettingsScope.SettingsScope_UserSettings,
                    out _settingsStore);
            }
            return _settingsStore;
        }
    }
    ```

     此属性首先获取对<xref:EnvDTE80.DTE2>接口，其中包含自动化对象模型中，从<xref:System.Windows.FrameworkElement.DataContext%2A>的用户控件，然后使用 DTE 若要获取的实例<xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager>接口。 然后它使用该实例将返回当前用户设置。

4. 填写`Button_Click`事件，如下所示。

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {
        int exists = 0;
        SettingsStore.CollectionExists("MySettings", out exists);
        if (exists != 1)
        {
            SettingsStore.CreateCollection("MySettings");
        }
        SettingsStore.SetString("MySettings", "MySetting", txtblk.Text);
    }
    ```

     这将在文本框中的内容写入到注册表中的"Mysetting"集合中的"MySetting"字段。 如果集合不存在，则创建它。

5. 添加以下处理程序`OnLoaded`用户控件的事件。

    ```csharp
    private void OnLoaded(Object sender, RoutedEventArgs e)
    {
        string value;
        SettingsStore.GetStringOrDefault(
            "MySettings", "MySetting", "", out value);
        txtblk.Text = value;
    }
    ```

     此代码设置为"MySetting"的当前值的文本框中的文本。

6. 生成用户控件。

7. 在中**解决方案资源管理器**，打开*source.extension.vsixmanifest*。

8. 在清单编辑器中，设置**产品名称**到**保存我的设置起始页**。

     此功能设置启动页的名称，因为它是出现在**自定义起始页**列表中**选项**对话框。

9. 构建*StartPage.xaml*。

## <a name="test-the-control"></a>测试控件

1. 按 F5  。

     此时将打开 Visual Studio 的实验实例。

2. 在实验实例上**工具**菜单上，单击**选项**。

3. 在中**环境**节点中，单击**启动**，然后在**自定义起始页**列表中，选择 **[已安装的扩展] 保存我设置起始页**.

     单击 **“确定”** 。

4. 关闭已打开，，然后在启动页**视图**菜单上，单击**起始页**。

5. 在启动页上单击**MyControl**选项卡。

6. 在文本框中，键入**Cat**，然后单击**保存我的设置**。

7. 关闭启动页并重新打开它。

     应在文本框中显示单词"Cat"。

8. 将"Dog"一词替换为单词"Cat"。 请不要单击该按钮。

9. 关闭启动页并重新打开它。

     在文本框中，应显示单词"Dog"，即使您没有保存设置因为 Visual Studio 工具窗口将在内存中，即使它们都将关闭，直到关闭 Visual Studio 本身也是如此。

10. 关闭 Visual Studio 的实验实例。

11. 按**F5**以重新打开实验实例。

12. 应在文本框中显示单词"Cat"。

## <a name="next-steps"></a>后续步骤

您可以修改此用户控件来保存和检索任意数量的自定义设置通过使用从不同的事件处理程序的不同值来获取和设置`SettingsStore`属性。 只要您使用不同`propertyName`每次调用的参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A>，值不会相互覆盖注册表中。

## <a name="see-also"></a>请参阅

- <xref:EnvDTE80.DTE2?displayProperty=fullName>
- [将 Visual Studio 命令添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
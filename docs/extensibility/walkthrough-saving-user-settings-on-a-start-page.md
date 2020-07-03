---
title: 演练：在起始页上保存用户设置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8dd20513defd1db8848cf6a80a29e04c127c9dd4
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903161"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>演练：在起始页上保存用户设置

你可以保留起始页的用户设置。 按照此演练操作，你可以创建一个控件，用于在用户单击按钮时将设置保存到注册表，然后在每次加载起始页时检索该设置。 由于起始页项目模板包含一个可自定义的用户控件，并且默认起始页 XAML 调用了该控件，因此您无需修改起始页本身。

此演练中实例化的设置存储是接口的实例，该实例在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore> 调用时读取并写入以下注册表位置： **HKCU\Software\Microsoft\VisualStudio\14.0 \\ \<CollectionName> **

在 Visual Studio 的实验实例中运行时，设置会将读取和写入操作存储到**HKCU\Software\Microsoft\VisualStudio\14.0Exp \\ \<CollectionName> 。**

有关如何保存设置的详细信息，请参阅[扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)。

## <a name="prerequisites"></a>必备条件

> [!NOTE]
> 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。
>
> 您可以使用 "**扩展管理器**" 下载 "起始页" 项目模板。

## <a name="set-up-the-project"></a>设置项目

1. 如[创建自定义起始页](creating-a-custom-start-page.md)中所述，创建起始页项目。 将项目命名为**SaveMySettings**。

2. 在**解决方案资源管理器**中，将以下程序集引用添加到 StartPageControl 项目：

    - EnvDTE

    - EnvDTE80

    - VisualStudio。

    - VisualStudio （web.config）

3. 打开*mycontrol.xaml*。

4. 在 "XAML" 窗格的顶级 <xref:System.Windows.Controls.UserControl> 元素定义中，在命名空间声明后面添加以下事件声明。

    ```xml
    Loaded="OnLoaded"
    ```

5. 在 "设计" 窗格中，单击控件的主区域，然后按 "**删除**"。

     此步骤删除 <xref:System.Windows.Controls.Border> 元素和其中的所有内容，并且仅留下顶级 <xref:System.Windows.Controls.Grid> 元素。

6. 从 "**工具箱**" 中，将 <xref:System.Windows.Controls.StackPanel> 控件拖动到网格。

7. 现在，将 <xref:System.Windows.Controls.TextBlock> 、 <xref:System.Windows.Controls.TextBox> 和按钮拖动到 <xref:System.Windows.Controls.StackPanel> 。

8. 为提供一个**x：Name**特性，为添加 <xref:System.Windows.Controls.TextBox> 一个 `Click` 事件， <xref:System.Windows.Controls.Button> 如下面的示例中所示。

    ```xml
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />
        <Button Click="Button_Click" Width="100">Save My Setting</Button>
    </StackPanel>
    ```

## <a name="implement-the-user-control"></a>实现用户控件

1. 在 "XAML" 窗格中，右键单击 `Click` 元素的特性 <xref:System.Windows.Controls.Button> ，然后单击 "**导航到事件处理程序**"。

     此步骤将打开*MyControl.xaml.cs*，并为事件创建存根处理程序 `Button_Click` 。

2. 将以下 `using` 指令添加到文件顶部。

     [!code-csharp[StartPageDTE#11](../extensibility/codesnippet/CSharp/walkthrough-saving-user-settings-on-a-start-page_1.cs)]

3. 添加私有 `SettingsStore` 属性，如下面的示例中所示。

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

     此属性首先从用户控件的中获取对接口的引用 <xref:EnvDTE80.DTE2> ，该接口包含自动化对象模型， <xref:System.Windows.FrameworkElement.DataContext%2A> 然后使用 DTE 获取接口的实例 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> 。 然后，它将使用该实例来返回当前用户设置。

4. `Button_Click`按如下所示填写事件。

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

     这会将文本框的内容写入注册表中的 "Mysetting" 集合中的 "MySetting" 字段。 如果该集合不存在，则创建它。

5. 为用户控件的事件添加以下处理程序 `OnLoaded` 。

    ```csharp
    private void OnLoaded(Object sender, RoutedEventArgs e)
    {
        string value;
        SettingsStore.GetStringOrDefault(
            "MySettings", "MySetting", "", out value);
        txtblk.Text = value;
    }
    ```

     此代码将文本框的文本设置为 "MySetting" 的当前值。

6. 生成用户控件。

7. 在**解决方案资源管理器**中，打开*source.extension.vsixmanifest*。

8. 在清单编辑器中，将 "**产品名称**" 设置为 **"保存我的设置" "起始页**"。

     此功能设置起始页的名称，因为它将显示在 "**选项**" 对话框的 "**自定义起始页**" 列表中。

9. 生成*StartPage. xaml*。

## <a name="test-the-control"></a>测试控件

1. 按 **F5**。

     此时将打开 Visual Studio 的实验实例。

2. 在实验实例中，单击 "**工具**" 菜单上的 "**选项**"。

3. 在 "**环境**" 节点中，单击 "**启动**"，然后在 "**自定义起始页**" 列表中，选择 "**已安装扩展" "保存我的设置起始页**"。

     单击 **“确定”** 。

4. 如果 "起始页" 处于打开状态，请将其关闭，然后在 "**视图**" 菜单上单击 "**起始页**"。

5. 在 "开始" 页上，单击 " **mycontrol.xaml** " 选项卡。

6. 在文本框中，键入**Cat**，然后单击 **"保存我的设置**"。

7. 关闭起始页，然后重新打开它。

     文本框中应显示 "Cat" 一词。

8. 将单词 "Cat" 替换为 "Dog"。 不要单击该按钮。

9. 关闭起始页，然后重新打开它。

     即使未保存设置，也不会在文本框中显示 "Dog" 字样，因为 Visual Studio 会在内存中保留工具窗口，即使它们已关闭，在 Visual Studio 本身关闭时也是如此。

10. 关闭 Visual Studio 的实验实例。

11. 按**F5**重新打开实验实例。

12. 文本框中应显示 "Cat" 一词。

## <a name="next-steps"></a>后续步骤

您可以通过使用不同事件处理程序中的不同值来修改和检索任意数量的自定义设置，以获取和设置 `SettingsStore` 属性。 只要 `propertyName` 对的每个调用使用不同的参数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A> ，这些值就不会在注册表中相互覆盖。

## <a name="see-also"></a>另请参阅

- <xref:EnvDTE80.DTE2?displayProperty=fullName>
- [将 Visual Studio 命令添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)

---
title: 演练：在"开始"页上保存用户设置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8c791bb33d6c6a3952c14d5073857b0c3131cecf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697081"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>演练：在"开始"页上保存用户设置

您可以保留"开始页面"的用户设置。 通过本演练，您可以创建一个控件，在用户单击按钮时将设置保存到注册表中，然后在每次加载"开始页"时检索该设置。 由于"开始页"项目模板包含可自定义的用户控件，以及默认的"开始页 XAML"调用该控件，因此您不必修改"起始页"本身。

本演练中实例化的设置存储是<xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore>接口的实例，该接口在调用时读取并写入以下注册表位置 **：HKCU_Software_Microsoft_VisualStudio_14.0\\\<集合名称>**

当它在 Visual Studio 的实验实例中运行时，设置存储读取并写入**HKCU_软件_Microsoft_VisualStudio_14.0Exp\\\<集合名称>。**

有关如何保留设置的详细信息，请参阅[扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)。

## <a name="prerequisites"></a>先决条件

> [!NOTE]
> 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。
>
> 您可以使用**扩展管理器**下载"开始页"项目模板。

## <a name="set-up-the-project"></a>设置项目

1. 创建"[创建自定义起始页"](creating-a-custom-start-page.md)中所述的"开始页"项目。 命名项目 **"保存我的设置"。**

2. 在**解决方案资源管理器中**，向 StartPageControl 项目添加以下程序集引用：

    - EnvDTE

    - EnvDTE80

    - 微软.VisualStudio.OLE.Interop

    - 微软.VisualStudio.shell.Interop.11.0

3. 打开*MyControl.xaml*。

4. 在顶级<xref:System.Windows.Controls.UserControl>元素定义中，在 XAML 窗格中，在命名空间声明之后添加以下事件声明。

    ```xml
    Loaded="OnLoaded"
    ```

5. 在设计窗格中，单击控件的主要区域，然后按 **"删除**"。

     此步骤将删除<xref:System.Windows.Controls.Border>元素及其中的所有内容，并仅保留顶级<xref:System.Windows.Controls.Grid>元素。

6. 从**工具箱**中，将<xref:System.Windows.Controls.StackPanel>控件拖动到网格。

7. 现在将<xref:System.Windows.Controls.TextBlock>.<xref:System.Windows.Controls.TextBox>和 按钮拖动到<xref:System.Windows.Controls.StackPanel>。

8. 为 添加 的<xref:System.Windows.Controls.TextBox> **x：name**属性`Click`，并为<xref:System.Windows.Controls.Button>添加事件，如以下示例所示。

    ```xml
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />
        <Button Click="Button_Click" Width="100">Save My Setting</Button>
    </StackPanel>
    ```

## <a name="implement-the-user-control"></a>实现用户控制

1. 在 XAML 窗格中，右键`Click`单击元素的属性<xref:System.Windows.Controls.Button>，然后单击 **"导航到事件处理程序**"。

     此步骤*将MyControl.xaml.cs*打开，并为`Button_Click`事件创建一个存根处理程序。

2. 将以下`using`指令添加到文件顶部。

     [!code-csharp[StartPageDTE#11](../extensibility/codesnippet/CSharp/walkthrough-saving-user-settings-on-a-start-page_1.cs)]

3. 添加私有`SettingsStore`属性，如以下示例所示。

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

     此属性首先从用户控件获取对包含<xref:EnvDTE80.DTE2>自动化对象模型<xref:System.Windows.FrameworkElement.DataContext%2A>的接口的引用，然后使用 DTE 获取接口的<xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager>实例。 然后，它使用该实例返回当前用户设置。

4. 请填写如下`Button_Click`事件。

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

     这将文本框的内容写入注册表中的"MySettings"集合中的"MySettings"字段。 如果集合不存在，则创建该集合。

5. 为用户控件`OnLoaded`的事件添加以下处理程序。

    ```csharp
    private void OnLoaded(Object sender, RoutedEventArgs e)
    {
        string value;
        SettingsStore.GetStringOrDefault(
            "MySettings", "MySetting", "", out value);
        txtblk.Text = value;
    }
    ```

     此代码将文本框的文本设置为"MySet"的当前值。

6. 生成用户控件。

7. 在**解决方案资源管理器**中，*开源.扩展.vsixmanifest*。

8. 在清单编辑器中，将**产品名称**设置为 **"保存我的设置开始页**"。

     此功能设置"开始页"的名称，因为它将显示在 **"选项**"对话框中的 **"自定义起始页**"列表中。

9. 生成*StartPage.xaml*。

## <a name="test-the-control"></a>测试控件

1. 按 **F5**。

     视觉工作室的实验实例打开。

2. 在实验实例中，在 **"工具"** 菜单上，单击 **"选项**"。

3. 在 **"环境"** 节点中，单击 **"启动**"，然后在 **"自定义开始页"** 列表中选择 **[已安装扩展] 保存我的设置"开始页**"。

     单击“确定”。

4. 如果"开始页"打开，请关闭它，然后在 **"查看"** 菜单上单击 **"开始页**"。

5. 在"开始"页上，单击 **"我的控制"** 选项卡。

6. 在文本框中，键入 **"Cat"，** 然后单击"**保存我的设置**"。

7. 关闭"开始页"，然后再次打开它。

     文本框中应显示"Cat"一词。

8. 将"猫"一词替换为"狗" 一词。 不要单击该按钮。

9. 关闭"开始页"，然后再次打开它。

     "Dog"一词应显示在文本框中，即使您没有保存设置，因为 Visual Studio 会将工具窗口保留在内存中，即使它们已关闭，直到 Visual Studio 本身关闭。

10. 关闭 Visual Studio 的实验实例。

11. 按**F5**重新打开实验实例。

12. 文本框中应显示"Cat"一词。

## <a name="next-steps"></a>后续步骤

您可以使用不同事件处理程序的不同值来获取和设置`SettingsStore`属性，从而修改此用户控件以保存和检索任意数量的自定义设置。 只要对 的每次调用`propertyName`<xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A>使用不同的参数，这些值就不会在注册表中相互覆盖。

## <a name="see-also"></a>请参阅

- <xref:EnvDTE80.DTE2?displayProperty=fullName>
- [将可视化工作室命令添加到"开始"页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)

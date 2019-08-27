---
title: 创建编码的 UI 测试
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 54ebc36f9dd18010e07403c3b9692b62b2380d99
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62976330"
---
# <a name="walkthrough-create-edit-and-maintain-a-coded-ui-test"></a>演练：创建、编辑和维护编码的 UI 测试

在本演练中，你将了解如何创建、编辑和维护编码的 UI 测试来测试 Windows Presentation Framework (WPF) 应用。 本演练提供数个解决方案，用于更正由于各种计时问题和控件重构而中断的测试。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="create-a-wpf-app"></a>创建 WPF 应用

1. 创建新的“WPF 应用(.NET Framework)”项目，并将其命名为 SimpleWPFApp。

     “WPF 设计器”随即打开并显示项目的 MainWindow。

2. 如果当前未打开工具箱，请将其打开。 选择“视图”菜单，然后选择“工具箱”。

3. 在“所有 WPF 控件”部分，将一个“Button”、“CheckBox”和“ProgressBar”控件拖动到设计图面的主窗口中。

4. 选择“Button”控件。 在“属性”窗口中，将“名称”属性的值从 \<无名称> 更改为 button1。 然后将“内容”属性的值从 Button 更改为 Start。

5. 选择“ProgressBar”控件。 在“属性”窗口中，将“名称”属性的值从 \<无名称> 更改为 progressBar1。 然后将“最大值”属性的值从“100”更改为“10000”。

6. 选择“Checkbox”控件。 在“属性”窗口中，将“名称”属性的值从 \<无名称> 更改为 checkBox1，然后清除“IsEnabled”属性。

     ![简单 WPF 应用程序](../test/media/codedui_wpfapp.png)

7. 双击按钮控件，以添加单击事件处理程序。

     将在代码编辑器中显示 MainWindow.xmal.cs，并且游标位于新的 button1_Click 方法中。

8. 在 MainWindow 类的顶部，添加一个委托。 该委托将用于进度栏。 若要添加委托，请添加以下代码：

    ```csharp
    public partial class MainWindow : Window
    {
            private delegate void ProgressBarDelegate(System.Windows.DependencyProperty dp, Object value);

        public MainWindow()
        {

            InitializeComponent();
        }
    ```

9. 在 button1_Click 方法中，添加以下代码：

    ```csharp
    private void button1_Click(object sender, RoutedEventArgs e)
    {
        double progress = 0;

        ProgressBarDelegate updatePbDelegate =
            new ProgressBarDelegate(progressBar1.SetValue);

        do
        {
            progress ++;

            Dispatcher.Invoke(updatePbDelegate,
                System.Windows.Threading.DispatcherPriority.Background,
                new object[] { ProgressBar.ValueProperty, progress });
            progressBar1.Value = progress;
        }
        while (progressBar1.Value != progressBar1.Maximum);

        checkBox1.IsEnabled = true;
    }
    ```

10. 保存该文件。

### <a name="run-the-wpf-app"></a>运行 WPF 应用

1. 在“调试”菜单上，选择“启动调试”或按 F5。

2. 注意该复选框控件此时处于禁用状态。 选择“启动”。

     几秒后，进度栏应 100% 完成。

3. 现在，你可以选择该复选框控件。

4. 关闭 SimpleWPFApp。

## <a name="create-a-shortcut-to-the-wpf-app"></a>创建 WPF 应用的快捷方式

1. 查找你之前创建的 SimpleWPFApp 应用程序。

2. 创建 SimpleWPFApp 应用程序的桌面快捷方式。 右键单击 SimpleWPFApp.exe 并选择“复制”。 在桌面上右键单击，然后选择“粘贴快捷方式”。

    > [!TIP]
    > 使用应用程序的快捷方式可以快速启动应用程序，因此便于为应用程序添加或修改编码的 UI 测试。

## <a name="create-a-coded-ui-test-for-simplewpfapp"></a>为 SimpleWPFApp 创建编码的 UI 测试

1. 在“解决方案资源管理器”中，右键单击解决方案，然后依次选择“添加” > “新建项目”。

2. 搜索并选择“编码的 UI 测试项目”项目模板，并继续执行这些步骤，直到完成项目的创建。

   > [!NOTE]
   > 如未看到“编码的 UI 测试项目”模板，则需要安装[编码的 UI 测试组件](../test/use-ui-automation-to-test-your-code.md#install-the-coded-ui-test-component)。

     新的编码的 UI 测试项目（名为 CodedUITestProject1）将添加到解决方案中，并且系统随即显示“为编码的 UI 测试生成代码”对话框。

1. 选择“录制操作、编辑 UI 映射或添加断言”选项，然后选择“确定”。

     随即显示“UIMap - 编码的 UI 测试生成器”对话框，且 Visual Studio 窗口将最小化。

     有关对话框中选项的详细信息，请参阅[创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md)。

1. 在“UIMap - 编码的 UI 测试生成器”对话框中选择“开始录制”。

     ![开始录制](../test/media/cuit_builder_record.png)

     如果需要，你可以暂停记录（例如，如果你必须处理传入的邮件）。

     ![暂停录制](../test/media/cuit_.png)

    > [!WARNING]
    > 将录制在桌面上执行的所有操作。 如果你正在执行可能会导致敏感数据被包括在录制中的操作，则暂停录制。

1. 使用桌面快捷方式启动 SimpleWPFApp。

     像以前一样，注意该复选框控件此时处于禁用状态。

1. 在 SimpleWPFApp 上选择“启动”。

     几秒后，进度栏应 100% 完成。

1. 选中现在处于启用状态的复选框控件。

1. 关闭 SimpleWPFApp 应用程序。

1. 在“UIMap - 编码的 UI 测试生成器”对话框中，选择“生成代码”。

1. 在“方法名称”中键入 SimpleAppTest，然后选择“添加并生成”。 几秒后，编码的 UI 测试将出现，并且会添加到解决方案中。

1. 关闭“UIMap - 编码的 UI 测试生成器”。

     此时，CodedUITest1.cs 文件会出现在代码编辑器中。

1. 保存你的项目。

### <a name="run-the-test"></a>运行测试

1. 从“测试”菜单中，选择“窗口”，然后选择“测试资源管理器”。

2. 从 **“生成”** 菜单中选择 **“生成解决方案”**。

3. 在 CodedUITest1.cs 文件中，找到 CodedUITestMethod 方法，右键单击并选择“运行测试”，或从“测试资源管理器”中运行该测试。

   当编码的 UI 测试运行时，SimpleWPFApp 将可见。 它会执行你在前面的过程中执行的步骤。 但是，当测试尝试选中复选框控件对应的复选框时，“测试结果”窗口会显示测试未通过。 原因是测试尝试选中该复选框，但不知道复选框控件此时处于禁用状态，直至进度栏 100% 完成为止。 通过可用于编码的 UI 测试的各种 `UITestControl.WaitForControlXXX()` 方法可以更正此问题和类似问题。 下面的过程将演示如何使用 `WaitForControlEnabled()` 方法更正导致此测试未通过的问题。 有关详细信息，请参阅[播放期间让编码的 UI 测试等待特定事件](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)。

## <a name="edit-and-rerun-the-coded-ui-test"></a>编辑并重新运行编码的 UI 测试

1. 在“测试资源管理器”窗口中，选择未通过的测试，然后在 StackTrace 部分中，选择指向 UIMap.SimpleAppTest() 的第一个链接。

2. 将打开 UIMap.Designer.cs 文件，并在代码中突出显示错误点：

    ```csharp
    // Select 'CheckBox' check box
    uICheckBoxCheckBox.Checked = this.SimpleAppTestParams.UICheckBoxCheckBoxChecked;
    ```

3. 若要更正此问题，可以使用 `WaitForControlEnabled()` 方法使编码的 UI 测试等待 CheckBox 控件被启用，然后再继续此行。

    > [!WARNING]
    > 请不要修改 UIMap.Designer.cs 文件。 每次使用“UIMap - 编码的 UI 测试生成器”生成代码时，都会覆盖所有代码更改。 如果必须修改录制的方法，请将其复制到 UIMap.cs 文件并对其重命名。 UIMap.cs 文件可用于重写 UIMapDesigner.cs 文件中的方法和属性。 必须在 CodedUITest.cs 文件中删除对原始方法的引用，并将其替换为重命名的方法名称。

4. 在解决方案资源管理器中，找到编码的 UI 测试项目中的 UIMap.uitest。

5. 打开 *UIMap.uitest* 的快捷菜单并选择“打开”。

     编码的 UI 测试编辑器中将显示编码的 UI 测试。 此时你可以查看并编辑编码的 UI 测试。

6. 在“UI 操作”窗格中，选择要移动到 UIMap.cs 或 UIMap.vb 文件的测试方法 (SimpleAppTest)。 通过将该方法移动到不同的文件中，可以添加自定义代码，重新编译测试代码时，不会覆盖这些自定义代码。

7. 选择“编码的 UI 测试编辑器”工具栏上的“移动代码”按钮。

8. 将显示一个 Microsoft Visual Studio 对话框。 该对话框将警告你，该方法将从 UIMap.uitest 文件移动到 UIMap.cs 文件，无法再使用编码的 UI 测试编辑器来编辑该方法。 选择 **“是”**。

     将从 UIMap.uitest 文件中移除该测试方法，并且“UI 操作”窗格中不再显示该测试方法。 若要编辑移动的测试文件，请从解决方案资源管理器中打开 UIMap.cs 文件。

9. 在 Visual Studio 工具栏上，选择“保存”。

     对测试方法的更新保存在 UIMap.Designer 文件中。

    > [!WARNING]
    > 一旦移动了该方法，你就不再能使用编码的 UI 测试编辑器对其进行编辑。 你必须使用代码编辑器添加并维护你的自定义代码。

10. 将方法由 `SimpleAppTest()` 重命名为 `ModifiedSimpleAppTest()`

11. 将下面的 using 语句添加到文件中：

    ```csharp
    using Microsoft.VisualStudio.TestTools.UITesting.WpfControls;
    ```

12. 在之前标识的有问题的代码行之前添加下面的 `WaitForControlEnabled()` 方法：

    ```csharp
    uICheckBoxCheckBox.WaitForControlEnabled();

    // Select 'CheckBox' check box
    uICheckBoxCheckBox.Checked = this.SimpleAppTestParams.UICheckBoxCheckBoxChecked;
    ```

13. 在 CodedUITest1.cs 文件中，查找 CodedUITestMethod 方法，注释掉或重命名对原始 SimpleAppTest() 方法的引用，然后将其替换为新的 ModifiedSimpleAppTest()：

    ```csharp
    [TestMethod]
            public void CodedUITestMethod1()
            {
                // To generate code for this test, select "Generate Code for Coded UI Test" from the shortcut menu and select one of the menu items.
                // For more information on generated code, see http://go.microsoft.com/fwlink/?LinkId=179463
                //this.UIMap.SimpleAppTest();
                this.UIMap.ModifiedSimpleAppTest();
            }
    ```

14. 在 **“生成”** 菜单上，选择 **“生成解决方案”**。

15. 右键单击 **CodedUITestMethod** 方法，然后选择“运行测试”。

16. 此时，编码的 UI 测试已成功完成测试中的所有步骤，“测试资源管理器”窗口中将显示“已通过”。

## <a name="refactor-a-control-in-simplewpfapp"></a>在 SimpleWPFApp 中重构控件

1. 在 MainWindow.xaml 文件中，在设计器中选择按钮控件。

2. 在属性窗口的顶部，将“名称”属性值从 button1 更改为 buttonA。

3. 在 **“生成”** 菜单上，选择 **“生成解决方案”**。

4. 在“测试资源管理器”中，运行“CodedUITestMethod1”。

     由于编码的 UI 测试找不到最初在 UIMap 映射为 button1 的按钮控件，因此测试未通过。 重构会以此方式对编码的 UI 测试产生影响。

5. 在“测试资源管理器”的 StackTrace 部分中，选择 UIMpa.ModifiedSimpleAppTest() 旁边的第一个链接。

     此时，将打开 UIMap.cs 文件。 代码中将突出显示错误点：

    ```csharp
    // Click 'Start' button
    Mouse.Click(uIStartButton, new Point(27, 10));
    ```

     请注意，此过程前面的代码行使用了 `UiStartButton`，这是重构之前的 UIMap 名称。

     若要更正此问题，可使用编码的 UI 测试生成器向 UIMap 中添加重构的控件。 可以更新测试的代码以使用该代码，如下一过程所示。

## <a name="map-refactored-control-rerun-the-test"></a>在图中显示重构的控件并重新运行测试

1. 在 CodedUITest1.cs 文件的 CodedUITestMethod1() 方法中，右键单击并选择“为编码的 UI 测试生成代码”，然后选择“使用编码的 UI 测试生成器”。

     此时，将出现“UIMap - 编码的 UI 测试生成器”。

2. 使用你之前创建的桌面快捷方式，运行你在之前创建的 SimpleWPFApp 应用程序。

3. 在“UIMap - 编码的 UI 测试生成器”对话框中，将十字线工具拖到 SimpleWPFApp 中的“启动”按钮。

     “启动”按钮包含在蓝色框内。 编码的 UI 测试生成器需要几秒钟来为选定控件处理数据和显示控件属性。 请注意，AutomationUId 的值为 buttonA。

4. 在控件的属性中，选择左上角的箭头以展开 UI 控件图。 请注意，已选择 **UIStartButton1**。

5. 在工具栏中，选择“将控件添加到 UI 控件图”。

     窗口底部的状态通过显示“所选控件已添加到 UI 控件图中”来验证操作。

6. 在“UIMap - 编码的 UI 测试生成器”对话框中，选择“生成代码”。

     此时，将显示“编码的 UI 测试生成器 - 生成代码”对话框，其中包含一个注释，指示不需要任何新方法，只为 UI 控件图的更改生成代码。

7. 选择“生成”。

8. 关闭 SimpleWPFApp。

9. 关闭“UIMap - 编码的 UI 测试生成器”。

10. 在解决方案资源管理器中，打开 UIMap.Designer.cs 文件。

11. 在 UIMap.Designer.cs 文件中，找到 UIStartButton1 属性。 请注意，`SearchProperties` 设置为 `"buttonA"`：

    ```csharp
    public WpfButton UIStartButton1
            {
                get
                {
                    if ((this.mUIStartButton1 == null))
                    {
                        this.mUIStartButton1 = new WpfButton(this);
                        #region Search Criteria
                        this.mUIStartButton1.SearchProperties[WpfButton.PropertyNames.AutomationId] = "buttonA";
                        this.mUIStartButton1.WindowTitles.Add("MainWindow");
                        #endregion
                    }
                    return this.mUIStartButton1;
                }
            }
    ```

     现在，你可以修改编码的 UI 测试，以使用新映射的控件。 如前一过程所述，如果要在编码的 UI 测试中替代任何方法或属性，必须在 UIMap.cs 文件中执行此操作。

12. 在 UIMap.cs 文件中，添加一个构造函数，并指定 `UIStartButton` 属性的 `SearchProperties` 属性，以使用值为 `"buttonA":` 的 `AutomationID` 属性

    ```csharp
    public UIMap()
            {
                this.UIMainWindowWindow.UIStartButton.SearchProperties[WpfButton.PropertyNames.AutomationId] = "buttonA";
            }
    ```

13. 在 **“生成”** 菜单上，选择 **“生成解决方案”**。

14. 在“测试资源管理器”中，运行“CodedUITestMethod1”。

     此时，编码的 UI 测试已成功完成测试中的所有步骤。 在“测试结果”窗口中，你会看到状态“已通过”。

## <a name="videos"></a>视频

![视频链接](../data-tools/media/playvideo.gif)[编码的 UI 测试入门](https://onedrive.live.com/?id=2DB0E1EFE1C1D3B8%21110&cid=2DB0E1EFE1C1D3B8)

## <a name="faq"></a>FAQ

[编码的 UI 测试常见问题解答](https://social.msdn.microsoft.com/Forums/vsautotest/3a74dd2c-cef8-4923-abbf-7a91f489e6c4/faqs)

## <a name="see-also"></a>请参阅

- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
- [支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
- [使用编码的 UI 测试编辑器编辑编码的 UI 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)

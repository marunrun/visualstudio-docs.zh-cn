---
title: 演练：创建、编辑和维护编码的 UI 测试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: f7c25ba7-5c9c-455b-9242-701cda56f90c
caps.latest.revision: 43
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d14de396e24874f39a09172a483ebef81a5886f2
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851236"
---
# <a name="walkthrough-creating-editing-and-maintaining-a-coded-ui-test"></a>演练：创建、编辑和维护编码的 UI 测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，你将创建一个简单的 Windows Presentation Foundation (WPF) 应用程序来演示如何创建、编辑和维护编码的 UI 测试。 本演练为更正由各种计时问题和控件重构中断的测试提供了解决方案。

## <a name="prerequisites"></a>先决条件
 本演练需要：

- Visual Studio Enterprise

### <a name="create-a-simple-wpf-application"></a>创建一个简单的 WPF 应用程序

1. 在“文件”菜单上，指向“新建”，然后选择“项目”。

     此时将出现 **“新建项目”** 对话框。

2. 在“已安装”窗格中，展开 **Visual C#** ，然后选择“Windows 桌面”。

3. 在中间窗格之上，验证是否将目标框架下拉列表设置为“.NET Framework 4.5”。

4. 在中间窗格中，选择“WPF 应用程序”模板。

5. 在“名称”文本框中，键入 **SimpleWPFApp**。

6. 选择要用于保存项目的文件夹。 在“位置”文本框中，键入文件夹的名称。

7. 选择 **“确定”** 。

     用于 Visual Studio 的 WPF 设计器将打开，并显示项目的主窗口。

8. 如果当前未打开工具箱，请将其打开。 选择“视图”菜单，然后选择“工具箱”。

9. 在“所有 WPF 控件”部分，将一个“Button”、“CheckBox”和“ProgressBar”控件拖动到设计图面的主窗口中。

10. 选择 Button 控件。 在“属性”窗口中，将“名称”属性的值从 \<无名称> 更改为 button1。 然后将“内容”属性的值从 Button 更改为 Start。

11. 选择 ProgressBar 控件。 在“属性”窗口中，将“名称”属性的值从 \<无名称> 更改为 progressBar1。 然后将“最大值”属性的值从“100”更改为“10000”。

12. 选择 Checkbox 控件。 在“属性”窗口中，将“名称”属性的值从 \<无名称> 更改为 checkBox1，然后清除“IsEnabled”属性。

     ![简单的 WPF 应用程序](../test/media/codedui-wpfapp.png "CodedUI_WPFApp")

13. 双击按钮控件，以添加单击事件处理程序。

     将在代码编辑器中显示 MainWindow.xmal.cs，并且光标位于新的 button1_Click 方法中。

14. 在 MainWindow 类的顶部，添加一个委托。 该委托将用于进度栏。 若要添加委托，请添加以下代码：

    ```csharp
    public partial class MainWindow : Window
    {
            private delegate void ProgressBarDelegate(System.Windows.DependencyProperty dp, Object value);

        public MainWindow()
        {

            InitializeComponent();
        }

    ```

15. 在 button1_Click 方法中，添加以下代码：

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

16. 保存该文件。

### <a name="verify-the-wpf-application-runs-correctly"></a>验证 WPF 应用程序是否正常运行

1. 在“调试”菜单上，选择“启动调试”或按 **F5**。

2. 注意该复选框控件此时处于禁用状态。 选择“启动”。

     几秒后，进度栏应 100% 完成。

3. 现在，你可以选择该复选框控件。

4. 关闭 SimpleWPFApp。

### <a name="create-and-run-a-coded-ui-test-for-simplewpfapp"></a>为 SimpleWPFApp 创建和运行编码的 UI 测试

1. 查找你之前创建的 SimpleWPFApp 应用程序。 默认情况下，该应用程序将位于 C:\Users\\<username\>\Documents\Visual Studio \<version>\Projects\SimpleWPFApp\SimpleWPFApp\bin\Debug\SimpleWPFApp.exe

2. 创建 SimpleWPFApp 应用程序的桌面快捷方式。 右键单击 SimpleWPFApp.exe 并选择“复制”。 在桌面上右键单击，然后选择“粘贴快捷方式”。

    > [!TIP]
    > 使用应用程序的快捷方式可以快速启动应用程序，因此便于为应用程序添加或修改编码的 UI 测试。

3. 在解决方案资源管理器中，右键单击该解决方案，选择“添加”，然后选择“新建项目”。

     此时，将显示 **“添加新项目”** 对话框。

4. 在“已安装”窗格中，展开 **Visual C#** ，然后选择“测试”。

5. 在中间窗格中，选择“编码的 UI 测试项目”模板。

6. 选择 **“确定”** 。

     在解决方案资源管理器中，将名为 **CodedUITestProject1** 的新编码的 UI 测试项目添加到你的解决方案中。

     此时将显示“为编码的 UI 测试生成代码”对话框。

7. 选择“录制操作、编辑 UI 映射或添加断言”选项，然后选择“确定”。

     将显示“UIMap - 编码的 UI 测试生成器”，且 Visual Studio 窗口将最小化。

     有关对话框中的选项的详细信息，请参阅[创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)。

8. 在“UIMap - 编码的 UI 测试生成器”中选择“开始记录”。

     ![开始记录](../test/media/cuit-builder-record.png "CUIT_Builder_Record")

     如果需要，你可以暂停记录（例如，如果你必须处理传入的邮件）。

     ![暂停录制](../test/media/cuit.png "CUIT_")

    > [!WARNING]
    > 将录制在桌面上执行的所有操作。 如果你正在执行可能会导致敏感数据被包括在录制中的操作，则暂停录制。

9. 使用桌面快捷方式启动 SimpleWPFApp。

     像以前一样，注意该复选框控件此时处于禁用状态。

10. 在 SimpleWPFApp 上选择“启动”。

     几秒后，进度栏应 100% 完成。

11. 选中现在处于启用状态的复选框控件。

12. 关闭 SimpleWPFApp 应用程序。

13. 在“UIMap - 编码的 UI 测试生成器”中，选择“生成代码”。

14. 在“方法名称”中键入 **SimpleAppTest**，然后选择“添加并生成”。 几秒后，编码的 UI 测试将出现，并且会添加到“解决方案”中。

15. 关闭“UIMap – 编码的 UI 测试生成器”。

     CodedUITest1.cs 文件将出现在代码编辑器中。

16. 保存你的项目。

### <a name="run-the-coded-ui-test"></a>运行编码的 UI 测试

1. 从“测试”菜单中，选择“窗口”，然后选择“测试资源管理器”。

2. 从“生成”菜单中选择“生成解决方案”。

3. 在 CodedUITest1.cs 文件中，找到 **CodedUITestMethod** 方法、右键单击并选择“运行测试”，或从“测试资源管理器”中运行该测试。

     当编码的 UI 测试运行时，SimpleWPFApp 将可见。 它会执行你在前面的过程中执行的步骤。 但是，当测试尝试选中复选框控件对应的复选框时，“测试结果”窗口将显示测试未通过。 原因是测试尝试选中该复选框，但不知道复选框控件此时处于禁用状态，直至进度栏 100% 完成为止。 通过可用于编码的 UI 测试的各种 `UITestControl.WaitForControlXXX()` 方法可以更正此问题和类似问题。 下面的过程将演示如何使用 `WaitForControlEnabled()` 方法更正导致此测试未通过的问题。 有关详细信息，请参阅[播放期间让编码的 UI 测试等待特定事件](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md)。

### <a name="edit-and-rerun-the-coded-ui-test"></a>编辑并重新运行编码的 UI 测试

1. 在“测试资源管理器”窗口中，选择未通过的测试，然后在 **StackTrace** 部分中，选择指向 **UIMap.SimpleAppTest()** 的第一个链接。

2. 将打开 UIMap.Designer.cs 文件，并在代码中突出显示错误点：

    ```csharp

    // Select 'CheckBox' check box
    uICheckBoxCheckBox.Checked = this.SimpleAppTestParams.UICheckBoxCheckBoxChecked;
    ```

3. 若要更正此问题，可以使用 `WaitForControlEnabled()` 方法使编码的 UI 测试等待 CheckBox 控件被启用，然后再继续此行。

    > [!WARNING]
    > 请不要修改 UIMap.Designer.cs 文件。 每次使用 UIMap - 编码的 UI 测试生成器生成代码时，都会覆盖你在 UIMapDesigner.cs 文件中所做出的任何更改。 如果必须修改录制的方法，则必须将其复制到 UIMap.cs 文件并对其重命名。 UIMap.cs 文件可用于重写 UIMapDesigner.cs 文件中的方法和属性。 必须在 Coded UITest.cs 文件中删除对原始方法的引用，并将其替换为重命名的方法名称。

4. 在解决方案资源管理器中，找到编码的 UI 测试项目中的 **UIMap.uitest**。

5. 打开 **UIMap.uitest** 的快捷菜单并选择“打开”。

     编码的 UI 测试编辑器中将显示编码的 UI 测试。 此时你可以查看并编辑编码的 UI 测试。

6. 在“UI 操作”窗格中，选择要移动到 UIMap.cs 或 UIMap.vb 文件的测试方法 (SimpleAppTest)，以便使用在重新编译测试代码时不会重写的自定义代码功能。

7. 选择“编码的 UI 测试编辑器”工具栏上的“移动代码”按钮。

8. 将显示一个 Microsoft Visual Studio 对话框。 该对话框将警告你，该方法将从 UIMap.uitest 文件移动到 UIMap.cs 文件，并且你将不能再使用编码的 UI 测试编辑器来编辑该方法。 选择 **“是”** 。

     将从 UIMap.uitest 文件中移除该测试方法，并且“UI 操作”窗格中将不再显示该测试方法。 若要编辑移动的测试文件，请从解决方案资源管理器中打开 UIMap.cs 文件。

9. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 工具栏上，选择“保存”。

     对测试方法的更新保存在 UIMap.Designer 文件中。

    > [!CAUTION]
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

13. 在 CodedUITest1.cs 文件中，查找 **CodedUITestMethod** 方法并注释掉或重命名对原始 SimpleAppTest() 方法的引用，然后将其替换为新的 ModifiedSimpleAppTest()：

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

14. 在“生成”菜单上，选择“生成解决方案”。

15. 右键单击 **CodedUITestMethod** 方法，然后选择“运行测试”。

16. 此时，编码的 UI 测试已成功完成测试中的所有步骤，“测试资源管理器”窗口中将显示“已通过”。

### <a name="refactor-a-control-in-the-simplewpfapp"></a>在 SimpleWPFApp 中重构控件

1. 在 MainWindow.xaml 文件中，在设计器中选择按钮控件。

2. 在“属性”窗口的顶部，将“名称”属性值从 button1 更改为 buttonA。

3. 在“生成”菜单上，选择“生成解决方案”。

4. 在测试资源管理器中，运行 **CodedUITestMethod1**。

     由于编码的 UI 测试找不到最初在 UIMap 映射为 button1 的按钮控件，因此测试未通过。 重构会以此方式对编码的 UI 测试产生影响。

5. 在“测试资源管理器”窗口的 **StackTrace** 部分中，选择 **UIMpa.ModifiedSimpleAppTest()** 旁边的第一个链接。

     将打开 UIMap.cs 文件。 代码中将突出显示错误点：

    ```csharp

    // Click 'Start' button
    Mouse.Click(uIStartButton, new Point(27, 10));
    ```

     请注意，此过程前面的代码行使用了 `UiStartButton`，这是重构之前的 UIMap 名称。

     若要更正此问题，可使用编码的 UI 测试生成器向 UIMap 中添加重构的控件。 可以更新测试的代码以使用该代码，如下一过程所示。

### <a name="map-refactored-control-and-edit-and-rerun-the-coded-ui-test"></a>映射重构的控件并编辑和重新运行编码的 UI 测试

1. 在 CodedUITest1.cs 文件的 **CodedUITestMethod1()** 方法中，右键单击并选择“为编码的 UI 测试生成代码”，然后选择“使用编码的 UI 测试生成器”。

     将出现“UIMap – 编码的 UI 测试生成器”。

2. 使用你之前创建的桌面快捷方式，运行你在之前创建的 SimpleWPFApp 应用程序。

3. 在“UIMap – 编码的 UI 测试生成器”中，将十字线工具拖至 SimpleWPFApp 中的“Start”按钮。

     “Start”按钮包围在蓝色框中，编码的 UI 测试生成器需要几秒钟来为选定控件处理数据并显示控件属性。 请注意，**AutomationUId** 命名为 **buttonA**。

4. 在控件的属性中，选择左上角的箭头以展开 UI 控件图。 请注意，已选择 **UIStartButton1**。

5. 在工具栏中，选择“将控件添加到 UI 控件图”。

     窗口底部的状态通过显示“所选控件已添加到 UI 控件图中”来验证操作。

6. 在“UIMap - 编码的 UI 测试生成器”中，选择“生成代码”。

     将显示“编码的 UI 测试生成器 – 生成代码”，其中包含一个注释，指示不需要任何新方法，并且只为 UI 控件图的更改生成代码。

7. 选择“生成”。

8. 关闭 SimpleWPFApp.exe。

9. 关闭“UIMap – 编码的 UI 测试生成器”。

     “UIMap – 编码的 UI 测试生成器”需要几秒钟来处理 UI 控件图更改。

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

     现在，你可以修改编码的 UI 测试，以使用新映射的控件。 如前一过程所述，如果要在编码的 UI 测试中重写任何方法或属性，则必须在 UIMap.cs 文件中执行此操作。

12. 在 UIMap.cs 文件中，添加一个构造函数，并指定 `SearchProperties` 属性的 `UIStartButton` 属性，以使用值为 `AutomationID` 的 `"buttonA":` 属性

    ```csharp

    public UIMap()
            {
                this.UIMainWindowWindow.UIStartButton.SearchProperties[WpfButton.PropertyNames.AutomationId] = "buttonA";
            }

    ```

13. 在“生成”菜单上，选择“生成解决方案”。

14. 在“测试资源管理器”中，运行“CodedUITestMethod1”。

     此时，编码的 UI 测试已成功完成测试中的所有步骤。  在“测试结果”窗口中，你会看到状态“已通过”。

## <a name="external-resources"></a>外部資源

### <a name="videos"></a>视频
 ![链接到视频](../data-tools/media/playvideo.gif "PlayVideo")[编码的 UI 测试-DeepDive-第1集-GettingStarted](https://skydrive.live.com/?cid=2db0e1efe1c1d3b8&id=2DB0E1EFE1C1D3B8%21118)

 ![链接到视频](../data-tools/media/playvideo.gif "PlayVideo")[编码的 UI 测试-DeepDive-第2集-维护和调试](https://skydrive.live.com/?cid=2db0e1efe1c1d3b8&id=2DB0E1EFE1C1D3B8%21116)

 ![链接到视频](../data-tools/media/playvideo.gif "PlayVideo")[编码的 UI 测试-DeepDive-第-3](https://skydrive.live.com/?cid=2db0e1efe1c1d3b8&id=2DB0E1EFE1C1D3B8%21117)

### <a name="hands-on-lab"></a>动手实验
 [MSDN 虚拟实验室：使用 Visual Studio 2010 创建编码的 UI 测试的简介](https://windows.microsoft.com/en-US/windows/products/windows-media-player)

### <a name="faq"></a>常见问题
 [编码的 UI 测试常见问题 - 1](https://blogs.msdn.com/b/mathew_aniyan/archive/tags/faq/)

 [编码的 UI 测试常见问题 - 2](https://social.msdn.microsoft.com/Forums/en-US/vsautotest/thread/3a74dd2c-cef8-4923-abbf-7a91f489e6c4)

### <a name="forum"></a>论坛
 [Visual Studio UI 自动测试（包括 CodedUI）](https://social.msdn.microsoft.com/Forums/en-US/vsautotest)

## <a name="see-also"></a>请参阅
 [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)[入门使用 WPF 设计器](https://msdn.microsoft.com/18e61d03-b96a-4058-a166-8ec6b3f6116b)[支持编码的 Ui 测试的配置和平台，以及](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)[使用编码的 Ui 测试编辑器编辑编码的 ui 测试](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)的操作录制

---
title: 使用编码的 UI 测试来测试 UWP 应用
ms.date: 05/31/2018
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- uwp
ms.openlocfilehash: aad17d244d70051a363a4cde294c592968093ba0
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286747"
---
# <a name="create-a-coded-ui-test-to-test-a-uwp-app"></a>创建编码的 UI 测试来测试 UWP 应用

本文介绍如何为通用 Windows 平台 (UWP) 应用创建编码的 UI 测试。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="create-a-uwp-app-to-test"></a>创建用于测试的 UWP 应用

第一步是创建简单的 UWP 应用，用于运行测试。

1. 在 Visual Studio 中，使用针对 Visual C# 或 Visual Basic 的“空白应用(通用 Windows)”模板创建新项目  。

   ::: moniker range="vs-2017"

   ![空白应用通用 Windows 模板](../test/media/blank-uwp-app-template.png)

   ::: moniker-end

1. 在“新建通用 Windows 平台项目”对话框中，选择“确定”接受默认平台版本   。

1. 在“解决方案资源管理器”中，打开 MainPage.xaml   。

   文件随即在 XAML 设计器中打开  。

1. 从“工具箱”中，将按钮控件和文本框控件拖动到设计界面  。

     ![设计 UWP 应用](../test/media/toolbox-controls.png)

1. 为控件指定名称。 选择文本框控件，然后在“属性”窗口的“名称”字段中输入“文本框”    。 选择按钮控件，然后在“属性”窗口的“名称”字段输入“按钮”    。

1. 双击该按钮控件并向 `Button_Click` 方法的主体添加以下代码。 此代码只将文本框中的文本设置为按钮控件的名称，以便我们能够使用稍后创建的编码的 UI 测试进行验证。

   ```csharp
   this.textBox.Text = this.button.Name;
   ```

   ```vb
   Me.textBox.Text = Me.button.Name
   ```

1. 按 Ctrl+F5 运行应用。 显示的内容应与以下类似：

   ![带按钮和文本框的 UWP 应用](media/uwp-app.png)

## <a name="create-a-coded-ui-test"></a>创建编码的 UI 测试

1. 若要向解决方案添加测试项目，请右键单击“解决方案资源管理器”中的解决方案，然后选择“添加” > “新项目”。

1. 搜索并选择“编码的 UI 测试项目(通用 Windows)”模板  。

   ::: moniker range="vs-2017"

   ![新编码的 UI 测试项目](../test/media/coded-ui-test-project-uwp-template.png)

   ::: moniker-end

   > [!NOTE]
   > 如果未看到“编码的 UI 测试项目(通用 Windows)”模板，则需要[安装编码的 UI 测试组件](../test/use-ui-automation-to-test-your-code.md#install-the-coded-ui-test-component)。

1. 在“为编码的 UI 测试生成代码”对话框中，选择“手动编辑测试”   。

   ![“为编码的 UI 测试生成代码”对话框](../test/media/manually-edit-the-test.png)

1. 如果尚未运行 UWP 应用，请按 Ctrl+F5 启动应用。

1. 将在光标放在 `CodedUITestMethod1` 方法上，然后选择“测试” > “为编码的 UI 测试生成代码” > “使用编码的 UI 测试生成器”，从而 打开“编码的 UI 测试生成器”对话框。

1. 将控件添加到 UI 控件图。 使用“编码的 UI 测试生成器”十字准线工具选择 UWP 应用中的按钮控件  。 在“添加断言”对话框中，展开“UI 控件图”窗格（如有必要），然后选择“将控件添加到 UI 控件图”    。

     ![向 UI 映射添加控件](../test/media/add-control-to-ui-control-map.png)

1. 若要将文本框控件添加到 UI 控件图，请重复上一个步骤。

1. 在“编码的 UI 测试生成器”对话框中，选择“生成代码”或按 Ctrl+G。 然后选择“生成”，创建用于 UI 控件图更改的代码  。

     ![为 UI 映射生成代码](../test/media/generate-code-dialog.png)

1. 若要验证单击按钮时文本框中的文本是否更改为“按钮”，请单击按钮  。

     ![单击 button 控件设置 textbox 值](../test/media/uwp-app-button-textbox.png)

1. 添加断言，验证文本框控件中的文本。 使用十字准线工具选择文本框控件，然后在“添加断言”对话框中选择“文本”属性   。 然后，选择“添加断言”或按 Alt+A。 在“断言失败消息”框中，输入“文本框值异常”   。 然后选择“确定”  。

     ![选择带有十字准线的文本框，然后添加断言](../test/media/add-assertion-for-text.png)

1. 为断言生成测试代码。 在“编码的 UI 测试生成器”对话框中，选择“生成代码”   。 在“生成代码”对话框中，选择“添加并生成”   。

     ![为文本框断言生成代码](../test/media/add-and-generate-assert-method.png)

   在“解决方案资源管理器”中，打开 UIMap.Designer.cs，查看为断言方法和控件添加的代码   。

   > [!TIP]
   > 如果使用 Visual Basic，则打开 CodedUITest1.vb  。 然后，在 `CodedUITestMethod1()` 测试方法代码中，右键单击对断言方法 `Me.UIMap.AssertMethod1()` 的调用，然后选择“转到定义”  。 这将在代码编辑器中打开 UIMap.Designer.vb ，可查看为断言方法和控件添加的代码  。

    > [!WARNING]
    > 请不要直接修改 UIMap.designer.cs 或 UIMap.Designer.vb 文件   。 如果直接修改，生成测试时将覆盖所做更改。

    断言方法如下所示：

    ```csharp
    public void AssertMethod1()
    {
        #region Variable Declarations
        XamlEdit uITextBoxEdit = this.UIUWPAppWindow.UITextBoxEdit;
        #endregion

        // Verify that the 'Text' property of 'textBox' text box equals 'button'
        Assert.AreEqual(this.AssertMethod1ExpectedValues.UITextBoxEditText, uITextBoxEdit.Text, "Textbox value is unexpected.");
    }
    ```

    ```vb
    Public Sub AssertMethod1()
        Dim uITextBoxEdit As XamlEdit = Me.UIApp2Window.UITextBoxEdit

        'Verify that the 'Text' property of 'textBox' text box equals 'button'
        Assert.AreEqual(Me.AssertMethod1ExpectedValues.UITextBoxEditText, uITextBoxEdit.Text, "Textbox value is unexpected.")
    End Sub
    ```

1. 接下来，需要获取想要测试的 UWP [应用](#create-a-uwp-app-to-test)的 AutomationId。 打开 Windows“启动”菜单，查看应用的磁贴  。 然后，将十字准线工具![目标图标](media/target-icon.png) 从“编码的 UI 测试生成器”对话框拖动到应用的磁贴中  。 当磁贴周围出现蓝色框时，释放鼠标。

   ![十字准线工具](media/cross-hair-tool.png)

   此时，会打开“添加断言”对话框并显示应用的“AutomationId”   。 右键单击“AutomationId”，选择“将值复制到剪贴板”   。

   ![“添加断言”对话框中的 AutomationID](../test/media/automation-id.png)

1. 向测试方法添加代码以启动 UWP 应用。 在“解决方案资源管理器”中，打开 CodedUITest1.cs 或 CodedUITest1.vb    。 在 `AssertMethod1` 调用中添加代码，启动 UWP 应用：

   ```csharp
   XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App")
   ```

   ```vb
   XamlWindow myAppWindow = XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App");
   ```

   将示例代码中的自动化 ID 替换为上一步中复制到剪贴板的值。

   > [!IMPORTANT]
   > 整理自动化 ID 的开头，删除 P~ 等字符  。 如果不除去这些字符，当测试尝试启动应用时，将引发 `Microsoft.VisualStudio.TestTools.UITest.Extension.PlaybackFailureException`。

1. 接下来，将代码添加到测试方法，单击按钮。 在 `XamlWindow.Launch` 后面的行中，添加点击按钮控件的手势：

   ```csharp
   Gesture.Tap(this.UIMap.UIUWPAppWindow.UIButtonButton);
   ```

   ```vb
   Gesture.Tap(Me.UIMap.UIUWPAppWindow.UIButtonButton)
   ```

   添加代码后，完整的 `CodedUITestMethod1` 测试方法应如下所示：

   ```csharp
   [TestMethod]
   public void CodedUITestMethod1()
   {
       XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App");

       Gesture.Tap(this.UIMap.UIUWPAppWindow.UIButtonButton);

       // To generate code for this test, select "Generate Code for Coded UI Test" from the shortcut menu and select one of the menu items.
       this.UIMap.AssertMethod1();
   }
   ```

   ```vb
   <CodedUITest(CodedUITestType.WindowsStore)>
   Public Class CodedUITest1

       <TestMethod()>
       Public Sub CodedUITestMethod1()

           ' Launch the app.
           XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App")

           '// Tap the button.
           Gesture.Tap(Me.UIMap.UIUWPAppWindow.UIButtonButton)

           Me.UIMap.AssertMethod1()
       End Sub
   ```

1. 生成测试项目，然后通过选择“测试” > “Windows” > “测试资源管理器”来打开“测试资源管理器”。

1. 选择“全部运行”，运行测试  。

   打开应用，轻触按钮，并填充文本框的“文本”属性  。 断言方法将验证文本框的“文本”属性  。

   完成测试后，“测试资源管理器”将显示已通过该测试  。

   ![已通过的测试显示在测试资源管理器中](../test/media/test-explorer-coded-ui-test-passed.png)

## <a name="q--a"></a>问题解答

### <a name="q-why-dont-i-see-the-option-to-record-my-coded-ui-test-in-the-generate-code-for-a-coded-ui-test-dialog"></a>问：为什么在“生成编码的 UI 测试的代码”对话框中看不到用于记录编码的 UI 测试的选项？

**答**：UWP 应用不支持记录选项。

### <a name="q-can-i-create-a-coded-ui-test-for-my-uwp-apps-based-on-winjs"></a>问：我能否为基于 WinJS 的 UWP 应用创建编码的 UI 测试？

**答**：否，仅支持基于 XAML 的应用。

### <a name="q-why-cant-i-modify-the-code-in-the-uimapdesigner-file"></a>问：为什么无法修改 UIMap.Designer 文件中的代码？

**答**：每次使用“编码的 UI 测试生成器”生成代码时，都将覆盖在 UIMapDesigner.cs 文件中所做的任何代码更改   。 如果必须修改录制的方法，请将其复制到 UIMap.cs 文件并对其重命名  。 UIMap.cs 文件可用于重写 UIMapDesigner.cs 文件中的方法和属性   。 在 CodedUITest.cs 文件中删除对原始方法的引用，并将其替换为重命名的方法名称  。

## <a name="see-also"></a>请参阅

- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
- [为 UWP 控件设置唯一的自动化属性](../test/set-a-unique-automation-property-for-windows-store-controls-for-testing.md)

---
title: 创建 Windows 窗体工具箱控件 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d7e7749302252c5d56f21c58de9b6ac23f898572
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739579"
---
# <a name="create-a-windows-forms-toolbox-control"></a>创建 Windows 窗体工具箱控件

Visual Studio 扩展工具 （VS SDK） 中包含的 Windows 窗体工具箱控件项目模板允许您创建**工具箱**控件，该控件在安装扩展时会自动添加。 本演练演示如何使用模板创建可分发给其他用户的简单计数器控件。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-the-toolbox-control"></a>创建工具箱控件

Windows 窗体工具箱控件模板创建一个未定义的用户控件，并提供将控件添加到**工具箱**所需的所有功能。

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>使用 Windows 窗体工具箱控件创建扩展名

1. 创建名为 的`MyWinFormsControl`VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 打开项目时，添加名为 的`Counter`Windows**窗体工具箱控件**项模板。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在 **"添加新项目"** 对话框中，转到**可视化 C#** > **可扩展性**并选择**Windows 窗体工具箱控件**

3. 这将添加用户控件，一个`ProvideToolboxControlAttribute`<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>将控件放在**工具箱**中，以及**Microsoft.VisualStudio.Toolbox 控制**资产条目在 VSIX 清单中进行部署。

### <a name="build-a-user-interface-for-the-control"></a>为控件构建用户界面

该`Counter`控件需要两个子控件：<xref:System.Windows.Forms.Label>一个用于显示当前计数，和<xref:System.Windows.Forms.Button>将计数重置为 0。 不需要其他子控件，因为调用方将以编程方式增加计数器。

#### <a name="to-build-the-user-interface"></a>构建用户界面

1. 在**解决方案资源管理器**中，双击*Counter.cs*在设计器中打开它。

2. 删除 **"单击此处"！** 添加 Windows 窗体工具箱控件项模板时默认包含的按钮。

3. 从**工具箱**中，拖动控件`Label`，然后将其下方`Button`的控件拖动到设计图面。

4. 将用户整体控件的大小调整到 150、50 像素，并将按钮控件的大小调整到 50、20 像素。

5. 在 **"属性"** 窗口中，为设计图面上的控件设置以下值。

    |控制|properties|值|
    |-------------|--------------|-----------|
    |`Label1`|**Text**|""|
    |`Button1`|**名称**|btnReset|
    |`Button1`|**Text**|重置|

### <a name="code-the-user-control"></a>编写用户控件的代码

该`Counter`控件将公开一个方法以递增计数器、每当计数器增加时引发的事件、**一个"重置"** 按钮以及存储当前计数、显示文本以及是否显示或隐藏 **"重置"** 按钮的三个属性。 `ProvideToolboxControl` 特性确定 **控件会出现在“工具箱”**`Counter` 的什么位置。

#### <a name="to-code-the-user-control"></a>编写用户控件的代码

1. 双击窗体以在代码窗口中打开其加载事件处理程序。

2. 在事件处理程序方法的上方，在控件类中创建一个整数来存储计数器值和一个字符串来存储显示文本，如下例所示。

    ```csharp
    int currentValue;
    string displayText;
    ```

3. 创建以下公共财产声明。

    ```csharp
    public int Value {
        get { return currentValue; }
    }

    public string Message {
        get { return displayText; }
        set { displayText = value; }
    }

    public bool ShowReset {
        get { return btnReset.Visible; }
        set { btnReset.Visible = value; }
    }

    ```

    调用方可以访问这些属性以获取和设置计数器的显示文本，并显示或隐藏 **"重置"** 按钮。 调用方可以获取只`Value`读属性的当前值，但不能直接设置该值。

4. 将以下代码放在控件的`Load`事件中。

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    在<xref:System.Windows.Forms.UserControl.Load>事件中设置**Label**文本可使目标属性在应用其值之前加载。 在构造函数中设置 **"标签**"文本将导致**标签**为空。

5. 创建以下公共方法以增加计数器。

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. 向控件类添加`Incremented`事件的声明。

    ```csharp
    public event EventHandler Incremented;
    ```

    调用方可以向此事件添加处理程序以响应计数器值的更改。

7. 返回到设计视图并双击 **"重置**"按钮以生成`btnReset_Click`事件处理程序，然后填写它，如以下示例所示。

    ```csharp
    private void btnReset_Click(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = displayText + Value;
    }

    ```

8. 在类定义正上方的 `ProvideToolboxControl` 特性声明中，将第一个参数的值从 `"MyWinFormsControl.Counter"` 改为 `"General"`。 这会设置将在“工具箱” **** 中托管控件的项组名称。

    以下示例演示了 `ProvideToolboxControl` 特性和调整后的类定义。

    ```csharp
    [ProvideToolboxControl("General", false)]
    public partial class Counter : UserControl
    ```

### <a name="test-the-control"></a>测试控件

 要测试**工具箱**控件，请先在开发环境中测试它，然后在编译的应用程序中对其进行测试。

#### <a name="to-test-the-control"></a>测试控件

1. 按**F5** **以开始调试**。

    此命令生成项目并打开已安装控件的 Visual Studio 的第二个实验实例。

2. 在可视化工作室的实验实例中，创建**Windows 窗体应用程序**项目。

3. 在**解决方案资源管理器**中，双击*Form1.cs*在设计器中打开它（如果尚未打开）。

4. 在 **"工具箱**"中`Counter`，控件应显示在 **"常规"** 部分中。

5. 将`Counter`控件拖动到窗体中，然后选择它。 `Message``ShowReset`和`Value`属性将显示在 **"属性"** 窗口中，以及从 继承的属性<xref:System.Windows.Forms.UserControl>。

6. 将 `Message` 属性设置为 `Count:`。

7. 将<xref:System.Windows.Forms.Button>控件拖动到窗体，然后将按钮的名称和文本属性设置为`Test`。

8. 双击按钮以在代码视图中打开*Form1.cs*并创建单击处理程序。

9. 在单击处理程序中，调用`counter1.Increment()`。

10. 在构造函数中，在`InitializeComponent`调用 后键入`counter1``.``Incremented +=`，然后按**Tab**两次。

    Visual Studio 为`counter1.Incremented`事件生成表单级处理程序。

11. 突出显示事件`Throw`处理程序中的语句，键入`mbox`，然后按**Tab**两次从 mbox 代码段生成消息框。

12. 在下一行上，`if`/`else`添加以下块以设置 **"重置"** 按钮的可见性。

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. 按 **F5**。

    窗体将打开。 该`Counter`控件显示以下文本。

    **计数： 0**

14. 单击“测试”****。

    计数器增量和可视化工作室显示一个消息框。

15. 关闭消息框。

    **"重置**"按钮将消失。

16. 单击 **"测试**"，直到计数器每次达到**5**个关闭消息框。

    **"重置"** 按钮重新出现。

17. 单击“重置”。****

    计数器重置为**0**。

## <a name="next-steps"></a>后续步骤

生成**工具箱**控件时，Visual Studio 会在项目的 [bin_调试] 文件夹中创建名为*ProjectName.vsix*的文件。 通过将 *.vsix*文件上载到网络或网站，可以部署控件。 当用户打开 *.vsix*文件时，将安装该控件并将其添加到用户计算机上的 Visual Studio**工具箱**中。 或者，您可以将 *.vsix*文件上载到[可视化工作室应用商店](https://marketplace.visualstudio.com/)，以便用户可以通过在 **"工具** > **扩展和更新**"对话框中浏览来找到它。

## <a name="see-also"></a>请参阅

- [扩展视觉工作室的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)
- [创建 WPF 工具箱控件](../extensibility/creating-a-wpf-toolbox-control.md)
- [扩展视觉工作室的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)
- [Windows 窗体控件开发基础知识](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)

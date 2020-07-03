---
title: 创建 Windows 窗体工具箱控件 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
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
ms.openlocfilehash: d7c4d14f2970f9d77e78fd90dd58efcdac100e4c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903955"
---
# <a name="create-a-windows-forms-toolbox-control"></a>创建 Windows 窗体工具箱控件

Visual Studio 扩展性工具（VS SDK）中包含的 Windows 窗体工具箱控件项模板使你能够创建在安装扩展时自动添加的**工具箱**控件。 本演练演示如何使用模板创建可分发给其他用户的简单计数器控件。

## <a name="prerequisites"></a>必备条件

从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-the-toolbox-control"></a>创建工具箱控件

Windows 窗体工具箱控件模板可创建未定义的用户控件，并提供将该控件添加到 "**工具箱**" 所需的所有功能。

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>使用 Windows 窗体工具箱控件创建扩展

1. 创建一个名为的 VSIX 项目 `MyWinFormsControl` 。 通过搜索 "vsix"，可以在 "**新建项目**" 对话框中找到 vsix 项目模板。

2. 项目打开时，添加一个名为的**Windows 窗体工具箱控件**项模板 `Counter` 。 在**解决方案资源管理器**中，右键单击项目节点，然后选择 "**添加**  >  **新项**"。 在 "**添加新项**" 对话框中，选择 " **Visual c #**  >  **扩展性**" 并选择 **"Windows 窗体工具箱控件**

3. 这将添加一个用户控件，将控件放置在 "工具箱" 中，将 " `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> **VisualStudio. ToolboxControl** " 资产条目添加到部署的 VSIX 清单中。 **Toolbox**

### <a name="build-a-user-interface-for-the-control"></a>为控件生成用户界面

`Counter`控件需要两个子控件： <xref:System.Windows.Forms.Label> 用于显示当前计数的，以及 <xref:System.Windows.Forms.Button> 用于将计数重置为0的。 不需要其他子控件，因为调用方将以编程方式递增计数器。

#### <a name="to-build-the-user-interface"></a>构建用户界面

1. 在**解决方案资源管理器**中，双击*Counter.cs*以在设计器中将其打开。

2. 删除**单击此处！** 添加 Windows 窗体工具箱控件项模板时默认包含的按钮。

3. 将控件从 "**工具箱**" 拖动 `Label` `Button` 到设计图面上。

4. 将总体用户控件的大小调整为150、50像素，并将按钮控件的大小调整为 50 20 像素。

5. 在 "**属性**" 窗口中，为设计图面上的控件设置以下值。

    |控制|properties|值|
    |-------------|--------------|-----------|
    |`Label1`|**文本**|""|
    |`Button1`|**Name**|btnReset|
    |`Button1`|**文本**|重置|

### <a name="code-the-user-control"></a>编码用户控件

`Counter`控件将公开一个用于递增计数器的方法、一个要在计数器增加时引发的事件、一个 "**重置**" 按钮，以及三个用于存储当前计数、显示文本以及是否显示或隐藏 "**重置**" 按钮的属性。 `ProvideToolboxControl` 特性确定 **控件会出现在“工具箱”**`Counter` 的什么位置。

#### <a name="to-code-the-user-control"></a>编码用户控件

1. 双击窗体以在代码窗口中打开其 load 事件处理程序。

2. 在事件处理程序方法之上，在控件类中创建一个整数来存储计数器值，并创建一个用于存储显示文本的字符串，如下面的示例中所示。

    ```csharp
    int currentValue;
    string displayText;
    ```

3. 创建以下公共属性声明。

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

    调用方可以访问这些属性来获取和设置计数器的显示文本，以及显示或隐藏 "**重置**" 按钮。 调用方可以获得只读属性的当前值 `Value` ，但不能直接设置该值。

4. 在控件的事件中添加以下代码 `Load` 。

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    在事件中设置**标签**文本 <xref:System.Windows.Forms.UserControl.Load> 后，可以在应用其值之前加载目标属性。 在构造函数中设置**标签**文本将导致空**标签**。

5. 创建以下公共方法以递增计数器。

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. 将事件的声明添加 `Incremented` 到 control 类。

    ```csharp
    public event EventHandler Incremented;
    ```

    调用方可以向此事件添加处理程序，以响应计数器值的更改。

7. 返回到 "设计" 视图，然后双击 "**重置**" 按钮以生成 `btnReset_Click` 事件处理程序，然后填写该事件处理程序，如下面的示例中所示。

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

 若要测试 **"工具箱**" 控件，请先在开发环境中对其进行测试，然后在已编译的应用程序中对其进行测试。

#### <a name="to-test-the-control"></a>测试控件

1. 按**F5** **启动调试**。

    此命令生成项目，并打开已安装控件的第二个 Visual Studio 实验实例。

2. 在 Visual Studio 的实验实例中，创建一个**Windows 窗体应用程序**项目。

3. 在**解决方案资源管理器**中，双击 " *Form1.cs* " 以在设计器中将其打开（如果尚未打开）。

4. 在 "**工具箱**" 中， `Counter` 控件应显示在 "**常规**" 部分中。

5. 将一个 `Counter` 控件拖到窗体上，然后选择它。 `Value`、 `Message` 和 `ShowReset` 属性将显示在 "**属性**" 窗口中，以及从继承的属性 <xref:System.Windows.Forms.UserControl> 。

6. 将 `Message` 属性设置为 `Count:`。

7. 将一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上，然后将该按钮的 "名称" 和 "文本" 属性设置为 `Test` 。

8. 双击按钮以在代码视图中打开*Form1.cs* ，并创建一个 click 处理程序。

9. 在单击处理程序中调用 `counter1.Increment()` 。

10. 在构造函数中，在调用后， `InitializeComponent` 键入， `counter1``.``Incremented +=` 然后按**tab**两次。

    Visual Studio 将为事件生成窗体级处理程序 `counter1.Incremented` 。

11. 突出显示 `Throw` 事件处理程序中的语句，键入 `mbox` ，然后按**tab**两次，以从 mbox 代码段生成消息框。

12. 在下一行中，添加以下 `if` / `else` 块以设置 "**重置**" 按钮的可见性。

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. 按 **F5**。

    此时将打开窗体。 `Counter`控件将显示以下文本。

    **计数：0**

14. 单击“测试”。

    计数器会递增，Visual Studio 将显示一个消息框。

15. 关闭消息框。

    "**重置**" 按钮将会消失。

16. 单击 "**测试**"，直到计数器每次都达到**5**个关闭消息框。

    **重新设置**按钮将再次出现。

17. 单击“重置”。

    计数器将重置为**0**。

## <a name="next-steps"></a>后续步骤

生成 **"工具箱**" 控件时，Visual Studio 将在项目的 \bin\debug\ 文件夹中创建一个名为*项目名称 .vsix*的文件。 可以通过将 *.vsix*文件上载到网络或网站来部署此控件。 当用户打开 *.vsix*文件时，控件将安装并添加到用户计算机上的 Visual Studio**工具箱**中。 或者，你可以将 *.vsix*文件上载到[Visual Studio Marketplace](https://marketplace.visualstudio.com/) ，以便用户可以通过在 "**工具**" "  >  **扩展和更新**" 对话框中浏览来查找它。

## <a name="see-also"></a>另请参阅

- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)
- [创建 WPF 工具箱控件](../extensibility/creating-a-wpf-toolbox-control.md)
- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)
- [Windows 窗体控件开发基础知识](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)

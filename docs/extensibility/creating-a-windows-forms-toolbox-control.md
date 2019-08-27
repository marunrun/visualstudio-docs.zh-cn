---
title: 创建 Windows 窗体工具箱控件 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3887a2d54f2744504f587b848bc1395090c3904c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345413"
---
# <a name="create-a-windows-forms-toolbox-control"></a>创建 Windows 窗体工具箱控件

Visual Studio 扩展性工具 (VS SDK) 中包含的 Windows 窗体工具箱控件项目模板允许你创建**工具箱**时安装该扩展会自动添加的控件。 本演练演示如何使用模板来创建可以分发给其他用户的简单计数器控件。

## <a name="prerequisites"></a>系统必备

从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-the-toolbox-control"></a>创建工具箱控件

Windows 窗体工具箱控件模板创建未定义的用户控件，并提供了将控件添加到所需的功能的所有**工具箱**。

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>使用 Windows 窗体工具箱控件创建的扩展

1. 创建一个名为的 VSIX 项目`MyWinFormsControl`。 您可以发现中的 VSIX 项目模板**新的项目**对话框中的，通过搜索"vsix"。

2. 项目打开后，添加**Windows 窗体工具箱控件**项模板名为`Counter`。 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 在中**添加新项**对话框中，转到**Visual C#**  > **扩展性**，然后选择**Windows 窗体工具箱控件**

3. 这将添加一个用户控件， `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>放置在控件**工具箱**，和一个**Microsoft.VisualStudio.ToolboxControl**资产部署的 VSIX 清单中的项。

### <a name="build-a-user-interface-for-the-control"></a>构建用户界面控件

`Counter`控件需要两个子控件：<xref:System.Windows.Forms.Label>若要显示的当前计数，和一个<xref:System.Windows.Forms.Button>将计数重置为 0。 需要没有其他子控件，因为调用方将以编程方式递增计数器。

#### <a name="to-build-the-user-interface"></a>构建用户界面

1. 在中**解决方案资源管理器**，双击*Counter.cs*以在设计器中打开它。

2. 删除**单击此处 ！** 添加 Windows 窗体工具箱控件项目模板时，默认情况下包含的按钮。

3. 从**工具箱**，拖动`Label`控件，然后`Button`它下面至设计图面上的控件。

4. 重设大小为 150 整个用户控件、 为 50，50 像素，并且调整按钮大小控制 20 像素。

5. 在中**属性**窗口中，设置以下值： 在设计图面上的控件。

    |控件|属性|“值”|
    |-------------|--------------|-----------|
    |`Label1`|**文本**|""|
    |`Button1`|**名称**|btnReset|
    |`Button1`|**文本**|重置|

### <a name="code-the-user-control"></a>代码的用户控件

`Counter`控件将公开一个方法，用于递增计数器，每当增加计数器的数值，将引发一个事件**重置**按钮和用于存储当前计数、 显示文本，以及是否要显示的三个属性或隐藏**重置**按钮。 `ProvideToolboxControl` 特性确定 **控件会出现在“工具箱”** `Counter` 的什么位置。

#### <a name="to-code-the-user-control"></a>编写用户控件的代码

1. 双击要在代码窗口中打开其 load 事件处理程序的窗体。

2. 上面的事件处理程序方法，控件类中创建一个整数来存储计数器值和要存储在下面的示例所示显示文本的字符串。

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

    调用方可以访问这些属性，来获取和设置的计数器的显示文本以显示或隐藏**重置**按钮。 调用方可以获取的当前值的只读的`Value`属性，但它们无法直接设置的值。

4. 将以下代码放入`Load`控件事件。

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    设置**标签**中的文本<xref:System.Windows.Forms.UserControl.Load>事件，要加载之前应用其值的目标属性。 设置**标签**构造函数中的文本将导致在一个空**标签**。

5. 创建以下公共方法，以递增计数器。

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. 添加的声明`Incremented`到控件类的事件。

    ```csharp
    public event EventHandler Incremented;
    ```

    调用方可以将处理程序添加到此事件来响应中的计数器值的更改。

7. 返回设计视图中，双击**重置**按钮以生成`btnReset_Click`事件处理程序，并在下面的示例中所示填充。

    ```csharp
    private void btnReset_Click(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = displayText + Value;
    }

    ```

8. 在类定义正上方的 `ProvideToolboxControl` 特性声明中，将第一个参数的值从 `"MyWinFormsControl.Counter"` 改为 `"General"`。 这会设置将在“工具箱”  中托管控件的项组名称。

    以下示例演示了 `ProvideToolboxControl` 特性和调整后的类定义。

    ```csharp
    [ProvideToolboxControl("General", false)]
    public partial class Counter : UserControl
    ```

### <a name="test-the-control"></a>测试控件

 若要测试**工具箱**控制、 首次在开发环境中进行测试，然后编译的应用程序进行测试。

#### <a name="to-test-the-control"></a>测试控件

1. 按**F5**到**开始调试**。

    此命令生成项目并打开 Visual Studio 的安装有控件的第二个实验实例。

2. 在 Visual Studio 的实验实例中，创建**Windows 窗体应用程序**项目。

3. 在中**解决方案资源管理器**，双击*Form1.cs*如果尚未打开在设计器中打开。

4. 在中**工具箱**，则`Counter`控件应显示在**常规**部分。

5. 拖动`Counter`控制向窗体，并将其选中。 `Value`， `Message`，并`ShowReset`属性将显示在**属性**窗口中，则继承的属性以及<xref:System.Windows.Forms.UserControl>。

6. 将 `Message` 属性设置为 `Count:`。

7. 拖动<xref:System.Windows.Forms.Button>控制窗体，，然后设置该按钮的名称和文本属性`Test`。

8. 双击按钮以打开*Form1.cs*在代码视图并创建一个 click 处理程序。

9. 单击处理程序，在调用`counter1.Increment()`。

10. 在构造函数中，在调用`InitializeComponent`，类型`counter1``.``Incremented +=`，然后按**选项卡**两次。

    Visual Studio 将生成的窗体级别处理程序`counter1.Incremented`事件。

11. 突出显示`Throw`事件处理程序类型中的语句`mbox`，然后按**选项卡**两次以与 mbox 代码段中生成一个消息框。

12. 在下一步的行中，添加以下`if` / `else`块，以设置的可见性**重置**按钮。

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. 按 F5  。

    此时将打开窗体。 `Counter`控件将显示以下文本。

    **计数：0**

14. 单击“测试”  。

    计数器递增和 Visual Studio 将显示一个消息框。

15. 关闭消息框。

    **重置**按钮就会消失。

16. 单击**测试**直到计数器达到**5**关闭消息框每次。

    **重置**按钮随即再次显示。

17. 单击“重置”  。

    该计数器将重置为**0**。

## <a name="next-steps"></a>后续步骤

在生成**工具箱**控件，Visual Studio 将创建名为的文件*ProjectName.vsix*你的项目的 \bin\debug\ 文件夹中。 可以将该控件部署通过上传 *.vsix*文件到网络或网站。 当用户在打开 *.vsix*安装文件，该控件并将其添加到 Visual Studio**工具箱**用户的计算机上。 或者，可以上传 *.vsix*的文件[Visual Studio Marketplace](https://marketplace.visualstudio.com/) ，以便用户可以通过在浏览找到它**工具** >  **扩展和更新**对话框。

## <a name="see-also"></a>请参阅

- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)
- [创建 WPF 工具箱控件](../extensibility/creating-a-wpf-toolbox-control.md)
- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)
- [Windows 窗体控件开发基础知识](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)

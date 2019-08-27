---
title: WPF 介绍 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: b8d7cf43-d1f2-4f3d-adb0-4f3a6428edc0
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7b4061a5bc253782e7ca28478259efb4027c61f9
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65674743"
---
# <a name="introduction-to-wpf"></a>WPF 介绍
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 Windows Presentation Foundation (WPF)，你可以创建适用于 Windows 且具有非凡视觉效果的桌面客户端应用程序。  
  
 ![Contoso Healthcare UI 示例](../designers/media/wpfintrofigure24.png "WPFIntroFigure24")  
  
 WPF 的核心是一个与分辨率无关且基于矢量的呈现引擎，旨在充分利用现代图形硬件。 WPF 通过一套完善的应用程序开发功能对该核心进行了扩展，这些功能包括可扩展应用程序标记语言 (XAML)、控件、数据绑定、布局、二维和三维图形、动画、样式、模板、文档、媒体、文本和版式。 WPF 包含在 .NET Framework 中，因此你可以生成整合其他 .NET Framework 类库元素的应用程序。  
  
 本概述适用于新用户，介绍了 WPF 的主要功能和概念。  
  
## <a name="Programming_with_WPF"></a> 使用 WPF 进行编程  
 WPF 作为大部分位于 <xref:System.Windows> 命名空间中的 .NET Framework 类型的一个子集存在。 如果你之前使用托管技术（如 ASP.NET 和 Windows 窗体）通过 .NET Framework 生成过应用程序，则不会对基本的 WPF 编程体验感到陌生；你可以使用最喜欢的 .NET 编程语言（如 C# 或 Visual Basic）来完成实例化类、设置属性、调用方法以及处理事件等所有操作。  
  
 WPF 还包括增强属性和事件的其他编程构造： [依赖项属性](https://msdn.microsoft.com/library/ms752914\(v=vs.100\).aspx) 和 [路由事件](https://msdn.microsoft.com/library/ms742806\(v=vs.100\).aspx)。  
  
## <a name="Markup_And_Codebehind"></a> 标记和代码隐藏  
 通过 WPF，你可以使用 *标记* 和 *代码隐藏*开发应用程序，这是 ASP.NET 开发人员已经熟悉的体验。 通常使用 XAML 标记实现应用程序的外观，同时使用托管编程语言（代码隐藏）来实现其行为。 这种外观和行为的分离具有以下优点：  
  
- 降低了开发和维护成本，因为特定于外观的标记与特定于行为的代码不紧密耦合。  
  
- 开发效率更高，因为设计人员在实现应用程序外观的同时，开发人员可以实现应用程序的行为。  
  
- WPF 应用程序的[全球化和本地化](https://msdn.microsoft.com/library/ms788718\(v=vs.100\).aspx) 得以简化。  
  
  以下是 WPF 标记和代码隐藏的简介。  
  
### <a name="markup"></a>标记  
 XAML 是一种基于 XML 的标记语言，用于以声明形式实现应用程序的外观。 它通常用于创建窗口、对话框、页和用户控件，并填充控件、形状和图形。  
  
 下面的示例使用 XAML 来实现包含一个按钮的窗口的外观。  
  
```xaml  
<Window  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    Title="Window with Button"  
    Width="250" Height="100">  
  
  <!-- Add button to window -->  
  <Button Name="button">Click Me!</Button>  
  
</Window>  
```  
  
 具体而言，此 XAML 通过分别使用 `Window` 和 `Button` 元素来定义窗口和按钮。 每个元素均配置了特性（如 `Window` 元素的 `Title` 特性）来指定窗口的标题栏文本。 在运行时，WPF 会将标记中定义的元素和特性转换为 WPF 类的实例。 例如， `Window` 元素被转换为 <xref:System.Windows.Window> 类的实例，该类的 <xref:System.Windows.Window.Title%2A> 属性是 `Title` 特性的值。  
  
 下图显示上一个示例中的 XAML 定义的用户界面 (UI)。  
  
 ![包含按钮的窗口](../designers/media/wpfintrofigure10.png "WPFIntroFigure10")  
  
 由于 XAML 是基于 XML 的，因此使用它编写的 UI 汇集在嵌套元素的层次结构中，称为 [元素树](https://msdn.microsoft.com/library/ms753391\(v=vs.100\).aspx)。 元素树提供了一种直观的逻辑方式来创建和管理 UI。  
  
### <a name="code-behind"></a>代码隐藏  
 应用程序的主要行为是实现响应用户交互的功能，包括处理事件（例如，单击菜单、工具栏或按钮）以及相应地调用业务逻辑和数据访问逻辑。 在 WPF 中，通常在与标记相关联的代码中实现此行为。 此类代码称为代码隐藏。 下面的示例演示上一个示例的更新标记和代码隐藏。  
  
```xaml  
<Window  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    x:Class="SDKSample.AWindow"  
    Title="Window with Button"  
    Width="250" Height="100">  
  
  <!-- Add button to window -->  
  <Button Name="button" Click="button_Click">Click Me!</Button>  
  
</Window>  
```  
  
```csharp  
using System.Windows; // Window, RoutedEventArgs, MessageBox   
  
namespace SDKSample  
{  
    public partial class AWindow : Window  
    {  
        public AWindow()  
        {  
            // InitializeComponent call is required to merge the UI   
            // that is defined in markup with this class, including    
            // setting properties and registering event handlers  
            InitializeComponent();  
        }  
  
        void button_Click(object sender, RoutedEventArgs e)  
        {  
            // Show message box when button is clicked  
            MessageBox.Show("Hello, Windows Presentation Foundation!");  
        }  
    }  
}  
```  
  
```vb  
Namespace SDKSample  
  
    Partial Public Class AWindow  
        Inherits System.Windows.Window  
  
        Public Sub New()  
  
            ' InitializeComponent call is required to merge the UI   
            ' that is defined in markup with this class, including    
            ' setting properties and registering event handlers  
            InitializeComponent()  
  
        End Sub   
  
        Private Sub button_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)  
  
            ' Show message box when button is clicked  
            MessageBox.Show("Hello, Windows Presentation Foundation!")  
  
        End Sub   
  
    End Class   
  
End Namespace  
  
```  
  
 在此示例中，代码隐藏实现派生自 <xref:System.Windows.Window> 类的类。 `x:Class` 特性用于将标记与代码隐藏类相关联。 从代码隐藏类的构造函数调用 `InitializeComponent`，以将标记中定义的 UI 与代码隐藏类合并在一起。 （生成应用程序时将为你生成 `InitializeComponent`，因此你无需手动实现它。）`x:Class` 和 `InitializeComponent` 的组合可确保你的实现无论在何时创建都会得到正确初始化。 代码隐藏类还可实现按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的事件处理程序。 单击该按钮后，事件处理程序会通过调用 <xref:System.Windows.MessageBox.Show%2A?displayProperty=fullName> 方法显示一个消息框。  
  
 下图显示单击该按钮后的结果。  
  
 ![消息框](../designers/media/wpfintrofigure25.png "WPFIntroFigure25")  
  
## <a name="Controls"></a> 控件  
 应用程序模型带来的用户体验是构造的控件。 在 WPF 中，“控件”是适用于 WPF 类这一类别的总括术语，这些类托管在窗口或页中、具有用户界面并实现一些行为。  
  
 有关详细信息，请参阅 [控件](https://msdn.microsoft.com/library/3f255a8a-35a8-4712-9065-472ff7d75599)。  
  
### <a name="wpf-controls-by-function"></a>按功能分类的 WPF 控件  
 下面列出了内置的 WPF 控件。  
  
- **按钮**： <xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Controls.Primitives.RepeatButton>。  
  
- **数据显示**： <xref:System.Windows.Controls.DataGrid>、 <xref:System.Windows.Controls.ListView>和 <xref:System.Windows.Controls.TreeView>。  
  
- **日期显示和选项**： <xref:System.Windows.Controls.Calendar> 和 <xref:System.Windows.Controls.DatePicker>。  
  
- **对话框**： <xref:Microsoft.Win32.OpenFileDialog>、 <xref:System.Windows.Controls.PrintDialog>和 <xref:Microsoft.Win32.SaveFileDialog>。  
  
- **数字墨迹**： <xref:System.Windows.Controls.InkCanvas> 和 <xref:System.Windows.Controls.InkPresenter>。  
  
- **文档**： <xref:System.Windows.Controls.DocumentViewer>、 <xref:System.Windows.Controls.FlowDocumentPageViewer>、 <xref:System.Windows.Controls.FlowDocumentReader>、 <xref:System.Windows.Controls.FlowDocumentScrollViewer>和 <xref:System.Windows.Controls.StickyNoteControl>。  
  
- **输入**： <xref:System.Windows.Controls.TextBox>、 <xref:System.Windows.Controls.RichTextBox>和 <xref:System.Windows.Controls.PasswordBox>。  
  
- **布局**： <xref:System.Windows.Controls.Border>、 <xref:System.Windows.Controls.Primitives.BulletDecorator>、 <xref:System.Windows.Controls.Canvas>、 <xref:System.Windows.Controls.DockPanel>、 <xref:System.Windows.Controls.Expander>、 <xref:System.Windows.Controls.Grid>、 <xref:System.Windows.Controls.GridView>、 <xref:System.Windows.Controls.GridSplitter>、 <xref:System.Windows.Controls.GroupBox>、 <xref:System.Windows.Controls.Panel>、 <xref:System.Windows.Controls.Primitives.ResizeGrip>、 <xref:System.Windows.Controls.Separator>、 <xref:System.Windows.Controls.Primitives.ScrollBar>、 <xref:System.Windows.Controls.ScrollViewer>、 <xref:System.Windows.Controls.StackPanel>、 <xref:System.Windows.Controls.Primitives.Thumb>、 <xref:System.Windows.Controls.Viewbox>、 <xref:System.Windows.Controls.VirtualizingStackPanel>、 <xref:System.Windows.Window>和 <xref:System.Windows.Controls.WrapPanel>。  
  
- **媒体**： <xref:System.Windows.Controls.Image>、 <xref:System.Windows.Controls.MediaElement>和 <xref:System.Windows.Controls.SoundPlayerAction>。  
  
- **菜单**： <xref:System.Windows.Controls.ContextMenu>、 <xref:System.Windows.Controls.Menu>和 <xref:System.Windows.Controls.ToolBar>。  
  
- **导航**： <xref:System.Windows.Controls.Frame>、 <xref:System.Windows.Documents.Hyperlink>、 <xref:System.Windows.Controls.Page>、 <xref:System.Windows.Navigation.NavigationWindow>和 <xref:System.Windows.Controls.TabControl>。  
  
- **选项**： <xref:System.Windows.Controls.CheckBox>、 <xref:System.Windows.Controls.ComboBox>、 <xref:System.Windows.Controls.ListBox>、 <xref:System.Windows.Controls.RadioButton>和 <xref:System.Windows.Controls.Slider>。  
  
- **用户信息**： <xref:System.Windows.Controls.AccessText>、 <xref:System.Windows.Controls.Label>、 <xref:System.Windows.Controls.Primitives.Popup>、 <xref:System.Windows.Controls.ProgressBar>、 <xref:System.Windows.Controls.Primitives.StatusBar>、 <xref:System.Windows.Controls.TextBlock>和 <xref:System.Windows.Controls.ToolTip>。  
  
## <a name="Input_And_Commanding"></a> 输入和命令  
 最常检测和响应用户输入的控件。 [WPF 输入系统](https://msdn.microsoft.com/library/ms754010\(v=vs.100\).aspx) 使用直接事件和路由事件来支持文本输入、焦点管理和鼠标定位。  
  
 应用程序通常具有复杂的输入要求。 WPF 提供了 [命令系统](https://msdn.microsoft.com/library/ms752308\(v=vs.100\).aspx) ，用于将用户输入操作与对这些操作做出响应的代码分隔开来。  
  
## <a name="Layout"></a> 布局  
 创建用户界面时，按照位置和大小排列控件以形成布局。 任何布局的一项关键要求都是适应窗口大小和显示设置的变化。 WPF 为你提供一流的可扩展布局系统，而不强制你编写代码以适应这些情况下的布局。  
  
 布局系统的基础是相对定位，这提高了适应不断变化的窗口和显示条件的能力。 此外，该布局系统还可管理控件之间的协商以确定布局。 协商是一个两步过程：首先，控件将需要的位置和大小告知父级；其次，父级将控件可以有的空间告知控件。  
  
 该布局系统通过基 WPF 类公开给子控件。 对于通用的布局（如网格、堆叠和停靠），WPF 包括若干布局控件：  
  
- <xref:System.Windows.Controls.Canvas>：子控件提供其自己的布局。  
  
- <xref:System.Windows.Controls.DockPanel>：子控件与面板的边缘对齐。  
  
- <xref:System.Windows.Controls.Grid>：子控件按行和列放置。  
  
- <xref:System.Windows.Controls.StackPanel>：子控件垂直或水平堆叠。  
  
- <xref:System.Windows.Controls.VirtualizingStackPanel>：子控件在水平或垂直的行上进行虚拟化和排列。  
  
- <xref:System.Windows.Controls.WrapPanel>：子控件按从左到右的顺序放置，在当前行上的控件超出允许的空间时，换行到下一行。  
  
  下面的示例使用 <xref:System.Windows.Controls.DockPanel> 布置几个 <xref:System.Windows.Controls.TextBox> 控件。  
  
  [!code-xml[IntroToWPFSnippets#LayoutMARKUP](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/LayoutWindow.xaml#layoutmarkup)]  
  
  <xref:System.Windows.Controls.DockPanel> 允许子 <xref:System.Windows.Controls.TextBox> 控件，以告诉它如何排列这些控件。 为了完成此操作， <xref:System.Windows.Controls.DockPanel> 实现 <xref:System.Windows.Controls.DockPanel.Dock%2A> 属性，该属性公开给子控件，以允许每个子控件指定停靠样式。  
  
> [!NOTE]
> 由父控件实现以便子控件使用的属性是 WPF 构造，称为 [附加属性](https://msdn.microsoft.com/library/ms749011\(v=vs.100\).aspx)。  
  
 下图显示上一个示例中的 XAML 标记的结果。  
  
 ![DockPanel 页](../designers/media/wpfintrofigure11.png "WPFIntroFigure11")  
  
## <a name="Data_Binding"></a> 数据绑定  
 大多数应用程序旨在为用户提供查看和编辑数据的方法。 对于 WPF 应用程序，已对存储和访问数据的工作提供技术（如 SQL Server 和 ADO.NET）。 访问数据并将数据加载到应用程序的托管对象后，WPF 应用程序的复杂工作开始。 从根本上来说，这涉及到两件事：  
  
1. 将数据从托管对象复制到控件，在控件中可以显示和编辑数据。  
  
2. 确保使用控件对数据所做的更改将复制回托管对象。  
  
   为了简化应用程序开发，WPF 提供了一个数据绑定引擎来自动执行这些步骤。 数据绑定引擎的核心单元是 <xref:System.Windows.Data.Binding> 类，其工作是将控件（绑定目标）绑定到数据对象（绑定源）。 下图阐释了这种关系。  
  
   ![基本数据绑定示意图](../designers/media/databindingmostbasic.png "DataBindingMostBasic")  
  
   下面的示例演示如何将 <xref:System.Windows.Controls.TextBox> 绑定到自定义 `Person` 对象的实例。 下面的代码演示了 `Person` 实现。  
  
   [!code-csharp[SimpleDataBindingSnippets#PersonClassCODE](../snippets/csharp/VS_Snippets_Wpf/SimpleDataBindingSnippets/CSharp/Person.cs#personclasscode)]
   [!code-vb[SimpleDataBindingSnippets#PersonClassCODE](../snippets/visualbasic/VS_Snippets_Wpf/SimpleDataBindingSnippets/VisualBasic/Person.vb#personclasscode)]  
  
   下面的标记将 <xref:System.Windows.Controls.TextBox> 绑定到自定义 `Person` 对象的实例。  
  
   [!code-xml[SimpleDataBindingSnippets#DataBindingMARKUP1](../snippets/csharp/VS_Snippets_Wpf/SimpleDataBindingSnippets/CSharp/DataBindingWindow.xaml#databindingmarkup1)]  
   [!code-xml[SimpleDataBindingSnippets#DataBindingMARKUP2](../snippets/csharp/VS_Snippets_Wpf/SimpleDataBindingSnippets/CSharp/DataBindingWindow.xaml#databindingmarkup2)]  
   [!code-xml[SimpleDataBindingSnippets#DataBindingMARKUP3](../snippets/csharp/VS_Snippets_Wpf/SimpleDataBindingSnippets/CSharp/DataBindingWindow.xaml#databindingmarkup3)]  
  
   [!code-csharp[SimpleDataBindingSnippets#DataBindingCODEBEHIND](../snippets/csharp/VS_Snippets_Wpf/SimpleDataBindingSnippets/CSharp/DataBindingWindow.xaml.cs#databindingcodebehind)]
   [!code-vb[SimpleDataBindingSnippets#DataBindingCODEBEHIND](../snippets/visualbasic/VS_Snippets_Wpf/SimpleDataBindingSnippets/VisualBasic/DataBindingWindow.xaml.vb#databindingcodebehind)]  
  
   在此示例中， `Person` 类在代码隐藏中实例化并被设置为 `DataBindingWindow`的数据上下文。 在标记中， <xref:System.Windows.Controls.TextBox.Text%2A> 的 <xref:System.Windows.Controls.TextBox> 属性被绑定至 `Person.Name` 属性（使用“`{Binding ... }`”XAML 语法）。 此 XAML 告知 WPF 将 <xref:System.Windows.Controls.TextBox> 控件绑定至窗口的 `Person` 属性中存储的 <xref:System.Windows.FrameworkElement.DataContext%2A> 对象。  
  
   WPF 数据绑定引擎提供了额外支持，包括验证、排序、筛选和分组。 此外，数据绑定支持在标准 WPF 控件显示的用户界面不恰当时，使用数据模板来为数据绑定创建自定义的用户界面。  
  
   有关详细信息，请参阅[数据绑定概述](https://msdn.microsoft.com/library/ms752347\(v=vs.100\).aspx)。  
  
## <a name="Graphics"></a> 图形  
 WPF 引入了一组广泛、可伸缩的灵活图形功能，具有以下优点：  
  
- **图形与分辨率和设备均无关**。 WPF 图形系统中的基本度量单位是与设备无关的像素（即 1/96 英寸），且不考虑实际屏幕分辨率，并为实现与分辨率和设备无关的呈现提供了基础。 每个与设备无关的像素都会自动缩放，以匹配呈现它的系统的每英寸点数 (dpi) 设置。  
  
- **精度更高**。 WPF 坐标系统使用双精度浮点数字度量，而不是单精度数字。 转换和不透明度值也表示为双精度数字。 WPF 还支持广泛的颜色域 (scRGB)，并集成了对管理来自不同颜色空间的输入的支持。  
  
- **高级图形和动画支持**。 WPF 通过为你管理动画场景简化了图形编程，你无需担心场景处理、呈现循环和双线性内插。 此外，WPF 还提供了点击测试支持和全面的 alpha 合成支持。  
  
- **硬件加速**。 WPF 图形系统充分利用图形硬件来尽量降低 CPU 使用率。  
  
### <a name="2-d-shapes"></a>二维形状  
 WPF 提供一个常用矢量绘制的二维形状库，如下图中所示的矩形和椭圆。  
  
 ![椭圆和矩形](../designers/media/wpfintrofigure4.PNG "WPFIntroFigure4")  
  
 形状的一个有趣功能是它们不只是用于显示；形状实现许多你期望的控件功能，包括键盘和鼠标输入。 下面的示例演示要处理的 <xref:System.Windows.UIElement.MouseUp> 的 <xref:System.Windows.Shapes.Ellipse> 事件。  
  
 [!code-xml[IntroToWPFSnippets#HandleEllipseMouseUpEventMARKUP](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/EllipseEventHandlingWindow.xaml#handleellipsemouseupeventmarkup)]  
  
 [!code-csharp[IntroToWPFSnippets#HandleEllipseMouseUpEventCODEBEHIND](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/EllipseEventHandlingWindow.xaml.cs#handleellipsemouseupeventcodebehind)]
 [!code-vb[IntroToWPFSnippets#HandleEllipseMouseUpEventCODEBEHIND](../snippets/visualbasic/VS_Snippets_Wpf/IntroToWPFSnippets/VisualBasic/EllipseEventHandlingWindow.xaml.vb#handleellipsemouseupeventcodebehind)]  
  
 下图显示了前面的代码生成的内容。  
  
 ![包含文本“你已单击省略号!”的窗口](../designers/media/wpfintrofigure12.png "WPFIntroFigure12")  
  
 有关详细信息，请参阅 [WPF 中的形状和基本绘图概述](https://msdn.microsoft.com/library/ms747393\(v=vs.100\).aspx)。  
  
### <a name="2-d-geometries"></a>二维几何图形  
 WPF 提供的二维形状包含基本形状的标准集。 但是，你可能需要创建自定义形状以帮助改进自定义用户界面的设计。 为此，WPF 提供了几何图形。 下图演示了使用几何图形来创建可直接绘制、用作画笔或用于剪辑其他形状和控件的自定义形状。  
  
 <xref:System.Windows.Shapes.Path> 对象可用于绘制封闭式或开放式形状、多个形状，甚至曲线形状。  
  
 <xref:System.Windows.Media.Geometry> 对象可用于剪辑、命中测试以及呈现二维图形数据。  
  
 ![Path 的各种用法](../designers/media/wpfintrofigure5.PNG "WPFIntroFigure5")  
  
 有关详细信息，请参阅 [几何图形概述](https://msdn.microsoft.com/library/ms751808\(v=vs.100\).aspx)  
  
### <a name="2-d-effects"></a>二维效果  
 WPF 二维功能的子集包括视觉效果，如渐变、位图、绘图、用视频绘画、旋转、缩放和倾斜。 这些效果都可以使用画笔实现；下图演示了一些示例。  
  
 ![不同画笔的图示](../designers/media/wpfintrofigure6.PNG "WPFIntroFigure6")  
  
 有关详细信息，请参阅 [WPF 画笔概述](https://msdn.microsoft.com/library/aa970904\(v=vs.100\).aspx)。  
  
### <a name="3-d-rendering"></a>三维呈现  
 WPF 还包括三维呈现功能，这些功能与二维图形集成，以创建更精彩、更有趣的用户界面。 例如，下图显示呈现在三维形状上的二维图像。  
  
 ![Visual3D 示例屏幕快照](../designers/media/wpfintrofigure13.png "WPFIntroFigure13")  
  
 有关详细信息，请参阅 [三维图形概述](https://msdn.microsoft.com/library/ms747437\(v=vs.100\).aspx)。  
  
## <a name="Animation"></a> 动画  
 WPF 动画支持可以使控件变大、抖动、旋转和淡出，以形成有趣的页面过渡等。 你可以对大多数 WPF 类，甚至自定义类进行动画处理。 下图显示了运行中的一个简单动画。  
  
 ![具有动画多维数据集的图像](../designers/media/wpfintrofigure7.png "WPFIntroFigure7")  
  
 有关详细信息，请参阅 [动画概述](https://msdn.microsoft.com/library/ms752312\(v=vs.100\).aspx)。  
  
## <a name="Media"></a> 媒体  
 传达丰富内容的一种方法是使用视听媒体。 WPF 为图像、视频和音频提供特殊支持。  
  
### <a name="images"></a>映像  
 图像对大多数应用程序很常见，WPF 提供多种方式来使用它们。 下图显示一个用户界面，该用户界面中的列表框中包含缩略图图像。 选中一个缩略图后，将显示该图像的原尺寸。  
  
 ![缩略图图像和完整尺寸图像](../designers/media/wpfintrofigure8.PNG "WPFIntroFigure8")  
  
 有关详细信息，请参阅 [图像概述](https://msdn.microsoft.com/library/ms748873\(v=vs.100\).aspx)。  
  
### <a name="video-and-audio"></a>视频和音频  
 <xref:System.Windows.Controls.MediaElement> 控件能够播放视频和音频，并且其足够灵活，可以用作其他自定义媒体播放器的基础。 下面的 XAML 标记实现一个媒体播放器。  
  
 [!code-xml[IntroToWPFSnippets#MediaElementMARKUP](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/MediaElementWindow.xaml#mediaelementmarkup)]  
  
 下图中的窗口显示了运行中的 <xref:System.Windows.Controls.MediaElement> 控件。  
  
 ![具有音频和视频的 MediaElement 控件](../designers/media/wpfintrofigure1.png "WPFIntroFigure1")  
  
 有关详细信息，请参阅 [WPF 图形、动画和媒体概述](https://msdn.microsoft.com/library/ms742562\(v=vs.100\).aspx)。  
  
## <a name="Text_and_Typography"></a> 文本和版式  
 为了促进高质量的文本呈现，WPF 提供以下功能：  
  
- OpenType 字体支持。  
  
- ClearType 增强功能。  
  
- 利用硬件加速的高性能。  
  
- 文本与媒体、图形和动画的集成。  
  
- 国际字体支持和回退机制。  
  
  作为文本与图形集成的演示，下图显示了文本修饰的应用程序。  
  
  ![具有各种文本修饰的文本](../designers/media/wpfintrofigure23.png "WPFIntroFigure23")  
  
  有关详细信息，请参阅 [Windows Presentation Foundation 中的版式](https://msdn.microsoft.com/library/ms742190\(v=vs.100\).aspx)。  
  
## <a name="WPF_Customization"></a> 自定义 WPF 应用程序  
 到目前为止，你已经了解用于开发应用程序的核心 WPF 构建块。 你可以使用该应用程序模型来托管和交付应用程序内容，它主要由控件组成。 若要简化用户界面中控件的排列，并确保保持该排列能够应对窗口大小和显示设置的更改，你可以使用 WPF 布局系统。 由于大多数应用程序允许用户与数据交互，因此你可以使用数据绑定来减少将用户界面与数据集成的工作。 若要增强你应用程序的可视化外观，可以使用 WPF 提供的综合图形、动画和媒体支持。  
  
 不过，在创建和管理真正独特且视觉效果非凡的用户体验时，基础知识通常是不够的。 标准的 WPF 控件可能无法与你所需的应用程序外观集成。 数据可能不会以最有效的方式显示。 你应用程序的整体用户体验可能不适合 Windows 主题的默认外观和感觉。 在许多方面，演示技术需要视觉扩展性，需要的程度与任何其他类型的扩展性一样。  
  
 为此，WPF 提供了多种机制用于创建独特的用户体验，包括控件、触发器、控件和数据模板、样式、用户界面资源以及主题和皮肤的丰富内容模型。  
  
### <a name="content-model"></a>内容模型  
 大多数 WPF 控件的主要用途是显示内容。 在 WPF 中，可以构成控件内容的项的类型和数目称为控件的 *内容模型*。 某些控件可以包含一种内容类型的一个项；例如， <xref:System.Windows.Controls.TextBox> 的内容是分配给 <xref:System.Windows.Controls.TextBox.Text%2A> 属性的一个字符串值。 下面的示例设置 <xref:System.Windows.Controls.TextBox>的内容。  
  
 [!code-xml[IntroToWPFSnippets#TextBoxContentMARKUP1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/TextBoxContentWindow.xaml#textboxcontentmarkup1)]  
[!code-xml[IntroToWPFSnippets#TextBoxContentMARKUP2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/TextBoxContentWindow.xaml#textboxcontentmarkup2)]  
[!code-xml[IntroToWPFSnippets#TextBoxContentMARKUP3](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/TextBoxContentWindow.xaml#textboxcontentmarkup3)]  
  
 下图显示结果。  
  
 ![包含文本的 TextBox 控件](../designers/media/wpfintrofigure21.png "WPFIntroFigure21")  
  
 但是，其他控件可以包含不同内容类型的多个项； <xref:System.Windows.Controls.Button>的内容（由 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性指定）可以包含各种项（包括布局控件、文本、图像和形状）。 下面的示例演示了 <xref:System.Windows.Controls.Button> ，其内容包括 <xref:System.Windows.Controls.DockPanel>、 <xref:System.Windows.Controls.Label>、 <xref:System.Windows.Controls.Border>和 <xref:System.Windows.Controls.MediaElement>。  
  
 [!code-xml[IntroToWPFSnippets#ButtonContentMARKUP1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/ButtonContentWindow.xaml#buttoncontentmarkup1)]  
[!code-xml[IntroToWPFSnippets#ButtonContentMARKUP2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/ButtonContentWindow.xaml#buttoncontentmarkup2)]  
[!code-xml[IntroToWPFSnippets#ButtonContentMARKUP3](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/ButtonContentWindow.xaml#buttoncontentmarkup3)]  
  
 下图显示此按钮的内容。  
  
 ![包含多种类型的内容的按钮](../designers/media/wpfintrofigure22.png "WPFIntroFigure22")  
  
 有关各种控件支持的内容类型的详细信息，请参阅 [WPF 内容模型](https://msdn.microsoft.com/library/bb613548\(v=vs.100\).aspx)。  
  
### <a name="triggers"></a>触发器  
 尽管 XAML 标记的主要用途是实现应用程序的外观，你也可以使用 XAML 来实现应用程序行为的某些方面。 其中一个示例是使用触发器来基于用户交互更改应用程序的外观。 有关详细信息，请参阅[样式设置和模板化](https://msdn.microsoft.com/library/ms745683\(v=vs.100\).aspx)。  
  
### <a name="control-templates"></a>控件模板  
 WPF 控件的默认用户界面通常是从其他控件和形状构造的。 例如， <xref:System.Windows.Controls.Button> 由 <xref:Microsoft.Windows.Themes.ButtonChrome> 和 <xref:System.Windows.Controls.ContentPresenter> 控件组成。 <xref:Microsoft.Windows.Themes.ButtonChrome> 提供了标准按钮外观，而 <xref:System.Windows.Controls.ContentPresenter> 显示按钮的内容，正如 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性所指定。  
  
 有时，某个控件的默认外观可能与应用程序的整体外观不一致。 在这种情况下，可以使用 <xref:System.Windows.Controls.ControlTemplate> 更改控件的用户界面的外观，而不更改其内容和行为。  
  
 例如，下面的示例演示如何使用 <xref:System.Windows.Controls.Button> 更改 <xref:System.Windows.Controls.ControlTemplate>的外观。  
  
 [!code-xml[IntroToWPFSnippets#ButtonControlTemplateWindowMARKUP](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/ControlTemplateButtonWindow.xaml#buttoncontroltemplatewindowmarkup)]  
  
 [!code-csharp[IntroToWPFSnippets#ButtonControlTemplateWindowCODEBEHIND](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/ControlTemplateButtonWindow.xaml.cs#buttoncontroltemplatewindowcodebehind)]
 [!code-vb[IntroToWPFSnippets#ButtonControlTemplateWindowCODEBEHIND](../snippets/visualbasic/VS_Snippets_Wpf/IntroToWPFSnippets/VisualBasic/ControlTemplateButtonWindow.xaml.vb#buttoncontroltemplatewindowcodebehind)]  
  
 在此示例中，默认按钮用户界面已被替换为 <xref:System.Windows.Shapes.Ellipse> ，它具有深蓝色边框并使用 <xref:System.Windows.Media.RadialGradientBrush>进行填充。 <xref:System.Windows.Controls.ContentPresenter> 控件显示 <xref:System.Windows.Controls.Button>的内容，“单击我!” 单击 <xref:System.Windows.Controls.Button> 后，在 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 控件的默认行为中，仍将引发 <xref:System.Windows.Controls.Button> 事件。 结果如下图所示。  
  
 ![省略号按钮和第二个窗口](../designers/media/wpfintrofigure2.png "WPFIntroFigure2")  
  
### <a name="data-templates"></a>数据模板  
 使用控件模板可以指定控件的外观，而使用数据模板则可以指定控件内容的外观。 数据模板经常用于改进绑定数据的显示方式。 下图显示 <xref:System.Windows.Controls.ListBox> 的默认外观，它绑定到 `Task` 对象的集合，其中每个任务都具有名称、描述和优先级。  
  
 ![具有默认外观的列表框](../designers/media/wpfintrofigure18.png "WPFIntroFigure18")  
  
 默认外观是你对 <xref:System.Windows.Controls.ListBox>的期望。 但是，每个任务的默认外观仅包含任务名称。 若要显示任务名称、描述和优先级，必须使用 <xref:System.Windows.Controls.ListBox> 更改 <xref:System.Windows.DataTemplate>控件绑定列表项的默认外观。 下面的 XAML 定义了此类 <xref:System.Windows.DataTemplate>，它通过使用 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 特性应用于每个任务。  
  
 [!code-xml[IntroToWPFSnippets#DataTemplateMARKUP1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/DataTemplateWindow.xaml#datatemplatemarkup1)]  
[!code-xml[IntroToWPFSnippets#DataTemplateMARKUP2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/DataTemplateWindow.xaml#datatemplatemarkup2)]  
[!code-xml[IntroToWPFSnippets#DataTemplateMARKUP3](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/DataTemplateWindow.xaml#datatemplatemarkup3)]  
[!code-xml[IntroToWPFSnippets#DataTemplateMARKUP4](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/DataTemplateWindow.xaml#datatemplatemarkup4)]  
  
 下图显示了此代码的作用。  
  
 ![使用数据模板的列表框](../designers/media/wpfintrofigure19.png "WPFIntroFigure19")  
  
 注意， <xref:System.Windows.Controls.ListBox> 已保留其行为和整体外观；仅列表框显示的内容外观已更改。  
  
 有关详细信息，请参阅 [数据模板化概述](https://msdn.microsoft.com/library/ms742521\(v=vs.100\).aspx)。  
  
### <a name="styles"></a>样式  
 通过样式功能，开发人员和设计人员能够对其产品的特定外观进行标准化。 WPF 提供了一个强样式模型，其基础是 <xref:System.Windows.Style> 元素。 下面的示例创建一个样式，该样式将窗口上的每个 <xref:System.Windows.Controls.Button> 的背景色设置为 `Orange`。  
  
 [!code-xml[IntroToWPFSnippets#StyleMARKUP1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/StyleWindow.xaml#stylemarkup1)]  
[!code-xml[IntroToWPFSnippets#StyleMARKUP2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/StyleWindow.xaml#stylemarkup2)]  
[!code-xml[IntroToWPFSnippets#StyleMARKUP3](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/StyleWindow.xaml#stylemarkup3)]  
[!code-xml[IntroToWPFSnippets#StyleMARKUP4](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/StyleWindow.xaml#stylemarkup4)]  
  
 由于此样式针对所有 <xref:System.Windows.Controls.Button> 控件，因此将自动应用于窗口中的所有按钮，如下图所示。  
  
 ![两个橙色按钮](../designers/media/wpfintrofigure20.png "WPFIntroFigure20")  
  
 有关详细信息，请参阅[样式设置和模板化](https://msdn.microsoft.com/library/ms745683\(v=vs.100\).aspx)。  
  
### <a name="resources"></a>资源  
 应用程序中的控件应共享相同的外观，它可以包括从字体和背景色到控件模板、数据模板和样式的所有内容。 你可以对用户界面资源使用 WPF 支持，以将这些资源封装在一个位置以便重复使用。  
  
 下面的示例定义 <xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Controls.Label>共享的通用背景色。  
  
 [!code-xml[IntroToWPFSnippets#ResourceWindowMARKUP1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/ResourcesWindow.xaml#resourcewindowmarkup1)]  
[!code-xml[IntroToWPFSnippets#ResourceWindowMARKUP2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/ResourcesWindow.xaml#resourcewindowmarkup2)]  
[!code-xml[IntroToWPFSnippets#ResourceWindowMARKUP3](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/ResourcesWindow.xaml#resourcewindowmarkup3)]  
  
 此示例通过使用 `Window.Resources` 属性元素实现背景色资源。 此资源可供 <xref:System.Windows.Window>的所有子级使用。 有各种资源作用域，具体如下（按解析顺序列出）：  
  
1. 单个控件（使用继承的 <xref:System.Windows.FrameworkElement.Resources%2A?displayProperty=fullName> 属性）。  
  
2. <xref:System.Windows.Window> 或 <xref:System.Windows.Controls.Page> （也使用继承的 <xref:System.Windows.FrameworkElement.Resources%2A?displayProperty=fullName> 属性）。  
  
3. <xref:System.Windows.Application> （使用 <xref:System.Windows.Application.Resources%2A?displayProperty=fullName> 属性）。  
  
   这些不同种类的作用域在定义和共享资源的方式方面为你提供了灵活性。  
  
   作为直接将你的资源与特定作用域关联的替代方法，可以通过使用单独的 <xref:System.Windows.ResourceDictionary> （可以在应用程序的其他部分引用）打包一个或多个资源。 例如，下面的示例定义资源字典中的默认背景色。  
  
   [!code-xml[IntroToWPFSnippets#ResourceDictionaryMARKUP1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/BackgroundColorResources.xaml#resourcedictionarymarkup1)]  
   [!code-xml[IntroToWPFSnippets#ResourceDictionaryMARKUP2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/BackgroundColorResources.xaml#resourcedictionarymarkup2)]  
  
   下面的示例引用上一个示例中定义的资源字典，以便在应用程序中共享它。  
  
   [!code-xml[IntroToWPFSnippets#ApplicationScopedResourceDictionaryMARKUP1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/App.xaml#applicationscopedresourcedictionarymarkup1)]  
   [!code-xml[IntroToWPFSnippets#ApplicationScopedResourceDictionaryMARKUP2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/App.xaml#applicationscopedresourcedictionarymarkup2)]  
  
   资源和资源字典是 WPF 主题和皮肤支持的基础。  
  
   有关详细信息，请参阅 [资源概述](https://msdn.microsoft.com/library/ms750613\(v=vs.100\).aspx)。  
  
### <a name="custom-controls"></a>自定义控件  
 尽管 WPF 提供了大量自定义支持，但你仍可能会遇到现有 WPF 控件不满足你的应用程序或其用户的需求的情况。 出现这种情况的原因有：  
  
- 不能通过自定义现有 WPF 实现的外观和感觉创建所需的用户界面。  
  
- 现有 WPF 实现不支持（或很难支持）所需的行为。  
  
  但是，此时，你可以充分利用三个 WPF 模型中的一个来创建新的控件。 每个模型都针对一个特定的方案并要求你的自定义控件派生自特定 WPF 基类。 下面列出了这三个模型：  
  
- **用户控件模型**。 自定义控件派生自 <xref:System.Windows.Controls.UserControl> 并由一个或多个其他控件组成。  
  
- **控件模型**。 自定义控件派生自 <xref:System.Windows.Controls.Control> ，并用于生成使用模板将其行为与其外观分隔开来的实现，非常类似大多数 WPF 控件。 派生自 <xref:System.Windows.Controls.Control> 使得你可以更自由地创建自定义用户界面（相较用户控件），但它可能需要花费更多精力。  
  
- **框架元素模型**。 当其外观由自定义呈现逻辑（而不是模板）定义时，自定义控件派生自 <xref:System.Windows.FrameworkElement> 。  
  
  下面的示例演示一个派生自 <xref:System.Windows.Controls.UserControl>的自定义数值加/减控件。  
  
  [!code-xml[IntroToWPFSnippets#UserControlMARKUP](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/NumericUpDown.xaml#usercontrolmarkup)]  
  
  [!code-csharp[IntroToWPFSnippets#UserControlCODEBEHIND1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/NumericUpDown.xaml.cs#usercontrolcodebehind1)]
  [!code-vb[IntroToWPFSnippets#UserControlCODEBEHIND1](../snippets/visualbasic/VS_Snippets_Wpf/IntroToWPFSnippets/VisualBasic/NumericUpDown.xaml.vb#usercontrolcodebehind1)]  
  [!code-csharp[IntroToWPFSnippets#UserControlCODEBEHIND2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/NumericUpDown.xaml.cs#usercontrolcodebehind2)]
  [!code-vb[IntroToWPFSnippets#UserControlCODEBEHIND2](../snippets/visualbasic/VS_Snippets_Wpf/IntroToWPFSnippets/VisualBasic/NumericUpDown.xaml.vb#usercontrolcodebehind2)]  

 下一个示例说明了将用户控件合并到 <xref:System.Windows.Window>所需的 XAML。  
  
 [!code-xml[IntroToWPFSnippets#UserControlWindowMARKUP1](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/UserControlWindow.xaml#usercontrolwindowmarkup1)]  
[!code-xml[IntroToWPFSnippets#UserControlWindowMARKUP2](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/UserControlWindow.xaml#usercontrolwindowmarkup2)]  
[!code-xml[IntroToWPFSnippets#UserControlWindowMARKUP3](../snippets/csharp/VS_Snippets_Wpf/IntroToWPFSnippets/CSharp/UserControlWindow.xaml#usercontrolwindowmarkup3)]  
  
 下图显示了 `NumericUpDown` 中托管的 <xref:System.Windows.Window>控件。  
  
 ![自定义用户控件](../designers/media/wpfintrofigure3.png "WPFIntroFigure3")  
  
 有关自定义控件的详细信息，请参阅 [控件创作概述](https://msdn.microsoft.com/library/ms745025\(v=vs.100\).aspx)。  
  
## <a name="WPF_Best_Practices"></a> WPF 最佳做法  
 与任何开发平台一样，可以采用多种方式使用 WPF 以实现所需的结果。 为确保你的 WPF 应用程序提供所需的用户体验并满足一般用户的需求，针对辅助功能、全球化和本地化以及性能提供了一些建议的最佳做法。 有关详细信息，请参阅以下主题：  
  
- [辅助功能最佳做法](https://msdn.microsoft.com/library/aa350483\(v=vs.100\).aspx)辅助功能最佳做法  
  
- [WPF 全球化和本地化概述](https://msdn.microsoft.com/library/ms788718\(v=vs.100\).aspx)  
  
- [优化 WPF 应用程序性能](https://msdn.microsoft.com/library/aa970683\(v=vs.100\).aspx)  
  
- [Windows Presentation Foundation 安全性](https://msdn.microsoft.com/library/aa970906\(v=vs.100\).aspx)  
  
## <a name="Summary"></a> 摘要  
 WPF 是一种综合演示技术，用于生成各种视觉效果非凡的客户端应用程序。 本简介已大致介绍了 WPF 的主要功能。  
  
 接着是如何生成 WPF 应用程序！  
  
 在你生成应用程序时，你可以回到本简介复习主要功能，并查找对本简介中所涵盖功能的更详细说明的参考。  
  
## <a name="see-also"></a>请参阅  
 [WPF 入门](../designers/getting-started-with-wpf.md)   
 [使用 Windows Presentation Foundation 创建现代桌面应用程序](../designers/create-modern-desktop-applications-with-windows-presentation-foundation.md)   
 [Windows Presentation Foundation](https://msdn.microsoft.com/library/ms754130\(v=vs.100\).aspx)

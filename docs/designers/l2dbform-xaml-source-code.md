---
title: L2DBForm.xaml 源代码
ms.date: 11/04/2016
ms.topic: sample
ms.assetid: 624e96d4-6d27-4195-8ac2-2f3835f6c57e
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 41796664d5456876edff81662cbab44edf7a82f2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72635287"
---
# <a name="l2dbformxaml-source-code"></a>L2DBForm.xaml 源代码

本主题包含并说明[使用 LINQ to XML 的 WPF 数据绑定示例](../designers/wpf-data-binding-using-linq-to-xml-example.md)的 XAML 源文件 L2DBForm.xaml  。

## <a name="overall-ui-structure"></a>总体 UI 结构

和典型的 WPF 项目一样，此文件包含一个父元素，该元素是一个与 <xref:System.Windows.Window> 命名空间中的派生类 `L2XDBFrom` 相关联的 `LinqToXmlDataBinding` XML 元素。

客户端区域包含在具有浅蓝色背景的 <xref:System.Windows.Controls.StackPanel> 中。 此面板包含四个 <xref:System.Windows.Controls.DockPanel> UI 区域，由 <xref:System.Windows.Controls.Separator> 条分隔。 **上一个主题** 的 [备注](../designers/walkthrough-linqtoxmldatabinding-example.md)中说明了这些区域的用途。

每个区域都包含一个标识该区域的标签。 在前两个区域中，此标签通过使用 <xref:System.Windows.FrameworkElement.LayoutTransform%2A>旋转 90 度。 该区域的其余部分包含对应于该区域用途的 UI 元素：文本块、文本框、按钮等。 有时使用子 <xref:System.Windows.Controls.StackPanel> 来对齐这些子控件。

## <a name="window-resource-section"></a>窗口资源区域

在第 9 行上的 `<Window.Resources>` 开始标记指示窗口资源区域的开始。 它在第 35 行上以结束标记结束。

`<ObjectDataProvider>` 标记跨越第 11 至第 25 行，声明一个名为 <xref:System.Windows.Data.ObjectDataProvider>的 `LoadedBooks`，它使用 <xref:System.Xml.Linq.XElement> 作为源。 此 <xref:System.Xml.Linq.XElement> 是通过分析嵌入的 XML 文档（一个 `CDATA` 元素）来初始化的。 请注意，在声明嵌入的 XML 文档以及分析该文档时将保留空格。 之所以保留空格是因为用于显示原始 XML 的 <xref:System.Windows.Controls.TextBlock> 控件没有专门的 XML 格式化功能。

最后，第 28 行至第 34 行定义一个名为 <xref:System.Windows.DataTemplate> 的 `BookTemplate` 。 此模板将用于显示“Book List”（书籍列表）  UI 区域中的条目。 它使用数据绑定和 LINQ to XML 动态属性通过下面的赋值来检索书籍 ID 和书名：

```xaml
Text="{Binding Path=Attribute[id].Value}"Text="{Binding Path=Value}"
```

## <a name="data-binding-code"></a>数据绑定代码

除 <xref:System.Windows.DataTemplate> 元素外，本文件中的许多其他位置也使用数据绑定。

在第 38 行的 `<StackPanel>` 开始标记中，此面板的 <xref:System.Windows.FrameworkElement.DataContext%2A> 属性设置为 `LoadedBooks` 数据提供程序。

```xaml
DataContext="{Binding Source={StaticResource LoadedBooks}}
```

设置数据上下文使名为 `tbRawXml` 的 <xref:System.Windows.Controls.TextBlock>（第 46 行）能够通过绑定到此数据提供程序的 `Xml` 属性来显示原始 XML：

```xaml
Text="{Binding Path=Xml}"
```

从第 58 行至第 62 行，“Book List”（书籍列表） <xref:System.Windows.Controls.ListBox>**UI 区域中的** 将其显示项的模板设置为在窗口资源区域中定义的 `BookTemplate` ：

```xaml
ItemTemplate ="{StaticResource BookTemplate}"
```

然后，第 59 行至第 62 行将书籍的实际值绑定到此列表框：

```xaml
<ListBox.ItemsSource>
    <Binding Path="Elements[{http://www.mybooks.com}book]"/>
</ListBox.ItemsSource>
```

在第三个 UI 区域 **“Edit Selected Book”（编辑所选书籍）** 中，首先将父 <xref:System.Windows.FrameworkElement.DataContext%2A> 的 <xref:System.Windows.Controls.StackPanel> 绑定到 **“Book List”（书籍列表）** UI 区域中的当前所选项（第 82 行）：

```xaml
DataContext="{Binding ElementName=lbBooks, Path=SelectedItem}"
```

然后使用双向数据绑定，使书籍元素的当前值显示在此面板的两个文本框中并从中进行更新。 数据绑定到动态属性类似于在 `BookTemplate` 数据模板中使用数据绑定：

```xaml
Text="{Binding Path=Attribute[id].Value}"...Text="{Binding Path=Value}"
```

最后一个 UI 区域“Add New Book”（新增书籍）不在其 XAML 代码中使用数据绑定  。 数据绑定在 L2DBForm.xaml.cs 文件的事件处理代码中  。

## <a name="example"></a>示例

### <a name="description"></a>说明

> [!NOTE]
> 建议您将下面的代码复制到代码编辑器（如 Visual Studio 中的 C# 源代码编辑器）中，以便更易于跟踪行号。

### <a name="code"></a>代码

```xml
<Window x:Class="LinqToXmlDataBinding.L2XDBForm"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:system="clr-namespace:System;assembly=mscorlib"
    xmlns:xlinq="clr-namespace:System.Xml.Linq;assembly=System.Xml.Linq"
    xmlns:local="clr-namespace:LinqToXmlDataBinding"
    Title="WPF Data Binding using LINQ-to-XML" Height="665" Width="500" ResizeMode="NoResize">

    <Window.Resources>
        <!-- Books provider and inline data -->
        <ObjectDataProvider x:Key="LoadedBooks" ObjectType="{x:Type xlinq:XElement}" MethodName="Parse">
            <ObjectDataProvider.MethodParameters>
                <system:String xml:space="preserve">
<![CDATA[
<books xmlns="http://www.mybooks.com">
  <book id="0">book zero</book>
  <book id="1">book one</book>
  <book id="2">book two</book>
  <book id="3">book three</book>
</books>
]]>
                </system:String>
                <xlinq:LoadOptions>PreserveWhitespace</xlinq:LoadOptions>
            </ObjectDataProvider.MethodParameters>
        </ObjectDataProvider>

        <!-- Template for use in Books List listbox. -->
        <DataTemplate x:Key="BookTemplate">
            <StackPanel Orientation="Horizontal">
                <TextBlock Margin="3" Text="{Binding Path=Attribute[id].Value}"/>
                <TextBlock Margin="3" Text="-"/>
                <TextBlock Margin="3" Text="{Binding Path=Value}"/>
            </StackPanel>
        </DataTemplate>
    </Window.Resources>

    <!-- Main visual content container -->
    <StackPanel Background="lightblue" DataContext="{Binding Source={StaticResource LoadedBooks}}">
        <!-- Raw XML display section -->
        <DockPanel Margin="5">
            <Label  Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" FontWeight="Bold">XML
            <Label.LayoutTransform>
                <RotateTransform Angle="90"/>
            </Label.LayoutTransform>
            </Label>
            <TextBlock Name="tbRawXml" Height="200" Background="LightGray" Text="{Binding Path=Xml}" TextTrimming="CharacterEllipsis" />
        </DockPanel>

        <Separator Height="4" Margin="5" />

        <!-- List box to display all books section -->
        <DockPanel Margin="5">
            <Label  Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" FontWeight="Bold">Book List
                <Label.LayoutTransform>
                    <RotateTransform Angle="90"/>
                </Label.LayoutTransform>
            </Label>
            <ListBox Name="lbBooks" Height="200" Width="415" ItemTemplate ="{StaticResource BookTemplate}">
                <ListBox.ItemsSource>
                    <Binding Path="Elements[{http://www.mybooks.com}book]"/>
                </ListBox.ItemsSource>
            </ListBox>
            <Button Margin="5" DockPanel.Dock="Right" Height="30" Width ="130" Content="Remove Selected Book" Click="OnRemoveBook">
            <Button.LayoutTransform>
                <RotateTransform Angle="90"/>
            </Button.LayoutTransform>
            </Button>
        </DockPanel>

        <Separator Height="4" Margin="5" />

        <!-- Edit current selection section -->
        <DockPanel Margin="5">
            <TextBlock Margin="5" Height="30" Width="65" DockPanel.Dock="Right" Background="LightGray" TextWrapping="Wrap" TextAlignment="Center">
                    Changes are live!
                <TextBlock.LayoutTransform>
                    <RotateTransform Angle="90"/>
                </TextBlock.LayoutTransform>
            </TextBlock>
            <StackPanel>
                <Label Width="450" Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Left" FontWeight="Bold">Edit Selected Book</Label>
                <StackPanel Margin="1" DataContext="{Binding ElementName=lbBooks, Path=SelectedItem}">
                    <StackPanel Orientation="Horizontal">
                        <Label Width="40">ID:</Label>
                        <TextBox Name="editAttributeTextBox" Width="410" Text="{Binding Path=Attribute[id].Value}">
                            <TextBox.ToolTip>
                                <TextBlock FontWeight="Bold" TextAlignment="Center">
                                    <Label>Edit the selected book ID and see it changed.</Label>
                                </TextBlock>
                            </TextBox.ToolTip>
                        </TextBox>
                    </StackPanel>
                    <StackPanel Orientation="Horizontal">
                        <Label Width="40">Value:</Label>
                        <TextBox Name="editValueTextBox" Width="410" Text="{Binding Path=Value}" Height="25">
                            <TextBox.ToolTip>
                                <TextBlock FontWeight="Bold" TextAlignment="Center">
                                    <Label>Edit the selected book Value and see it changed.</Label>
                                </TextBlock>
                            </TextBox.ToolTip>
                        </TextBox>
                    </StackPanel>
                </StackPanel>
            </StackPanel>
        </DockPanel>

        <Separator Height="4" Margin="5" />

        <!-- Add new book section -->
        <DockPanel Margin="5">
            <Button Margin="5" Height="30" DockPanel.Dock="Right" Click ="OnAddBook">Add Book
                <Button.LayoutTransform>
                    <RotateTransform Angle="90"/>
                </Button.LayoutTransform>
            </Button>
            <StackPanel>
                <Label Width="450" Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Left" FontWeight="Bold">Add New Book</Label>
                <StackPanel Margin="1">
                    <StackPanel Orientation="Horizontal">
                        <Label Width="40">ID:</Label>
                        <TextBox Name="tbAddID" Width="410">
                            <TextBox.ToolTip>
                                <TextBlock FontWeight="Bold" TextAlignment="Center">
                                    <Label>Enter a book ID and Value pair, then click Add Book.</Label>
                                </TextBlock>
                            </TextBox.ToolTip>
                        </TextBox>
                    </StackPanel>
                    <StackPanel Orientation="Horizontal">
                        <Label Width="40">Value:</Label>
                        <TextBox Name="tbAddValue" Width="410" Height="25">
                            <TextBox.ToolTip>
                                <TextBlock FontWeight="UltraBold" TextAlignment="Center">
                                    <Label>Enter a book ID and Value pair, then click Add Book.</Label>
                                </TextBlock>
                            </TextBox.ToolTip>
                        </TextBox>
                    </StackPanel>
                </StackPanel>
            </StackPanel>
        </DockPanel>
    </StackPanel>
</Window>
```

### <a name="comments"></a>注释

有关与 WPF UI 元素相关联的事件处理程序的 C# 源代码，请参阅 [L2DBForm.xaml.cs 源代码](../designers/l2dbform-xaml-cs-source-code.md)。

## <a name="see-also"></a>请参阅

- [演练：LinqToXmlDataBinding 示例](../designers/walkthrough-linqtoxmldatabinding-example.md)
- [L2DBForm.xaml.cs 源代码](../designers/l2dbform-xaml-cs-source-code.md)
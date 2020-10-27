---
title: 在 Visual Studio 中通过 XAML 设计器使用设计时数据
description: 了解如何在 XAML 中使用设计时数据。
ms.date: 09/29/2020
ms.topic: overview
author: alihamie
ms.author: tglee
manager: jillfra
monikerRange: vs-2019
ms.openlocfilehash: b9477868d265e9ad8b927d9e13b67112c0ea14f7
ms.sourcegitcommit: 6b62e09026b6f1446187c905b789645f967a371c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92298476"
---
# <a name="use-design-time-data-with-the-xaml-designer-in-visual-studio"></a>在 Visual Studio 中通过 XAML 设计器使用设计时数据

有些布局没有数据很难进行可视化。 在本文档中，我们将审查从事桌面项目的开发人员可在 XAML 设计器中模拟数据的一种方法。 此方法是使用现有可忽略的“d:”命名空间来实现的。 利用这种方法，可快速将设计时数据添加到页面或控件中，而无需创建完整的模拟视图模型，或者只需测试属性更改会如何影响应用程序，而无需担心这些更改会影响你的发布版本。 所有 d: 数据仅由 XAML 设计器使用，无可忽略的命名空间值编译到应用程序中。

> [!NOTE]
> 如果你使用 Xamarin.Forms，请参阅 [Xamarin.Forms 设计时数据](/xamarin/xamarin-forms/xaml/xaml-previewer/design-time-data)

## <a name="design-time-data-basics"></a>设计时数据基本信息

设计时数据是你设置的模拟数据，使控件更易于在 XAML 设计器中进行可视化。 首先，将以下代码行添加到 XAML 文档的标头（如果这些代码行尚不存在）：

```xml 
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

添加命名空间后，可将 `d:` 置于任何特性或控件之前，使其仅在 XAML 设计器中显示，而不在运行时显示。

例如，可将文本添加到通常绑定了数据的 TextBlock。

```xml
<TextBlock Text="{Binding Name}" d:Text="Name!" />
```

[![TextBlock 中包含文本的设计时数据](media\xaml-design-time-textblock.png "标签中包含文本的设计时数据")](media\xaml-design-time-textblock.png#lightbox)

在此示例中，如果没有 `d:Text`，则 XAML 设计器对于 TextBlock 不显示任何内容。 而是显示“Name!”， 在此情况下，TextBlock 在运行时将具有实际数据。

可将 `d:` 与任何 UWP 或 WPF .NET Core 控件（如颜色、字号和间距）的特性结合使用。 甚至可以将其添加到控件本身。

```xml
<d:Button Content="Design Time Button" />
```

[![具有按钮控件的设计时数据](media\xaml-design-time-button.png "具有按钮控件的设计时数据")](media\xaml-design-time-button.png#lightbox)

在此示例中，按钮仅在设计时显示。 使用此方法可为自定义控件放置占位符，或者可试用不同的控件。 在运行时期间，所有 `d:` 特性和控件都将被忽略。

## <a name="preview-images-at-design-time"></a>在设计时预览图像

可为绑定到页面或动态加载的图像设置设计时源。 将要在 XAML 设计器中显示的图像添加到项目中。 然后，可在设计时在 XAML 设计器中显示该图像：

```xml
<Image Source={Binding ProfilePicture} d:Source="DesignTimePicture.jpg" />
```

> [!NOTE]
> 此示例中的图像必须存在于解决方案中。

## <a name="design-time-data-for-listviews"></a>ListView 的设计时数据

ListView 是一种在桌面应用中显示数据的常用方法。 但是，如果没有任何数据，ListView 就难以进行可视化。 可使用此功能创建内联设计时数据 ItemSource。 XAML 设计器在设计时在 ListView 中显示该数组中的内容。 这是一个 WPF .NET Core 示例。 若要使用 system:String 类型，请确保在 XAML 标头中包含 `xmlns:system="clr-namespace:System;assembly=mscorlib`。

```xml
<StackPanel>
    <ListView ItemsSource="{Binding Items}">
        <d:ListView.ItemsSource>
            <x:Array Type="{x:Type system:String}">
                <system:String>Item One</system:String>
                <system:String>Item Two</system:String>
                <system:String>Item Three</system:String>
            </x:Array>
        </d:ListView.ItemsSource>
    <ListView.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding ItemName}" d:Text="{Binding .}" />
        </DataTemplate>
    </ListView.ItemTemplate>
   </ListView>
</StackPanel>
```

[![具有 ListView 的设计时数据](media\xaml-design-time-listview-strings.png "具有 ListView 的设计时数据")](media\xaml-design-time-listview-strings.png#lightbox)

上一个示例显示了在 XAML 设计器中具有三个 TextBlock 的 ListView。

你也可以创建一个数据对象数组。 例如，可将 `City` 数据对象的公共属性构建为设计时数据。

```csharp
namespace Cities.Models
{
    public class City
    {
        public string Name { get; set; }
        public string Country { get; set; }
    }
}
```

若要在 XAML 中使用类，则必须在根节点中导入该命名空间。

```xaml
xmlns:models="clr-namespace:Cities.Models"
```

```xml
<StackPanel>
    <ListView ItemsSource="{Binding Items}">
        <d:ListView.ItemsSource>
            <x:Array Type="{x:Type models:City}">
                <models:City Name="Seattle" Country="United States"/>
                <models:City Name="London" Country="United Kingdom"/>
                <models:City Name="Panama City" Country="Panama"/>
            </x:Array>
        </d:ListView.ItemsSource>
        <ListView.ItemTemplate>
            <DataTemplate>
                 <StackPanel Orientation="Horizontal" >
                    <TextBlock Text="{Binding Name}" Margin="0,0,5,0" />
                    <TextBlock Text="{Binding Country}" />
                 </StackPanel>
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>
</StackPanel>
```

[![具有 ListView 的实际模型设计时数据](media\xaml-design-time-listview-models.png "具有 ListView 的实际模型设计时数据")](media\xaml-design-time-listview-models.png#lightbox)

这样做的好处是，你可将控件绑定到模型的设计时静态版本。

## <a name="use-design-time-data-with-custom-types-and-properties"></a>将设计时数据与自定义类型和属性一起使用

默认情况下，此功能仅适用于平台控件和属性。 在本部分中，我们将执行所需的步骤，使你能够将自己的自定义控件用作设计时控件，这是面向使用 Visual Studio 2019 预览版本 [16.8](/visualstudio/releases/2019/preview-notes) 或更高版本的客户提供的新功能。 要实现此操作，需要满足三个要求：

- 一个自定义 xmlns 命名空间 

    ```xml
    xmlns:myControls="http://MyCustomControls"
    ```

- 一个命名空间的设计时版本。 只需在末尾追加/设计即可实现。

     ```xml
    xmlns:myDesignTimeControls="http://MyCustomControls/design"
    ```

- 将设计时前缀添加到 mc:Ignorable

    ```xml
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d myDesignTimeControls"
    ```

完成所有这些步骤后，可以使用 `myDesignTimeControls` 前缀来创建设计时控件。

```xml
<myDesignTimeControls:MyButton>I am a design time Button</myDesignTimeControls:MyButton>
```

### <a name="creating-a-custom-xmlns-namespace"></a>创建自定义 xmlns 命名空间

若要在 WPF .NET Core 中创建自定义 xmlns 命名空间，需要将自定义 XML 命名空间映射到控件所在的 CLR 命名空间。 可通过在 `AssemblyInfo.cs` 文件中添加 `XmlnsDefinition` 程序集级别属性来实现此操作。 可在项目的根层次结构中找到该文件。

   ```C#
[assembly: XmlnsDefinition("http://MyCustomControls", "MyViews.MyButtons")]
   ```

## <a name="troubleshooting"></a>疑难解答

如果你遇到此部分中未列出的问题，请通过使用[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)工具来告知我们。

### <a name="requirements"></a>要求

- 设计时数据需要 Visual Studio 2019 版本 [16.7](/visualstudio/releases/2019/release-notes) 或更高版本。

- 支持目标是适用于 .NET Core 的 Windows Presentation Foundation (WPF) 和 UWP 的 Windows 桌面项目。 如果已启用“适用于 .NET Framework 的新版 WPF XAML 设计器”预览功能，则此功能还可用于 .NET Framework。

- 从 Visual Studio 2019 版本 16.7 开始，此功能适用于 WPF 和 UWP 框架中的所有内置控件。 16.8 预览版本现已提供对第三方控件的支持。

### <a name="the-xaml-designer-stopped-working"></a>XAML 设计器停止工作

尝试关闭并重新打开 XAML 文件，清理并重新生成项目。

## <a name="see-also"></a>请参阅

- [具有 Xamarin.Forms 预览器的设计时数据](/xamarin/xamarin-forms/xaml/xaml-Designer/design-time-data/)
- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)
---
title: 为 UWP 控件设置唯一的自动化属性以进行测试
ms.date: 05/31/2018
ms.topic: conceptual
ms.author: gewarren
manager: jillfra
ms.workload:
- uwp
author: gewarren
ms.openlocfilehash: fd939162ff4063a66ac0afe1e6830a0d3b32bab2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429378"
---
# <a name="set-a-unique-automation-property-for-uwp-controls-for-testing"></a>为 UWP 控件设置唯一的自动化属性以进行测试

若想针对基于 XAML 的 UWP 应用程序运行编码的 UI 测试，每个控件必须由唯一的自动化属性标识。 可以根据应用中 XAML 控件的类型分配唯一自动化属性。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="static-xaml-definition"></a>静态 XAML 定义

若要为 XAML 文件中定义的控件指定唯一自动化属性，可以隐式或显式设置 AutomationProperties.AutomationId 或 AutomationProperties.Name，如以下示例所示。 设置这两个值中的任意一个都可以为控件指定唯一自动化属性，以在创建编码的 UI 测试或操作录制时标识控件。

### <a name="set-the-property-implicitly"></a>隐式设置属性

使用控件 XAML 中的 Name 属性将 AutomationProperties.AutomationId 设为“ButtonX”。

```xaml
<Button Name="ButtonX" Height="31" HorizontalAlignment="Left" Margin="23,26,0,0"  VerticalAlignment="Top" Width="140" Click="ButtonX_Click" />
```

使用控件 XAML 中的 Content 属性将 AutomationProperties.Name 设为“ButtonY”。

```xaml
<Button Content="ButtonY" Height="31" HorizontalAlignment="Left" Margin="23,76,0,0" VerticalAlignment="Top" Width="140" Click="ButtonY_Click" />
```

### <a name="set-the-property-explicitly"></a>显式设置属性

在控件 XAML 中将 AutomationProperties.AutomationId 显式设为“ButtonX”。

```xaml
<Button AutomationProperties.AutomationId="ButtonX" Height="31" HorizontalAlignment="Left" Margin="23,26,0,0"  VerticalAlignment="Top" Width="140" Click="ButtonX_Click" />
```

在控件 XAML 中将 AutomationProperties.Name 显式设为“ButtonY”。

```xaml
<Button AutomationProperties.Name="ButtonY" Height="31" HorizontalAlignment="Left" Margin="23,76,0,0" VerticalAlignment="Top" Width="140" Click="ButtonY_Click" />
```

## <a name="assign-unique-names"></a>分配唯一的名称

在 Blend for Visual Studio 中，可以选择一个选项为按钮、列表框、组合框和文本框等交互元素分配唯一名称，因此授予了控件 AutomationProperties.Name 的唯一值。

为了将唯一的名称分配到现有控件，请选择“工具” > “命名交互元素”。

![Blend for Visual Studio 中的命名交互元素](../test/media/cuit_windowsstoreproperty_blend_1.png)

若要自动为新添加的控件指定唯一的名称，请选择“工具” > “选项”以打开“选项”对话框。 选择“XAML 设计器”，然后选择“在创建时自动命名交互元素”。 选择“确定”关闭对话框。

## <a name="use-a-data-template"></a>使用数据模板

可以使用 ItemTemplate 定义简单模板，从而将列表框中的值与变量绑定在一起：

```xaml
<ListBox Name="listBox1" ItemsSource="{Binding Source={StaticResource employees}}">
   <ListBox.ItemTemplate>
      <DataTemplate>
         <StackPanel Orientation="Horizontal">
            <TextBlock Text="{Binding EmployeeName}" />
            <TextBlock Text="{Binding EmployeeID}" />
         </StackPanel>
      </DataTemplate>
   </ListBox.ItemTemplate>
</ListBox>
```

也可以使用 ItemContainerStyle 定义模板，从而将值与变量绑定在一起：

```xaml
<ListBox Name="listBox1" ItemsSource="{Binding Source={StaticResource employees}}">
   <ListBox.ItemContainerStyle>
      <Style TargetType="ListBoxItem">
         <Setter Property="Template">
            <Setter.Value>
               <ControlTemplate TargetType="ListBoxItem">
                  <Grid>
                     <Button Content="{Binding EmployeeName}" AutomationProperties.AutomationId="{Binding EmployeeID}"/>
                  </Grid>
               </ControlTemplate>
            </Setter.Value>
         </Setter>
      </Style>
   </ListBox.ItemContainerStyle>
</ListBox>
```

对于这两个示例，必须替代 ItemSource 的 ToString() 方法，如以下代码示例所示。 此代码可确保设置唯一的 AutomationProperties.Name 值，因为无法通过绑定为每个数据绑定列表项设置唯一自动化属性。 在这种情况下，设置唯一的 Automation Properties.Name 值就足够了。

> [!NOTE]
> 使用这种方法，还可以通过绑定将列表项的内部内容设为 Employee 类中的字符串。 如示例所示，可以为每个列表项中的按钮控件分配唯一自动化 ID（即员工 ID）。

```csharp
Employee[] employees = new Employee[]
{
   new Employee("john", "4384"),
   new Employee("margaret", "7556"),
   new Employee("richard", "8688"),
   new Employee("george", "1293")
};

listBox1.ItemsSource = employees;

public override string ToString()
{
    return EmployeeName + EmployeeID; // Unique Identification to be set as the AutomationProperties.Name
}
```

## <a name="use-a-control-template"></a>使用控件模板

可以使用控件模板，让代码中定义的每个特定类型实例获得唯一自动化属性。 创建模板，将 AutomationProperty 与控件实例的唯一 ID 绑定在一起。 下面的 XAML 展示了一种使用控件模板创建此类绑定的方法：

```xaml
<Style x:Key="MyButton" TargetType="Button">
<Setter Property="Template">
   <Setter.Value>
<ControlTemplate TargetType="Button">
   <Grid>
      <CheckBox HorizontalAlignment="Left" AutomationProperties.AutomationId="{TemplateBinding Content}"></CheckBox>
      <Button Width="90" HorizontalAlignment="Right" Content="{TemplateBinding Content}" AutomationProperties.AutomationId="{TemplateBinding Content}"></Button>
   </Grid>
</ControlTemplate>
   </Setter.Value>
</Setter>
</Style>
```

使用此控件模板定义一个按钮的两个实例时，自动化 ID 在模板中设为控件的唯一内容字符串，如下面的 XAML 所示：

```xaml
<Button Content="Button1" Style="{StaticResource MyButton}" Width="140"/>
<Button Content="Button2" Style="{StaticResource MyButton}" Width="140"/>
```

### <a name="dynamic-controls"></a>动态控件

如果控件是通过代码动态创建，而不是静态创建或通过 XAML 文件中的模板创建而成，必须为控件设置 Content 或 Name 属性。 此操作可确保每个动态控件都拥有唯一自动化属性。 例如，如果必须在用户选择列表项时显示复选框，可以设置这些属性，如下所示：

```csharp
private void CreateCheckBox(string txt, StackPanel panel)
{
   CheckBox cb = new CheckBox();
   cb.Content = txt; // Sets the AutomationProperties.Name
   cb.Height = 50;
   cb.Width = 100;
   cb.Name = "DynamicCheckBoxAid"+ txt; // Sets the AutomationProperties.AutomationId
   panel.Children.Add(cb);
}
```

## <a name="see-also"></a>请参阅

- [使用编码的 UI 测试来测试 UWP 应用](../test/test-uwp-app-with-coded-ui-test.md)

---
title: 使用 T4 文本模板的运行时文本生成
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- Preprocessed Text Template project item
- TextTemplatingFilePreprocessor custom tool
- text templates, TransformText() method
- text templates, generating files at run time
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 050af194c9fbdcabf99a880a0e9c5c4bf8913a3a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823937"
---
# <a name="run-time-text-generation-with-t4-text-templates"></a>使用 T4 文本模板的运行时文本生成

使用 Visual Studio 运行时文本模板，可以在运行时在应用程序中生成文本字符串。 执行应用程序的计算机无需安装 Visual Studio。 运行时模板有时被称为"预处理过的文本模板"，因为在编译时，该模板会生成在运行时执行的代码。

每个模板都将出现在生成的字符串和程序代码的片段的文本的混合。 程序片段的字符串的变量部分提供值，还可以控制条件和重复部分。

例如，可以创建一份 HTML 报告的应用程序中使用以下模板。

```html
<#@ template language="C#" #>
<html><body>
<h1>Sales for Previous Month</h2>
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
This report is Company Confidential.
</body></html>
```

请注意该模板是 HTML 页，在其中的变量部分已被替换为在程序代码。 您可以通过编写静态 HTML 页面的原型开始此类页面的设计。 然后可以使用程序代码到下从有一次生成各不相同的内容替换表和其他变量部分。

在应用程序可以使用模板是更轻松地查看输出的最终形式，比在一长串写语句。 对输出的窗体的更改是更容易且更可靠。

## <a name="creating-a-run-time-text-template-in-any-application"></a>在任何应用程序中创建运行时文本模板

### <a name="to-create-a-run-time-text-template"></a>若要创建运行时文本模板

1. 在解决方案资源管理器，在你的项目的快捷菜单上选择**外** > **新项**。

2. 在中**添加新项**对话框中，选择**运行时文本模板**。 (在 Visual Basic 中查找下**常见项** > **常规**。)

3. 键入你的模板文件的名称。

    > [!NOTE]
    > 模板文件的名称将用作生成的代码中的类名称。 因此，它不应具有空格或标点。

4. 选择“添加”。

    创建新文件扩展名 **.tt**。 其**自定义工具**属性设置为**TextTemplatingFilePreprocessor**。 它包含以下行：

    ```
    <#@ template language="C#" #>
    <#@ assembly name="System.Core" #>
    <#@ import namespace="System.Linq" #>
    <#@ import namespace="System.Text" #>
    <#@ import namespace="System.Collections.Generic" #>
    ```

## <a name="converting-an-existing-file-to-a-run-time-template"></a>将现有文件转换为运行时模板

创建模板的好办法是输出的将现有示例。 例如，如果你的应用程序将在生成 HTML 文件，您可以首先创建一个普通的 HTML 文件。 请确保其正常运行，并且其外观正确无误。 然后将其包含在 Visual Studio 项目并将其转换为模板。

### <a name="to-convert-an-existing-text-file-to-a-run-time-template"></a>若要将现有文本文件转换为运行时模板

1. 在 Visual Studio 项目中包括该文件。 在解决方案资源管理器，在项目的快捷菜单上选择**外** > **现有项**。

2. 设置文件的**自定义工具**属性设置为**TextTemplatingFilePreprocessor**。 在解决方案资源管理器，在该文件的快捷菜单上选择**属性**。

    > [!NOTE]
    > 如果已设置该属性，请确保它是**TextTemplatingFilePreprocessor**而不**TextTemplatingFileGenerator**。 如果已具有扩展名的文件包含在发生这种情况 **.tt**。

3. 更改到的文件扩展名 **.tt**。 尽管此步骤是可选的但它可帮助您避免在不适当的编辑器中打开该文件。

4. 从文件名称的主要部分中删除任何空格或标点。 例如，"我的 Web Page.tt"将是不正确，但是"MyWebPage.tt"是正确的。 文件名称将用作生成的代码中的类名称。

5. 在文件开头插入以下行。 如果您正在 Visual Basic 项目中，将为"C#"与"VB"。

    `<#@ template language="C#" #>`

## <a name="the-content-of-the-run-time-template"></a>运行时模板的内容

### <a name="template-directive"></a>模板指令

创建文件时，将保留该模板的第一行：

`<#@ template language="C#" #>`

语言参数将取决于你的项目的语言。

### <a name="plain-content"></a>纯文本内容

编辑 **.tt**文件以包含你希望应用程序生成的文本。 例如：

```html
<html><body>
<h1>Sales for January</h2>
<!-- table to be inserted here -->
This report is Company Confidential.
</body></html>
```

### <a name="embedded-program-code"></a>嵌入在程序代码

您可以插入程序代码之间`<#`和`#>`。 例如：

```csharp
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
```

```vb
<table>
<#
    For i As Integer = 1 To 10
#>
    <tr><td>Test name <#= i #> </td>
      <td>Test value <#= i*i #> </td></tr>
<#
    Next
#>
</table>
```

请注意之间插入语句`<# ... #>`之间插入表达式`<#= ... #>`。 有关详细信息，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

## <a name="using-the-template"></a>使用模板

### <a name="the-code-built-from-the-template"></a>从模板生成代码

在您保存 **.tt**文件，子公司 **.cs**或 **.vb**生成文件。 若要查看此文件中的**解决方案资源管理器**，展开 **.tt**文件节点。 在 Visual Basic 项目中，首先选择**显示所有文件**中**解决方案资源管理器**工具栏。

请注意附属文件包含分部类包含一个名为方法`TransformText()`。 可以从应用程序调用此方法。

### <a name="generating-text-at-run-time"></a>在运行时生成的文本

在应用程序代码中，您可以生成模板使用如下所示的内容：

```csharp
MyWebPage page = new MyWebPage();
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

```vb
Dim page = New My.Templates.MyWebPage
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

若要在特定的命名空间中放置生成的类，设置**自定义工具 Namespace**文本模板文件的属性。

### <a name="debugging-runtime-text-templates"></a>调试运行时文本模板

调试和测试运行时文本模板为普通代码相同的方式。

文本模板中，可以设置断点。 如果在从 Visual Studio 的调试模式下启动应用程序，可以单步执行代码并按常规方式计算监视表达式。

### <a name="passing-parameters-in-the-constructor"></a>在构造函数中传递参数

通常一个模板必须从应用程序的其他部分中导入一些数据。 若要使此简单，由模板生成的代码是一个分部类。 在项目中，可以在另一个文件中创建相同的类的另一个部分。 该文件可以包含带参数、 属性和由嵌入在模板中的代码以及由其他应用程序可以访问的函数的构造函数。

例如，可以创建一个单独的文件**MyWebPageCode.cs**:

```csharp
partial class MyWebPage
{
    private MyData m_data;
    public MyWebPage(MyData data) { this.m_data = data; }}
```

模板文件中**MyWebPage.tt**，可以编写：

```html
<h2>Sales figures</h2>
<table>
<# foreach (MyDataItem item in m_data.Items)
   // m_data is declared in MyWebPageCode.cs
   { #>
      <tr><td> <#= item.Name #> </td>
          <td> <#= item.Value #> </td></tr>
<# } // end of foreach
#>
</table>
```

若要在应用程序中使用此模板：

```csharp
MyData data = ...;
MyWebPage page = new MyWebPage(data);
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

#### <a name="constructor-parameters-in-visual-basic"></a>在 Visual Basic 中的构造函数参数

在 Visual Basic 中，单独的文件**MyWebPageCode.vb**包含：

```vb
Namespace My.Templates
  Partial Public Class MyWebPage
    Private m_data As MyData
    Public Sub New(ByVal data As MyData)
      m_data = data
    End Sub
  End Class
End Namespace
```

模板文件可能包含：

```html
<#@ template language="VB" #>
<html><body>
<h1>Sales for January</h2>
<table>
<#
    For Each item In m_data.Items
#>
    <tr><td>Test name <#= item.Name #> </td>
      <td>Test value <#= item.Value #> </td></tr>
<#
    Next
#>
</table>
This report is Company Confidential.
</body></html>
```

通过将参数传递的构造函数中调用模板可以：

```vb
Dim data = New My.Templates.MyData
    ' Add data values here ....
Dim page = New My.Templates.MyWebPage(data)
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

#### <a name="passing-data-in-template-properties"></a>在模板属性中传递数据

将数据传递到模板的替代方法是将公共属性添加到分部类定义中的模板类。 你的应用程序可以调用之前设置的属性`TransformText()`。

此外可以向模板类的分部定义中添加字段。 这使您可以连续执行模板之间传递数据。

### <a name="use-partial-classes-for-code"></a>使用代码的分部类

许多开发人员希望避免在模板中编写太多的代码。 相反，您可以为模板文件具有相同名称的分部类中定义方法。 从模板中调用这些方法。 在这种方式，模板显示更清楚地目标输出字符串将如下所示。 可以从创建它所显示的数据的逻辑分隔讨论结果的外观。

### <a name="assemblies-and-references"></a>程序集和引用

如果希望模板代码以引用.NET 或其他程序集，如**System.Xml.dll**，将其添加到项目的**引用**以通常的方式。

如果你想要为相同的方式导入命名空间`using`语句中，您可以执行此操作与`import`指令：

```
<#@ import namespace="System.Xml" #>
```

必须将这些指令放置在文件的开头处后立即`<#@template`指令。

### <a name="shared-content"></a>共享的内容

如果您有几个模板间共享的文本，可以将其放在单独的文件并将其包含在它应在其中显示每个文件：

```
<#@include file="CommonHeader.txt" #>
```

包含的内容可以包含的程序代码和纯文本的任意组合，它可以包含其他 include 指令和其他指令。

Include 指令可以任意位置使用文本模板文件或包含的文件中。

### <a name="inheritance-between-run-time-text-templates"></a>运行时文本模板之间的继承

可以共享运行时通过编写一个基本类模板，才能是抽象的模板之间的内容。 使用`inherits`参数的`<@#template#>`指令来引用另一个运行时模板类。

#### <a name="inheritance-pattern-fragments-in-base-methods"></a>继承模式：基方法中的片段

在下面的示例中使用的模式，请注意以下几点：

- 类的基类`SharedFragments`定义类功能块中的方法`<#+ ... #>`。

- 基类中包含任何自由文本。 相反，其文本块的所有出现在类功能方法。

- 在派生的类调用中定义的方法`SharedFragments`。

- 应用程序调用`TextTransform()`方法的派生类中，但不是转换类的基类`SharedFragments`。

- 基类和派生类是运行时文本模板;即**自定义工具**属性设置为**TextTemplatingFilePreprocessor**。

**SharedFragments.tt:**

```
<#@ template language="C#" #>
<#+
protected void SharedText(int n)
{
#>
   Shared Text <#= n #>
<#+
}
// Insert more methods here if required.
#>
```

**MyTextTemplate1.tt:**

```
<#@ template language="C#" inherits="SharedFragments" #>
begin 1
   <# SharedText(2); #>
end 1
```

**MyProgram.cs:**

```csharp
...
MyTextTemplate1 t1  = new MyTextTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**生成的输出：**

```
begin 1
    Shared Text 2
end 1
```

#### <a name="inheritance-pattern-text-in-base-body"></a>继承模式：基本的正文中的文本

使用模板继承此备用方法，在基模板中定义的文本的大容量。 派生的模板提供的数据和文本片段适合基本内容。

**AbstractBaseTemplate1.tt:**

```
<#@ template language="C#" #>

Here is the description for this derived template:
  <#= this.Description #>

Here is the fragment specific to this derived template:
<#
  this.PushIndent("  ");
  SpecificFragment(42);
  this.PopIndent();
#>
End of common template.
<#+
  // State set by derived class before calling TextTransform:
  protected string Description = "";
  // 'abstract' method to be defined in derived classes:
  protected virtual void SpecificFragment(int n) { }
#>
```

**DerivedTemplate1.tt:**

```
<#@ template language="C#" inherits="AbstractBaseTemplate1" #>
<#
  // Set the base template properties:
  base.Description = "Description for this derived class";

  // Run the base template:
  base.TransformText();

#>
End material for DerivedTemplate1.

<#+
// Provide a fragment specific to this derived template:

protected override void SpecificFragment(int n)
{
#>
   Specific to DerivedTemplate1 : <#= n #>
<#+
}
#>
```

**应用程序代码：**

```csharp
...
DerivedTemplate1 t1 = new DerivedTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**生成的输出：**

```
Here is the description for this derived template:
  Description for this derived class

Here is the fragment specific to this derived template:
     Specific to DerivedTemplate1 : 42
End of common template.
End material for DerivedTemplate1.
```

## <a name="related-topics"></a>相关主题

设计时模板：如果你想要使用模板生成代码，将成为你的应用程序的一部分，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

运行时模板可以使用任何应用程序中，在编译时确定的模板和其内容。 但是，如果你想要编写 Visual Studio 扩展插件从在运行时更改的模板生成文本，请参阅[VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

## <a name="see-also"></a>请参阅

- [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)
- [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)
- [T4 工具箱](http://olegsych.com/T4Toolbox/)

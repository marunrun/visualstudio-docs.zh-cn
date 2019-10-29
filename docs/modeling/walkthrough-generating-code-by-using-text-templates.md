---
title: 演练：使用文本模板生成代码
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [text templates], generating application code
- walkthroughs [text templates]
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d24a2ea1b614cb0ca82bdcf1c4954aba9a9174c
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984409"
---
# <a name="walkthrough-generate-code-by-using-text-templates"></a>演练：使用文本模板生成代码

代码生成允许生成强类型化的程序代码，但可在源模型更改时轻松对其进行更改。 与之相比，另一种编写可接受配置文件的完全泛型程序的替代技术更灵活，但生成的代码既不易读取和更改，也没有这么好的性能。 本演练将演示这一优势。

## <a name="typed-code-for-reading-xml"></a>读取 XML 的类型化代码

System.Xml 命名空间提供用于加载 XML 文档的综合工具，然后将其在内存中自由导航。 遗憾的是，所有节点都具有相同的类型 XmlNode。 因此，很容易引起编程错误，比如得到错误类型的子节点或错误属性。

在此示例项目中，模板读取示例 XML 文件，并生成对应于每种节点类型的类。 在手动编写的代码中，可以使用这些类来导航 XML 文件。 此外，还可以在使用相同节点类型的任何其他文件上运行应用程序。 示例 XML 文件的目的是提供想要应用程序处理的所有节点类型的示例。

> [!NOTE]
> Visual Studio 附带的应用程序[xsd.exe](/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe)可以从 XML 文件生成强类型的类。 此处显示的模板作为示例提供。

下面是示例文件：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<catalog>
  <artist id ="Mike%20Nash" name="Mike Nash Quartet">
    <song id ="MikeNashJazzBeforeTeatime">Jazz Before Teatime</song>
    <song id ="MikeNashJazzAfterBreakfast">Jazz After Breakfast</song>
  </artist>
  <artist id ="Euan%20Garden" name="Euan Garden">
    <song id ="GardenScottishCountry">Scottish Country Garden</song>
  </artist>
</catalog>
```

在本演练构造的项目中，可以编写类似于下面的代码，键入时 IntelliSense 会提示正确的属性和子名称：

```csharp
Catalog catalog = new Catalog(xmlDocument);
foreach (Artist artist in catalog.Artist)
{
  Console.WriteLine(artist.name);
  foreach (Song song in artist.Song)
  {
    Console.WriteLine("   " + song.Text);
  }
}
```

将其与可能未使用模板编写的非类型化代码相比：

```csharp
XmlNode catalog = xmlDocument.SelectSingleNode("catalog");
foreach (XmlNode artist in catalog.SelectNodes("artist"))
{
    Console.WriteLine(artist.Attributes["name"].Value);
    foreach (XmlNode song in artist.SelectNodes("song"))
    {
         Console.WriteLine("   " + song.InnerText);
     }
}
```

在强类型的版本中，对 XML 架构的更改将导致类的更改。 编译器将突出显示应用程序代码中必须更改的部分。 在使用泛型 XML 代码的非类型化版本中，没有此类支持。

在此项目中，使用单个模板文件生成使类型化版本成为可能的类。

## <a name="set-up-the-project"></a>设置项目

### <a name="create-or-open-a-c-project"></a>创建或打开 C# 项目

可以将此技术应用于任何代码项目。 本演练使用 C# 项目，出于测试目的，我们使用控制台应用程序。

1. 在“文件” 菜单上，单击“新建” ，然后单击“项目”。

2. 单击“” 节点，然后在“模板” 窗格中，单击“控制台应用程序”

### <a name="add-a-prototype-xml-file-to-the-project"></a>将原型 XML 文件添加到项目

此文件的目的是提供想要应用程序能够读取的 XML 节点类型的示例。 可以是一个将用于测试应用程序的文件。 模板将为此文件中的每种节点类型生成 C# 类。

该文件应为项目的一部分，以便模板进行读取，但不会将其内置于已编译的应用程序中。

1. 在“解决方案资源管理器”中，右键单击项目，单击“添加” ，然后单击“新项”。

2. 在“添加新项” 对话框，从“模板” 窗格选择“XML 文件” 。

3. 将示例内容添加到该文件。

4. 本演练中，命名文件 `exampleXml.xml`。 将文件的内容设置为上一节中所示的 XML。

### <a name="add-a-test-code-file"></a>添加测试代码文件

将 C# 文件添加到项目，并在其中编写希望能够进行编写的代码示例。 例如:

```csharp
using System;
namespace MyProject
{
  class CodeGeneratorTest
  {
    public void TestMethod()
    {
      Catalog catalog = new Catalog(@"..\..\exampleXml.xml");
      foreach (Artist artist in catalog.Artist)
      {
        Console.WriteLine(artist.name);
        foreach (Song song in artist.Song)
        {
          Console.WriteLine("   " + song.Text);
} } } } }
```

在此阶段，此代码将无法进行编译。 编写模板时，将生成使代码成功编译的类。

更全面的测试将针对示例 XML 文件的已知内容检查此测试函数的输出。 但在本演练中，如果该测试方法能够编译，我们将视为成功。

### <a name="add-a-text-template-file"></a>添加模板文件

添加文本模板文件，并将输出扩展名设置为 *.cs*。

1. 在“解决方案资源管理器”中，右键单击项目，单击“添加”，然后单击“新项”。

2. 在“添加新项” 对话框中，从“模板” 窗格选择“文本模板” 。

    > [!NOTE]
    > 确保添加的是文本模板，而不是预处理文本模板。

3. 在文件的模板指令中，将 `hostspecific` 属性更改为 `true`。

     此更改将使模板代码获得对 Visual Studio 服务的访问权限。

4. 在输出指令中，将扩展属性更改为“.cs”，使该模板生成 C# 文件。 在 Visual Basic 项目中，将其更改为“.vb”。

5. 保存该文件。 在此阶段，文本模板文件应包含这些行：

    ```
    <#@ template debug="false" hostspecific="true" language="C#" #>
    <#@ output extension=".cs" #>
    ```

请注意，.cs 文件在解决方案资源管理器中显示为模板文件的附属文件。 可单击模板文件名称旁边的 [+] 进行查看。 只要保存或将焦点从模板文件移开，就会从模板文件生成此文件。 所生成的文件将编译为项目的一部分。

为方便起见，开发模板文件时，请排列模板文件和所生成文件的窗口，使它们彼此相邻。 这样就可以立即看到模板的输出。 你还会注意到，模板生成无效的 C# 代码时，将在错误消息窗口显示错误。

只要保存模板文件，就会丢失任何直接在所生成文件中执行的编辑。 因此，应避免编辑生成的文件，或仅为短期实验编辑它。 在 IntelliSense 正在运行的生成文件中，尝试编辑小段代码有时很有用，然后将其复制到模板文件。

## <a name="develop-the-text-template"></a>开发文本模板

我们将遵照有关敏捷开发的最佳建议，逐步开发模板，清除每个增量中的某些错误，直至测试代码能够正常编译和运行。

### <a name="prototype-the-code-to-be-generated"></a>原型化要生成的代码

测试代码需要文件中每个节点的类。 因此，如果将这些行追加到模板中，然后保存，某些编译错误将会消失：

```csharp
class Catalog {}
class Artist {}
class Song {}
```

这有助于了解需要执行的操作，但应从示例 XML 文件中的节点类型生成声明。 从模板中删除这些实验行。

### <a name="generate-application-code-from-the-model-xml-file"></a>从模型 XML 文件生成应用程序代码

若要读取 XML 文件并生成类声明，用以下模板代码替换模板内容：

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml"#>
<#@ import namespace="System.Xml" #>
<#
 XmlDocument doc = new XmlDocument();
 // Replace this file path with yours:
 doc.Load(@"C:\MySolution\MyProject\exampleXml.xml");
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
#>
  public partial class <#= node.Name #> {}
<#
 }
#>
```

用项目的正确路径替换文件路径。

请注意代码块分隔符 `<#...#>`。 这些分隔符将生成文本的程序代码片段括起来。 表达式块分隔符 `<#=...#>` 会将可对字符串进行评估的表达式括起来。

编写为应用程序生成源代码的模板时，需要处理两个单独的程序文本。 在保存模板或将焦点移到另一个窗口时，该代码块分隔符内的程序将会运行。 将它所生成的文本（显示在分隔符外）复制到生成的文件，并成为应用程序代码的一部分。

`<#@assembly#>` 指令的行为类似于引用，使程序集可供模板代码使用。 通过模板看到的程序集列表独立于应用程序项目中的引用列表。

`<#@import#>` 指令的行为类似于 `using` 语句，允许在导入的命名空间中使用类的短名称。

遗憾的是，虽然此模板生成代码，但是在示例 XML 文件中，它会为每个节点生成类声明，因此如果存在几个 `<song>` 节点的实例，将会出现几个类 song 的声明。

### <a name="read-the-model-file-then-generate-the-code"></a>读取模型文件，然后生成代码

许多文本模板遵循这样一种模式，其中模板的第一部分读取源文件，第二部分生成模板。 需要读取所有示例文件以汇总所包含的节点类型，然后生成类声明。 需要另一个 `<#@import#>` 才可使用 `Dictionary<>:`

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml"#>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.Collections.Generic" #>
<#
 // Read the model file
 XmlDocument doc = new XmlDocument();
 doc.Load(@"C:\MySolution\MyProject\exampleXml.xml");
 Dictionary <string, string> nodeTypes =
        new Dictionary<string, string>();
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
   nodeTypes[node.Name] = "";
 }
 // Generate the code
 foreach (string nodeName in nodeTypes.Keys)
 {
#>
  public partial class <#= nodeName #> {}
<#
 }
#>
```

### <a name="add-an-auxiliary-method"></a>添加辅助方法

类功能控制块是一个可以在其中定义辅助方法的块。 采用 `<#+...#>` 分隔块，并且在文件中它必须显示为最后一个块。

如果更愿意类名称以大写字母开头，可以将该模板的最后部分替换为以下模板代码：

```
// Generate the code
 foreach (string nodeName in nodeTypes.Keys)
 {
#>
  public partial class <#= UpperInitial(nodeName) #> {}
<#
 }
#>
<#+
 private string UpperInitial(string name)
 { return name[0].ToString().ToUpperInvariant() + name.Substring(1); }
#>
```

在此阶段，生成的 *.cs*文件包含以下声明：

```csharp
public partial class Catalog {}
public partial class Artist {}
public partial class Song {}
```

可以使用相同的方法添加更多详细信息，例如子节点的属性、特性和内部文本。

### <a name="access-the-visual-studio-api"></a>访问 Visual Studio API

设置 `<#@template#>` 指令的 `hostspecific` 属性允许模板获取对 Visual Studio API 的访问权限。 模板可通过该步骤获取项目文件的位置，避免在模板代码中使用绝对文件路径。

```
<#@ template debug="false" hostspecific="true" language="C#" #>
...
<#@ assembly name="EnvDTE" #>
...
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
// Open the prototype document.
XmlDocument doc = new XmlDocument();
doc.Load(System.IO.Path.Combine(dte.ActiveDocument.Path, "exampleXml.xml"));
```

## <a name="complete-the-text-template"></a>完成文本模板

以下模板内容生成使测试代码可以编译并运行的代码。

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.Collections.Generic" #>
using System;using System.Collections.Generic;using System.Linq;using System.Xml;namespace MyProject{
<#
 // Map node name --> child name --> child node type
 Dictionary<string, Dictionary<string, XmlNodeType>> nodeTypes = new Dictionary<string, Dictionary<string, XmlNodeType>>();

 // The Visual Studio host, to get the local file path.
 EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
 // Open the prototype document.
 XmlDocument doc = new XmlDocument();
 doc.Load(System.IO.Path.Combine(dte.ActiveDocument.Path, "exampleXml.xml"));
 // Inspect all the nodes in the document.
 // The example might contain many nodes of the same type,
 // so make a dictionary of node types and their children.
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
   Dictionary<string, XmlNodeType> subs = null;
   if (!nodeTypes.TryGetValue(node.Name, out subs))
   {
     subs = new Dictionary<string, XmlNodeType>();
     nodeTypes.Add(node.Name, subs);
   }
   foreach (XmlNode child in node.ChildNodes)
   {
     subs[child.Name] = child.NodeType;
   }
   foreach (XmlNode child in node.Attributes)
   {
     subs[child.Name] = child.NodeType;
   }
 }
 // Generate a class for each node type.
 foreach (string className in nodeTypes.Keys)
 {
    // Capitalize the first character of the name.
#>
    partial class <#= UpperInitial(className) #>
    {      private XmlNode thisNode;      public <#= UpperInitial(className) #>(XmlNode node)       { thisNode = node; }

<#
    // Generate a property for each child.
    foreach (string childName in nodeTypes[className].Keys)
    {
      // Allow for different types of child.
      switch (nodeTypes[className][childName])
      {
         // Child nodes:
         case XmlNodeType.Element:
#>
      public IEnumerable<<#=UpperInitial(childName)#>><#=UpperInitial(childName) #>      {         get         {            foreach (XmlNode node in                thisNode.SelectNodes("<#=childName#>"))              yield return new <#=UpperInitial(childName)#>(node);       } }
<#
         break;
         // Child attributes:
         case XmlNodeType.Attribute:
#>
      public string <#=childName #>      { get { return thisNode.Attributes["<#=childName#>"].Value; } }
<#
         break;
         // Plain text:
         case XmlNodeType.Text:
#>
      public string Text  { get { return thisNode.InnerText; } }
<#
         break;
       } // switch
     } // foreach class child
  // End of the generated class:
#>
   }
<#
 } // foreach class

   // Add a constructor for the root class
   // that accepts an XML filename.
   string rootClassName = doc.SelectSingleNode("*").Name;
#>
   partial class <#= UpperInitial(rootClassName) #>   {      public <#= UpperInitial(rootClassName) #>(string fileName){        XmlDocument doc = new XmlDocument();        doc.Load(fileName);        thisNode = doc.SelectSingleNode("<#=rootClassName#>");}   }}
<#+
   private string UpperInitial(string name)
   {
      return name[0].ToString().ToUpperInvariant() + name.Substring(1);
   }
#>
```

### <a name="run-the-test-program"></a>运行测试程序

在控制台应用程序的主要部分中，以下几行将执行测试方法。 按 F5，在调试模式下运行程序：

```csharp
using System;
namespace MyProject
{
  class Program
  {
    static void Main(string[] args)
    {
      new CodeGeneratorTest().TestMethod();
      // Allow user to see the output:
      Console.ReadLine();
    }
  }
}
```

### <a name="write-and-update-the-application"></a>编写和更新应用程序

现可以使用生成的类而不是泛型 XML 代码来编写强类型样式的应用程序。

更改 XML 架构时，可轻松地生成新的类。 编译器将告知开发人员必须更新应用程序代码的位置。

若要在示例 XML 文件更改时重新生成类，请单击 "**解决方案资源管理器**" 工具栏中的 "**转换所有模板**"。

## <a name="conclusion"></a>结束语

本演练演示了代码生成的几种方法及其优势：

- *代码生成* 是指从 *模型*创建应用程序的部分源代码。 模型包含以适合应用程序域的方式呈现的信息，并可能在应用程序的生存期内发生更改。

- 强类型化是代码生成的一个优点。 模型以更适合用户的方式呈现信息，而生成的代码允许应用程序的其他部分能够使用一组类型来处理信息。

- 在编写新代码和更新架构时，IntelliSense 和编译器都有助于创建符合模型架构的代码。

- 将单个简单模板文件添加到项目可提供这些优势。

- 可以增量式地快速开发和测试文本模板。

在本演练中，程序代码实际上是从模型实例中生成的，该实例是应用程序会处理的一个典型 XML 文件示例。 在更正规的方法中，XML 架构将以 .xsd 文件或域特定语言定义的形式成为模板的输入。 这种方法将使模板在确定特征（如关系的多重性）方面更轻松。

## <a name="troubleshoot-the-text-template"></a>排查文本模板问题

若在“错误列表”中看到模板转换或编译错误，或者若未正确生成输出文件，可以借助[使用 TextTransform 实用工具生成文件](../modeling/generating-files-with-the-texttransform-utility.md)中所述的技术解决文本模板的问题。

## <a name="see-also"></a>请参阅

- [使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)
- [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)
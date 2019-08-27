---
title: MSBuild 内联任务 | Microsoft Docs
ms.date: 09/21/2017
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tasks
ms.assetid: e72e6506-4a11-4edf-ae8d-cfb5a3b9d8a0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 37597d1e1f4fde2b2e81e7aa7868c0aaff935337
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68416852"
---
# <a name="msbuild-inline-tasks"></a>MSBuild 内联任务
通常，MSBuild 任务通过编译实现 <xref:Microsoft.Build.Framework.ITask> 接口的类进行创建。 有关详细信息，请参阅[任务](../msbuild/msbuild-tasks.md)。

 从 .NET Framework 版本 4 开始，你可以在项目文件中创建内联任务。 无需创建单独的程序集来承载该任务。 这使得更易于跟踪源代码和部署任务。 源代码将集成到脚本中。

 在 MSBuild 15.8 中，添加了可创建 .NET Standard 跨平台内联任务的 [RoslynCodeTaskFactory](../msbuild/msbuild-roslyncodetaskfactory.md)。  如果需要在 .NET Core 上使用内联任务，则必须使用 RoslynCodeTaskFactory。
## <a name="the-structure-of-an-inline-task"></a>内联任务的结构
 内联任务由 [UsingTask](../msbuild/usingtask-element-msbuild.md) 元素包含。 内联任务和包含它的 `UsingTask` 元素通常包括在 .targets 文件中，并根据需要导入到其他项目文件  。 下面是一个基本的内联任务。 请注意，它不执行任何操作。

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <!-- This simple inline task does nothing. -->
  <UsingTask
    TaskName="DoNothing"
    TaskFactory="CodeTaskFactory"
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll" >
    <ParameterGroup />
    <Task>
      <Reference Include="" />
      <Using Namespace="" />
      <Code Type="Fragment" Language="cs">
      </Code>
    </Task>
  </UsingTask>
</Project>
```

 示例中的 `UsingTask` 元素具有三个属性，用于描述任务和编译该任务的内联任务工厂。

- `TaskName` 属性命名任务，在本例中，即为 `DoNothing`。

- `TaskFactory` 属性命名实现内联任务工厂的类。

- `AssemblyFile` 属性提供内联任务工厂的位置。 或者，可以使用 `AssemblyName` 属性来指定内联任务工厂类的完全限定的名称，它通常位于全局程序集缓存 (GAC) 中。

`DoNothing` 任务的其余元素为空，用于说明内联任务的顺序和结构。 本主题后面部分将提供更为全面的示例。

- `ParameterGroup` 元素是可选的。 如果指定，它会声明任务的参数。 有关输入和输出参数的详细信息，请参阅本主题后面的[输入和输出参数](#input-and-output-parameters)。

- `Task` 元素描述且包含任务源代码。

- `Reference` 元素指定对在代码中使用的 .NET 程序集的引用。 这相当于在 Visual Studio 中添加对项目的引用。 `Include` 属性指定引用的程序集的路径。

- `Using` 元素列出你想要访问的命名空间。 这类似于 Visual C# 中的 `Using` 语句。 `Namespace` 属性指定要包含的命名空间。

`Reference` 和 `Using` 元素都与语言无关。 可以用任何一种受支持的 .NET CodeDom 语言（例如，Visual Basic 或 Visual C#）编写内联任务。

> [!NOTE]
> 由 `Task` 元素包含的元素均特定于任务工厂，在本例中，即代码任务工厂。

### <a name="code-element"></a>代码元素
 最后一个出现在 `Task`元素内的子元素是 `Code` 元素。 `Code` 元素包含或定位你想要编译到任务中的代码。 放置于 `Code` 元素中的内容具体取决于你希望如何编写任务。

 `Language` 属性指定编写代码的语言。 可接受的值为 `cs`（对于 C#）或 `vb`（对于 Visual Basic）。

 `Type` 属性指定 `Code` 元素中找到的代码类型。

- 如果 `Type` 的值为 `Class`，则 `Code` 元素将包含派生自 <xref:Microsoft.Build.Framework.ITask> 接口的类的代码。

- 如果 `Type` 的值为 `Method`，则代码将定义 <xref:Microsoft.Build.Framework.ITask> 接口的 `Execute` 方法的替代。

- 如果 `Type` 的值为 `Fragment`，则代码将定义 `Execute` 方法的内容，但不定义签名和 `return` 语句。

通常，该代码本身会出现在 `<![CDATA[` 标记和 `]]>` 标记之间。 由于代码位于 CDATA 部分中，因此你不必担心转义保留字符（例如，“\<”或“>”）。

或者，可以使用 `Code` 元素的 `Source` 属性来指定包含任务代码的文件的位置。 源文件中的代码的类型必须为由 `Type` 属性所指定的类型。 如果存在 `Source` 属性，则 `Type` 的默认值为 `Class`。 如果 `Source` 不存在，则默认值为 `Fragment`。

> [!NOTE]
> 当在源文件中定义任务类时，类名必须符合对应的 [UsingTask](../msbuild/usingtask-element-msbuild.md) 元素的 `TaskName` 属性。

## <a name="helloworld"></a>HelloWorld
 下面是一个更全面的内联任务。 HelloWorld 任务 在默认错误日志记录设备上显示“Hello, World!”，该设备通常为系统控制台或 Visual Studio **输出**窗口。 示例中包含了 `Reference` 元素，这仅用于阐释目的。

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <!-- This simple inline task displays "Hello, world!" -->
  <UsingTask
    TaskName="HelloWorld"
    TaskFactory="CodeTaskFactory"
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll" >
    <ParameterGroup />
    <Task>
      <Reference Include="System.Xml"/>
      <Using Namespace="System"/>
      <Using Namespace="System.IO"/>
      <Code Type="Fragment" Language="cs">
<![CDATA[
// Display "Hello, world!"
Log.LogError("Hello, world!");
]]>
      </Code>
    </Task>
  </UsingTask>
</Project>
```

 可以将 HelloWorld 任务保存在名为 HelloWorld.targets 的文件中，然后按照如下所示从项目中调用它  。

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="HelloWorld.targets" />
  <Target Name="Hello">
    <HelloWorld />
  </Target>
</Project>
```

## <a name="input-and-output-parameters"></a>输入和输出参数
 内联任务参数是 `ParameterGroup` 元素的子元素。 每个参数将定义它的元素的名称作为其名称。 以下代码定义参数 `Text`。

```xml
<ParameterGroup>
  <Text />
</ParameterGroup>
```

 参数可能有以下一个或多个属性：

- `Required` 是可选属性，默认值为 `false`。 如果为 `true`，则该参数是必需的，且必须在调用任务之前为其赋予值。

- `ParameterType` 是可选属性，默认值为 `System.String`。 可以将它设置为任何完全限定的类型（项或值），通过使用 System.Convert.ChangeType，可将其转换为字符串或从字符串转换为完全限定的类型。 （换言之，可传递至外部任务或可从外部任务传递的任何类型。）

- `Output` 是可选属性，默认值为 `false`。 如果为 `true`，则必须先为该参数赋予值，然后才能通过 Execute 方法返回。

例如，应用于对象的

```xml
<ParameterGroup>
  <Expression Required="true" />
  <Files ParameterType="Microsoft.Build.Framework.ITaskItem[]" Required="true" />
  <Tally ParameterType="System.Int32" Output="true" />
</ParameterGroup>
```

定义以下三个参数：

- `Expression` 为必需的输入参数，其类型为 System.String。

- `Files` 是必需的项列表输入参数。

- `Tally` 是输出参数，其类型为 System.Int32。

如果 `Code` 元素具有 `Fragment` 或 `Method` 的 `Type` 特性，则将自动为每个参数创建属性。 否则，属性必须在源代码中显示声明，并且必须与其参数定义完全匹配。

## <a name="example"></a>示例
 以下内联任务将给定文件中令牌的每个匹配项替换为给定的值。

```xml
<Project xmlns='http://schemas.microsoft.com/developer/msbuild/2003' ToolsVersion="15.0">

  <UsingTask TaskName="TokenReplace" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll">
    <ParameterGroup>
      <Path ParameterType="System.String" Required="true" />
      <Token ParameterType="System.String" Required="true" />
      <Replacement ParameterType="System.String" Required="true" />
    </ParameterGroup>
    <Task>
      <Code Type="Fragment" Language="cs"><![CDATA[
string content = File.ReadAllText(Path);
content = content.Replace(Token, Replacement);
File.WriteAllText(Path, content);

]]></Code>
    </Task>
  </UsingTask>

  <Target Name='Demo' >
    <TokenReplace Path="C:\Project\Target.config" Token="$MyToken$" Replacement="MyValue"/>
  </Target>
</Project>
```

## <a name="see-also"></a>请参阅
- [任务](../msbuild/msbuild-tasks.md)
- [演练：创建内联任务](../msbuild/walkthrough-creating-an-inline-task.md)

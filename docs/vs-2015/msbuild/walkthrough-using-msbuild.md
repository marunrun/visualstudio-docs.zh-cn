---
title: 演练：使用 MSBuild | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tutorial
ms.assetid: b8a8b866-bb07-4abf-b9ec-0b40d281c310
caps.latest.revision: 34
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b6e77934f8e565800eb4a7a753df4beb3b003fbb
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445590"
---
# <a name="walkthrough-using-msbuild"></a>演练：使用 MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild 是 Microsoft 和 Visual Studio 的生成平台。 本演练介绍 MSBuild 的构建基块，并演示如何编写、操作和调试 MSBuild 项目。 学习内容：  
  
- 创建和操作的项目文件。  
  
- 如何使用生成属性  
  
- 如何使用生成项。  
  
  可从 Visual Studio 或命令窗口运行 MSBuild。 本演练将使用 Visual Studio 创建 MSBuild 项目文件。 可在 Visual Studio 中编辑项目文件，并使用命令窗口生成项目并检查结果。  
  
## <a name="creating-an-msbuild-project"></a>创建 MSBuild 项目  
 Visual Studio 项目系统以 MSBuild 为基础。 因此可使用 Visual Studio 轻松创建新项目文件。 本部分将创建 Visual C# 项目文件。 可选择改为创建 Visual Basic 项目文件。 在本演练的上下文中，两种项目文件的差异很小。  
  
#### <a name="to-create-a-project-file"></a>创建项目文件  
  
1. 打开 Visual Studio。  
  
2. 在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
3. 在“新建项目”对话框中，选择 Visual C# 项目类型，然后选择“Windows 窗体应用程序”模板。 在“名称”框中键入 `BuildApp`。 输入解决方案的“位置”，例如 `D:\`。 接受“创建解决方案目录”（已选）、“添加到源代码管理”（未选）和“解决方案名称”(`BuildApp`) 的默认值。  
  
     单击“确定”创建项目文件。  
  
## <a name="examining-the-project-file"></a>检查项目文件  
 上一节中使用 Visual Studio 创建了一个 Visual C# 项目文件。 该项目文件在**解决方案资源管理器**中由名为 BuildApp 的项目节点表示。 可使用 Visual Studio 代码编辑器来检查项目文件。  
  
#### <a name="to-examine-the-project-file"></a>检查项目文件  
  
1. 在**解决方案资源管理器中**，单击项目节点 BuildApp。  
  
2. 请注意，在“属性”浏览器中，**项目文件**属性是 BuildApp.csproj。 所有项目文件名称中都带有后缀“proj”。 如果创建了 Visual Basic 项目，则项目文件名称将为 BuildApp.vbproj。  
  
3. 右键单击项目节点，然后单击“卸载项目”。  
  
4. 再次右键单击项目节点，然后单击“编辑 BuildApp.csproj”。  
  
     该项目文件出现在代码编辑器中。  
  
## <a name="targets-and-tasks"></a>目标和任务  
 项目文件是 XML 格式的文件，带有根节点[项目](../msbuild/project-element-msbuild.md)。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<Project ToolsVersion="12.0" DefaultTargets="Build"  xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
```  
  
 必须在 Project 元素中指定 xmlns 命名空间。  
  
 生成应用程序的工作由 [Target](../msbuild/target-element-msbuild.md) 和 [Task](../msbuild/task-element-msbuild.md) 元素完成。  
  
- 任务是工作的最小单位，换言之，它是生成的“原子”。 任务是可单独执行的组件，具有输入和输出。 目前尚没有在项目文件中引用或定义的任务。 以下各部分介绍如何将项目添加到项目文件。 有关详细信息，请参阅[任务](../msbuild/msbuild-tasks.md)主题。  
  
- 目标是任务的已命名序列。 有两个目标，请参阅项目文件的末尾，它们目前包含在 HTML 注释中：BeforeBuild 和 AfterBuild。  
  
  ```  
  <Target Name="BeforeBuild">  
  </Target>  
  <Target Name="AfterBuild">  
  </Target>  
  ```  
  
   有关详细信息，请参阅[目标](../msbuild/msbuild-targets.md)主题。  
  
  项目节点具有可选的 DefaultTargets 属性，用于选择要在此例生成中生成的默认目标。  
  
```  
<Project ToolsVersion="12.0" DefaultTargets="Build" ...  
```  
  
 该生成目标不是在项目文件中定义的。 而是通过 [Import](../msbuild/import-element-msbuild.md) 元素从文件 Microsoft.CSharp.targets 导入的。  
  
```  
<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />  
```  
  
 无论是否使用导入的文件，都会将其有效插入项目文件。  
  
 MSBuild 跟踪生成的目标，并保证每个目标生成次数不超过一次。  
  
## <a name="adding-a-target-and-a-task"></a>添加目标和任务  
 将目标添加到项目文件。 将任务添加到打印出消息的目标。  
  
#### <a name="to-add-a-target-and-a-task"></a>添加目标和任务  
  
1. 将这些行添加到项目文件中，添加到 Import 语句之后：  
  
   ```  
   <Target Name="HelloWorld">  
   </Target>  
   ```  
  
    这将创建名为 HelloWorld 的目标。 请注意，编辑项目文件时会拥有 Intellisense 支持。  
  
2. 将行添加到 HelloWorld 目标，以便生成如下所示的结果：  
  
   ```  
   <Target Name="HelloWorld">  
     <Message Text="Hello"></Message>  <Message Text="World"></Message>  
   </Target>  
   ```  
  
3. 保存项目文件。  
  
   Message 任务是 MSBuild 所附带的许多任务之一。 若要了解可用任务的完整列表以及用法信息，请参阅[任务参考](../msbuild/msbuild-task-reference.md)。  
  
   Message 任务将文本属性的字符串值作为输入并显示在输出设备上。 HelloWorld 目标执行 Message 任务两次：第一次显示“Hello”，第二次显示“World”。  
  
## <a name="building-the-target"></a>生成目标  
 从 **Visual Studio 命令提示符**运行 MSBuild，生成上面定义的 HelloWorld 目标。 使用 /Target 或 /t 命令行开关选择该目标。  
  
> [!NOTE]
> 以下各部分将 **Visual Studio 命令提示符**称为**命令窗口**。  
  
#### <a name="to-build-the-target"></a>生成目标  
  
1. 单击“启动”，然后单击“所有程序”。 在 **Visual Studio Tools** 文件夹中找到并单击“Visual Studio 命令提示符”。  
  
2. 从命令窗口导航到包含项目文件的文件夹，此例中为 D:\BuildApp\BuildApp。  
  
3. 使用命令开关 /t:HelloWorld 运行 MSBuild。 这将选择并生成 HelloWorld 目标：  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
4. 在“命令窗口”检查输出。 应看到两行“Hello”和“World”：  
  
    ```  
    Hello  
    World  
    ```  
  
> [!NOTE]
> 如果出现的是 `The target "HelloWorld" does not exist in the project`，则可能是忘记将项目文件保存到代码编辑器中。 请保存文件并重试。  
  
 通过在代码编辑器和命令窗口之间进行交替，可更改项目文件并快速查看结果。  
  
> [!NOTE]
> 如果运行不带 /t 命令开关的 MSBuild，MSBuild 将生成由 Project 元素（在本例中为“Build”）的 DefaultTarget 属性给定的目标。 此操作生成 Windows 窗体应用程序 BuildApp.exe。  
  
## <a name="build-properties"></a>生成属性  
 生成属性是引导生成的名称/值对。 已在项目文件顶部定义了几个生成属性：  
  
```  
<PropertyGroup>  
...  
  <ProductVersion>10.0.11107</ProductVersion>  
  <SchemaVersion>2.0</SchemaVersion>  
  <ProjectGuid>{30E3C9D5-FD86-4691-A331-80EA5BA7E571}</ProjectGuid>  
  <OutputType>WinExe</OutputType>  
...  
</PropertyGroup>  
```  
  
 所有属性都是 PropertyGroup 元素的子元素。 属性的名称是子元素的名称，属性的值是子元素的文本元素。 例如，应用于对象的  
  
```  
<TargetFrameworkVersion>v12.0</TargetFrameworkVersion>  
```  
  
 定义名为 TargetFrameworkVersion 的属性，并为其指定字符串值“v12.0”。  
  
 可能会随时重新定义生成属性。 如果  
  
```  
<TargetFrameworkVersion>v3.5</TargetFrameworkVersion>  
```  
  
 稍后出现在项目文件中，或稍后出现在项目文件中的导入文件中，则 TargetFrameworkVersion 会采用新值“v3.5”。  
  
## <a name="examining-a-property-value"></a>检查属性值  
 若要获取属性值，请使用以下语法，其中 PropertyName 是属性的名称：  
  
```  
$(PropertyName)  
```  
  
 使用此语法可检查项目文件中的一些属性。  
  
#### <a name="to-examine-a-property-value"></a>检查属性值  
  
1. 从代码编辑器中使用以下代码替换 HelloWorld 目标：  
  
    ```  
    <Target Name="HelloWorld">  
      <Message Text="Configuration is $(Configuration)" />  
      <Message Text="MSBuildToolsPath is $(MSBuildToolsPath)" />  
    </Target>  
    ```  
  
2. 保存项目文件。  
  
3. 在“命令窗口”输入并执行此行：  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
4. 检查输出。 应看到这两行（.NET Framework 版本可能不同）：  
  
    ```  
    Configuration is Debug  
    MSBuildToolsPath is C:\Program Files\MSBuild\12.0\bin  
    ```  
  
> [!NOTE]
> 如果未看到这两行，则可能是忘记将项目文件保存到代码编辑器中。 请保存文件并重试。  
  
### <a name="conditional-properties"></a>条件属性  
 许多属性（如配置）都是按条件进行定义的，也就是说，条件属性出现在 property 元素中。 仅当条件评估结果为“true”时才定义或重新定义条件属性。 请注意，会向未定义的属性给定空字符串的默认值。 例如，应用于对象的  
  
```  
<Configuration   Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
```  
  
 表示“如果尚未定义配置属性，请定义该属性并为其指定‘Debug’值”。  
  
 几乎所有 MSBuild 元素都可以具有条件属性。 有关使用条件属性的详细讨论，请参阅[条件](../msbuild/msbuild-conditions.md)。  
  
### <a name="reserved-properties"></a>保留属性  
 MSBuild 保留了一些属性名称，用于存储有关项目文件和 MSBuild 二进制文件的信息。 MSBuildToolsPath 就是保留属性的一个示例。 与其他属性一样，可使用 $ 符号引用保留属性。 有关详细信息，请参阅[如何：引用的名称或项目文件的位置](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md)并[MSBuild 保留属性和已知属性](../msbuild/msbuild-reserved-and-well-known-properties.md)。  
  
### <a name="environment-variables"></a>环境变量  
 可使用与生成属性相同的方式引用项目文件中的环境变量。 例如，若要使用项目文件中的 PATH 环境变量，可使用 $(Path)。 如果项目包含与环境变量具有相同名称的属性定义，则项目中的属性将替代环境变量的值。 有关详细信息，请参阅[如何：在生成中使用环境变量](../msbuild/how-to-use-environment-variables-in-a-build.md)。  
  
## <a name="setting-properties-from-the-command-line"></a>从命令行设置属性  
 可使用 /property 或 /p 命令行开关在命令行上定义属性。 从命令行接收的属性值将替代在项目文件和环境变量中设置的属性值。  
  
#### <a name="to-set-a-property-value-from-the-command-line"></a>在命令行中设置属性值  
  
1. 在“命令窗口”输入并执行此行：  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld /p:Configuration=Release  
   ```  
  
2. 检查输出。 应看到此行：  
  
   ```  
   Configuration is Release.  
   ```  
  
   MSBuild 创建配置属性并赋予其“发布”值。  
  
## <a name="special-characters"></a>特殊字符  
 某些字符在 MSBuild 项目文件中具有特殊意义。 这些字符的示例包括分号 (;) 和星号 (*)。 若要将这些特殊字符用作项目文件中的文本，必须使用语法 %xx 对它们进行指定，其中 xx 表示字符的 ASCII 十六进制值。  
  
 更改 Message 任务以显示具有特殊字符的配置属性的值，使其更易读。  
  
#### <a name="to-use-special-characters-in-the-message-task"></a>在 Message 任务中使用特殊字符  
  
1. 从代码编辑器中使用此行替换这两个 Message 任务：  
  
   ```  
   <Message Text="%24(Configuration) is %22$(Configuration)%22" />  
   ```  
  
2. 保存项目文件。  
  
3. 在“命令窗口”输入并执行此行：  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 检查输出。 应看到此行：  
  
   ```  
   $(Configuration) is "Debug"  
   ```  
  
   有关详细信息，请参阅 [MSBuild 特殊字符](../msbuild/msbuild-special-characters.md)。  
  
## <a name="build-items"></a>生成项  
 项是一段信息，通常是文件名，用作生成系统的输入。 例如，表示源文件的项集合可能会传递到名为“Compile”的任务，以将它们编译为程序集。  
  
 所有项都是 ItemGroup 元素的子元素。 项名称是子元素的名称，项值是子元素的包含属性的值。 具有相同名称的项值将收集到该名称的项类型中。  例如，应用于对象的  
  
```  
<ItemGroup>  
    <Compile Include="Program.cs" />  
    <Compile Include="Properties\AssemblyInfo.cs" />  
</ItemGroup>  
```  
  
 定义包含两个项的项组。 项类型编译有两个值："Program.cs"和"Properties\AssemblyInfo.cs"。  
  
 以下代码通过在一个 Include 属性中声明两个文件（用分号分隔）来创建相同的项类型。  
  
```  
<ItemGroup>  
    <Compile Include="Program.cs;Properties\AssemblyInfo.cs" />  
</ItemGroup>  
```  
  
 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。  
  
> [!NOTE]
> 文件路径相对于包含 MSBuild 项目文件的文件夹。  
  
## <a name="examining-item-type-values"></a>检查项类型值  
 若要获取项类型的值，请使用以下语法，其中 ItemType 是项类型的名称：  
  
```  
@(ItemType)  
```  
  
 使用此语法可检查项目文件中的编译项类型。  
  
#### <a name="to-examine-item-type-values"></a>检查项类型值  
  
1. 从代码编辑器中使用以下代码替换 HelloWorld 目标任务：  
  
   ```  
   <Target Name="HelloWorld">  
     <Message Text="Compile item type contains @(Compile)" />  
   </Target>  
   ```  
  
2. 保存项目文件。  
  
3. 在“命令窗口”输入并执行此行：  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 检查输出。 应看到这一长行：  
  
   ```  
   Compile item type contains Form1.cs;Form1.Designer.cs;Program.cs;Properties\AssemblyInfo.cs;Properties\Resources.Designer.cs;Properties\Settings.Designer.cs  
   ```  
  
   默认情况下，用分号分隔项类型的值。  
  
   若要更改项类型的分隔符，请使用以下语法，其中 ItemType 是项类型，Separator 是一个或多个分隔字符的字符串：  
  
```  
@(ItemType, Separator)  
```  
  
 更改 Message 任务以使用回车和换行 (％0A％0D) 显示每行的编译项。  
  
#### <a name="to-display-item-type-values-one-per-line"></a>每行显示一个项类型值  
  
1. 从代码编辑器中使用此行替换 Message 任务：  
  
    ```  
    <Message Text="Compile item type contains @(Compile, '%0A%0D')" />  
    ```  
  
2. 保存项目文件。  
  
3. 在“命令窗口”输入并执行此行：  
  
     `msbuild buildapp.csproj /t:HelloWorld`  
  
4. 检查输出。 应看到这些行：  
  
    ```  
    Compile item type contains Form1.cs  
    Form1.Designer.cs  
    Program.cs  
    Properties\AssemblyInfo.cs  
    Properties\Resources.Designer.cs  
    Properties\Settings.Designer.cs  
    ```  
  
### <a name="include-exclude-and-wildcards"></a>Include、Exclude 和通配符  
 可配合使用通配符“*”、“\*\*”和“?”和 Include 属性将项添加到项类型。 例如，应用于对象的  
  
```  
<Photos Include="images\*.jpeg" />  
```  
  
 将图片文件夹中所有文件扩展名为“.jpeg”的文件添加到照片项类型，而  
  
```  
<Photos Include="images\**.jpeg" />  
```  
  
 将图片文件夹和其所有子文件夹中所有文件扩展名为“.jpeg”的文件添加到照片项类型。 有关更多示例，请参见[如何：选择生成的文件](../msbuild/how-to-select-the-files-to-build.md)。  
  
 注意，项在声明时会被添加到项类型。 例如，应用于对象的  
  
```  
<Photos Include="images\*.jpeg" />  
<Photos Include="images\*.gif" />  
```  
  
 创建一个名为照片的项类型，其中包含图片文件夹中的所有文件，这些文件的扩展名为“.jpeg”或“.gif”。 这等效于以下行：  
  
```  
<Photos Include="images\*.jpeg;images\*.gif" />  
```  
  
 可使用 Exclude 属性从项类型中排除项。 例如，应用于对象的  
  
```  
<Compile Include="*.cs" Exclude="*Designer*">  
```  
  
 将所有文件扩展名为“.cs”的文件添加到编译项类型，除了名称中包含字符串“Designer”的文件。 有关更多示例，请参见[如何：从生成中排除文件](../msbuild/how-to-exclude-files-from-the-build.md)。  
  
 Exclude 属性只会影响由 Include 属性添加的项（这两个属性均位于项元素中）。 例如，应用于对象的  
  
```  
<Compile Include="*.cs" />  
<Compile Include="*.res" Exclude="Form1.cs">  
```  
  
 不会排除在之前的项元素中添加的文件 Form1.cs。  
  
##### <a name="to-include-and-exclude-items"></a>包含和排除项  
  
1. 从代码编辑器中使用此行替换 Message 任务：  
  
    ```  
    <Message Text="Compile item type contains @(XFiles)" />  
    ```  
  
2. 在 Import 元素后添加此项组：  
  
    ```  
    <ItemGroup>  
       <XFiles Include="*.cs;properties/*.resx" Exclude="*Designer*" />  
    </ItemGroup>  
    ```  
  
3. 保存项目文件。  
  
4. 在“命令窗口”输入并执行此行：  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
5. 检查输出。 应看到此行：  
  
    ```  
    Compile item type contains Form1.cs;Program.cs;Properties/Resources.resx  
    ```  
  
## <a name="item-metadata"></a>项元数据  
 除了从 Include 和 Exclude 属性收集的信息外，项还可能包含元数据。 对于需要关于项的详细信息而不仅仅是项值的任务，可使用此元数据。  
  
 项元数据可通过创建元素（其中元数据的名称作为项的子元素）在项目文件中进行声明。 项可以有零个或零个以上的元数据值。 例如，以下 CSFile 项具有值为“Fr”的区域性元数据：  
  
```  
<ItemGroup>  
    <CSFile Include="main.cs">  
        <Culture>Fr</Culture>  
    </CSFile>  
</ItemGroup>  
```  
  
 若要获取项类型的元数据值，请使用以下语法，其中 ItemType 是项类型的名称，MetaDataName 是元数据的名称：  
  
```  
%(ItemType.MetaDataName)  
```  
  
#### <a name="to-examine-item-metadata"></a>检查项元数据  
  
1. 从代码编辑器中使用此行替换 Message 任务：  
  
   ```  
   <Message Text="Compile.DependentUpon: %(Compile.DependentUpon)" />  
   ```  
  
2. 保存项目文件。  
  
3. 在“命令窗口”输入并执行此行：  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 检查输出。 应看到这些行：  
  
   ```  
   Compile.DependentUpon:  
   Compile.DependentUpon: Form1.cs  
   Compile.DependentUpon: Resources.resx  
   Compile.DependentUpon: Settings.settings  
   ```  
  
   请注意，短语“Compile.Dependent Upon”会多次出现。 在目标中使用具有此语法的元数据会造成“批处理”。 批处理是指针对每个唯一元数据值执行一次目标中的任务。 这是等效于常见的“for 循环”编程结构的 MSBuild 脚本。 有关详细信息，请参阅[批处理](../msbuild/msbuild-batching.md)。  
  
### <a name="well-known-metadata"></a>常见元数据  
 无论何时向项列表添加项时，都会向该项分配一些常见元数据。 例如，%(Filename) 会返回任何项的文件名。 若要了解完整的常见元数据列表，请参阅[常见项元数据](../msbuild/msbuild-well-known-item-metadata.md)。  
  
##### <a name="to-examine-well-known-metadata"></a>检查常见元数据  
  
1. 从代码编辑器中使用此行替换 Message 任务：  
  
   ```  
   <Message Text="Compile Filename: %(Compile.Filename)" />  
   ```  
  
2. 保存项目文件。  
  
3. 在“命令窗口”输入并执行此行：  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 检查输出。 应看到这些行：  
  
   ```  
   Compile Filename: Form1  
   Compile Filename: Form1.Designer  
   Compile Filename: Program  
   Compile Filename: AssemblyInfo  
   Compile Filename: Resources.Designer  
   Compile Filename: Settings.Designer  
   ```  
  
   通过比较上面两个示例，可以看到，虽然并非每个编译项类型中的项都有 DependentUpon 元数据，但所有项都具有常见 Filename 元数据。  
  
### <a name="metadata-transformations"></a>元数据转换  
 项列表可以转换为新的项列表。 若要转换项列表，请使用以下语法，其中 ItemType 是项类型的名称，MetaDataName 是元数据的名称：  
  
```  
@(ItemType -> '%(MetadataName)')  
```  
  
 例如，可使用表达式 `@(SourceFiles -> '%(Filename).obj')` 将源文件的项列表转换为对象文件的集合。 有关详细信息，请参阅[转换](../msbuild/msbuild-transforms.md)。  
  
##### <a name="to-transform-items-using-metadata"></a>使用元数据转换项  
  
1. 从代码编辑器中使用此行替换 Message 任务：  
  
   ```  
   <Message Text="Backup files: @(Compile->'%(filename).bak')" />  
   ```  
  
2. 保存项目文件。  
  
3. 在“命令窗口”输入并执行此行：  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 检查输出。 应看到此行：  
  
   ```  
   Backup files: Form1.bak;Form1.Designer.bak;Program.bak;AssemblyInfo.bak;Resources.Designer.bak;Settings.Designer.bak  
   ```  
  
   请注意，此语法中表示的元数据不会造成批处理。  
  
## <a name="whats-next"></a>接下来的内容  
 要了解如何一步步创建简单项目文件，请尝试[演练：从头开始创建 MSBuild 项目文件](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)。  
  
## <a name="see-also"></a>请参阅
[MSBuild 概述](msbuild.md)  
 [MSBuild 参考](../msbuild/msbuild-reference.md)

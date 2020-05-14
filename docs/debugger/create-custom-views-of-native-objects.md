---
title: 创建 C++ 对象的自定义视图
description: 使用 Natvis 框架自定义 Visual Studio 在调试器中显示本机类型的方式
ms.date: 03/02/2020
ms.topic: conceptual
f1_keywords:
- natvis
dev_langs:
- C++
ms.assetid: 2d9a177a-e14b-404f-a6af-49498eff0bd7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 4f8bdd8d26ba450b1aedd790d644c183607c44af
ms.sourcegitcommit: b4e0cc76d94fe8cf6d238c4cc09512d17131a195
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2020
ms.locfileid: "81224506"
---
# <a name="create-custom-views-of-c-objects-in-the-debugger-using-the-natvis-framework"></a>使用 Natvis 框架在调试器中创建C++对象的自定义视图

Visual Studio *Natvis* 框架可以自定义本机类型在调试器变量窗口（例如**局部变量**、**监视**以及**数据提示**窗口）中显示的方式。 Natvis 的可视化功能可以让你创建的类型在调试期间更加直观清晰。

Natvis 替换了 Visual Studio 早期版本中的 *autoexp.dat* 文件，提供了 XML 语法、更好的诊断功能、版本控制功能以及多文件支持功能。

> [!NOTE]
> Natvis 自定义项使用类和结构，但不使用 typedefs。

## <a name="natvis-visualizations"></a><a name="BKMK_Why_create_visualizations_"></a>纳特维斯可视化

你可以使用 Natvis 框架为自己创建的类型创建可视化规则，让开发人员在调试过程中更轻松地查看这些类型。

例如，下图显示的类型 [Windows::UI::Xaml::Controls::TextBox](/uwp/api/Windows.UI.Xaml.Controls.TextBox) 的变量在调试器窗口中未应用任何自定义可视化。

![TextBox 默认可视化](../debugger/media/dbg_natvis_textbox_default.png "TextBox 默认可视化")

突出显示的行显示 `Text` 类的 `TextBox` 属性。 由于类的层次结构很复杂，因此很难找到这个属性。 调试器不知道如何解释自定义字符串类型，所以你看不到文本框中的字符串。

如果应用了 Natvis 自定义可视化工具规则，那么在变量窗口中，同样的`TextBox`看起来就简单得多。 类的重要成员会显示在一起，并且调试器会显示自定义字符串类型的基础字符串值。

![使用可视化工具的 TextBox 数据](../debugger/media/dbg_natvis_textbox_visualizer.png "使用可视化工具的 TextBox 数据")

## <a name="use-natvis-files-in-c-projects"></a><a name="BKMK_Using_Natvis_files"></a>在 C++ 项目中使用 .natvis 文件

Natvis 使用 *.natvis*文件来指定可视化规则。 *.natvis*文件是具有 *.natvis*扩展名的 XML 文件。 Natvis 架构在 *%VSINSTALLDIR%_Xml_Schemas_natvis.xsd 中*定义。

*.natvis* 文件的基本结构由一个或多个代表可视化条目的 `Type` 元素构成。 每个 `Type` 元素的完全限定名称都在其 `Name` 属性中指定。

```xml
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">
  <Type Name="MyNamespace::CFoo">
    .
    .
  </Type>

  <Type Name="...">
    .
    .
  </Type>
</AutoVisualizer>
```

Visual Studio 在 *%VSINSTALLDIR%_Common7_Packages_调试器_可视化器*文件夹中提供了一些 *.natvis*文件。 这些文件具有许多常见类型的可视化规则，并可用作为新类型的编写可视化效果的示例。

### <a name="add-a-natvis-file-to-a-c-project"></a>将 .natvis 文件添加到C++项目

您可以将 *.natvis*文件添加到任何C++项目。

**要添加新的 *.natvis*文件，**

1. 选择**解决方案资源管理器**中的C++项目节点，然后选择 **"项目** > **添加新项**"，或右键单击项目并选择"**Add** > **添加新项**"。

1. 在"**添加新项目"** 对话框中，选择**可视C++** > **实用程序** > **调试器可视化文件 （.natvis）。**

1. 命名文件，然后选择 **"添加**"。

   新文件将添加到**解决方案资源管理器**，并在可视化工作室文档窗格中打开。

Visual Studio 调试器会自动在 C++ 项目中加载 *.natvis* 文件，默认情况下，还会在生成项目时，在 *.pdb* 文件中包含它们。 在调试生成的应用时，调试器会从 *.pdb* 文件加载 *.natvis* 文件，即使你没有打开该项目也是如此。 如果不想在 *.pdb* 中包含 *.natvis* 文件，可以从生成的 *.pdb* 文件中将其排除。

**从 *.pdb* 中排除 *.natvis* 文件：**

1. 在**解决方案资源管理器**中选择 *.natvis* 文件，然后选择**属性**图标，或右键单击该文件并选择**属性**。

1. 按下**从生成中排除**旁边的箭头并选择**是**，然后选择**确定**。

>[!NOTE]
>如果是调试可执行的项目，则使用解决方案项来添加 *.pdb* 中不包含的 *.natvis* 文件，因为没有可用的 C++ 项目。

>[!NOTE]
>从 *.pdb* 加载的 Natvis 规则仅适用于 *.pdb* 引用的模块中的类型。 例如，如果 *Module1.pdb* 包含一个名为 `Test` 的类型的 Natvis 条目，则它仅适用于 *Module1.dll* 中的 `Test` 类。 如果另一个模块也定义了一个名为 `Test` 的类，则 *Module1.pdb* 的 Natvis 条目不适用于它。 

**要通过 VSIX 包安装和注册 *.natvis*文件，请执行：**

VSIX 软件包可以安装和注册 *.natvis*文件。 无论它们安装在何处，所有已注册的 *.natvis*文件都会在调试期间自动拾取。

1. 在 VSIX 包中包括 *.natvis*文件。 例如，对于以下项目文件：
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="14.0">
     <ItemGroup>
       <VSIXSourceItem Include="Visualizer.natvis" />
     </ItemGroup>
   </Project>
   ```

2. 在*源.扩展.vsixmanifest*文件中注册 *.natvis*文件：
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
     <Assets>
       <Asset Type="NativeVisualizer" Path="Visualizer.natvis"  />
     </Assets>
   </PackageManifest>
   ```

### <a name="natvis-file-locations"></a><a name="BKMK_natvis_location"></a>纳特维斯文件位置

如果你希望将 *.natvis* 文件应用于多个项目，可以将它们添加到用户目录或系统目录中。 

将按照以下顺序来评估 *.Natvis* 文件：

1. 所调试的 *.pdb* 文件中内嵌的所有的 *.natvis* 文件，除非加载的项目中存在同名文件。

2. 加载的 C++ 项目或顶级解决方案中的所有 *.natvis* 文件。 这包括所有已加载的 C++ 项目（包括类库），但不包括其他语言的项目。

3. 通过 VSIX 包安装和注册的任何 *.natvis*文件。

::: moniker range="vs-2017"

4. 特定于用户的 Natvis 目录 (例如， *%USERPROFILE%\Documents\Visual Studio 2017\Visualizers*)。

::: moniker-end

::: moniker range=">= vs-2019"

4. 特定于用户的 Natvis 目录 (例如， *%USERPROFILE%\Documents\Visual Studio 2019\Visualizers*)。

::: moniker-end

5. 系统级 Natvis 目录 (*%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers*)。 此目录中包含随 Visual Studio 一起安装的 *.natvis* 文件。 如果你具有管理员权限，可以将文件添加到此目录中。

## <a name="modify-natvis-files-while-debugging"></a>调试时修改 .natvis 文件

你可以在调试项目时，在 IDE 中修改 *.natvis* 文件。 在用于调试的同一个 Visual Studio 实例中打开该文件，进行修改，然后保存。 保存后，**监视**和**局部变量**窗口就会随之更新，显示所做的更改。

你还可以在调试的解决方案中添加或删除 *.natvis* 文件，Visual Studio 会随之添加或删除相关的可视化效果。

在调试时，无法更新 *.pdb* 文件中内嵌的 *.natvis* 文件。 

如果你在 Visual Studio 以外修改 *.natvis* 文件，所做的更改不会自动生效。 要更新调试器窗口，可以在 **"立即"** 窗口中重新评估 **.natvisreload 命令**。 更改随后就会生效，无需重新启动调试会话。

还可以使用 **.natvisreload** 命令将 *.natvis* 文件升级到较新的版本。 例如，*.natvis* 文件可能被纳入了源代码管理中，并且你需要获取其他人最近所做的更改。

## <a name="expressions-and-formatting"></a><a name="BKMK_Expressions_and_formatting"></a>表达式和格式
Natvis 可视化效果使用 C++ 表达式指定需显示的数据项。 除了[上下文运算符 (C++)](../debugger/context-operator-cpp.md) 中所述的、调试器中的 C++ 表达式的增强功能和限制外，还要注意以下事项：

- Natvis 表达式在可视化对象上下文而非当前堆栈框架中进行计算。 例如，`x`在 Natvis 表达式中，是指可视化对象中名为**x**的字段，而不是当前函数中名为**x**的局部变量。 您无法访问 Natvis 表达式中的局部变量，尽管可以访问全局变量。

- Natvis 表达式不允许函数计算或副作用。 函数调用和赋值运算符会被忽略。 由于[调试器内部函数](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state)没有副作用，因此可以从任何 Natvis 表达式随意调用，即使系统不允许进行其他函数调用也是如此。

- 要控制表达式的显示方式，可以使用 [C++ 中的格式说明符](format-specifiers-in-cpp.md#BKMK_Visual_Studio_2012_format_specifiers)中所述的任何格式说明符。 如果条目由 Natvis 在内部使用，格式说明符将被忽略，例如 [ArrayItems 扩展](../debugger/create-custom-views-of-native-objects.md#BKMK_ArrayItems_expansion)中的 `Size` 表达式。

## <a name="natvis-views"></a>Natvis 视图

你可以定义不同的 Natvis 视图，以便用不同的方式来显示类型。 例如，下面是 `std::vector` 的一个可视化效果，定义了一个名为 `simple` 的简化视图。 默认视图和 `simple` 视图中都显示了 `DisplayString` 和 `ArrayItems` 元素，但 `simple` 视图中却未显示 `[size]` 和 `[capacity]` 项。

```xml
<Type Name="std::vector&lt;*&gt;">
    <DisplayString>{{ size={_Mylast - _Myfirst} }}</DisplayString>
    <Expand>
        <Item Name="[size]" ExcludeView="simple">_Mylast - _Myfirst</Item>
        <Item Name="[capacity]" ExcludeView="simple">_Myend - _Myfirst</Item>
        <ArrayItems>
            <Size>_Mylast - _Myfirst</Size>
            <ValuePointer>_Myfirst</ValuePointer>
        </ArrayItems>
    </Expand>
</Type>
```

在**监视**窗口中，使用 **,view** 格式说明符来指定替代视图。 simple 视图将显示为 **vec,view(simple)**：

![具有简单视图的监视窗口](../debugger/media/watch-simpleview.png "具有简单视图的监视窗口")

## <a name="natvis-errors"></a><a name="BKMK_Diagnosing_Natvis_errors"></a>纳特维斯错误

当调试器遇到可视化条目中的错误时，会忽略它们。 要么以原始格式显示类型，要么选择其他合适的可视化效果。 你可以使用 Natvis 的诊断功能来了解调试器忽略可视化条目的原因，还可以查看基础语法和分析错误。

**要打开 Natvis 诊断：**

- 在 **"工具** > **选项**"（或**调试** > **选项**）>**调试** > **输出窗口**下，将**Natvis 诊断消息（仅C++）** 设置为**错误**、**警告**或**详细，** 然后选择 **"确定**"。

错误将显示在 **"输出"** 窗口中。

## <a name="natvis-syntax-reference"></a><a name="BKMK_Syntax_reference"></a>纳特维斯语法参考

### <a name="autovisualizer-element"></a><a name="BKMK_AutoVisualizer"></a>自动可视化器元素
`AutoVisualizer` 元素是 *.natvis* 文件的根节点，并包含命名空间 `xmlns:` 属性。

```xml
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">
.
.
</AutoVisualizer>
```

该`AutoVisualizer`元素可以具有[类型](#BKMK_Type)[、HResult、UI](#BKMK_HResult)[可视化器](#BKMK_UIVisualizer)和[自定义可视化器](#BKMK_CustomVisualizer)子级。

### <a name="type-element"></a><a name="BKMK_Type"></a>类型元素

基本`Type`如下所示：

```xml
<Type Name="[fully qualified type name]">
  <DisplayString Condition="[Boolean expression]">[Display value]</DisplayString>
  <Expand>
    ...
  </Expand>
</Type>
```

 该`Type`元素指定：

1. 可视化效果应用于什么类型（属性`Name`）。

2. 该类型的对象的值是什么样的（ `DisplayString` 元素）。

3. 用户在变量窗口中展开类型时，该类型的成员应当以什么形式显示（`Expand` 节点）。

#### <a name="templated-classes"></a>模板化类
`Type`元素`Name`的属性接受星号`*`作为通配符，可用于模板化类名称。

在以下示例中，无论对象是 `CAtlArray<int>` 还是 `CAtlArray<float>`，都使用了相同的可视化效果。 如果 `CAtlArray<float>` 有特定的可视化条目，它的优先级将高于通用的条目。

```xml
<Type Name="ATL::CAtlArray&lt;*&gt;">
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>
</Type>
```

可以使用 $T1 和 $T2 这样的宏，在可视化条目中引用模板参数。 有关这些宏的示例，请参阅 Visual Studio 随附的 *.natvis* 文件。

#### <a name="visualizer-type-matching"></a><a name="BKMK_Visualizer_type_matching"></a>可视化工具类型匹配
如果无法验证某个可视化条目，则使用下一个可用的可视化效果。

#### <a name="inheritable-attribute"></a>可继承的特性
可选的 `Inheritable` 属性用于指定，一个可视化效果是仅适用于一个基类型，还是适用于一个基类型和所有的派生类型。 `Inheritable` 的默认值为 `true`。

在以下示例中，可视化效果仅适用于类型`BaseClass`：

```xml
<Type Name="Namespace::BaseClass" Inheritable="false">
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>
</Type>
```

#### <a name="priority-attribute"></a>优先级特性

如果某个定义的分析失败，可选的 `Priority` 属性会指定使用备用定义的顺序。 `Priority` 的值包括：`Low`、`MediumLow`、`Medium`、`MediumHigh` 和 `High`。 默认值为 `Medium`。 `Priority`属性只区分同一个 *.natvis* 文件中的优先级。

下面的示例会首先分析与 2015 STL 匹配的条目。 如果分析失败，就会使用 STL 的 2013 版本的备用条目：

```xml
<!-- VC 2013 -->
<Type Name="std::reference_wrapper&lt;*&gt;" Priority="MediumLow">
     <DisplayString>{_Callee}</DisplayString>
    <Expand>
        <ExpandedItem>_Callee</ExpandedItem>
    </Expand>
</Type>

<!-- VC 2015 -->
<Type Name="std::reference_wrapper&lt;*&gt;">
    <DisplayString>{*_Ptr}</DisplayString>
    <Expand>
        <Item Name="[ptr]">_Ptr</Item>
    </Expand>
</Type>
```

### <a name="optional-attribute"></a>可选特性
你可以将 `Optional` 属性放在任一节点上。 如果某个可选节点内的某个子表达式的分析失败，调试器就会忽略该节点，但会应用 `Type` 规则的其余部分。 在下面的类型中， `[State]` 不可选，但 `[Exception]` 可选。  如果 `MyNamespace::MyClass` 包含名为 `M_exceptionHolder` 的字段，就会同时显示 `[State]` 节点和 `[Exception]` 节点，但如果不包含 `_M_exceptionHolder` 字段，就会只显示 `[State]` 节点。

```xml
<Type Name="MyNamespace::MyClass">
    <Expand>
      <Item Name="[State]">_M_State</Item>
      <Item Name="[Exception]" Optional="true">_M_exceptionHolder</Item>
    </Expand>
</Type>
```

### <a name="condition-attribute"></a><a name="BKMK_Condition_attribute"></a>条件属性

可选的 `Condition` 属性可用于许多可视化元素，指定何时使用可视化规则。 如果条件属性内的表达式解析为 `false`，就不应用可视化规则。 如果其计算结果为 `true`，或者没有 `Condition` 属性，就会应用可视化规则。 你可以将此属性用于可视化条目中的 if-else 逻辑。

例如，以下可视化效果具有智能指针`DisplayString`类型的两个元素。 当`_Myptr`成员为空时，第一个`DisplayString`元素的条件解析为`true`，以便窗体显示。 当`_Myptr`成员不为空时，条件将计算为`false`，第二`DisplayString`个元素将显示。

```xml
<Type Name="std::auto_ptr&lt;*&gt;">
  <DisplayString Condition="_Myptr == 0">empty</DisplayString>
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>
  <Expand>
    <ExpandedItem>_Myptr</ExpandedItem>
  </Expand>
</Type>
```

### <a name="includeview-and-excludeview-attributes"></a>IncludeView 和 ExcludeView 特性

`IncludeView` 和 `ExcludeView` 属性用于指定是否在特定视图内显示元素。 例如，在下面的 Natvis `std::vector` 规范中，`simple` 视图不显示 `[size]` 和 `[capacity]` 项。

```xml
<Type Name="std::vector&lt;*&gt;">
    <DisplayString>{{ size={_Mylast - _Myfirst} }}</DisplayString>
    <Expand>
        <Item Name="[size]" ExcludeView="simple">_Mylast - _Myfirst</Item>
        <Item Name="[capacity]" ExcludeView="simple">_Myend - _Myfirst</Item>
        <ArrayItems>
            <Size>_Mylast - _Myfirst</Size>
            <ValuePointer>_Myfirst</ValuePointer>
        </ArrayItems>
    </Expand>
</Type>
```

可以针对类型和各个成员使用 `IncludeView` 和 `ExcludeView` 属性。

### <a name="version-element"></a><a name="BKMK_Versioning"></a>版本元素
`Version` 元素用于将可视化条目的范围限定在特定模块和版本内。 `Version` 元素有助于避免名称冲突、减少无意间的不匹配，还允许在不同的类型版本中使用不同的可视化效果。

如果某个由不同模块使用的公共头文件定义了一个类型，则只有当该类型位于指定的模块版本中时，版本化的可视化效果才会显示。

在下面的示例中，可视化效果只适用于在 `Windows.UI.Xaml.dll` 版本 1.0 到 1.5 中找到的 `DirectUI::Border` 类型。

```xml
<Type Name="DirectUI::Border">
  <Version Name="Windows.UI.Xaml.dll" Min="1.0" Max="1.5"/>
  <DisplayString>{{Name = {*(m_pDO->m_pstrName)}}}</DisplayString>
  <Expand>
    <ExpandedItem>*(CBorder*)(m_pDO)</ExpandedItem>
  </Expand>
</Type>
```

你不需要两者兼`Min`。 `Max` 它们是可选属性。 不支持通配符。

该`Name`属性在格式*文件名.ext*中，如*hello.exe*或*某些.dll*。 不允许路径名称。

### <a name="displaystring-element"></a><a name="BKMK_DisplayString"></a>显示字符串元素
`DisplayString` 元素用于指定要显示为变量值的字符串。 它接受混合表达式的任意字符串。 大括号内的所有内容都可解释为表达式。 例如，以下 `DisplayString` 条目：

```xml
<Type Name="CPoint">
  <DisplayString>{{x={x} y={y}}}</DisplayString>
</Type>
```

表示类型`CPoint`变量显示如下图所示：

 ![使用显示字符串元素](../debugger/media/dbg_natvis_cpoint_displaystring.png "使用显示字符串元素")

在 `DisplayString` 表达式中，属于 `CPoint` 成员的 `x` 和 `y` 位于大括号内，因此它们的值会被计算。 该示例还介绍了如何用双层大括号（`{{` 或 `}}`）对大括号进行转义。

> [!NOTE]
> `DisplayString` 元素是唯一接受任意字符串和大括号语法的元素。 所有其他可视化元素仅接受调试器可以计算的表达式。

### <a name="stringview-element"></a><a name="BKMK_StringView"></a>字符串查看元素

`StringView` 元素用于定义一个值，调试器可以将该值发送给内置的文本可视化工具。 例如，假设 `ATL::CStringT` 类型有以下可视化效果：

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>
</Type>
```

`CStringT` 对象将显示在一个变量窗口中，如下例所示：

![CStringT DisplayString 元素](../debugger/media/dbg_natvis_displaystring_cstringt.png "CStringT DisplayString 元素")

添加`StringView`元素告诉调试器它可以将值显示为文本可视化。

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>
  <StringView>m_pszData,su</StringView>
</Type>
```

在调试期间，您可以选择变量旁边的放大镜图标，然后选择 **"文本可视化器**"以显示**m_pszData**指向的字符串。

 ![使用 StringView 可视化工具的 CStringT 数据](../debugger/media/dbg_natvis_stringview_cstringt.png "使用 StringView 可视化工具的 CStringT 数据")

表达式 `{m_pszData,su}` 包含一个 C++ 格式说明符 **su**，用于将值显示为 Unicode 字符串。 有关详细信息，请参阅 [C++ 中的格式说明符](../debugger/format-specifiers-in-cpp.md)。

### <a name="expand-element"></a><a name="BKMK_Expand"></a>展开元素

可选的 `Expand` 节点用于自定义当你在变量窗口中展开类型时，该可视化类型的子项。 `Expand` 节点接受用于定义子元素的子节点列表。

- 如果未在可视化条目中指定 `Expand` 节点，子项将使用默认的展开规则。

- 如果指定的 `Expand` 节点下面没有子节点，类型就无法在调试器窗口中展开。

#### <a name="item-expansion"></a><a name="BKMK_Item_expansion"></a>项目扩展

 `Item` 元素是 `Expand` 节点中最基本、最常见的元素。 `Item` 定义单个子元素。 例如，一个包含 `top`、`left`、`right` 和 `bottom` 字段的 `CRect` 类具有以下可视化条目：

```xml
<Type Name="CRect">
  <DisplayString>{{top={top} bottom={bottom} left={left} right={right}}}</DisplayString>
  <Expand>
    <Item Name="Width">right - left</Item>
    <Item Name="Height">bottom - top</Item>
  </Expand>
</Type>
```

在调试器窗口中，`CRect`类型如下所示：

![具有 Item 元素扩展的 CRect](../debugger/media/dbg_natvis_expand_item_crect1.png "具有 Item 元素扩展的 CRect")

调试器将计算 `Width` 和 `Height` 元素中指定的表达式，然后在变量窗口的**值**列中显示值。

调试器会为每个自定义展开自动创建 **[Raw View]** 节点。 上面的屏幕截图中的 **[Raw View]** 节点是展开的，显示了对象的默认原始视图与其 Natvis 可视化效果的区别。 默认展开会为基类创建一个子树，并将基类的所有数据成员以子项的形式列出。

> [!NOTE]
> 如果项元素的表达式指向复杂类型，**则 Item**节点本身是可展开的。

#### <a name="arrayitems-expansion"></a><a name="BKMK_ArrayItems_expansion"></a> Size
使用 `ArrayItems` 节点，让 Visual Studio 调试器将类型解释为一个数组并显示其各个元素。 `std::vector` 的可视化效果是一个很好的示例：

```xml
<Type Name="std::vector&lt;*&gt;">
  <DisplayString>{{size = {_Mylast - _Myfirst}}}</DisplayString>
  <Expand>
    <Item Name="[size]">_Mylast - _Myfirst</Item>
    <Item Name="[capacity]">(_Myend - _Myfirst)</Item>
    <ArrayItems>
      <Size>_Mylast - _Myfirst</Size>
      <ValuePointer>_Myfirst</ValuePointer>
    </ArrayItems>
  </Expand>
</Type>
```

`std::vector` 在变量窗口中展开时显示其自身的元素：

![使用 ArrayItems 扩展的 std::vector](../debugger/media/dbg_natvis_expand_arrayitems_stdvector.png "使用 ArrayItems 扩展的 std::vector")

节点`ArrayItems`必须具有：

- 用于使调试器了解数组长度的 `Size` 表达式（必须计算为整数）。
- 一个 `ValuePointer` 表达式，指向第一个元素（必须为非 `void*` 元素类型的指针）。

数组下限的默认值为 0。 要修改此值，请使用 `LowerBound` 元素。 Visual Studio 随附的 *.Natvis* 文件中提供了示例。

>[!NOTE]
>可以使用 `[]` 运算符（例如 `vector[i]`）以及任何使用了 `ArrayItems` 的一维数组可视化效果，即使该类型本身（例如 `CATLArray`）不允许使用此运算符。

您还可以指定多维数组。 在这种情况下，调试器需要稍微多一些信息才能正确显示子元素：

```xml
<Type Name="Concurrency::array&lt;*,*&gt;">
  <DisplayString>extent = {_M_extent}</DisplayString>
  <Expand>
    <Item Name="extent">_M_extent</Item>
    <ArrayItems Condition="_M_buffer_descriptor._M_data_ptr != 0">
      <Direction>Forward</Direction>
      <Rank>$T2</Rank>
      <Size>_M_extent._M_base[$i]</Size>
      <ValuePointer>($T1*) _M_buffer_descriptor._M_data_ptr</ValuePointer>
    </ArrayItems>
  </Expand>
</Type>
```

- `Direction` 指定数组是采用行优先顺序还是列优先顺序。
- `Rank` 指定数组的秩。
- `Size` 元素接受将其替换为维索引以查找该维度中数组的长度的隐式 `$i` 参数。 在前面的示例中，表达式`_M_extent.M_base[0]`应给出第 0 个维度、`_M_extent._M_base[1]`第 1 个维度等的长度。

下面是调试器窗口中显示的一个二维 `Concurrency::array` 对象：

![具有阵列项目扩展的二维数组](../debugger/media/dbg_natvis_expand_arrayitems_2d.png "具有阵列项目扩展的二维数组")

#### <a name="indexlistitems-expansion"></a><a name="BKMK_IndexListItems_expansion"></a>索引列表项目扩展

仅当数组元素在内存中连续排列时，才能使用 `ArrayItems` 展开。 调试器只需递增其指针，就可以获取下一个元素。 如果你需要操作值节点的索引，可以使用 `IndexListItems` 节点。 下面是 `IndexListItems` 节点的可视化处理：

```xml
<Type Name="Concurrency::multi_link_registry&lt;*&gt;">
  <DisplayString>{{size = {_M_vector._M_index}}}</DisplayString>
  <Expand>
    <Item Name="[size]">_M_vector._M_index</Item>
    <IndexListItems>
      <Size>_M_vector._M_index</Size>
      <ValueNode>*(_M_vector._M_array[$i])</ValueNode>
    </IndexListItems>
  </Expand>
</Type>
```

`ArrayItems` 和 `IndexListItems` 之间的唯一区别是 `ValueNode`，它期望带有隐式元素 `$i` 参数的第 i<sup></sup> 个元素的完整表达式。

>[!NOTE]
>可以使用 `[]` 运算符（例如 `vector[i]`）以及任何使用了 `IndexListItems` 的一维数组可视化效果，即使该类型本身（例如 `CATLArray`）不允许使用此运算符。

#### <a name="linkedlistitems-expansion"></a><a name="BKMK_LinkedListItems_expansion"></a>链接列表项目扩展

如果可视化类型表示一个链接列表，则调试器可以通过使用 `LinkedListItems` 节点显示其子级。 `CAtlList`以下类型的可视化使用`LinkedListItems`：

```xml
<Type Name="ATL::CAtlList&lt;*,*&gt;">
  <DisplayString>{{Count = {m_nElements}}}</DisplayString>
  <Expand>
    <Item Name="Count">m_nElements</Item>
    <LinkedListItems>
      <Size>m_nElements</Size>
      <HeadPointer>m_pHead</HeadPointer>
      <NextPointer>m_pNext</NextPointer>
      <ValueNode>m_element</ValueNode>
    </LinkedListItems>
  </Expand>
</Type>
```

`Size` 元素引用该列表的长度。 `HeadPointer` 指向第一个元素， `NextPointer` 引用下一个元素，而 `ValueNode` 引用项的值。

调试器将在 `LinkedListItems` 节点元素（而不是父列表类型）环境中计算 `NextPointer` 和 `ValueNode` 表达式。 在前面的示例中，`CAtlList` 有一个 `CNode` 类（位于 `atlcoll.h` 中），它是链接列表的节点。 `m_pNext` 和 `m_element` 是 `CNode` 类（而不是 `CAtlList` 类）的字段。

`ValueNode` 可以保留为空或使用 `this` 来引用 `LinkedListItems` 节点本身。

#### <a name="customlistitems-expansion"></a>CustomListItems 展开

`CustomListItems` 展开允许编写自定义逻辑，以遍历数据结构（如哈希表）。 使用 `CustomListItems` 来可视化数据结构，这些数据结构可以使用 C++ 表达式进行所有运算，但不太适合 `ArrayItems`、`IndexListItems` 或 `LinkedListItems` 模式。

借助在展开内定义的变量和对象，你可以在 `CustomListItems` 展开中使用 `Exec` 来执行内部代码。 可以将逻辑运算符、算术运算符和赋值运算符与  `Exec` 一起使用。 除了C++表达式赋值`Exec`器支持的[调试器内部函数](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state)外，不能用于计算函数。

下面的 `CAtlMap` 可视化工具是一个很好的例子，其中的 `CustomListItems` 用得很恰当。

```xml
<Type Name="ATL::CAtlMap&lt;*,*,*,*&gt;">
    <AlternativeType Name="ATL::CMapToInterface&lt;*,*,*&gt;"/>
    <AlternativeType Name="ATL::CMapToAutoPtr&lt;*,*,*&gt;"/>
    <DisplayString>{{Count = {m_nElements}}}</DisplayString>
    <Expand>
      <CustomListItems MaxItemsPerView="5000" ExcludeView="Test">
        <Variable Name="iBucket" InitialValue="-1" />
        <Variable Name="pBucket" InitialValue="m_ppBins == nullptr ? nullptr : *m_ppBins" />
        <Variable Name="iBucketIncrement" InitialValue="-1" />

        <Size>m_nElements</Size>
        <Exec>pBucket = nullptr</Exec>
        <Loop>
          <If Condition="pBucket == nullptr">
            <Exec>iBucket++</Exec>
            <Exec>iBucketIncrement = __findnonnull(m_ppBins + iBucket, m_nBins - iBucket)</Exec>
            <Break Condition="iBucketIncrement == -1" />
            <Exec>iBucket += iBucketIncrement</Exec>
            <Exec>pBucket = m_ppBins[iBucket]</Exec>
          </If>
          <Item>pBucket,na</Item>
          <Exec>pBucket = pBucket->m_pNext</Exec>
        </Loop>
      </CustomListItems>
    </Expand>
</Type>
```

#### <a name="treeitems-expansion"></a><a name="BKMK_TreeItems_expansion"></a>树项目扩展
 如果可视化类型表示一个树，则调试器可以通过使用 `TreeItems` 节点遍历该树并显示其子级。 下面是使用`std::map``TreeItems`节点的类型的可视化效果：

```xml
<Type Name="std::map&lt;*&gt;">
  <DisplayString>{{size = {_Mysize}}}</DisplayString>
  <Expand>
    <Item Name="[size]">_Mysize</Item>
    <Item Name="[comp]">comp</Item>
    <TreeItems>
      <Size>_Mysize</Size>
      <HeadPointer>_Myhead->_Parent</HeadPointer>
      <LeftPointer>_Left</LeftPointer>
      <RightPointer>_Right</RightPointer>
      <ValueNode Condition="!((bool)_Isnil)">_Myval</ValueNode>
    </TreeItems>
  </Expand>
</Type>
```

语法类似于 `LinkedListItems` 节点。 `LeftPointer`、`RightPointer` 和 `ValueNode` 是在树节点类的上下文中计算的。 `ValueNode` 可以保留为空或使用 `this` 来引用 `TreeItems` 节点本身。

#### <a name="expandeditem-expansion"></a><a name="BKMK_ExpandedItem_expansion"></a>扩展项目扩展
 通过将基类或数据成员的属性显示为可视化类型的子项，`ExpandedItem` 元素生成了一个聚合的子视图。 调试器将计算指定的表达式，并将结果的子节点附加到该可视化类型的子列表中。

例如，智能指针类型`auto_ptr<vector<int>>`通常显示为：

 ![自动&#95;ptr&#60;矢量&#60;&#62;&#62; 默认扩展](../debugger/media/dbg_natvis_expand_expandeditem_default.png "默认扩展")

 要查看矢量的值，就必须在变量窗口中穿过 `_Myptr` 成员，向下深入两个级别。 通过添加 `ExpandedItem` 元素，就可以从层次结构中去除 `_Myptr` 变量并直接查看矢量元素：

```xml
<Type Name="std::auto_ptr&lt;*&gt;">
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>
  <Expand>
    <ExpandedItem>_Myptr</ExpandedItem>
  </Expand>
</Type>
```

 ![自动&#95;&#60;向量&#60;&#62;&#62; 扩展项目扩展](../debugger/media/dbg_natvis_expand_expandeditem_visualized.png "ExpandedItem 展开")

下面的示例介绍了如何将基类的属性聚合到一个派生类中。 假定 `CPanel` 类派生自 `CFrameworkElement`。 `ExpandedItem` 节点的可视化会将基 `CFrameworkElement` 类的属性附加到 `CPanel` 类的子列表中，而不是重复这些属性。

```xml
<Type Name="CPanel">
  <DisplayString>{{Name = {*(m_pstrName)}}}</DisplayString>
  <Expand>
    <Item Name="IsItemsHost">(bool)m_bItemsHost</Item>
    <ExpandedItem>*(CFrameworkElement*)this,nd</ExpandedItem>
  </Expand>
</Type>
```

关闭派生类的可视化匹配的 nd 格式说明符肯定在这****。 否则，表达式`*(CFrameworkElement*)this`将导致再次应用`CPanel`可视化效果，因为默认可视化类型匹配规则认为它是最合适的。 使用**nd**格式指定器指示调试器使用基类可视化，或者如果基类没有可视化，则使用默认扩展。

#### <a name="synthetic-item-expansion"></a><a name="BKMK_Synthetic_Item_expansion"></a> Synthetic Item 展开
 `ExpandedItem` 元素通过消除层次结构提供更简单的数据视图，`Synthetic` 节点则恰好相反。 它允许您创建不是表达式的结果的人工子元素。 人工元素可以有自己的子元素。 在下面的示例中， `Concurrency::array` 类型的可视化效果使用 `Synthetic` 节点向用户显示诊断消息：

```xml
<Type Name="Concurrency::array&lt;*,*&gt;">
  <DisplayString>extent = {_M_extent}</DisplayString>
  <Expand>
    <Item Name="extent" Condition="_M_buffer_descriptor._M_data_ptr == 0">_M_extent</Item>
    <ArrayItems Condition="_M_buffer_descriptor._M_data_ptr != 0">
      <Rank>$T2</Rank>
      <Size>_M_extent._M_base[$i]</Size>
      <ValuePointer>($T1*) _M_buffer_descriptor._M_data_ptr</ValuePointer>
    </ArrayItems>
    <Synthetic Name="Array" Condition="_M_buffer_descriptor._M_data_ptr == 0">
      <DisplayString>Array members can be viewed only under the GPU debugger</DisplayString>
    </Synthetic>
  </Expand>
</Type>
```

 ![并发：：具有合成元素扩展的数组](../debugger/media/dbg_natvis_expand_synthetic.png "并发：：具有合成元素扩展的数组")

### <a name="hresult-element"></a><a name="BKMK_HResult"></a>HResult 元素
 借助 `HResult` 元素，你可以自定义显示在调试器窗口中的 **HRESULT** 信息。 `HRValue` 元素必须包含要自定义的 **HRESULT** 的 32 位值。 `HRDescription` 元素包含要显示在调试器窗口中的信息。

```xml

<HResult Name="MY_E_COLLECTION_NOELEMENTS">
  <HRValue>0xABC0123</HRValue>
  <HRDescription>No elements in the collection.</HRDescription>
</HResult>
```

### <a name="uivisualizer-element"></a><a name="BKMK_UIVisualizer"></a>UI可视化器元素
`UIVisualizer` 元素向调试器注册图形可视化工具插件。 图形可视化工具会创建一个对话框或其他界面，用符合其数据类型的方式显示变量或对象。 可视化工具插件必须被编写为 [VSPackage](../extensibility/internals/vspackages.md)，并且必须公开一项调试器可以使用的服务。 *.Natvis* 文件包含插件的注册信息，例如名称、所公开服务的 GUID 以及它可以直观显示的类型。

下面是 UIVisualizer 元素的示例：

```xml
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">
    <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}"
        Id="1" MenuName="Vector Visualizer"/>
    <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}"
        Id="2" MenuName="List Visualizer"/>
.
.
</AutoVisualizer>
```

- `ServiceId` - `Id` 属性对用来标识 `UIVisualizer`。 `ServiceId` 是可视化工具包公开的服务的 GUID。 如果服务提供了多个可视化工具，`Id` 是用来区分它们的唯一标识符。 在上面的示例中，同一个可视化工具服务提供了两个可视化工具。

- `MenuName` 属性用于定义可视化工具名称，该名称会显示在调试器的放大镜图标旁边的下拉列表中。 例如：

  ![UIVisualizer 菜单快捷菜单](../debugger/media/dbg_natvis_vectorvisualizer.png "UIVisualizer 菜单快捷菜单")

*.natvis* 文件中定义的每种类型都必须明确列出能够显示它的所有 UI 可视化工具。 调试器会将类型条目中的可视化工具引用与注册的可视化工具相匹配。 例如，下面的 `std::vector` 类型条目引用的是前一个示例中的 `UIVisualizer`。

```xml
<Type Name="std::vector&lt;int,*&gt;">
  <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}" Id="1" />
</Type>
```

 在用于查看内存中位图`UIVisualizer`[的图像监视](https://marketplace.visualstudio.com/search?term=%22Image%20Watch%22&target=VS&category=All%20categories&vsVersion=&sortBy=Relevance)扩展中，可以看到 一个示例。

### <a name="customvisualizer-element"></a><a name="BKMK_CustomVisualizer"></a>CustomVisualizer 元素
 `CustomVisualizer` 是一个扩展点，用于指定你编写的 VSIX 扩展，以便在 Visual Studio 代码中控制可视化效果。 有关编写 VSIX 扩展的更多信息，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

编写自定义可视化工具比 XML Natvis 定义要费事得多，但 Natvis 在支持方面的限制对你没有影响。 自定义可视化工具有权访问所有的调试器扩展性 API，因此可以查询和修改调试对象进程，也可以与 Visual Studio 的其他部分通信。

 可以在 `CustomVisualizer` 元素上使用 `Condition`、`IncludeView` 和 `ExcludeView` 属性。

 ## <a name="limitations"></a>限制

Natvis 自定义项使用类和结构，但不使用 typedefs。

Natvis 不支持基元类型的可视化工具（例如`int`，，）`bool`或指向基元类型的指针。 在这种情况下，一个选项是使用适合您的用例的[格式指定器](../debugger/format-specifiers-in-cpp.md)。 例如，如果在代码`double* mydoublearray`中使用，则可以在调试器**的"监视"** 窗口中使用数组格式指定器，例如显示前 100 个元素的表达式`mydoublearray, [100]`。

---
title: 创建本机对象的自定义视图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- natvis
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 2d9a177a-e14b-404f-a6af-49498eff0bd7
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: daa4eba0949262e0bfbfa67c9b0ab3ee814558e4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440834"
---
# <a name="create-custom-views-of-native-objects"></a>创建本机对象的自定义视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio Natvis 框架允许你在调试器变量窗口（例如 **“监视”** 窗口、 **“局部变量”** 窗口和 **“数据提示”** 窗口）中自定义 Visual Studio 显示本机类型的方式。  

 Natvis 代替 Visual Studio 早期版本中使用的 **autoexp.dat** 文件，并提供 XML 语法、更好的诊断、版本控制和多个文件支持。  

> [!NOTE]
> 当发生以下情况时，Natvis 框架不能用于可视化：  
> 
> - 在调试器类型设置为 **“混合”** 的情况下调试 C++ Windows 桌面项目。  
>   - 在托管兼容模式下的 Windows 桌面应用程序中执行混合模式调试（**“工具”/“选项”/“调试”/“常规”/“使用托管兼容模式”**）。  
>   - 在本机兼容模式下的 Windows 桌面应用程序中进行调试（**“工具”/“选项”/“调试”/“常规”/“使用本机兼容模式”**）。  

## <a name="BKMK_Why_create_visualizations_"></a> 为什么创建 Natvis 可视化？  
 可使用 Natvis 框架为你创建的类型创建可视化规则，以便开发人员可以在调试期间轻松查看它们。  

 例如，下图显示了类型 [Windows::UI::Xaml::Controls::TextBox](http://go.microsoft.com/fwlink/?LinkId=258422) 的变量，此类型显示在未应用任何自定义可视化的调试器中。  

 ![TextBox 默认可视化](../debugger/media/dbg-natvis-textbox-default.png "DBG_NATVIS_TextBox_Default")  

 高亮行显示的是 `TextBox` 类的 `Text` 属性。 Complex 类层次结构使得难以找到此值；此外，由于调试器无法解读对象使用的自定义字符串类型，因此你看不到文本框中的字符串。  

 应用自定义可视化规则后，同一个 `TextBox` 在变量窗口中变得更简单。 可以同时查看类的重要成员，且调试器显示自定义字符串类型的基础字符串值。  

 ![使用可视化工具的 TextBox 数据](../debugger/media/dbg-natvis-textbox-visualizer.png "DBG_NATVIS_TextBox_Visualizer")  

## <a name="BKMK_Using_Natvis_files"></a> 使用 Natvis 文件  
 .natvis 文件是具有 .natvis 扩展名的 XML 文件。 **%VSINSTALLDIR%\Xml\Schemas\natvis.xsd**中定义了架构。  

 .natvis 文件的基本结构是一个或多个 `Type` 元素，其中每个 `Type` 元素都表示某个类型的可视化条目，该类型在 `Name` 特性中指定了完全限定名称。  

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

 Visual Studio 在 **%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers** 文件夹中提供了一些 .natvis 文件。 这些文件包含许多通用类型的可视化规则，并且在你编写新类型的可视化效果时可作为示例。  

## <a name="adding-natvis-files-to-your-projects"></a>将 .natvis 文件添加到你的项目  
 可以将 .natvis 文件添加到任何 C++ 项目。  

 要添加新 .natvis 文件，请在打开的 C++ 项目中，选择“解决方案资源管理器” 中的项目节点，然后单击“添加”/“新建项”/“Visual C++”/“实用工具”/“调试器可视化文件 (.natvis)” 。 调试器将自动从 C++ 项目加载 Natvis 文件。 默认情况下，你项目中的 Natvis 文件还会插入到项目生成的 .pdb 文件中。 这表示如果调试此项目生成的的二进制文件，调试器将从 .pdb 加载 Natvis 文件，即使你没有打开该项目时也是如此。 如果不想将 .natvis 文件包含在 .pdb 中，右键单击“解决方案资源管理器”中的 .natvis 文件 ，然后在“配置属性”  窗口中将“从生成中排除”  设置为“是” 。  

 建议使用 Visual Studio 编辑 Natvis 文件。在调试时所做的任何更改均将在保存文件时自动生效。 还可从 IntelliSense 获得改善的编辑体验。  

 从 .pdb 加载的 Natvis 文件仅适用于 pdb 所引用的模块中的类型。 例如，如果 Module1.pdb 为名为 `Test`的类型定义一个条目，则此条目仅适用于 Module1.dll 中的 **Test** 类。 如果另一个模块还定义了一个名为 **Test**的类，则 Module1.pdb 的 natvis 条目将不适用于它。  

## <a name="BKMK_natvis_location"></a> 部署 .natvis 文件  
 如果 .natvis 文件仅适用于你在 Visual Studio 项目中创建的类型，则无需执行任何操作；该 .natvis 包含在 .pdb 中。 但你可以将 .natvis 文件添加到用户目录或系统目录（如果你希望它们适用于多个项目）。  

 评估 .natvis 文件顺序如下：  

1. 嵌入到你正在调试的 .pdb 中的 .natvis 文件（除非已加载的项目中有一个同名文件）  

2. 是已加载的 C++ 项目或顶级解决方案项的一部分的 .natvis 文件。 这包括所有已加载的 C++ 项目（包括类库），但不包括使用其他语言的项目（例如，不能从 C# 项目加载 .natvis 文件）。 对于可执行项目，应使用解决方案项托管任何尚不存在于 .pdb 中的 .natvis 文件，因为没有任何可用的 C++ 项目。  

3. 特定于用户的 natvis 目录 (**%USERPROFILE%\My Documents\Visual Studio 2015\Visualizers**)  

4. 系统级 Natvis 目录 (**%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers**)。 这就是复制随 Visual Studio 一起安装的 .natvis 文件的位置。 如果具有管理员权限，则也可以向此目录添加其他文件。  

## <a name="modifying-natvis-files-while-debugging"></a>在调试时，修改 .natvis 文件  
 可以在包含 .natvis 文件的项目中调试项目时修改 IDE 中的该文件。 打开 IDE 中的文件（使用正在调试的 Visual Studio 的相同实例）、对其进行修改并保存。 一旦保存了该文件，就应更新 **“监视”** 窗口和 **“局部变量”** 窗口以反映这些更改。 如果在 IDE 外部修改 .natvis 文件，则所做的更改不会自动生效。 若要更新窗口，可以评估“监视”  窗口中的 **.natvisreload** 命令。 这可使更改在无需重新启动调试会话的情况下生效。  

 还可以添加或删除正在调试的解决方案的 .natvis 文件，并且 Visual Studio 将添加或删除相关的可视化效果。  

 如果一个 .natvis 文件嵌入到 .pdb 中，则不能在调试时修改该文件。  

 将 natvis 文件升级到较新版本时（例如，如果它已签入源控件并且你想要选取其他人对文件所做的最新更改），请使用 **.natvisreload** 命令。 建议使用 Visual Studio XML 编辑器来编辑 natvis 文件。  

## <a name="BKMK_Expressions_and_formatting"></a> 表达式和格式化  
 Natvis 的可视化功能使用 C++ 表达式来指定要显示的数据项。 除了增强功能和限制的C++中所述的调试器中的表达式[上下文运算符 (C++)](../debugger/context-operator-cpp.md)，你应注意以下差异：  

- Natvis 表达式在可视化对象上下文而非当前堆栈框架中进行计算。 例如，如果在 Natvis 表达式中使用 `x` ，则它指的是可视化对象中名为 `x` 的字段，而非当前执行的函数中名为 `x` 的局部变量。 你可以访问全局变量，但不能访问 Natvis 表达式内的局部变量。  

- Natvis 表达式不允许函数求值或副作用。 这意味着函数调用和赋值运算符被忽略。 由于[调试器内部函数](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state)没有副作用，因此可以从任何 Natvis 表达式随意调用，即使系统不允许进行其他函数调用也是如此。  

  若要控制表达式在变量窗口中的显示方式，可以使用任何中所述的格式说明符[格式说明符](../debugger/format-specifiers-in-cpp.md#BKMK_Visual_Studio_2012_format_specifiers)一部分[中的格式说明符C++](../debugger/format-specifiers-in-cpp.md)主题。 请注意当虚拟化项供内部使用 Natvis，例如，将忽略格式说明符`Size`ArrayItems 扩展中的表达式。  

## <a name="natvis-views"></a>Natvis 视图  
 Natvis 视图允许你以多种方式查看任何类型。 例如，可以定义一个名为 **simple** 的视图，它为你提供一种类型的简化视图。 例如，下面是 `std::vector`的可视化效果：  

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

 `DisplayString` 和 `ArrayItems` 元素用于默认视图和简单视图中，虽然 `[size]` 和 `[capacity]` 项已从简单视图中排除。 可以使用 **,view** 格式说明符来指定替代视图。 在“监视”  窗口中，将简单视图指定为 **vec,view(simple)**：  

 ![具有简单视图的监视窗口](../debugger/media/watch-simpleview.png "监视 SimpleView")  

## <a name="BKMK_Diagnosing_Natvis_errors"></a> 诊断 Natvis 错误  
 可使用 Natvis 诊断来对语法和分析错误进行故障排除。 如果调试器在可视化条目中遇到错误，它将忽略这些错误，并显示原始形式的类型或选取其他适当的可视化效果。 若要了解某个可视化条目被忽略的原因并了解有哪些基础错误，可以打开 Natvis 诊断 **“工具”/“选项”/“调试”/“输出窗口”/“Natvis 诊断消息（仅适用于 C++）”** 选项。 错误都显示在 **“输出”** 窗口中。  

## <a name="BKMK_Syntax_reference"></a> Natvis 语法参考  

### <a name="BKMK_AutoVisualizer"></a> AutoVisualizer 元素  
 `AutoVisualizer`  元素是 .natvis 文件的根节点并包含命名空间 `xmlns:` 属性。  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">  
.  
.  
</AutoVisualizer>  
```  

### <a name="BKMK_Type"></a> Type 元素  
 一个基本类型如下所示：  

```xml  
<Type Name="[fully qualified type name]">  
  <DisplayString Condition="[Boolean expression]">[Display value]</DisplayString>  
  <Expand>  
    ...  
  </Expand>  
</Type>  

```  

 它指定：  

1. 应对此可视化效果使用哪种类型（ `Type Name` 属性）。  

2. 该类型的对象的值是什么样的（ `DisplayString` 元素）。  

3. 当用户在变量窗口（ `Expand` 节点）中展开类型的成员时，它们应如何显示。  

   **模板化类** `Name` 元素的 `Type` 特性接受一个星号 `*` 作为可用于模板化类名的通配符：  

```xml  
<Type Name="ATL::CAtlArray&lt;*&gt;">  
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>  
</Type>  

```  

 在此示例中，无论对象是 `CAtlArray<int>` 还是 `CAtlArray<float>`，都将使用相同的可视化效果。 如果存在 `CAtlArray<float>` 的特定可视化条目，则其优先于泛型条目。  

 请注意，可使用宏 $T1 和 $T2 等在可视化条目中引用模板参数。 要查找这些宏的示例，请参阅随 Visual Studio 一起提供的 .natvis 文件。  

#### <a name="BKMK_Visualizer_type_matching"></a> 可视化工具类型匹配  
 如果可视化条目无法进行验证，则使用下一个可用的可视化效果。  

#### <a name="inheritable-attribute"></a>可继承的特性  
 你可以指定某一可视化效果是仅适用于基类型还是适用于基类型和所有具有可选 `Inheritable` 特性的派生类型。 如下所示，可视化效果仅适用于 `BaseClass` 类型：  

```xml  
<Type Name="Namespace::BaseClass" Inheritable="true">  
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>  
</Type>  
```  

 `Inheritable` 的默认值为 `true`。  

#### <a name="priority-attribute"></a>优先级特性  
 `Priority` 特性指定某个定义无法分析时使用备用定义的顺序。 `Priority` 的可能的值是：`Low`、`MediumLow`、`Medium``MediumHigh` 和`High`，默认值是 `Medium`。  

 优先级特性应仅用于区分同一 .natvis 文件内的优先级，而非不同文件的优先级。  

 在下面的示例中，我们将首先分析与 2015 STL 匹配的条目，如果分析失败，则将使用 STL 的 2013 年版的备用条目：  

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

#### <a name="BKMK_Versioning"></a> Version 元素  
 使用 `Version` 元素将可视化效果的作用范围限定为特定模块及其版本，以便最大程度地减少名称冲突，并使不同的可视化效果可用于类型的不同版本。 例如：  

```xml  
<Type Name="DirectUI::Border">  
  <Version Name="Windows.UI.Xaml.dll" Min="1.0" Max="1.5"/>  
  <DisplayString>{{Name = {*(m_pDO->m_pstrName)}}}</DisplayString>  
  <Expand>  
    <ExpandedItem>*(CBorder*)(m_pDO)</ExpandedItem>  
  </Expand>  
</Type>  
```  

 在此示例中，可视化效果仅适用于在 1.0 至 1.5 版的 `DirectUI::Border` 中找到的 `Windows.UI.Xaml.dll` 类型。 请注意，添加版本元素时需将可视化条目的作用范围限定为特定模块及版本并且减少无意匹配，但如果类型在由不同模块使用的通用头文件中定义，则当类型不属于特定模块时，带有版本的可视化效果不适用。  

#### <a name="optional-attribute"></a>可选特性  
 `Optional` 特性可以出现在任何节点上。 如果无法分析可选节点内的任何子表达式，则忽略该节点，但其余 Type 元素仍然有效。 在下面的类型中， `[State]` 不可选，但 `[Exception]` 可选。  这表示，如果 `MyNamespace::MyClass` 包含一个名为 _`M_exceptionHolder`的字段，你将同时看到 `[State]` 节点和 `[Exception]` 节点；但如果 `_M_exceptionHolder` 缺失，则你将只看到 `[State]` 节点。  

```xml  
<Type Name="MyNamespace::MyClass">  
    <Expand>  
      <Item Name="[State]">_M_State</Item>  
      <Item Name="[Exception]" Optional="true">_M_exceptionHolder</Item>  
    </Expand>  
</Type>  
```  

### <a name="BKMK_Condition_attribute"></a> 条件属性  
 可选 `Condition` 属性可用于许多可视化元素并指定应何时使用可视化规则。 如果条件特性内的表达式解析为 `false`，则将不应用由该元素指定的可视化规则。 如果计算结果为 true，或如果没有 `Condition` 特性，则可视化规则被应用于该类型。 你可以借助此特性在可视化条目中使用 `if-else` 逻辑。 例如，下面的可视化效果具有智能指针类型的两个 `DisplayString` 元素：  

```xml  
<Type Name="std::auto_ptr&lt;*&gt;">  
  <DisplayString Condition="_Myptr == 0">empty</DisplayString>  
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>  
  <Expand>  
    <ExpandedItem>_Myptr</ExpandedItem>  
  </Expand>  
</Type>  

```  

 当 `_Myptr` 成员为 `null`时，第一个 `DisplayString` 元素的条件解析为 `true`，以便显示窗体。 当 `_Myptr` 成员不为 `null`时，条件的计算结果为 `false`，且显示第二个 `DisplayString` 元素。  

### <a name="includeview-and-excludeview-attributes"></a>IncludeView 和 ExcludeView 特性  
 这些特性指定是否在不同的视图中显示元素。 例如，已知 `std::vector`的 Natvis 规范：  

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

 简单视图不显示简单视图中的 [size] 和 [capacity] 项。 如果我们已使用 `IncludeView="simple"` 而不是 `ExcludeView`，则 `[size]` 和 `[capacity]` 项将显示在简单视图中而不是默认视图中。  

 你可以在类型以及单个成员上使用 `IncludeView` 和 `ExcludeView` 特性。  

### <a name="BKMK_DisplayString"></a> DisplayString  
 `DisplayString` 元素指定字符串显示为变量的值。 它接受混合表达式的任意字符串。 大括号内的所有内容都可解释为表达式。 例如， `DisplayString` 条目如下所示：  

```xml  
<Type Name="CPoint">  
  <DisplayString>{{x={x} y={y}}}</DisplayString>   
</Type>  

```  

 表示 `CPoint` 类型的变量如下所示：  

 ![使用 DisplayString 元素](../debugger/media/dbg-natvis-cpoint-displaystring.png "DBG_NATVIS_CPoint_DisplayString")  

 在 `DisplayString` 表达式中， `x` 和 `y`（ `CPoint`的成员）位于大括号内，因此可计算得出它们的值。 该表达式还演示如何通过使用双大括号（ `{{` 或 `}}` ）转义一个大括号。  

> [!NOTE]
> `DisplayString` 元素是唯一接受任意字符串和大括号语法的元素。 所有其他可视化元素只接受由调试器计算的表达式。  

### <a name="BKMK_StringView"></a> StringView  
 `StringView` 元素定义其值即将发送到内置文本可视化工具的表达式。 例如，假设我们拥有 `ATL::CStringT` 类型的以下可视化效果：  

```xml  
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">  
  <DisplayString>{m_pszData,su}</DisplayString>  
</Type>  

```  

 `CStringT` 对象类似于：  

 ![CStringT DisplayString 元素](../debugger/media/dbg-natvis-displaystring-cstringt.png "DBG_NATVIS_DisplayString_CStringT")  

 可视化效果可以在变量窗口中显示 `CStringT` 对象，如下所示：  

 添加 `StringView` 元素将向调试器指示此值可采用文本可视化方式进行查看：  

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">  
  <DisplayString>{m_pszData,su}</DisplayString>  
  <StringView>m_pszData,su</StringView>  
</Type>  
```  

 请注意显示于下方值旁边的放大镜图标。 选择图标将启动文本可视化工具，此工具将显示 `m_pszData` 指向的字符串。  

 ![使用 StringView 可视化工具的 CStringT 数据](../debugger/media/dbg-natvis-stringview-cstringt.png "DBG_NATVIS_StringView_CStringT")  

> [!NOTE]
> 请注意，表达式 `{m_pszData,su}` 包含 C++ 格式说明符 `su` ，可将值显示为 Unicode 字符串。 有关更多信息，请参见 [Format Specifiers in C++](../debugger/format-specifiers-in-cpp.md) 。  

### <a name="BKMK_Expand"></a> Expand  
 当用户在变量窗口中展开 `Expand` 节点时，它用于自定义该可视化类型的子级。 它接受定义子元素的子节点列表。  

 `Expand` 节点是可选的。  

- 如果未在可视化条目中指定 `Expand` 节点，则使用 Visual Studio 的默认展开规则。  

- 如果在类型下方无子节点的情况下指定 `Expand` 节点，将不会在调试器窗口中展开该类型。  

#### <a name="BKMK_Item_expansion"></a> Item 展开  
 `Item` 元素是用于 `Expand` 节点的最基本和最常见的元素。 `Item` 定义单个子元素。 例如，假设你拥有包含 `CRect` 、 `top`、 `left`和 `right`字段的 `bottom` 类以及以下可视化条目：  

```xml  
<Type Name="CRect">  
  <DisplayString>{{top={top} bottom={bottom} left={left} right={right}}}</DisplayString>  
  <Expand>  
    <Item Name="Width">right - left</Item>  
    <Item Name="Height">bottom - top</Item>  
  </Expand>  
</Type>  

```  

 `CRect` 类型将如下所示：  

 ![具有 Item 元素扩展的 CRect](../debugger/media/dbg-natvis-expand-item-crect1.png "DBG_NATVIS_Expand_Item_CRect1")  

 在 `Width` 和 `Height` 元素中指定的表达式在值列中计算并显示。 无论何时使用自定义展开，调试器都会自动创建 `[Raw View]` 节点。 它在上面的屏幕快照中展开，以显示对象的原始视图与其可视化效果的不同。 Visual Studio 默认展开创建基类的子树并列出基类的所有数据成员作为子级。  

> [!NOTE]
> 如果项元素的表达式指向一个复杂类型，则 `Item` 节点本身可展开。  

#### <a name="BKMK_ArrayItems_expansion"></a> Size  
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

 在变量窗口中展开时，`std::vector` 显示了它的各个元素：  

 ![使用 ArrayItems 扩展的 std:: vector](../debugger/media/dbg-natvis-expand-arrayitems-stdvector.png "DBG_NATVIS_Expand_ArrayItems_StdVector")  

 `ArrayItems` 节点至少必须具有：  

1. 用于使调试器了解数组长度的 `Size` 表达式（必须计算为整数）  

2. 应指向第一个元素（必须是非 `ValuePointer` 元素类型的指针）的 `void*`表达式。  

   数组下限的默认值为 0。 通过使用 `LowerBound` 元素（相关示例可在随 Visual Studio 一起提供的 .natvis 文件中找到）可以重写该值。  

   你现在可以联合使用 `[]` 运算符与 `ArrayItems` 扩展，例如 `vector[i]`。 [] 运算符可与使用 `ArrayItems` 或 `IndexListItems`的一维数组的任何可视化效果联合使用，即使该类型本身不允许此运算符（例如 `CATLArray`）。  

   还可以指定多维数组。 调试器只需稍多信息即可在这种情况下正确显示子元素：  

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

 `Direction` 指定数组是行优先顺序还是列优先顺序。 `Rank` 指定数组的秩。 `Size` 元素接受将其替换为维索引以查找该维度中数组的长度的隐式 `$i` 参数。 例如，在前面的示例中，表达式 `_M_extent.M_base[0]` 应指定第 0 个维度的长度， `_M_extent._M_base[1]` 应指定第 1 个维度的长度，依此类推。  

 下面是二维 `Concurrency::array` 对象在调试器中的显示效果：  

 ![具有 ArrayItems 扩展的二维数组](../debugger/media/dbg-natvis-expand-arrayitems-2d.png "DBG_NATVIS_Expand_ArrayItems_2D")  

#### <a name="BKMK_IndexListItems_expansion"></a> IndexListItems 展开  
 仅当数组元素在内存中连续排列时，才可使用 `ArrayItems` 扩展。 调试器通过将其指针递增到当前元素，即可到达下一个元素。 要支持需要操纵值节点索引的情况，可以使用 `IndexListItems` 节点。 下面是使用 `IndexListItems` 节点的可视化效果：  

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

 你现在可以联合使用 `[]` 运算符与 `IndexListItems` 扩展，例如 `vector[i]`。 `[]` 运算符可与使用 `ArrayItems` 或 `IndexListItems`的一维数组的任何可视化效果联合使用，即使该类型本身不允许此运算符（例如 `CATLArray`）。  

 `ArrayItems` 和 `IndexListItems` 之间的唯一区别是 `ValueNode` 期望具有隐式<sup>参数的 i</sup> th `$i` 元素的完整表达式。  

#### <a name="BKMK_LinkedListItems_expansion"></a> LinkedListItems 展开  
 如果可视化类型表示一个链接列表，则调试器可以通过使用 `LinkedListItems` 节点显示其子级。 下面是 `CAtlList` 类型使用此功能的可视化效果：  

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

- `NextPointer` 和 `ValueNode` 表达式将在链接列表节点元素的上下文（而非父列表类型）中计算。 在上面的示例中， `CAtlList` 具有表示链接列表节点的 `CNode` 类（可在 `atlcoll.h`中找到）。 `m_pNext` 和 `m_element` 为该 `CNode` 类的字段，而非 `CAtlList` 类的字段。  

- `ValueNode` 可以留空或使用 `this` 来引用链接列表节点自身。  

#### <a name="customlistitems-expansion"></a>CustomListItems 展开  
 借助 `CustomListItems` 展开，你可以编写自定义逻辑，用于遍历哈希表等数据结构。 应使用 `CustomListItems` 来实现数据结构的可视化，在此数据结构中，需要评估的所有内容都可通过 C++ 表达式表示，但不太适合 `ArrayItems`, `TreeItems`或 `LinkedListItems.`的模式  

 CAtlMap 的可视化工具是 `CustomListItems` 适用的一个精彩示例。  

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

#### <a name="BKMK_TreeItems_expansion"></a> TreeItems 展开  
 如果可视化类型表示一个树，则调试器可以通过使用 `TreeItems` 节点遍历该树并显示其子级。 下面是 `std::map` 类型使用此功能的可视化效果：  

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

 该语法非常类似于 `LinkedListItems` 节点。 `LeftPointer`、 `RightPointer`和 `ValueNode` 在树节点类的上下文中计算，且 `ValueNode` 可以留空或使用 `this` 来引用树节点自身。  

#### <a name="BKMK_ExpandedItem_expansion"></a> ExpandedItem 展开  
 通过显示基类或数据成员的属性（仿佛它们是该可视化类型的子级）， `ExpandedItem` 元素可用于生成合成子视图。 指定的表达式得到计算，结果的子节点被追加到该可视化类型的子列表。 例如，假设我们拥有智能指针类型 `auto_ptr<vector<int>>` ，此类型通常显示为：  

 ![自动&#95;ptr&#60;矢量&#60;int&#62; &#62;默认扩展](../debugger/media/dbg-natvis-expand-expandeditem-default.png "DBG_NATVIS_Expand_ExpandedItem_Default")  

 要查看矢量的值，你需要在变量窗口中经 _Myptr 成员深入两个级别。 通过添加 `ExpandedItem` 元素，可以消除层次结构中的 `_Myptr` 变量并直接查看矢量元素：  

```xml  
<Type Name="std::auto_ptr&lt;*&gt;">  
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>  
  <Expand>  
    <ExpandedItem>_Myptr</ExpandedItem>  
  </Expand>  
</Type>  

```  

 ![自动&#95;ptr&#60;矢量&#60;int&#62; &#62; ExpandedItem 扩展](../debugger/media/dbg-natvis-expand-expandeditem-visualized.png "DBG_NATVIS_Expand_ExpandedItem_Visualized")  

 下面的示例演示如何从派生类中的基类聚合属性。 假定 `CPanel` 类派生自 `CFrameworkElement`。 不重复来自基项 `CFrameworkElement` 类的属性，而是 `ExpandedItem` 节点允许这些属性追加到 `CPanel` 类的子列表。 关闭派生类的可视化匹配的 **nd** 格式说明符肯定在这。 否则，表达式 `*(CFrameworkElement*)this` 将导致再次应用 `CPanel` 可视化效果，因为默认可视化类型匹配规则认为它是最适合的选项。 如果基类没有可视化效果，则使用 **nd** 格式说明符指示调试器使用基类可视化效果或基类默认展开。  

```xml  
<Type Name="CPanel">  
  <DisplayString>{{Name = {*(m_pstrName)}}}</DisplayString>  
  <Expand>  
    <Item Name="IsItemsHost">(bool)m_bItemsHost</Item>  
    <ExpandedItem>*(CFrameworkElement*)this,nd</ExpandedItem>  
  </Expand>  
</Type>  

```  

#### <a name="BKMK_Synthetic_Item_expansion"></a> Synthetic Item 展开  
 `ExpandedItem` 元素通过消除层次结构提供更简单的数据视图， `Synthetic` 节点则恰好相反。 它允许你创建人工子元素（即，不是由表达式产生的子元素）。 此子元素可以包含其自身的子元素。 在下面的示例中， `Concurrency::array` 类型的可视化效果使用 `Synthetic` 节点向用户显示诊断消息：  

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

 ![具有 Sythentic 元素 expansio](../debugger/media/dbg-natvis-expand-synthetic.png "DBG_NATVIS_Expand_Synthetic")  

### <a name="BKMK_HResult"></a> HResult  
 `HResult` 元素允许你自定义为调试器窗口中的 HRESULT 显示的信息。 `HRValue` 元素必须包含要自定义的 HRESULT 的 32 位值。 `HRDescription` 元素包含在调试器中显示的信息。  

```  

<HResult Name="MY_E_COLLECTION_NOELEMENTS">  
  <HRValue>0xABC0123</HRValue>  
  <HRDescription>No elements in the collection.</HRDescription>  
</HResult>  
```  

### <a name="BKMK_UIVisualizer"></a> UIVisualizer  
 `UIVisualizer` 元素用于向调试器注册图形可视化工具插件。 图形可视化工具插件可用来创建对话框或其他界面，以一种适合于变量或对象数据类型的方式来显示变量或对象。 可视化工具插件必须编写为 [VSPackage](../extensibility/internals/vspackages.md) 并且需要公开可供调试器使用的服务。 .natvis 文件包含插件的注册信息，例如其名称、公开服务的 GUID 以及它可以直观显示的类型。  

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

 用于使调试器了解数组长度的 `UIVisualizer` 由 `ServiceId` - `Id` 属性对进行标识。 `ServiceId` 是可视化工具包公开的服务的 GUID， `Id` 是服务提供多个可视化工具时，可用于区分可视化工具的唯一标识符。 在上面的示例中，同一可视化工具服务可提供两个可视化工具。  

 `MenuName` 属性是用户打开调试器变量窗口中放大镜图标旁边的下拉菜单时看到的可视化工具名称，例如：  

 ![UIVisualizer 菜单快捷方式菜单](../debugger/media/dbg-natvis-vectorvisualizer.png "DBG_NATVIS_VectorVisualizer")  

 在 .natvis 文件中定义的每个类型都必须显式列出可显示它们的 UI 可视化工具。 调试器会匹配类型条目中的可视化工具引用，以便将类型与注册的可视化工具进行匹配。 例如， `std::vector` 的以下类型条目引用了上述示例中的 UIVisualizer。  

```xml
<Type Name="std::vector&lt;int,*&gt;">  
  <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}" Id="1" />  
</Type>  
```  

 可以看到用于查看内存中的位图的图像监视扩展中 UIVisualizer 的示例：[ImageWatch](https://visualstudiogallery.msdn.microsoft.com/e682d542-7ef3-402c-b857-bbfba714f78d)  

### <a name="customvisualizer-element"></a>CustomVisualizer 元素  
 `CustomVisualizer` 是一个扩展点，它指定 VSIX 扩展，可编写此扩展来控制在 Visual Studio 中运行的代码中的可视化效果。 有关编写 VSIX 扩展的详细信息，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。 编写自定义可视化工具的工作量比编写 XML natvis 定义大得多，但你不会受到 natvis 所支持的内容或不支持的内容的约束。 自定义可视化工具有权访问调试器扩展性 API 的全集，调试器扩展性 API 可用于查询和修改调试对象进程或与 Visual Studio 的其他部件进行通信。  

 可在 CustomVisualizer 元素上使用 `Condition`、 `IncludeView`和 `ExcludeView` 特’性。

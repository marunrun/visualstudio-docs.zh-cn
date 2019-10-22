---
title: EditorConfig 适用的 .NET 语言约定
ms.date: 09/23/2019
ms.topic: reference
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- language code style rules [EditorConfig]
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: e4f49df2c775bc3bb95888d76da133898ab9c76e
ms.sourcegitcommit: 88f576ac32af31613c1a10c1548275e1ce029f4f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71186530"
---
# <a name="language-conventions"></a>语言约定

Visual Studio 中 EditorConfig 的语言约定分为两类：适用于 Visual Basic 和 C# 的约定，以及特定于 C# 的约定。 语言约定会影响编程语言的各个方面的使用方式，例如修饰符和括号。

> [!TIP]
> - 若要查看以首选编程语言编写的代码示例，请使用浏览器窗口右上角的语言选取器选择它。
>
>   ![代码语言选取器控件](media/code-language-picker.png)
>
> - 使用“本文中”链接跳转到页面的不同部分  。

## <a name="rule-format"></a>规则格式

语言约定的规则具有以下常规格式：

`option_name = value:severity`

对于每个语言约定，可指定一个定义是否或何时以此样式为首选项的值。 许多规则都接受 `true` 值（以此样式为首选项）或 `false` 值（不以此样式为首选项）。 其他规则接受 `when_on_single_line` 或 `never` 等值。 此规则的第二部分指定[严重性](#severity-levels)。

::: moniker range=">=vs-2019"

> [!NOTE]
> 由于语言约定由分析器强制执行，因此还可以使用分析器的默认配置语法来设置其严重性。 语法采用形式 `dotnet_diagnostic.<rule ID>.severity = <severity>`（例如，`dotnet_diagnostic.IDE0040.severity = silent`）。 有关详细信息，请参阅[在 EditorConfig 文件中设置规则严重性](../code-quality/use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)。

::: moniker-end

## <a name="severity-levels"></a>严重性级别

语言约定严重性指定在哪个级别执行该样式。 下表列出了可能的严重性值及其效果：

Severity | 效果
:------- | ------
`error` | 如违反此样式规则，显示编译器错误。
`warning` | 如违反此样式规则，显示编译器警告。
`suggestion` | 如违反此样式规则，会将其作为建议向用户显示。 建议显示为前两个字符下的三个灰点。
`silent` | 如违反此规则，不会向用户显示任何内容。 但代码生成功能会以此样式生成代码。 严重性为 `silent` 的规则参与清理，并在“快速操作和重构”菜单中显示  。
`none` | 如违反此规则，不会向用户显示任何内容。 但代码生成功能会以此样式生成代码。 “快速操作和重构”菜单中永远不会出现严重性为 `none` 的规则  。 大多数情况下，此情况被视为“禁用”或“忽略”。

::: moniker range=">=vs-2019"

## <a name="automatically-configure-code-styles"></a>自动配置代码样式

自 Visual Studio 2019 版本 16.3 起，在样式冲突发生之后，可以在[快速操作](quick-actions.md)灯泡菜单中配置代码样式规则。

更改代码样式约定：

1. 将鼠标悬停在编辑器中的波浪线上，然后打开显示的灯泡菜单。 选择“配置或取消”问题 > “配置 \<规则 ID> 代码样式”   。

   ![在 Visual Studio 的灯泡菜单中配置代码样式](media/vs-2019/configure-code-style.png)

2. 请在此处选择其中某个代码样式选项。

   ![配置代码样式设置](media/vs-2019/configure-code-style-setting.png)

   Visual Studio 在 EditorConfig 文件中添加或修改配置设置，如预览框中所示。

若要更改代码样式冲突的严重性，请执行相同的步骤，但请选择“配置 \<规则 ID > 严重性”，而不选择“配置 \<规则 ID > 代码样式”   。 有关详细信息，请参阅[自动配置规则严重性](../code-quality/use-roslyn-analyzers.md#automatically-configure-rule-severity)。

::: moniker-end

## <a name="net-code-style-settings"></a>.NET 代码样式设置

本节中的样式规则均适用于 C# 和 Visual Basic。

- [“This.”和“Me.”限定符](#this-and-me)
  - dotnet\_style\_qualification\_for_field
  - dotnet\_style\_qualification\_for_property
  - dotnet\_style\_qualification\_for_method
  - dotnet\_style\_qualification\_for_event
- [语言关键字，而非类型引用的框架类型名称](#language-keywords)
  - dotnet\_style\_predefined\_type\_for\_locals\_parameters_members
  - dotnet\_style\_predefined\_type\_for\_member_access
- [修饰符首选项](#normalize-modifiers)
  - dotnet\_style\_require\_accessibility_modifiers
  - csharp\_preferred\_modifier_order
  - visual\_basic\_preferred\_modifier_order
  - dotnet\_style\_readonly\_field
- [括号首选项](#parentheses-preferences)
  - dotnet\_style\_parentheses\_in\_arithmetic\_binary\_operators
  - dotnet\_style\_parentheses\_in\_other\_binary\_operators
  - dotnet\_style\_parentheses\_in\_other\_operators
  - dotnet\_style\_parentheses\_in\_relational\_binary\_operators
- [表达式级首选项](#expression-level-preferences)
  - dotnet\_style\_object_initializer
  - dotnet\_style\_collection_initializer
  - dotnet\_style\_explicit\_tuple_names
  - dotnet\_style\_prefer\_inferred\_tuple_names
  - dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names
  - dotnet\_style\_prefer\_auto\_properties
  - dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method
  - dotnet\_style\_prefer\_conditional\_expression\_over\_assignment
  - dotnet\_style\_prefer\_conditional\_expression\_over\_return
  - dotnet\_style\_prefer\_compound\_assignment
- [“NULL”检查首选项](#null-checking-preferences)
  - dotnet\_style\_coalesce_expression
  - dotnet\_style\_null_propagation

### <a name="this-and-me"></a>“This.” 和“Me.” 限定符

此样式规则可应用于字段、属性、方法或事件。 值为“true”表示代码符号以 `this.` (C#) 或 `Me.` (Visual Basic) 开头为首选项  。 值为“false”表示码位元素不以 `this.` 或 `Me.` 开头为首选项   。

这些规则可在 .editorconfig 文件中以如下方式出现  ：

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_qualification_for_field = false:suggestion
dotnet_style_qualification_for_property = false:suggestion
dotnet_style_qualification_for_method = false:suggestion
dotnet_style_qualification_for_event = false:suggestion
```

#### <a name="dotnet_style_qualification_for_field"></a>dotnet\_style\_qualification\_for_field

|||
|-|-|
| **规则名称** | dotnet_style_qualification_for_field |
| **规则 ID** | IDE0003 和 IDE0009 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 字段以 `this.` (C#) 或 `Me.` (Visual Basic) 开头为首选项<br /><br />`false` - 字段不以 `this.` 或 `Me.` 开头为首选项  |
| **Visual Studio 默认值** | `false:silent` |

代码示例：

```csharp
// dotnet_style_qualification_for_field = true
this.capacity = 0;

// dotnet_style_qualification_for_field = false
capacity = 0;
```

```vb
' dotnet_style_qualification_for_field = true
Me.capacity = 0

' dotnet_style_qualification_for_field = false
capacity = 0
```

#### <a name="dotnet_style_qualification_for_property"></a>dotnet\_style\_qualification\_for_property

|||
|-|-|
| **规则名称** | dotnet_style_qualification_for_property |
| **规则 ID** | IDE0003 和 IDE0009 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 属性以 `this.` (C#) 或 `Me.` (Visual Basic) 开头为首选项<br /><br />`false` - 属性不以 `this.` 或 `Me.` 开头为首选项  |
| **Visual Studio 默认值** | `false:silent` |

代码示例：

```csharp
// dotnet_style_qualification_for_property = true
this.ID = 0;

// dotnet_style_qualification_for_property = false
ID = 0;
```

```vb
' dotnet_style_qualification_for_property = true
Me.ID = 0

' dotnet_style_qualification_for_property = false
ID = 0
```

#### <a name="dotnet_style_qualification_for_method"></a>dotnet\_style\_qualification\_for_method

|||
|-|-|
| **规则名称** | dotnet_style_qualification_for_method |
| **规则 ID** | IDE0003 和 IDE0009 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 方法以 `this.` (C#) 或 `Me.` (Visual Basic) 开头为首选项。<br /><br />`false` - 方法不以 `this.` 或 `Me.` 开头为首选项  。 |
| **Visual Studio 默认值** | `false:silent` |

代码示例：

```csharp
// dotnet_style_qualification_for_method = true
this.Display();

// dotnet_style_qualification_for_method = false
Display();
```

```vb
' dotnet_style_qualification_for_method = true
Me.Display()

' dotnet_style_qualification_for_method = false
Display()
```

#### <a name="dotnet_style_qualification_for_event"></a>dotnet\_style\_qualification\_for_event

|||
|-|-|
| **规则名称** | dotnet_style_qualification_for_event |
| **规则 ID** | IDE0003 和 IDE0009 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 事件以 `this.` (C#) 或 `Me.` (Visual Basic) 开头为首选项。<br /><br />`false` - 事件不以 `this.` 或 `Me.` 开头为首选项  。 |
| **Visual Studio 默认值** | `false:silent` |

代码示例：

```csharp
// dotnet_style_qualification_for_event = true
this.Elapsed += Handler;

// dotnet_style_qualification_for_event = false
Elapsed += Handler;
```

```vb
' dotnet_style_qualification_for_event = true
AddHandler Me.Elapsed, AddressOf Handler

' dotnet_style_qualification_for_event = false
AddHandler Elapsed, AddressOf Handler
```

### <a name="language-keywords"></a>语言关键字，而非类型引用的框架类型名称

此样式规则可应用到本地变量、方法参数和类成员，也可作为针对类型成员访问表达式的单独规则。 值为“true”  表示，如果类型中有用于表示类型的关键字，首选语言关键字（例如 `int` 或 `Integer`），而不是类型名称（例如 `Int32`）。 值为“false”代表类型名称为首选项，而非语言关键字  。

这些规则可在 .editorconfig 文件中以如下方式出现  ：

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_predefined_type_for_locals_parameters_members = true:suggestion
dotnet_style_predefined_type_for_member_access = true:suggestion
```

#### <a name="dotnet_style_predefined_type_for_locals_parameters_members"></a>dotnet\_style\_predefined\_type\_for\_locals\_parameters_members

|||
|-|-|
| **规则名称** | dotnet_style_predefined_type_for_locals_parameters_members |
| **规则 ID** | IDE0012 和 IDE0014 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 对于类型（其中具有用于表示该类型的关键字），本地变量、方法参数和类成员的语言关键字为首选项，而非类型名称<br /><br />`false` - 本地变量、方法参数和类成员的类型名称为首选项，而非语言关键字 |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// dotnet_style_predefined_type_for_locals_parameters_members = true
private int _member;

// dotnet_style_predefined_type_for_locals_parameters_members = false
private Int32 _member;
```

```vb
' dotnet_style_predefined_type_for_locals_parameters_members = true
Private _member As Integer

' dotnet_style_predefined_type_for_locals_parameters_members = false
Private _member As Int32
```

#### <a name="dotnet_style_predefined_type_for_member_access"></a>dotnet\_style\_predefined\_type\_for\_member_access

|||
|-|-|
| **规则名称** | dotnet_style_predefined_type_for_member_access |
| **规则 ID** | IDE0013 和 IDE0015 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 对于类型（其中具有用于表示该类型的关键字），成员访问表达式的语言关键字为首选项，而非类型名称<br /><br />`false` - 成员访问表达式的类型名称为首选项，而非语言关键字 |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// dotnet_style_predefined_type_for_member_access = true
var local = int.MaxValue;

// dotnet_style_predefined_type_for_member_access = false
var local = Int32.MaxValue;
```

```vb
' dotnet_style_predefined_type_for_member_access = true
Dim local = Integer.MaxValue

' dotnet_style_predefined_type_for_member_access = false
Dim local = Int32.MaxValue
```

### <a name="normalize-modifiers"></a>修饰符首选项

本部分中的样式规则与修饰符首选项相关，包括要求使用可访问性修饰符、指定所需的修饰符排序顺序以及要求使用只读修饰符。

这些规则可在 .editorconfig 文件中以如下方式出现  ：

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_require_accessibility_modifiers = always:suggestion
dotnet_style_readonly_field = true:warning

# CSharp code style settings:
[*.cs]
csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async:suggestion

# Visual Basic code style settings:
[*.vb]
visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async:suggestion
```

#### <a name="dotnet_style_require_accessibility_modifiers"></a>dotnet\_style\_require\_accessibility_modifiers

|||
|-|-|
| **规则名称** | dotnet_style_require_accessibility_modifiers |
| **规则 ID** | IDE0040 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `always` - 优先指定可访问性修饰符。<br /><br />`for_non_interface_members` - 优先声明可访问性修饰符，公共接口成员除外。 （这与往常相同，并且已添加以用于未来验证（如果 C# 添加默认接口方法）  。）<br /><br />`never` - 不优先指定可访问性修饰符。<br /><br />`omit_if_default` - 优先指定可访问性修饰符（除非它们是默认修饰符）。 |
| **Visual Studio 默认值** | `for_non_interface_members:silent` |
| **引入的版本** | Visual Studio 2017 版本 15.5 |

代码示例：

```csharp
// dotnet_style_require_accessibility_modifiers = always
// dotnet_style_require_accessibility_modifiers = for_non_interface_members
class MyClass
{
    private const string thisFieldIsConst = "constant";
}

// dotnet_style_require_accessibility_modifiers = never
class MyClass
{
    const string thisFieldIsConst = "constant";
}
```

#### <a name="csharp_preferred_modifier_order"></a>csharp_preferred_modifier_order

|||
|-|-|
| **规则名称** | csharp_preferred_modifier_order |
| **规则 ID** | IDE0036 |
| **适用的语言** | C# |
| **值** | 一个或多个 C# 修饰符，如 `public`、`private` 和 `protected` |
| **Visual Studio 默认值** | `public, private, protected, internal, static, extern, new, virtual, abstract, sealed, override, readonly, unsafe, volatile, async:silent` |
| **引入的版本** | Visual Studio 2017 版本 15.5 |

- 如果对一系列修饰符设置该规则，则首选指定的排序。
- 如果文件中省略了此规则，则不优先使用修饰符顺序。

代码示例：

```csharp
// csharp_preferred_modifier_order = public,private,protected,internal,static,extern,new,virtual,abstract,sealed,override,readonly,unsafe,volatile,async
class MyClass
{
    private static readonly int _daysInYear = 365;
}
```

#### <a name="visual_basic_preferred_modifier_order"></a>visual_basic_preferred_modifier_order

|||
|-|-|
| **规则名称** | visual_basic_preferred_modifier_order |
| **规则 ID** | IDE0036 |
| **适用的语言** | Visual Basic |
| **值** | 一个或多个 Visual Basic 修饰符，如 `Partial`、`Private` 和 `Public` |
| **Visual Studio 默认值** | `Partial, Default, Private, Protected, Public, Friend, NotOverridable, Overridable, MustOverride, Overloads, Overrides, MustInherit, NotInheritable, Static, Shared, Shadows, ReadOnly, WriteOnly, Dim, Const,WithEvents, Widening, Narrowing, Custom, Async:silent` |
| **引入的版本** | Visual Studio 2017 版本 15.5 |

- 如果对一系列修饰符设置该规则，则首选指定的排序。
- 如果文件中省略了此规则，则不优先使用修饰符顺序。

代码示例：

```vb
' visual_basic_preferred_modifier_order = Partial,Default,Private,Protected,Public,Friend,NotOverridable,Overridable,MustOverride,Overloads,Overrides,MustInherit,NotInheritable,Static,Shared,Shadows,ReadOnly,WriteOnly,Dim,Const,WithEvents,Widening,Narrowing,Custom,Async
Public Class MyClass
    Private Shared ReadOnly daysInYear As Int = 365
End Class
```

#### <a name="dotnet_style_readonly_field"></a>dotnet_style_readonly_field

|||
|-|-|
| **规则名称** | dotnet_style_readonly_field |
| **规则 ID** | IDE0044 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 如果字段只是内联分配或者在构造函数中，偏向将它们标记为 `readonly` (C#) 或 `ReadOnly` (Visual Basic) 的字段<br /><br />`false` - 就字段是否应标记为 `readonly` (C#) 或 `ReadOnly` (Visual Basic) 无偏向 |
| **Visual Studio 默认值** | `true:suggestion` |
| **引入的版本** | Visual Studio 2017 15.7 版 |

代码示例：

```csharp
// dotnet_style_readonly_field = true
class MyClass
{
    private readonly int _daysInYear = 365;
}
```

```vb
' dotnet_style_readonly_field = true
Public Class MyClass
    Private ReadOnly daysInYear As Int = 365
End Class
```

### <a name="parentheses-preferences"></a>括号首选项

本部分中的样式规则涉及括号首选项，包括算术、关系和其他二元运算符的括号使用情况。

这些规则可在 .editorconfig 文件中以如下方式出现  ：

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_binary_operators = always_for_clarity:silent
dotnet_style_parentheses_in_other_operators = never_if_unnecessary:silent
```

#### <a name="dotnet_style_parentheses_in_arithmetic_binary_operators"></a>dotnet\_style\_parentheses\_in\_arithmetic\_binary_operators

|||
|-|-|
| **规则名称** | dotnet_style_parentheses_in_arithmetic_binary_operators |
| **规则 ID** | IDE0047 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `always_for_clarity` - 优先使用括号来声明算术运算符（`*`、`/`、`%`、`+`、`-`、`<<`、`>>`、`&`、`^`、`|`）优先级<br /><br />`never_if_unnecessary` - 算术运算符（`*`、`/`、`%`、`+`、`-`、`<<`、`>>`、`&`、`^`、`|`）的优先级显而易见时，最好不要使用括号 |
| **Visual Studio 默认值** | `always_for_clarity:silent` |
| **引入的版本** | Visual Studio 2017 版本 15.8 |

代码示例：

```csharp
// dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity
var v = a + (b * c);

// dotnet_style_parentheses_in_arithmetic_binary_operators = never_if_unnecessary
var v = a + b * c;
```

```vb
' dotnet_style_parentheses_in_arithmetic_binary_operators = always_for_clarity
Dim v = a + (b * c)

' dotnet_style_parentheses_in_arithmetic_binary_operators = never_if_unnecessary
Dim v = a + b * c
```

#### <a name="dotnet_style_parentheses_in_relational_binary_operators"></a>dotnet\_style\_parentheses\_in\_relational\_binary_operators

|||
|-|-|
| **规则名称** | dotnet_style_parentheses_in_relational_binary_operators |
| **规则 ID** | IDE0047 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `always_for_clarity` - 优先使用括号来声明关系运算符（`>`、`<`、`<=`、`>=`、`is`、`as`、`==`、`!=`）优先级<br /><br />`never_if_unnecessary` - 关系运算符（`>`、`<`、`<=`、`>=`、`is`、`as`、`==`、`!=`）的优先级显而易见时，最好不要使用括号 |
| **Visual Studio 默认值** | `always_for_clarity:silent` |
| **引入的版本** | Visual Studio 2017 版本 15.8 |

代码示例：

```csharp
// dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity
var v = (a < b) == (c > d);

// dotnet_style_parentheses_in_relational_binary_operators = never_if_unnecessary
var v = a < b == c > d;
```

```vb
' dotnet_style_parentheses_in_relational_binary_operators = always_for_clarity
Dim v = (a < b) = (c > d)

' dotnet_style_parentheses_in_relational_binary_operators = never_if_unnecessary
Dim v = a < b = c > d
```

#### <a name="dotnet_style_parentheses_in_other_binary_operators"></a>dotnet\_style\_parentheses\_in\_other\_binary_operators

|||
|-|-|
| **规则名称** | dotnet_style_parentheses_in_other_binary_operators |
| **规则 ID** | IDE0047 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `always_for_clarity` - 优先使用括号来声明其他二元运算符（`&&`、`||`、`??`）优先级<br /><br />`never_if_unnecessary` - 其他二元运算符（`&&`、`||`、`??`）的优先级显而易见时，最好不要使用括号 |
| **Visual Studio 默认值** | `always_for_clarity:silent` |
| **引入的版本** | Visual Studio 2017 版本 15.8 |

代码示例：

```csharp
// dotnet_style_parentheses_in_other_binary_operators = always_for_clarity
var v = a || (b && c);

// dotnet_style_parentheses_in_other_binary_operators = never_if_unnecessary
var v = a || b && c;
```

```vb
' dotnet_style_parentheses_in_other_binary_operators = always_for_clarity
Dim v = a OrElse (b AndAlso c)

' dotnet_style_parentheses_in_other_binary_operators = never_if_unnecessary
Dim v = a OrElse b AndAlso c
```

#### <a name="dotnet_style_parentheses_in_other_operators"></a>dotnet\_style\_parentheses\_in\_other_operators

|||
|-|-|
| **规则名称** | dotnet_style_parentheses_in_other_operators |
| **规则 ID** | IDE0047 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `always_for_clarity` - 优先使用括号来声明运算符先级<br /><br />`never_if_unnecessary` - 运算符的优先级显而易见时，最好不要使用括号 |
| **Visual Studio 默认值** | `never_if_unnecessary:silent` |
| **引入的版本** | Visual Studio 2017 版本 15.8 |

代码示例：

```csharp
// dotnet_style_parentheses_in_other_operators = always_for_clarity
var v = (a.b).Length;

// dotnet_style_parentheses_in_other_operators = never_if_unnecessary
var v = a.b.Length;
```

```vb
' dotnet_style_parentheses_in_other_operators = always_for_clarity
Dim v = (a.b).Length

' dotnet_style_parentheses_in_other_operators = never_if_unnecessary
Dim v = a.b.Length
```

### <a name="expression-level-preferences"></a>表达式级首选项

本节中的样式规则与表达式级别首选项有关，包括对象初始值设定项、集合初始值设定项、显式或推断元组名称和推断匿名类型的使用。

这些规则可在 .editorconfig 文件中以如下方式出现  ：

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_prefer_inferred_tuple_names = true:suggestion
dotnet_style_prefer_inferred_anonymous_type_member_names = true:suggestion
dotnet_style_prefer_auto_properties = true:silent
dotnet_style_prefer_conditional_expression_over_assignment = true:suggestion
dotnet_style_prefer_conditional_expression_over_return = true:suggestion
dotnet_style_prefer_compound_assignment = true:suggestion
```

#### <a name="dotnet_style_object_initializer"></a>dotnet\_style\_object_initializer

|||
|-|-|
| **规则名称** | dotnet_style_object_initializer |
| **规则 ID** | IDE0017 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 在可能情况下，更倾向使用对象初始值设定项来初始化对象<br /><br />`false` - 更倾向不使用对象初始值设定项来初始化对象  |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// dotnet_style_object_initializer = true
var c = new Customer() { Age = 21 };

// dotnet_style_object_initializer = false
var c = new Customer();
c.Age = 21;
```

```vb
' dotnet_style_object_initializer = true
Dim c = New Customer() With {.Age = 21}

' dotnet_style_object_initializer = false
Dim c = New Customer()
c.Age = 21
```

#### <a name="dotnet_style_collection_initializer"></a>dotnet\_style\_collection_initializer

|||
|-|-|
| **规则名称** | dotnet_style_collection_initializer |
| **规则 ID** | IDE0028 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 在可能情况下，更倾向使用集合初始值设定项来初始化集合<br /><br />`false` - 不使用集合初始值设定项来初始化集合为首选项  |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// dotnet_style_collection_initializer = true
var list = new List<int> { 1, 2, 3 };

// dotnet_style_collection_initializer = false
var list = new List<int>();
list.Add(1);
list.Add(2);
list.Add(3);
```

```vb
' dotnet_style_collection_initializer = true
Dim list = New List(Of Integer) From {1, 2, 3}

' dotnet_style_collection_initializer = false
Dim list = New List(Of Integer)
list.Add(1)
list.Add(2)
list.Add(3)
```

#### <a name="dotnet_style_explicit_tuple_names"></a>dotnet\_style\_explicit\_tuple_names

|||
|-|-|
| **规则名称** | dotnet_style_explicit_tuple_names |
| **规则 ID** | IDE0033 |
| **适用的语言** | C# 7.0+ 和 Visual Basic 15+ |
| **值** | `true` - 比起 ItemX 属性更倾向元祖名称<br /><br />`false` - 比起元组名称更倾向 ItemX 属性 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// dotnet_style_explicit_tuple_names = true
(string name, int age) customer = GetCustomer();
var name = customer.name;

// dotnet_style_explicit_tuple_names = false
(string name, int age) customer = GetCustomer();
var name = customer.Item1;
```

```vb
 ' dotnet_style_explicit_tuple_names = true
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.name

' dotnet_style_explicit_tuple_names = false
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.Item1
```

#### <a name="dotnet_style_prefer_inferred_tuple_names"></a>dotnet\_style\_prefer\_inferred\_tuple_names

|||
|-|-|
| **规则名称** | dotnet_style_prefer_inferred_tuple_names |
| **规则 ID** | IDE0037 |
| **适用的语言** | C# 7.1+ 和 Visual Basic 15+ |
| **值** | `true` - 首选推断元组元素名称<br /><br />`false` - 首选显式元组元素名称 |
| **Visual Studio 默认值** | `true:suggestion` |
| **引入的版本** | Visual Studio 2017 版本 15.6 |

代码示例：

```csharp
// dotnet_style_prefer_inferred_tuple_names = true
var tuple = (age, name);

// dotnet_style_prefer_inferred_tuple_names = false
var tuple = (age: age, name: name);
```

```vb
' dotnet_style_prefer_inferred_tuple_names = true
Dim tuple = (name, age)

' dotnet_style_prefer_inferred_tuple_names = false
Dim tuple = (name:=name, age:=age)
```

#### <a name="dotnet_style_prefer_inferred_anonymous_type_member_names"></a>dotnet\_style\_prefer\_inferred\_anonymous\_type\_member_names

|||
|-|-|
| **规则名称** | dotnet_style_prefer_inferred_anonymous_type_member_names |
| **规则 ID** | IDE0037 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 首选推断匿名类型成员名称<br /><br />`false` - 首选显式匿名类型成员名称 |
| **Visual Studio 默认值** | `true:suggestion` |
| **引入的版本** | Visual Studio 2017 版本 15.6 |

代码示例：

```csharp
// dotnet_style_prefer_inferred_anonymous_type_member_names = true
var anon = new { age, name };

// dotnet_style_prefer_inferred_anonymous_type_member_names = false
var anon = new { age = age, name = name };
```

```vb
' dotnet_style_prefer_inferred_anonymous_type_member_names = true
Dim anon = New With {name, age}

' dotnet_style_prefer_inferred_anonymous_type_member_names = false
Dim anon = New With {.name = name, .age = age}
```

#### <a name="dotnet_style_prefer_auto_properties"></a>dotnet\_style\_prefer\_auto\_properties

|||
|-|-|
| **规则名称** | dotnet_style_prefer_auto_properties |
| **规则 ID** | IDE0032 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 首选自动属性，而不是包含专用支持字段的属性<br /><br />`false` - 首选包含专用支持字段的属性，而不是自动属性 |
| **Visual Studio 默认值** | `true:suggestion` |
| **引入的版本** | Visual Studio 2017 15.7 版 |

代码示例：

```csharp
// dotnet_style_prefer_auto_properties = true
private int Age { get; }

// dotnet_style_prefer_auto_properties = false
private int age;

public int Age
{
    get
    {
        return age;
    }
}
```

```vb
' dotnet_style_prefer_auto_properties = true
Public ReadOnly Property Age As Integer

' dotnet_style_prefer_auto_properties = false
Private _age As Integer

Public ReadOnly Property Age As Integer
    Get
        return _age
    End Get
End Property
```

#### <a name="dotnet_style_prefer_is_null_check_over_reference_equality_method"></a>dotnet\_style\_prefer\_is\_null\_check\_over\_reference\_equality\_method

|||
|-|-|
| **规则名称** | dotnet_style_prefer_is_null_check_over_reference_equality_method |
| **规则 ID** | IDE0041 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 相对于 `object.ReferenceEquals`，优先使用通过模式匹配进行 null 检查<br /><br />`false` - 相对于通过模式匹配进行 null 检查，优先使用 `object.ReferenceEquals` |
| **Visual Studio 默认值** | `true:suggestion` |
| **引入的版本** | Visual Studio 2017 15.7 版 |

代码示例：

```csharp
// dotnet_style_prefer_is_null_check_over_reference_equality_method = true
if (value is null)
    return;

// dotnet_style_prefer_is_null_check_over_reference_equality_method = false
if (object.ReferenceEquals(value, null))
    return;
```

```vb
' dotnet_style_prefer_is_null_check_over_reference_equality_method = true
If value Is Nothing
    Return
End If

' dotnet_style_prefer_is_null_check_over_reference_equality_method = false
If Object.ReferenceEquals(value, Nothing)
    Return
End If
```

#### <a name="dotnet_style_prefer_conditional_expression_over_assignment"></a>dotnet\_style\_prefer\_conditional\_expression\_over_assignment

|||
|-|-|
| **规则名称** | dotnet_style_prefer_conditional_expression_over_assignment |
| **规则 ID** | IDE0045 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 与 if-else 语句相比，首选三元条件进行赋值<br /><br />`false` - 与三元条件相比，首选 if-else 语句进行赋值 |
| **Visual Studio 默认值** | `true:suggestion` |
| **引入的版本** | Visual Studio 2017 版本 15.8 |

代码示例：

```csharp
// dotnet_style_prefer_conditional_expression_over_assignment = true
string s = expr ? "hello" : "world";

// dotnet_style_prefer_conditional_expression_over_assignment = false
string s;
if (expr)
{
    s = "hello";
}
else
{
    s = "world";
}
```

```vb
' dotnet_style_prefer_conditional_expression_over_assignment = true
Dim s As String = If(expr, "hello", "world")

' dotnet_style_prefer_conditional_expression_over_assignment = false
Dim s As String
If expr Then
    s = "hello"
Else
    s = "world"
End If
```

#### <a name="dotnet_style_prefer_conditional_expression_over_return"></a>dotnet\_style\_prefer\_conditional\_expression\_over_return

|||
|-|-|
| **规则名称** | dotnet_style_prefer_conditional_expression_over_return |
| **规则 ID** | IDE0046 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 与 if-else 语句相比，return 语句首选三元条件<br /><br />`false` - 与三元条件相比，return 语句首选 if-else 语句 |
| **Visual Studio 默认值** | `true:suggestion` |
| **引入的版本** | Visual Studio 2017 版本 15.8 |

代码示例：

```csharp
// dotnet_style_prefer_conditional_expression_over_return = true
return expr ? "hello" : "world"

// dotnet_style_prefer_conditional_expression_over_return = false
if (expr)
{
    return "hello";
}
else
{
    return "world";
}
```

```vb
' dotnet_style_prefer_conditional_expression_over_return = true
Return If(expr, "hello", "world")

' dotnet_style_prefer_conditional_expression_over_return = false
If expr Then
    Return "hello"
Else
    Return "world"
End If
```

#### <a name="dotnet_style_prefer_compound_assignment"></a>dotnet\_style\_prefer\_compound\_assignment

|||
|-|-|
| **规则名称** | dotnet_style_prefer_compound_assignment |
| **规则 ID** | IDE0054 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 首选[复合赋值](/dotnet/csharp/language-reference/operators/assignment-operator#compound-assignment)表达式<br /><br />`false` - 不推荐使用复合赋值表达式 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// dotnet_style_prefer_compound_assignment = true
x += 1;

// dotnet_style_prefer_compound_assignment = false
x = x + 1;
```

```vb
' dotnet_style_prefer_compound_assignment = true
x += 1

' dotnet_style_prefer_compound_assignment = false
x = x + 1
```

### <a name="null-checking-preferences"></a>Null 检查首选项

本节中的样式规则与 Null 检查首选项有关。

这些规则可在 .editorconfig 文件中以如下方式出现  ：

```ini
# CSharp and Visual Basic code style settings:
[*.{cs,vb}]
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_null_propagation = true:suggestion
```

#### <a name="dotnet_style_coalesce_expression"></a>dotnet\_style\_coalesce_expression

|||
|-|-|
| **规则名称** | dotnet_style_coalesce_expression |
| **规则 ID** | IDE0029 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `true` - 比起三元运算符检查更倾向 null 合并表达式<br /><br />`false` - 比起 null 合并表达式更倾向三元运算符检查 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// dotnet_style_coalesce_expression = true
var v = x ?? y;

// dotnet_style_coalesce_expression = false
var v = x != null ? x : y; // or
var v = x == null ? y : x;
```

```vb
' dotnet_style_coalesce_expression = true
Dim v = If(x, y)

' dotnet_style_coalesce_expression = false
Dim v = If(x Is Nothing, y, x) ' or
Dim v = If(x IsNot Nothing, x, y)
```

#### <a name="dotnet_style_null_propagation"></a>dotnet\_style\_null_propagation

|||
|-|-|
| **规则名称** | dotnet_style_null_propagation |
| **规则 ID** | IDE0031 |
| **适用的语言** | C# 6.0+ 和 Visual Basic 14+ |
| **值** | `true` - 如可能，更倾向使用 null 条件运算符<br /><br />`false` - 如可能，更倾向使用三元 null 检查 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// dotnet_style_null_propagation = true
var v = o?.ToString();

// dotnet_style_null_propagation = false
var v = o == null ? null : o.ToString(); // or
var v = o != null ? o.String() : null;
```

```vb
' dotnet_style_null_propagation = true
Dim v = o?.ToString()

' dotnet_style_null_propagation = false
Dim v = If(o Is Nothing, Nothing, o.ToString()) ' or
Dim v = If(o IsNot Nothing, o.ToString(), Nothing)
```

## <a name="net-code-quality-settings"></a>.NET 代码质量设置

本节中的质量设置规则适用于 C# 和 Visual Basic 代码。 它们用于配置内置于 Visual Studio 集成开发环境 (IDE) 中的代码分析器。 有关使用 EditorConfig 文件配置 FxCop 分析器的信息，请参见[配置 FxCop 分析器](../code-quality/configure-fxcop-analyzers.md)。

- [参数首选项](#parameter-preferences)
  - dotnet\_code\_quality\_unused\_parameters

### <a name="parameter-preferences"></a>参数首选项

本节中的质量规则涉及方法参数。

这些规则可在 .editorconfig 文件中以如下方式出现  ：

```ini
# CSharp and Visual Basic code quality settings:
[*.{cs,vb}]
dotnet_code_quality_unused_parameters = all:suggestion
```

#### <a name="dotnet_code_quality_unused_parameters"></a>dotnet\_code\_quality\_unused\_parameters

|||
|-|-|
| **规则名称** | dotnet_code_quality_unused_parameters |
| **规则 ID** | IDE0060 |
| **适用的语言** | C# 和 Visual Basic |
| **值** | `all` - 标记具有包含未使用的参数的任何可访问性的方法<br /><br />`non_public` - 只标记包含未使用的参数的非公共方法 |
| **Visual Studio 默认值** | `all:suggestion` |

代码示例：

```csharp
// dotnet_code_quality_unused_parameters = all:suggestion
public int GetNum() { return 1; }

// dotnet_code_quality_unused_parameters = non_public:suggestion
public int GetNum(int arg1) { return 1; }
```

```vb
' dotnet_code_quality_unused_parameters = all:suggestion
Public Function GetNum()
    Return 1
End Function

' dotnet_code_quality_unused_parameters = non_public:suggestion
Public Function GetNum(arg1 As Integer)
    Return 1
End Function
```

## <a name="c-code-style-settings"></a>C# 代码样式设置

本节中的样式规则仅适用于 C#。

- [隐式和显式类型](#implicit-and-explicit-types)
  - csharp\_style\_var\_for\_built\_in_types
  - csharp\_style\_var\_when\_type\_is_apparent
  - csharp\_style\_var_elsewhere
- [Expression-Bodied 成员](#expression-bodied-members)
  - csharp\_style\_expression\_bodied_methods
  - csharp\_style\_expression\_bodied_constructors
  - csharp\_style\_expression\_bodied_operators
  - csharp\_style\_expression\_bodied_properties
  - csharp\_style\_expression\_bodied_indexers
  - csharp\_style\_expression\_bodied_accessors
  - csharp\_style\_expression\_bodied_lambdas
  - csharp\_style\_expression\_bodied\_local_functions
- [模式匹配](#pattern-matching)
  - csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check
  - csharp\_style\_pattern\_matching\_over\_as\_with\_null_check
- [内联变量声明](#inlined-variable-declarations)
  - csharp\_style\_inlined\_variable_declaration
- [表达式级首选项](#c-expression-level-preferences)
  - csharp\_prefer\_simple\_default_expression
- [“NULL”检查首选项](#c-null-checking-preferences)
  - csharp\_style\_throw_expression
  - csharp\_style\_conditional\_delegate_call
- [代码块首选项](#code-block-preferences)
  - csharp\_prefer_braces
- [未使用的值首选项](#unused-value-preferences)
  - csharp\_style\_unused\_value\_expression\_statement_preference
  - csharp\_style\_unused\_value\_assignment_preference
- [索引和范围首选项](#index-and-range-preferences)
  - csharp\_style\_prefer\_index_operator
  - csharp\_style\_prefer\_range_operator
- [其他首选项](#miscellaneous-preferences)
  - csharp\_style\_deconstructed\_variable_declaration
  - csharp\_style\_pattern\_local\_over\_anonymous_function
  - csharp\_using\_directive\_placement
  - csharp\_prefer\_static\_local_function
  - csharp\_prefer\_simple\_using_statement
  - csharp\_style\_prefer\_switch_expression

### <a name="implicit-and-explicit-types"></a>隐式和显式类型

本节中的样式规则与变量声明中的 [var](/dotnet/csharp/language-reference/keywords/var) 关键字和显式类型的使用有关。 此规则可单独应用于内置类型（前提是该类型为明显）和其他情况。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_style_var_for_built_in_types = true:suggestion
csharp_style_var_when_type_is_apparent = true:suggestion
csharp_style_var_elsewhere = true:suggestion
```

#### <a name="csharp_style_var_for_built_in_types"></a>csharp\_style\_var\_for\_built\_in_types

|||
|-|-|
| **规则名称** | csharp_style_var_for_built_in_types |
| **规则 ID** | IDE0007 和 IDE0008 |
| **适用的语言** | C#  |
| **值** | `true` - 使用 `var` 声明 `int` 等内置系统类型的变量为首选项<br /><br />`false` - 使用显示类型声明 `int` 等内置系统类型的变量为首选项，而非使用 `var` |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// csharp_style_var_for_built_in_types = true
var x = 5;

// csharp_style_var_for_built_in_types = false
int x = 5;
```

#### <a name="csharp_style_var_when_type_is_apparent"></a>csharp\_style\_var\_when\_type\_is_apparent

|||
|-|-|
| **规则名称** | csharp_style_var_when_type_is_apparent |
| **规则 ID** | IDE0007 和 IDE0008 |
| **适用的语言** | C#  |
| **值** | `true` - 声明表达式右侧已提到该类型时更倾向使用 `var`<br /><br />`false` - 声明表达式右侧已提到该类型时，使用显式类型为首选项，而非 `var` |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// csharp_style_var_when_type_is_apparent = true
var obj = new Customer();

// csharp_style_var_when_type_is_apparent = false
Customer obj = new Customer();
```

#### <a name="csharp_style_var_elsewhere"></a>csharp\_style\_var_elsewhere

|||
|-|-|
| **规则名称** | csharp_style_var_elsewhere |
| **规则 ID** | IDE0007 和 IDE0008 |
| **适用的语言** | C#  |
| **值** | `true` - 在任何情况下，`var` 为首选项，而非显式类型，除非由另一个代码样式规则替代<br /><br />`false` - 在任何情况下，显式类型为首选项，而非 `var`，除非由另一个代码样式规则替代 |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// csharp_style_var_elsewhere = true
var f = this.Init();

// csharp_style_var_elsewhere = false
bool f = this.Init();
```

### <a name="expression-bodied-members"></a>Expression-Bodied 成员

本节中的样式规则与在逻辑由单个表达式组成的情况下，[expression-bodied 成员](/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members)的使用有关。 此规则可应用于方法、构造函数、运算符、属性、索引器和访问器。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_style_expression_bodied_methods = false:silent
csharp_style_expression_bodied_constructors = false:silent
csharp_style_expression_bodied_operators = false:silent
csharp_style_expression_bodied_properties = true:suggestion
csharp_style_expression_bodied_indexers = true:suggestion
csharp_style_expression_bodied_accessors = true:suggestion
csharp_style_expression_bodied_lambdas = true:silent
csharp_style_expression_bodied_local_functions = false:silent
```

#### <a name="csharp_style_expression_bodied_methods"></a>csharp\_style\_expression\_bodied_methods

|||
|-|-|
| **规则名称** | csharp_style_expression_bodied_methods |
| **规则 ID** | IDE0022 |
| **适用的语言** | C# 6.0+  |
| **值** | `true` - 首选使用方法的表达式主体<br /><br />`when_on_single_line` - 当其将为单行时，首先方法的表达式主体<br /><br />`false` - 优先选择方法的块主体 |
| **Visual Studio 默认值** | `false:silent` |

代码示例：

```csharp
// csharp_style_expression_bodied_methods = true
public int GetAge() => this.Age;

// csharp_style_expression_bodied_methods = false
public int GetAge() { return this.Age; }
```

#### <a name="csharp_style_expression_bodied_constructors"></a>csharp\_style\_expression\_bodied_constructors

|||
|-|-|
| **规则名称** | csharp_style_expression_bodied_constructors |
| **规则 ID** | IDE0021 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 首选构造函数的表达式主体<br /><br />`when_on_single_line` - 当其将为单行时，首选构造函数的表达式主体<br /><br />`false` - 倾向于使用构造函数的块主体 |
| **Visual Studio 默认值** | `false:silent` |

代码示例：

```csharp
// csharp_style_expression_bodied_constructors = true
public Customer(int age) => Age = age;

// csharp_style_expression_bodied_constructors = false
public Customer(int age) { Age = age; }
```

#### <a name="csharp_style_expression_bodied_operators"></a>csharp\_style\_expression\_bodied_operators

|||
|-|-|
| **规则名称** | csharp_style_expression_bodied_operators |
| **规则 ID** | IDE0023 和 IDE0024 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 首选运算符的表达式主体<br /><br />`when_on_single_line` - 当其将为单行时，首选运算符的表达式主体<br /><br />`false` - 倾向于使用运算符的块主体 |
| **Visual Studio 默认值** | `false:silent` |

代码示例：

```csharp
// csharp_style_expression_bodied_operators = true
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
    => new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary);

// csharp_style_expression_bodied_operators = false
public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
{ return new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary); }
```

#### <a name="csharp_style_expression_bodied_properties"></a>csharp\_style\_expression\_bodied_properties

|||
|-|-|
| **规则名称** | csharp_style_expression_bodied_properties |
| **规则 ID** | IDE0025 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 首选属性的表达式主体<br /><br />`when_on_single_line` - 当其将为单行时，首选属性的表达式主体<br /><br />`false` - 倾向于使用属性的块主体 |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// csharp_style_expression_bodied_properties = true
public int Age => _age;

// csharp_style_expression_bodied_properties = false
public int Age { get { return _age; }}
```

#### <a name="csharp_style_expression_bodied_indexers"></a>csharp\_style\_expression\_bodied_indexers

|||
|-|-|
| **规则名称** | csharp_style_expression_bodied_indexers |
| **规则 ID** | IDE0026 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 首选索引的表达式主体<br /><br />`when_on_single_line` - 当其将为单行时，首选索引的表达式主体<br /><br />`false` - 倾向于使用索引器的块主体 |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// csharp_style_expression_bodied_indexers = true
public T this[int i] => _values[i];

// csharp_style_expression_bodied_indexers = false
public T this[int i] { get { return _values[i]; } }
```

#### <a name="csharp_style_expression_bodied_accessors"></a>csharp\_style\_expression\_bodied_accessors

|||
|-|-|
| **规则名称** | csharp_style_expression_bodied_accessors |
| **规则 ID** | IDE0027 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 首选取值函数的表达式主体<br /><br />`when_on_single_line` - 当其将为单行时，首选取值函数的表达式主体<br /><br />`false` - 倾向于使用访问器的块主体 |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// csharp_style_expression_bodied_accessors = true
public int Age { get => _age; set => _age = value; }

// csharp_style_expression_bodied_accessors = false
public int Age { get { return _age; } set { _age = value; } }
```

#### <a name="csharp_style_expression_bodied_lambdas"></a>csharp\_style\_expression\_bodied_lambdas

|||
|-|-|
| **规则名称** | csharp_style_expression_bodied_lambdas |
| **规则 ID** | IDE0053 |
| **值** | `true` - 首选 Lambdas 的表达式主体<br /><br />`when_on_single_line` - 当其将为单行时，首选 lambdas 的表达式主体<br /><br />`false` - 首选 lambdas 的块主体 |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// csharp_style_expression_bodied_lambdas = true
Func<int, int> square = x => x * x;

// csharp_style_expression_bodied_lambdas = false
Func<int, int> square = x => { return x * x; };
```

#### <a name="csharp_style_expression_bodied_local_functions"></a>csharp\_style\_expression\_bodied\_local_functions

从 C# 7.0 开始，C# [支持本地函数](/dotnet/csharp/programming-guide/classes-and-structs/local-functions)。 本地函数是一种嵌套在另一成员中的类型的私有方法。

|||
|-|-|
| **规则名称** | csharp_style_expression_bodied_local_functions |
| **规则 ID** | IDE0061 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 首选本地函数的表达式主体<br /><br />`when_on_single_line` - 当其将为单行时，首选本地函数的表达式主体<br /><br />`false` - 首选本地函数的块主体 |
| **Visual Studio 默认值** | `false:silent` |

代码示例：

```csharp
// csharp_style_expression_bodied_local_functions = true
void M()
{
    Hello();
    void Hello() => Console.WriteLine("Hello");
}

// csharp_style_expression_bodied_local_functions = false
void M()
{
    Hello();
    void Hello()
    {
        Console.WriteLine("Hello");
    }
}
```

### <a name="pattern-matching"></a>模式匹配

本节中的样式规则与 C# 中[模式匹配](/dotnet/csharp/pattern-matching)的使用有关。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion
```

#### <a name="csharp_style_pattern_matching_over_is_with_cast_check"></a>csharp\_style\_pattern\_matching\_over\_is\_with\_cast_check

|||
|-|-|
| **规则名称** | csharp_style_pattern_matching_over_is_with_cast_check |
| **规则 ID** | IDE0020 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 倾向于使用模式匹配，而不是带类型强制转换的 `is` 表达式<br /><br />`false` - 倾向于使用带类型强制转换的 `is` 表达式，而不是模式匹配 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_pattern_matching_over_is_with_cast_check = true
if (o is int i) {...}

// csharp_style_pattern_matching_over_is_with_cast_check = false
if (o is int) {var i = (int)o; ... }
```

#### <a name="csharp_style_pattern_matching_over_as_with_null_check"></a>csharp\_style\_pattern\_matching\_over\_as\_with\_null_check

|||
|-|-|
| **规则名称** | csharp_style_pattern_matching_over_as_with_null_check |
| **规则 ID** | IDE0019 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 倾向于使用模式匹配，而不是带 null 检查的 `as` 表达式，来确定内容是否为某个特定类型<br /><br />`false` - 倾向于使用带 null 检查的 `as` 表达式，而不是模式匹配，来确定内容是否为某个特定类型 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_pattern_matching_over_as_with_null_check = true
if (o is string s) {...}

// csharp_style_pattern_matching_over_as_with_null_check = false
var s = o as string;
if (s != null) {...}
```

### <a name="inlined-variable-declarations"></a>内联变量声明

此样式规则与 `out` 变量是否声明为内联有关。 从 C# 7 开始，可以[在方法调用的实际参数列表中声明 out 变量](/dotnet/csharp/language-reference/keywords/out-parameter-modifier#calling-a-method-with-an-out-argument)，而不是在单独的变量声明中。

#### <a name="csharp_style_inlined_variable_declaration"></a>csharp\_style\_inlined\_variable_declaration

|||
|-|-|
| **规则名称** | csharp_style_inlined_variable_declaration |
| **规则 ID** | IDE0018 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - `out` 变量在方法调用的参数列表中声明为内联为首选项（如可能）<br /><br />`false` - 在方法调用之前声明 `out` 变量为首选项 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_inlined_variable_declaration = true
if (int.TryParse(value, out int i) {...}

// csharp_style_inlined_variable_declaration = false
int i;
if (int.TryParse(value, out i) {...}
```

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_style_inlined_variable_declaration = true:suggestion
```

### <a name="c-expression-level-preferences"></a>C# 表达式级首选项

本节中的样式规则与表达式级首选项有关。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_prefer_simple_default_expression = true:suggestion
```

#### <a name="csharp_prefer_simple_default_expression"></a>csharp\_prefer\_simple\_default_expression

此样式规则与在编译器可以推断表达式类型的情况下，[默认值表达式的 `default` 文本](/dotnet/csharp/language-reference/operators/default#default-literal)的使用有关。

|||
|-|-|
| **规则名称** | csharp_prefer_simple_default_expression |
| **规则 ID** | IDE0034 |
| **适用的语言** | C# 7.1+  |
| **值** | `true` - 首选 `default` 次选 `default(T)`<br /><br />`false` - 首选 `default(T)` 次选 `default` |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_prefer_simple_default_expression = true
void DoWork(CancellationToken cancellationToken = default) { ... }

// csharp_prefer_simple_default_expression = false
void DoWork(CancellationToken cancellationToken = default(CancellationToken)) { ... }
```

### <a name="c-null-checking-preferences"></a>C# null 检查首选项

这些样式规则与 `null` 检查的相关语法有关，包括 `throw` 表达式或 `throw` 语句的使用，以及调用 [lambda 表达式](/dotnet/csharp/lambda-expressions)时是否执行 NULL 检查或使用条件合并运算符 (`?.`)。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = false:suggestion
```

#### <a name="csharp_style_throw_expression"></a>csharp\_style\_throw_expression

|||
|-|-|
| **规则名称** | csharp_style_throw_expression |
| **规则 ID** | IDE0016 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 更倾向使用 `throw` 表达式，而不是 `throw` 语句<br /><br />`false` - 更倾向使用 `throw` 语句，而不是 `throw` 表达式 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_throw_expression = true
this.s = s ?? throw new ArgumentNullException(nameof(s));

// csharp_style_throw_expression = false
if (s == null) { throw new ArgumentNullException(nameof(s)); }
this.s = s;
```

#### <a name="csharp_style_conditional_delegate_call"></a>csharp\_style\_conditional\_delegate_call

|||
|-|-|
| **规则名称** | csharp_style_conditional_delegate_call |
| **规则 ID** | IDE0041 |
| **适用的语言** | C# 6.0+  |
| **值** | `true` - 在调用 Lambda 表达式时使用条件合并运算符 (`?.`) 为首选项，而非执行 NULL 检查<br /><br />`false` - 在调用 Lambda 表达式之前执行 NULL 检查为首选项，而非使用条件合并运算符 (`?.`) |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_conditional_delegate_call = true
func?.Invoke(args);

// csharp_style_conditional_delegate_call = false
if (func != null) { func(args); }
```

### <a name="code-block-preferences"></a>代码块首选项

此样式规则与是否使用大括号 `{ }` 将代码块括起来有关。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_prefer_braces = true:silent
```

#### <a name="csharp_prefer_braces"></a>csharp\_prefer\_braces

|||
|-|-|
| **规则名称** | csharp_prefer_braces |
| **规则 ID** | IDE0011 |
| **适用的语言** | C# |
| **值** | `true` - 使用大括号为首选项，即使只有一个代码行，也是如此<br /><br />`false` - 如可能，不使用大括号为首选项 |
| **Visual Studio 默认值** | `true:silent` |

代码示例：

```csharp
// csharp_prefer_braces = true
if (test) { this.Display(); }

// csharp_prefer_braces = false
if (test) this.Display();
```

### <a name="unused-value-preferences"></a>未使用的值首选项

这些样式规则涉及未使用的表达式和值赋值。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_style_unused_value_expression_statement_preference = discard_variable:silent
csharp_style_unused_value_assignment_preference = discard_variable:suggestion
```

#### <a name="csharp_style_unused_value_expression_statement_preference"></a>csharp_style_unused_value_expression_statement_preference

|||
|-|-|
| **规则名称** | csharp_style_unused_value_expression_statement_preference |
| **规则 ID** | IDE0058 |
| **适用的语言** | C# |
| **值** | `discard_variable` - 首选将未使用的表达式分配给 [discard](/dotnet/csharp/discards) <br /><br />`unused_local_variable` - 首选将未使用的表达式分配给本地变量 |
| **Visual Studio 默认值** | `discard_variable:silent` |

代码示例：

```csharp
// Original code:
System.Convert.ToInt32("35");

// After code fix for IDE0058:

// csharp_style_unused_value_expression_statement_preference = discard_variable
_ = System.Convert.ToInt32("35");

// csharp_style_unused_value_expression_statement_preference = unused_local_variable
var unused = Convert.ToInt32("35");
```

#### <a name="csharp_style_unused_value_assignment_preference"></a>csharp_style_unused_value_assignment_preference

|||
|-|-|
| **规则名称** | csharp_style_unused_value_assignment_preference |
| **规则 ID** | IDE0059 |
| **适用的语言** | C# |
| **值** | `discard_variable` - 在分配未使用的值时，首选使用 [discard](/dotnet/csharp/discards)<br /><br />`unused_local_variable` - 在分配未使用的值时，首选使用本地变量 |
| **Visual Studio 默认值** | `discard_variable:suggestion` |

代码示例：

```csharp
// csharp_style_unused_value_assignment_preference = discard_variable
int GetCount(Dictionary<string, int> wordCount, string searchWord)
{
    _ = wordCount.TryGetValue(searchWord, out var count);
    return count;
}

// csharp_style_unused_value_assignment_preference = unused_local_variable
int GetCount(Dictionary<string, int> wordCount, string searchWord)
{
    var unused = wordCount.TryGetValue(searchWord, out var count);
    return count;
}
```

### <a name="index-and-range-preferences"></a>索引和范围首选项

这些样式规则涉及使用索引和范围操作符，这些操作符在 C# 8.0 及更高版本中可用。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_style_prefer_index_operator = true:suggestion
csharp_style_prefer_range_operator = true:suggestion
```

#### <a name="csharp_style_prefer_index_operator"></a>csharp\_style\_prefer\_index_operator

|||
|-|-|
| **规则名称** | csharp_style_prefer_index_operator |
| **规则 ID** | IDE0056 |
| **适用的语言** | C# 8.0+ |
| **值** | `true` - 在从集合末尾计算索引时，首选使用 `^` 操作符<br /><br />`false` - 在从集合末尾计算索引时，不推荐使用 `^` 操作符 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_prefer_index_operator = true
string[] names = { "Archimedes", "Pythagoras", "Euclid" };
var index = names[^1];

// csharp_style_prefer_index_operator = false
string[] names = { "Archimedes", "Pythagoras", "Euclid" };
var index = names[names.Length - 1];
```

#### <a name="csharp_style_prefer_range_operator"></a>csharp\_style\_prefer\_range_operator

|||
|-|-|
| **规则名称** | csharp_style_prefer_range_operator |
| **规则 ID** | IDE0057 |
| **适用的语言** | C# 8.0+ |
| **值** | `true` - 在提取集合的“切片”时，首选使用范围操作符 `..`<br /><br />`false` - 在提取集合的“切片”时，不推荐使用范围操作符 `..` |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_prefer_range_operator = true
string sentence = "the quick brown fox";
var sub = sentence[0..^4];

// csharp_style_prefer_range_operator = false
string sentence = "the quick brown fox";
var sub = sentence.Substring(0, sentence.Length - 4);
```

### <a name="miscellaneous-preferences"></a>其他首选项

本节包含各种样式规则。

.editorconfig 文件示例  ：

```ini
# CSharp code style settings:
[*.cs]
csharp_style_deconstructed_variable_declaration = true:suggestion
csharp_style_pattern_local_over_anonymous_function = true:suggestion
csharp_using_directive_placement = outside_namespace:silent
csharp_prefer_static_local_function = true:suggestion
csharp_prefer_simple_using_statement = true:suggestion
csharp_style_prefer_switch_expression = true:suggestion
```

#### <a name="csharp_style_deconstructed_variable_declaration"></a>csharp\_style\_deconstructed\_variable_declaration

|||
|-|-|
| **规则名称** | csharp_style_deconstructed_variable_declaration |
| **规则 ID** | IDE0042 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 首选析构变量声明<br /><br />`false` - 不首选变量声明中的析构 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_deconstructed_variable_declaration = true
var (name, age) = GetPersonTuple();
Console.WriteLine($"{name} {age}");

(int x, int y) = GetPointTuple();
Console.WriteLine($"{x} {y}");

// csharp_style_deconstructed_variable_declaration = false
var person = GetPersonTuple();
Console.WriteLine($"{person.name} {person.age}");

(int x, int y) point = GetPointTuple();
Console.WriteLine($"{point.x} {point.y}");
```

#### <a name="csharp_style_pattern_local_over_anonymous_function"></a>csharp\_style\_pattern\_local\_over\_anonymous_function

从 C# 7.0 开始，C# [支持本地函数](/dotnet/csharp/programming-guide/classes-and-structs/local-functions)。 本地函数是一种嵌套在另一成员中的类型的私有方法。

|||
|-|-|
| **规则名称** | csharp_style_pattern_local_over_anonymous_function |
| **规则 ID** | IDE0039 |
| **适用的语言** | C# 7.0+ |
| **值** | `true` - 首选本地函数，而非匿名函数<br /><br />`false` - 首选匿名函数，而不是本地函数 |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_style_pattern_local_over_anonymous_function = true
int fibonacci(int n)
{
    return n <= 1 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}

// csharp_style_pattern_local_over_anonymous_function = false
Func<int, int> fibonacci = null;
fibonacci = (int n) =>
{
    return n <= 1 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
};
```

#### <a name="csharp_using_directive_placement"></a>csharp\_using\_directive_placement

|||
|-|-|
| **规则名称** | csharp_using_directive_placement |
| **规则 ID** | IDE0065 |
| **适用的语言** | C# |
| **值** | `outside_namespace` - 首选将 `using` 指令放在名称空间之外<br /><br />`inside_namespace` - 首选将 `using` 指令放在名称空间中 |
| **Visual Studio 默认值** | `outside_namespace:silent` |

代码示例：

```csharp
// csharp_using_directive_placement = outside_namespace
using System;

namespace Conventions
{
    ...
}

// csharp_using_directive_placement = inside_namespace
namespace Conventions
{
    using System;
    ...
}
```

#### <a name="csharp_prefer_static_local_function"></a>csharp\_prefer\_static\_local_function

|||
|-|-|
| **规则名称** | csharp_prefer_static_local_function |
| **规则 ID** | IDE0062 |
| **适用的语言** | C# 8.0+ |
| **值** | `true` - 首选将局部函数标记为 `static`<br /><br />`false` - 不推荐将局部函数标记为 `static` |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_prefer_static_local_function = true
void M()
{
    Hello();
    static void Hello()
    {
        Console.WriteLine("Hello");
    }
}

// csharp_prefer_static_local_function = false
void M()
{
    Hello();
    void Hello()
    {
        Console.WriteLine("Hello");
    }
}
```

#### <a name="csharp_prefer_simple_using_statement"></a>csharp\_prefer\_simple\_using_statement

|||
|-|-|
| **规则名称** | csharp_prefer_simple_using_statement |
| **规则 ID** | IDE0063 |
| **适用的语言** | C# 8.0+ |
| **值** | `true` - 首选使用简单语句 `using` <br /><br />`false` - 不推荐使用简单语句 `using`  |
| **Visual Studio 默认值** | `true:suggestion` |

代码示例：

```csharp
// csharp_prefer_simple_using_statement = true
using var a = b;

// csharp_prefer_simple_using_statement = false
using (var a = b) { }
```

#### <a name="csharp_style_prefer_switch_expression"></a>csharp\_style\_prefer\_switch_expression

|||
|-|-|
| **规则名称** | csharp_style_prefer_switch_expression |
| **规则 ID** | IDE0066 |
| **适用的语言** | C# 8.0+ |
| **值** | `true` - 首选使用 `switch` 表达式（使用 C# 8.0 引入）<br /><br />`false` - 首选使用 [switch 语句](/dotnet/csharp/language-reference/keywords/switch) |
| **Visual Studio 默认值** | `true:suggestion` |
| **引入的版本** | Visual Studio 2019 版本 16.2 |

代码示例：

```csharp
// csharp_style_prefer_switch_expression = true
return x switch
{
    1 => 1 * 1,
    2 => 2 * 2,
    _ => 0,
};

// csharp_style_prefer_switch_expression = false
switch (x)
{
    case 1:
        return 1 * 1;
    case 2:
        return 2 * 2;
    default:
        return 0;
}
```

## <a name="see-also"></a>请参阅

- [格式设置约定](editorconfig-formatting-conventions.md)
- [命名约定](editorconfig-naming-conventions.md)
- [EditorConfig 的 .NET 编码约定设置](editorconfig-code-style-settings-reference.md)

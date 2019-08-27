---
title: EditorConfig 文件适用的 .NET 命名约定
ms.date: 08/07/2019
ms.topic: reference
helpviewer_keywords:
- naming conventions [EditorConfig]
- EditorConfig naming conventions
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ab118197c29ef950907839e8c04d6e49a9843f1a
ms.sourcegitcommit: 6f3cf7a1bfc81a61f9a603461a1c34fd2221f100
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957430"
---
# <a name="net-naming-conventions-for-editorconfig"></a>EditorConfig 适用的 .NET 命名约定

命名约定与类、属性和方法等码位元素的命名有关。 例如，可以指定公共成员必须采用大写形式，或者异步方法必须以“Async”结尾。 可以通过在 [.editorconfig 文件](../ide/create-portable-custom-editor-options.md)中指定这些规则来加以实施。 命名规则冲突显示在“错误列表”中，或者作为建议显示在名称之下，具体取决于为规则选择的严重性  。 不需要生成项目即可查看冲突。

对于每个命名约定，必须使用下面介绍的属性指定适用的符号、命名样式和实施约定的严重性。 属性的顺序并不重要。

首先，为命名规则选择一个标题，该标题可用于完全描述规则所需的每个属性。 例如，`public_members_must_be_capitalized` 是一个良好的描述性命名规则名称。 此页面将引用所选标题作为以下部分中的 <namingRuleTitle\>  。

## <a name="symbols"></a>符号

首先，识别应用命名规则的一组符号。 此属性采用以下格式：

`dotnet_naming_rule.<namingRuleTitle>.symbols = <symbolTitle>`

通过将 <symbolTitle\> 替换为描述性标题（如 `public_symbols`），为该组符号提供名称  。 将在三个属性名称中使用 <symbolTitle\>，这三个属性用于介绍应用规则的符号（符号种类、可访问性级别和修饰符）  。

### <a name="kinds-of-symbols"></a>符号种类

要描述应用命名规则的符号种类，请按照以下格式指定一个属性：

`dotnet_naming_symbols.<symbolTitle>.applicable_kinds = <values>`

以下列表显示了允许的值，可通过以逗号分隔值来指定多个值。

- \*（使用此值可指定所有符号）
- namespace
- class
- struct
- interface
- enum
- 属性
- 方法
- Field — 字段
- Event — 事件
- 委托
- 参数
- type_parameter
- 本地
- local_function

### <a name="accessibility-levels-of-symbols"></a>符号的可访问性级别

要描述应用命名规则的符号的可访问性级别，请按照以下格式指定一个属性名称：

`dotnet_naming_symbols.<symbolTitle>.applicable_accessibilities = <values>`

以下列表显示了允许的值，可通过以逗号分隔值来指定多个值。

- \*（使用此值可指定所有可访问性级别）
- public
- internal 或 friend
- private
- protected
- protected\_internal 或 protected_friend
- private\_protected
- 本地

   `local` 辅助功能级别适用于方法中定义的符号。 对于无法在代码中指定辅助功能的符号，定义命名约定非常有用。 例如，如果在常量命名约定 (`required_modifiers = const`) 上指定 `applicable_accessibilities = local`，则该规则只适用于方法中定义的常量，而不适用于类型中定义的常量。

   ```csharp
   class TypeName
   {
     // Constant defined in a type.
     const int X = 3;

     void Method()
     {
       // Constant defined in a method with "local" accessibility.
       const int Y = 4;
     }
   }
   ```

### <a name="symbol-modifiers-optional"></a>符号修饰符（可选）

要描述应用命名规则的符号的修饰符，请按照以下格式指定一个属性名称：

`dotnet_naming_symbols.<symbolTitle>.required_modifiers = <values>`

以下列表显示了允许的值（以逗号分隔多个值）：

- `abstract` 或 `must_inherit`
- `async`
- `const`
- `readonly`
- `static` 或 `shared`

   > [!NOTE]
   > 如果 `static` 或 `shared` 符号有命名规则，此规则也适用于 `const` 符号，因为它们是隐式静态的。 如果不希望将 `static` 命名规则应用于 `const` 符号，请为 `const` 符号单独创建命名规则。

命名规则与具有 `required_modifiers` 中指定的所有修饰符的签名匹配  。 如果忽略此属性，则使用一个空列表的默认值，即无需特定修饰符即可匹配。 这意味着符号的修饰符不会影响是否应用此规则。

> [!TIP]
> 请勿为 `required_modifiers` 指定 `*` 值。 相反，只需省略 `required_modifiers` 属性，命名规则将适用于任何类型的修饰符。

## <a name="style"></a>样式

识别了应用命名规则的一组符号，现在可以描述命名样式。 样式可以是名称采用特定前缀或特定后缀，也可以是名称中的各个文字以特定字符分隔。 还可以指定大写样式。 样式属性采用以下格式：

`dotnet_naming_rule.<namingRuleTitle>.style = <styleTitle>`

通过将 <styleTitle\> 值替换为描述性标题（如 `first_word_upper_case_style`），为样式提供名称  。 将在描述命名样式（前缀、后缀、文字分隔符和大写）的属性名称中使用 <styleTitle\> 值  。 使用其中一个或多个属性描述样式。

### <a name="require-a-prefix"></a>需要前缀

要指定符号名称必须以特定字符开始，请使用此属性：

`dotnet_naming_style.<styleTitle>.required_prefix = <prefix>`

### <a name="require-a-suffix"></a>需要后缀

要指定符号名称必须以特定字符结尾，请使用此属性：

`dotnet_naming_style.<styleTitle>.required_suffix = <suffix>`

### <a name="require-a-certain-word-separator"></a>需要特定文字分隔符

要指定必须以特定字符分隔符号名称中的各文字，请使用此属性：

`dotnet_naming_style.<styleTitle>.word_separator = <separator character>`

### <a name="require-a-capitalization-style"></a>需要大写样式

要指定符号名称使用特定大写样式，请使用此属性：

`dotnet_naming_style.<styleTitle>.capitalization = <value>`

此属性的允许值为：

- pascal_case
- camel_case
- first\_word_upper
- all\_upper
- all_lower

> [!NOTE]
> 必须在命名样式中指定大写样式，否则会忽略命名样式。

## <a name="severity"></a>严重性

要描述命名规则冲突的严重性，请按照以下格式指定一个属性：

`dotnet_naming_rule.<namingRuleTitle>.severity = <value>`

下表显示允许的严重性值及其含义：

严重性 | 效果
------------ | -------------
无 | 完全禁止显示规则。
重构或无提示 | 如未遵循此样式，则不会向用户显示任何内容，但自动生成的代码会遵循此样式。
建议 | 如未遵循此样式，则会以建议形式向用户显示此样式（如前两个字符下带点）。 这在编译时没有影响。
warning | 如未遵循此样式，“错误列表”中会显示编译器警告  。
error | 如未遵循此样式，“错误列表”中会显示编译器错误  。

> [!NOTE]
> 无需生成项目即可查看命名规则冲突。 它们会在编辑代码时显示在“错误列表”中或以建议形式显示  。

## <a name="rule-order"></a>规则顺序

::: moniker range="vs-2017"

命名约定在 EditorConfig 文件中的排序顺序应为从最具体到最抽象。 遇到的第一个可应用规则是唯一应用的规则。 但是，如果有多个具有相同名称的规则属性  ，则最近找到的具有该名称的属性具有优先权。 有关详细信息，请参阅[文件层次结构和优先级](create-portable-custom-editor-options.md#file-hierarchy-and-precedence)。

::: moniker-end

::: moniker range=">=vs-2019"

从 Visual Studio 2019 版本 16.2 开始，命名规则在 EditorConfig 文件中定义的顺序并不重要。 相反，Visual Studio 根据规则本身的定义自动对命名规则进行排序。 [EditorConfig 语言服务扩展](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig)可以分析 EditorConfig 文件，如果文件中的规则顺序与编译器在运行时使用的规则不同，该扩展还会进行报告。

如果使用的是 Visual Studio 的早期版本，则命名约定在 EditorConfig 文件中的排序顺序应为从最具体到最抽象。 遇到的第一个可应用规则是唯一应用的规则。 但是，如果有多个具有相同名称的规则属性  ，则最近找到的具有该名称的属性具有优先权。 有关详细信息，请参阅[文件层次结构和优先级](create-portable-custom-editor-options.md#file-hierarchy-and-precedence)。

::: moniker-end

## <a name="default-naming-styles"></a>默认命名样式

若未指定任何自定义命名规则，Visual Studio 将使用下列默认样式：

- 对于可访问性为 `public`、`private`、`internal`、`protected` 或 `protected_internal` 的类、结构、枚举、属性以及事件，默认的命名样式为帕斯卡拼写法。

- 对于可访问性为 `public`、`private`、`internal`、`protected` 或 `protected_internal` 的接口，默认的命名样式为帕斯卡拼写法并必须附加 l 前缀。 

## <a name="example"></a>示例

以下 .editorconfig 文件包含命名约定，该约定指定公共属性、方法、字段、事件和委托必须采用大写形式  。 请注意，此命名约定指定了多种应用规则的符号，以逗号分隔。

```ini
# Public members must be capitalized (public_members_must_be_capitalized)
[*.{cs,vb}]
dotnet_naming_rule.public_members_must_be_capitalized.symbols   = public_symbols
dotnet_naming_symbols.public_symbols.applicable_kinds           = property,method,field,event,delegate
dotnet_naming_symbols.public_symbols.applicable_accessibilities = public
dotnet_naming_symbols.public_symbols.required_modifiers         = readonly

dotnet_naming_rule.public_members_must_be_capitalized.style    = first_word_upper_case_style
dotnet_naming_style.first_word_upper_case_style.capitalization = first_word_upper

dotnet_naming_rule.public_members_must_be_capitalized.severity = suggestion
```

以下屏幕截图显示此命名约定在编辑器中的效果。 有两个公共变量的名称没有首字母大写。 一个是 `const`，另一个是 `readonly`。 因为命名规则仅应用于 `readonly` 符号，所以仅 `readonly` 变量显示命名规则建议。

![命名规则建议](media/editorconfig-naming-rule-suggestion.png)

现在，将冲突严重性更改为 `warning`：

```ini
dotnet_naming_rule.public_members_must_be_capitalized.severity = warning
```

如果关闭代码文件然后重新打开，而不是查看名称冲突下的建议，则会看见绿色波浪线和“错误列表”中的警告  ：

![命名规则警告](media/editorconfig-naming-rule-warning.png)

## <a name="see-also"></a>请参阅

- [语言约定](editorconfig-language-conventions.md)
- [格式设置约定](editorconfig-formatting-conventions.md)
- [Roslyn 命名约定](https://github.com/dotnet/roslyn/blob/master/.editorconfig#L63)
- [创建可移植的自定义编辑器选项](../ide/create-portable-custom-editor-options.md)
- [EditorConfig 的 .NET 编码约定设置](editorconfig-code-style-settings-reference.md)

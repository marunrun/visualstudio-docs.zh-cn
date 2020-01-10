---
title: 在 Visual Basic 中配置警告
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- errors [Visual Basic], warnings
- run-time errors, warnings
- warnings, configuring
ms.assetid: 99cf4781-bd4d-47b4-91b9-217933509f82
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 67f65ea691a02bac87f75f43e0a9938125bcd959
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585504"
---
# <a name="configuring-warnings-in-visual-basic"></a>在 Visual Basic 中配置警告

[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 编译器提供了可能导致运行时错误的代码的一组警告。 可以使用这些信息编写 bug 较少的更干净、更快速和更好的代码。 例如，如果用户尝试调用未赋值的对象变量的成员，从未设置返回值的函数返回或者执行有逻辑错误的 `Try` 块来捕获异常，该编译器都将生成警告。

有时该编译器替用户提供额外的逻辑，以便用户可以专注于正在进行的任务，而不用预先考虑可能出现的错误。 在早期版本的 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中，使用“Option Strict”限制 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 编译器提供的其他逻辑  。 通过配置警告，可以用更精细的方式在单个警告级别限制此逻辑。

你可能需要自定义项目，并关闭与你的应用程序无关的某些警告，而将其他警告变为错误。 本页说明如何打开和关闭单个警告。

## <a name="turning-warnings-off-and-on"></a>关闭和打开警告
配置警告有两种不同的方法：可以使用“项目设计器”  配置警告，也可以使用 **/warnaserror** 和 **/nowarn** 编译器选项进行配置。

使用“项目设计器”  页的“编译”  选项卡可以打开和关闭警告。 选中“禁用所有警告”  复选框可禁用所有警告；选中“将所有警告视为错误”  可将所有警告都视为错误。 有些个别警告可以根据所显示的表的需要，在错误和警告之间切换。

如果“Option Strict”  设置为“Off”  ，则不能将与“Option Strict”  相关的警告视为彼此独立。 如果“Option Strict”  设置为“On”  ，则将相关联的警告视为错误，而无论其状态如何。 如果通过在命令行编译器中指定 `/optionstrict:custom` 将“Option Strict”  设置为“自定义”  ，则可以不受限制地在开和关之间切换“Option Strict”  警告。

此外，还可以使用该编译器的 **/warnaserror** 命令行选项指定是否将警告视为错误。 可以将逗号分隔的列表添加到此选项，以通过使用 + 或 - 指定应将哪些警告视为错误或警告。 下表对可能的选项进行了详细说明。

|命令行选项|指定|
| - |---------------|
|`/warnaserror+`|将所有警告视为错误|
|`/warnsaserror`-|不将警告视为错误。 这是默认设置。|
|`/warnaserror+:<warning list` `>`|对于在逗号分隔列表中按其错误 ID 号列出的特定警告，将它们视为错误。|
|`/warnaserror-:<warning list>`|对于在逗号分隔列表中按其错误 ID 号列出的特定警告，不将它们视为错误。|
|`/nowarn`|不报告警告。|
|`/nowarn:<warning list>`|对于在逗号分隔列表中按其错误 ID 号列出的指定警告，不报告它们。|

该警告列表包含应视为错误的警告所对应的错误 ID 号，可以将这些错误 ID 号与命令行选项一起使用来打开或关闭特定的警告。 如果该警告列表包含无效的错误号，将会报告一个错误。

## <a name="examples"></a>示例
下表包含命令行参数示例，并对每个参数的作用进行了说明。

|参数|描述|
|--------------|-----------------|
|`vbc /warnaserror`|指定应将所有警告都视为错误。|
|`vbc /warnaserror:42024`|指定应将 42024 警告视为错误。|
|`vbc /warnaserror:42024,42025`|指定应将 42024 和 42025 警告视为错误。|
|`vbc /nowarn`|指定不应报告任何警告。|
|`vbc /nowarn:42024`|指定不应报告 42024 警告。|
|`vbc /nowarn:42024,42025`|指定不应报告 42024 和 42025 警告。|

## <a name="types-of-warnings"></a>警告类型
下面列出了你可能想将其视为错误的警告。

### <a name="implicit-conversion-warning"></a>隐式转换警告
针对隐式转换的实例生成。 使用 `&` 运算符时，这些实例不包含从内部数值类型到字符串的隐式转换。 新项目的默认值为 Off。

ID:42016

### <a name="late-bound-method-invocation-and-overload-resolution-warning"></a>后期绑定方法调用和重载决策警告
针对后期绑定的实例生成。 新项目的默认值为 Off。

ID:42017

### <a name="operands-of-type-object-warnings"></a>“Object”类型的操作数警告
当出现会引发“Option Strict On”错误的 `Object` 类型的操作数时生成  。 新项目的默认值为 On。

ID:42018 和 42019

### <a name="declarations-require-as-clause-warnings"></a>声明需要“As”子句警告
当缺少 `As` 子句的变量、函数或属性声明会引发“Option Strict On”错误时生成  。 假定未指定类型的变量属于类型 `Object`。 新项目的默认值为 On。

ID:42020（变量声明）、42021（函数声明）和 42022（属性声明）。

### <a name="possible-null-reference-exception-warnings"></a>可能的 Null 引用异常警告
当尚未向变量赋值就使用该变量时生成。 新项目的默认值为 On。

ID:42104、42030

### <a name="unused-local-variable-warning"></a>未使用的局部变量警告
当声明了局部变量但从未引用该变量时生成。 默认值为 On。

ID:42024

### <a name="access-of-shared-member-through-instance-variable-warning"></a>通过实例变量访问共享成员警告
通过可能有副作用的实例访问共享成员时，或者通过不是表达式右侧或正作为参数传入的实例变量访问共享成员时生成。 新项目的默认值为 On。

ID:42025

### <a name="recursive-operator-or-property-access-warnings"></a>递归运算符或属性访问警告
当例程主体使用定义它的同一运算符或属性时生成。 新项目的默认值为 On。

ID:42004（运算符）、42026（属性）

### <a name="function-or-operator-without-return-value-warning"></a>没有返回值的函数或运算符警告
当函数或运算符未指定返回值时生成。 这包括忽略与函数同名的隐式局部变量的 `Set`。 新项目的默认值为 On。

ID:42105（函数）、42016（运算符）

### <a name="overloads-modifier-used-in-a-module-warning"></a>在模块中使用重载修饰符警告
在 `Module` 中使用 `Overloads` 时生成。 新项目的默认值为 On。

ID:42028

### <a name="duplicate-or-overlapping-catch-blocks-warnings"></a>重复或重叠的 Catch 块警告
当因某个 `Catch` 块与其他已定义的 `Catch` 块相关联而从未到达该块时生成。 新项目的默认值为 On。

ID:42029、42031

## <a name="see-also"></a>请参阅

- [错误类型](/dotnet/visual-basic/programming-guide/language-features/error-types)
- [Try...Catch...Finally 语句](/dotnet/visual-basic/language-reference/statements/try-catch-finally-statement)
- [/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn)
- [/warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror)
- [项目设计器的“编译”页 (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md)
- [默认关闭的编译器警告](/cpp/preprocessor/compiler-warnings-that-are-off-by-default)

---
title: MSBuild 条件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, conditions
- conditions [MSBuild]
- Exists, MSBuild condition function
- HasTrailingSlash, MSBuild condition function
ms.assetid: 9d7aa308-b667-48ed-b4c9-a61e49eb0a85
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5994e3f5b17f50d707c4c5a00666d60c2efd3184
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88711698"
---
# <a name="msbuild-conditions"></a>MSBuild 条件

MSBuild 支持一组特定的条件，只要允许使用 `Condition` 属性，便应用这些条件。 下表对这些条件进行了说明。

|条件|描述|
|---------------|-----------------|
|'`stringA`' == '`stringB`'|如果 `stringA` 等于 `stringB`，则计算结果为 `true`。<br /><br /> 例如：<br /><br /> `Condition="'$(Configuration)'=='DEBUG'"`<br /><br /> 对于简单的字母数字字符串或布尔值，不需要单引号。 但对于空值，单引号是必需的。 此检查不区分大小写。|
|'`stringA`' != '`stringB`'|如果 `stringA` 不等于 `stringB`，则计算结果为 `true`。<br /><br /> 例如：<br /><br /> `Condition="'$(Configuration)'!='DEBUG'"`<br /><br /> 对于简单的字母数字字符串或布尔值，不需要单引号。 但对于空值，单引号是必需的。 此检查不区分大小写。|
|\<, >, \<=, >=|计算操作数的数值。 如果关系评估为 true，则返回 `true`。 操作数的计算结果必须为十进制或十六进制数。 十六进制数必须以“0x”开头。 **注意：** 在 XML 中，必须对字符 `<` 和 `>` 进行转义。 符号 `<` 表示为 `&lt;`。 符号 `>` 表示为 `&gt;`。|
|Exists('`stringA`')|如果存在名为 `stringA` 的文件或文件夹，则计算结果为 `true`。<br /><br /> 例如：<br /><br /> `Condition="!Exists('$(Folder)')"`<br /><br /> 对于简单的字母数字字符串或布尔值，不需要单引号。 但对于空值，单引号是必需的。|
|HasTrailingSlash('`stringA`')|如果指定的字符串末尾包含反斜杠 (\\) 或正斜杠 (/) 字符，则计算结果为 `true`。<br /><br /> 例如：<br /><br /> `Condition="!HasTrailingSlash('$(OutputPath)')"`<br /><br /> 对于简单的字母数字字符串或布尔值，不需要单引号。 但对于空值，单引号是必需的。|
|!|如果操作数计算结果为 `false`，则计算结果为 `true`。|
|`And`|如果两个操作数计算结果均为 `true`，则计算结果为 `true`。|
|`Or`|如果至少一个操作数计算结果为 `true`，则计算结果为 `true`。|
|()|如果内含表达式计算结果为 `true`，则分组机制的计算结果为 `true`。|
|$if$ ( %expression% ), $else$, $endif$|检查指定的 `%expression%` 是否与传递的自定义模板参数的字符串值相匹配。 如果 `$if$` 条件计算结果为 `true`，则其语句处于运行状态；否则，检查 `$else$` 条件。 如果 `$else$` 条件为 `true`，则其语句为运行状态；否则，`$endif$` 条件将结束表达式求值。<br /><br /> 有关用法的示例，请参阅 [Visual Studio Project/Item Template Parameter Logic](https://stackoverflow.com/questions/6709057/visual-studio-project-item-template-parameter-logic)（Visual Studio 项目/项模板参数逻辑）。|

在以下示例所示的情况下可以使用字符串方法，其中 [TrimEnd()](/dotnet/api/system.string.trimend) 函数仅用于比较字符串的相关部分，以区分 .NET Framework 与 .NET Core 目标框架。

```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <TargetFrameworks>net45;net48;netstandard2.1;netcoreapp2.1;netcoreapp3.1</TargetFrameworks>
    </PropertyGroup>

    <PropertyGroup Condition="'$(TargetFramework.TrimEnd(`0123456789`))' == 'net'">
        <!-- Properties for .NET Framework -->
    </PropertyGroup>

</Project>
```

在 MSBuild 项目文件中，没有真正的布尔类型。 布尔数据用属性表示，这些属性可能是空的，也可能设置为任何值。 因此，`'$(Prop)' == 'true'` 表示“如果 Prop 是 `true`，但 `'$(Prop)' != 'false'` 表示“如果 Prop 是 `true` 或者未设置，或者设置为其他内容。”

布尔逻辑只在条件的上下文中计算，因此，像 `<Prop2>'$(Prop1)' == 'true'</Prop>` 这样的属性设置是以（变量扩展后的）字符串的形式来表示的，而不是以布尔值的形式来计算。  

MSBuild 实现了一些特殊的处理规则，使其更容易处理用作布尔值的字符串属性。 接受布尔文本，因此 `Condition="true"` 和 `Condition="false"` 按预期方式工作。 MSBuild 还包括支持布尔求反运算符的特殊规则。 因此，如果 `$(Prop)` 为“true”，则 `!$(Prop)` 展开为 `!true`，这等于 `false`，与您预期的相同。

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [条件构造](../msbuild/msbuild-conditional-constructs.md)
- [演练：从头创建 MSBuild 项目文件](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)

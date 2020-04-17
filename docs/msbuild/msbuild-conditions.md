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
ms.assetid: 9d7aa308-b667-48ed-b4c9-a61e49eb0a85
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1f13910e2481e574e18c7a8efaee6601137c0720
ms.sourcegitcommit: b4e0cc76d94fe8cf6d238c4cc09512d17131a195
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2020
ms.locfileid: "81224467"
---
# <a name="msbuild-conditions"></a>MSBuild 条件

MSBuild 支持一组特定的条件，只要允许使用 `Condition` 属性，便应用这些条件。 下表对这些条件进行了说明。

|条件|描述|
|---------------|-----------------|
|'`stringA`' == '`stringB`'|如果 `stringA` 等于 `stringB`，则计算结果为 `true`。<br /><br /> 例如：<br /><br /> `Condition="'$(CONFIG)'=='DEBUG'"`<br /><br /> 对于简单的字母数字字符串或布尔值，不需要单引号。 但对于空值，单引号是必需的。 此检查不区分大小写。|
|'`stringA`' != '`stringB`'|如果 `stringA` 不等于 `stringB`，则计算结果为 `true`。<br /><br /> 例如：<br /><br /> `Condition="'$(CONFIG)'!='DEBUG'"`<br /><br /> 对于简单的字母数字字符串或布尔值，不需要单引号。 但对于空值，单引号是必需的。 此检查不区分大小写。|
|\<, >, \<=, >=|计算操作数的数值。 如果关系评估为 true，则返回 `true`。 操作数的计算结果必须为十进制或十六进制数。 十六进制数必须以“0x”开头。 **注意：** 在 XML 中，必须对字符 `<` 和 `>` 进行转义。 符号 `<` 表示为 `&lt;`。 符号 `>` 表示为 `&gt;`。|
|Exists('`stringA`')|如果存在名为 `stringA` 的文件或文件夹，则计算结果为 `true`。<br /><br /> 例如：<br /><br /> `Condition="!Exists('$(builtdir)')"`<br /><br /> 对于简单的字母数字字符串或布尔值，不需要单引号。 但对于空值，单引号是必需的。|
|HasTrailingSlash('`stringA`')|如果指定的字符串末尾包含反斜杠 (\\) 或正斜杠 (/) 字符，则计算结果为 `true`。<br /><br /> 例如：<br /><br /> `Condition="!HasTrailingSlash('$(OutputPath)')"`<br /><br /> 对于简单的字母数字字符串或布尔值，不需要单引号。 但对于空值，单引号是必需的。|
|!|如果操作数计算结果为 `false`，则计算结果为 `true`。|
|And|如果两个操作数计算结果均为 `true`，则计算结果为 `true`。|
|Or|如果至少一个操作数计算结果为 `true`，则计算结果为 `true`。|
|()|如果内含表达式计算结果为 `true`，则分组机制的计算结果为 `true`。|
|$if$ ( %expression% ), $else$, $endif$|检查指定的 `%expression%` 是否与传递的自定义模板参数的字符串值相匹配。 如果 `$if$` 条件计算结果为 `true`，则其语句处于运行状态；否则，检查 `$else$` 条件。 如果 `$else$` 条件为 `true`，则其语句为运行状态；否则，`$endif$` 条件将结束表达式求值。<br /><br /> 有关用法的示例，请参阅 [Visual Studio Project/Item Template Parameter Logic](https://stackoverflow.com/questions/6709057/visual-studio-project-item-template-parameter-logic)（Visual Studio 项目/项模板参数逻辑）。|

在以下示例所示的情况下可以使用字符串方法，其中 [TrimEnd()](/dotnet/api/system.string.trimend) 函数仅用于比较字符串的相关部分，以区分 .NET Framework 与 .NET Core 目标框架。

```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <TargetFrameworks>net45;net48;netstandard2.1;netcoreapp2.1;netcoreapp3.1</TargetFrameworks>
    </PropertyGroup>

    <PropertyGroup Condition="'$(TargetFramework.TrimEnd('0123456789.'))' == 'net'">
        <!-- Properties for .NET Framework -->
    </PropertyGroup>

</Project>
```

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [条件构造](../msbuild/msbuild-conditional-constructs.md)
- [演练：从头创建 MSBuild 项目文件](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)

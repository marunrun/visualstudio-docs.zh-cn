---
title: .VSCT 编译器 Command-Line 标志 |Microsoft Docs
description: Visual Studio 命令表编译器提供了命令行选项，以确保成功编译 .vsct 文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8d60b248a4941d176ac6ba4e808a94dbc67efbe7
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97488006"
---
# <a name="vsct-compiler-command-line-flags"></a>VSCT 编译器命令行标志
Visual Studio 命令表 (.VSCT) 编译器提供了命令行开关，以确保成功编译 .vsct 文件。

## <a name="command-line-parameters"></a>命令行参数
 若要在命令窗口中查看基本的 .VSCT 帮助 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]  ，请导航到 *Visual Studio SDK 安装路径*\VisualStudioIntegration\Tools\Bin\ 文件夹，然后键入：

```
vsct /?
```

 这样会返回：

```
Microsoft (R) Visual Studio (R) Command Table Compiler Version 3.00.2000

Syntax: vsct <infile> [<outfile>] [-S[symbols file]] [-D<preprocessor-define>]*
[-I<include-path>]* [-L<language>] [-E[C|H|N]:<name>]

  -D    Specify any additional preprocessor defines
  -I    Indicate what additional include paths to send to the preprocessor
  -L    Specify the language to use when selecting strings
  -E    Emit C# objects in the specified namespace for command items,
        followed by [L|F|H|N]:<value>
        F = Name of the file to emit (used if -EL is provided)
        L = Name of a language providing a CodeDOM provider
        N = namespace (required if -EL is provided)
        H = C++ header
  -c    Clean build skipping dependency checks
  -v    Verbose output
```

> [!NOTE]
> 字符- (破折号) 和/ (正斜杠) 都表示命令行参数。

 可接受的标志及其含义如下所示。

|开关|说明|
|------------|-----------------|
|-d|指定任何其他已定义的符号。|
|-I|指示解析文件引用时应使用的其他包含路径。|
|-l|指定 <xref:System.Globalization.CultureInfo> 区域性名称，例如 "en-us"。|
|-E|在指定的命名空间中发出命令项的 c # 对象，后跟 [C&#124;H&#124;N]：*filename*，其中 C = c #，H = c + + 标头，N = 命名空间。 C # 需要命名空间。|
|-v|详细输出。|

 -L 开关指示编译器选择一组字符串以生成对应于给定区域性名称的 cto 文件 <xref:System.Globalization.CultureInfo> 。 指定的区域性名称应与 .vsct 文件中一个或多个 [String 元素](../../extensibility/strings-element.md) 的 Language 特性匹配。 如果 String 元素没有 Language 特性，则它将从包含的 [CommandTable 元素](../../extensibility/commandtable-element.md)继承。

 .Vsct 文件可能包含多个字符串元素，并且每个元素都有不同的语言属性。 全球化是通过多次运行 .VSCT 编译器并更改每个区域性名称的-L 开关来实现的。

 如果-L 开关给定的区域性名称与任何字符串元素的 Language 特性都不匹配，则编译器将尝试匹配该语言，而不是区域。 例如，如果找不到 "en-us"，编译器将改为尝试 "en"。 如果失败，它将尝试操作系统的当前区域性。 如果失败，它将编译它找到的第一个字符串元素。

 -E 开关可用于发出 C 样式标头文件，其中包含命令表使用的符号，或发出包含命令符号对象的 c # 文件。

 -D 和-I 开关具有相同名称的 Cl.exe C 预处理器标志的语法。 具有 X = Y 格式的-D 定义用于扩展属性中基于 XML 的 \<Defined> 测试 `Condition` 。 -I 包含用于解析 \<Include> \<Extern> 和文件引用的路径 \<Bitmap> 。 有关详细信息，请参阅 [.VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)。

 .VSCT 编译器还可以反编译以前生成的二进制文件。 为此，请为提供一个二进制文件 \<infile> 。   如果二进制文件是由 .VSCT 编译器生成的，则它的符号将已嵌入，并且将生成输出中包含符号名称的输出 \<Symbols> 。 如果二进制文件是由 .CTC 编译器生成的，则输出将包含实际的 Guid 和 Id。 如果 Ctc.exe 的当前版本生成的 *. .ctsym 文件与二进制输入文件位于同一文件夹中，则将从该文件中加载符号，并将其用于输出。

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

---
title: VSCT 编译器命令行标志 |微软文档
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
ms.openlocfilehash: e4ee29710049453c3163c366eccf96e257b6028d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703957"
---
# <a name="vsct-compiler-command-line-flags"></a>VSCT 编译器命令行标志
可视化工作室命令表 （VSCT） 编译器提供命令行交换机，以确保成功编译 .vsct 文件。

## <a name="command-line-parameters"></a>命令行参数
 要查看从[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**命令**窗口的基本 VSCT 帮助，请查看*Visual Studio SDK 安装路径*[VisualStudio 集成]工具\Bin] 文件夹和类型：

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
> 字符 - （短划线） 和 / （前斜杠） 都是用于指示命令行参数的公认符号。

 可接受的标志及其含义如下所示。

|开关|描述|
|------------|-----------------|
|-d|指定任何其他定义的符号。|
|-I|指示解析文件引用时应使用的其他包含路径。|
|-l|指定<xref:System.Globalization.CultureInfo>区域性名称，例如"en-US"。|
|-E|在指定命名空间中为命令项发出 C# 对象，后跟 [C&#124;H&#124;N]：*文件名*C = C#，H = C++标头，N = 命名空间。 C# 需要命名空间。|
|-v|详细输出。|

 -L 开关指示编译器选择一组字符串来生成对应于给定<xref:System.Globalization.CultureInfo>区域性名称的二进制 .cto 文件。 指定的区域性名称应与 .vsct 文件中一个或多个[字符串元素](../../extensibility/strings-element.md)的语言属性匹配。 如果 Strings 元素没有语言属性，则从包含[命令表元素](../../extensibility/commandtable-element.md)继承它。

 .vsct 文件可能有多个字符串元素，并且每个元素可能具有不同的语言属性。 全球化是通过多次运行 VSCT 编译器并更改每个区域性名称的 -L 开关来实现的。

 如果 -L 开关提供的区域性名称与任何 Strings 元素的语言属性不匹配，编译器将尝试匹配该语言，而不是区域。 例如，如果找不到"en-US"，编译器将尝试"en"。" 否则，它将尝试操作系统的当前区域性。 否则，它将编译它找到的第一个字符串元素。

 -E 开关可用于发出包含命令表使用的符号的 C 样式标头文件，或发出包含命令符号对象的 C# 文件。

 -D 和 -I 开关具有具有相同名称的 Cl.exe C 预处理器标志的语法。 -具有 X_Y 格式的 D 定义用于扩展属性中\<`Condition`基于 XML 的已定义>测试。 -我包括用于解析\<包含>、extern \<> 和\<位图>文件引用的路径。 有关详细信息，请参阅[VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)。

 VSCT 编译器还可以取消编译以前构建的二进制文件。 为此，为\<infile>提供二进制文件。   如果二进制文件由 VSCT 编译器生成，它将已嵌入其符号，并将在输出的\<符号>部分中生成具有符号名称的输出。 如果二进制文件由 CTC 编译器生成，则输出将包含实际的 GUID 和 DO。 如果当前版本的 Ctc.exe 生成的 _.ctsym 文件与二进制输入文件位于同一文件夹中，则符号将从该文件加载并用于输出。

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

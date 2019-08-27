---
title: VSCT 编译器命令行标志 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 98cd0ec51ead200a904baeb409551cd1084f1f11
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440827"
---
# <a name="vsct-compiler-command-line-flags"></a>VSCT 编译器命令行标志
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 命令表 (VSCT) 编译器提供命令行开关以确保成功编译的.vsct 文件。  
  
## <a name="command-line-parameters"></a>命令行参数  
 若要查看从基本 VSCT 帮助[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]**命令**窗口中，导航到*Visual Studio SDK 安装路径*\VisualStudioIntegration\Tools\Bin\ 文件夹，然后键入：  
  
```  
vsct /?  
```  
  
 此命令返回：  
  
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
> 字符-（连字符） 和 / （正斜杠） 是这两个接受的表示法，该值指示命令行参数。  
  
 可接受标志和它们的含义如下所示。  
  
|开关|描述|  
|------------|-----------------|  
|-D|指定定义的任何其他符号。|  
|-I|指示附加的包含解析的文件引用时应使用的路径。|  
|-L|指定<xref:System.Globalization.CultureInfo>区域性名称，例如"EN-US"。|  
|-E|发出C#命令项的指定命名空间中的对象后跟 [C&#124;H&#124;N]:*文件名*其中 C = C#，H =C++标头，N = 命名空间。 需要适用于 C# 命名空间。|  
|-v|详细输出。|  
  
 -L 开关指示编译器选择字符串，以生成对应的二进制.cto 文件的一组给定<xref:System.Globalization.CultureInfo>区域性名称。 指定的区域性名称应与匹配一个或多个的 Language 特性[字符串元素](../../extensibility/strings-element.md).vsct 文件中。 如果字符串元素具有无语言属性，它继承自包含的[CommandTable 元素](../../extensibility/commandtable-element.md)。  
  
 .Vsct 文件可能有多个字符串元素，并且每个可能具有不同的语言属性。 全球化被通过运行多次的 VSCT 编译器并更改每个区域性名称-L 开关。  
  
 如果给定-L 开关的区域性名称不匹配任何字符串元素的 Language 特性，编译器将尝试匹配语言，而不是区域。 例如，如果找不到"EN-US"，编译器将改为尝试"en"。 如果不成功，它将尝试在操作系统的当前区域性。 如果不成功，它将编译它找到的第一个字符串元素。  
  
 -E 开关可用于发出包含命令表中，使用的符号的 C 样式标头文件或发出包含命令符号的对象的 C# 文件。  
  
 -D 和-我的交换机有具有相同名称的 Cl.exe C 预处理器标志的语法。 – D 具有格式 X = Y 并定义用于扩展的基于 XML 的\<定义 > 中的测试`Condition`属性。 – 我包含路径用于解析\<Include >， \<Extern > 和\<位图 > 文件引用。 有关详细信息，请参阅[VSCT XML Schema Reference](../../extensibility/vsct-xml-schema-reference.md)。  
  
 VSCT 编译器还可以反编译以前生成的二进制文件。 若要执行此操作，提供的二进制文件\<infile >。   如果二进制文件由 VSCT 编译器生成的它将具有已嵌入其符号，并将生成输出中的符号名称与\<符号 > 部分中的输出。 如果二进制文件由启动 CTC 编译器生成的输出将包含实际 Guid 和 Id。 如果生成的当前版本的 Ctc.exe *.ctsym 文件是二进制的输入文件所在的同一文件夹中，则将从该文件中加载符号，并将其用于输出。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 命令表 (。Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)   
 [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

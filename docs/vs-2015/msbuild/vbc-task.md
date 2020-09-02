---
title: Vbc 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Vbc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Vbc task [MSBuild]
- MSBuild, Vbc task
ms.assetid: 595278b1-2782-4577-b1ba-b4b5ab5625a3
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6edc8b246055dcd8efdb32f4118f81a535635d55
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683812"
---
# <a name="vbc-task"></a>Vbc 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包装可生成可执行文件 (.exe)、动态链接库 (.dll) 或代码模块 (.netmodule) 的 vbc.exe。 有关 vbc.exe 的详细信息，请参阅 [Visual Basic 命令行编译器](https://msdn.microsoft.com/library/6b57c444-50c7-4b88-8f59-ed65cff5e05c)。  
  
## <a name="parameters"></a>参数  
 下表描述了 `Vbc` 任务的参数。  
  
|参数|描述|  
|---------------|-----------------|  
|`AdditionalLibPaths`|可选 `String[]` 参数。<br /><br /> 指定要在其中查找 References 属性中指定的程序集的其他文件夹。|  
|`AddModules`|可选 `String[]` 参数。<br /><br /> 使编译器让指定文件中的所有类型信息可供当前正在编译的项目使用。 此参数对应于 vbc.exe 编译器的 [/addmodule](https://msdn.microsoft.com/library/fb4b89d4-4926-4f20-868d-427fa28497b2) 开关。|  
|`BaseAddress`|可选 `String` 参数。<br /><br /> 指定 DLL 的基址。 此参数对应于 vbc.exe 编译器的 [/baseaddress](https://msdn.microsoft.com/library/c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47) 开关。|  
|`CodePage`|可选 `Int32` 参数。<br /><br /> 指定要用于编译中所有源代码文件的代码页。 此参数对应于 vbc.exe 编译器的 [/codepage](https://msdn.microsoft.com/library/be36ec33-6800-4505-838c-4124564f5cc9) 开关。|  
|`DebugType`|可选 `String[]` 参数。<br /><br /> 让编译器生成调试信息。 此参数可以具有下列值：<br /><br /> -   `full`<br />-   `pdbonly`<br /><br /> 默认值为 `full`，该值允许将调试器附加到正在运行的程序。 `pdbonly` 的值允许在调试器中启动程序时进行源代码调试，但仅在正在运行的程序附加到调试器时才显示汇编语言代码。 有关详细信息，请参阅 [/debug (Visual Basic) ](https://msdn.microsoft.com/library/c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2)。|  
|`DefineConstants`|可选 `String[]` 参数。<br /><br /> 定义条件编译器常数。 符号/值对是使用下面的语法指定的，并且彼此之间用分号分隔：<br /><br /> *symbol1* `=` *value1* `;` *symbol2* `=` *value2*<br /><br /> 此参数对应于 vbc.exe 编译器的 [/define](https://msdn.microsoft.com/library/f735c57d-1cf9-4f2f-a26f-0de630fd4077) 开关。|  
|`DelaySign`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，任务会将公钥放在程序集中。 如果为 `false`，任务会充分为程序集签名。 默认值为 `false`。除非与 `KeyFile` 参数或 `KeyContainer` 参数一起使用，否则此参数无效。 此参数对应于 vbc.exe 编译器的 [/delaysign](https://msdn.microsoft.com/library/c76e61a4-1884-4252-9fb2-377f99caa690) 开关。|  
|`DisabledWarnings`|可选 `String` 参数。<br /><br /> 禁止显示指定的警告。 只需指定警告标识符的数值部分。 多个警告之间用分号分隔。 此参数对应于 vbc.exe 编译器的 [/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83) 开关。|  
|`DocumentationFile`|可选 `String` 参数。<br /><br /> 将文档注释处理到指定的 XML 文件中。 此参数替代 `GenerateDocumentation` 属性。 有关详细信息，请参阅 [/doc](https://msdn.microsoft.com/library/5fc32ec9-a149-4648-994c-a8d0cccd0a65)。|  
|`EmitDebugInformation`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则该任务生成调试信息并将它放置在 pdb 文件中。 有关详细信息，请参阅 [/debug (Visual Basic) ](https://msdn.microsoft.com/library/c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2)。|  
|`ErrorReport`|可选 `String` 参数。<br /><br /> 指定任务报告内部编译器错误的方式。 此参数可以具有下列值：<br /><br /> -   `prompt`<br />-   `send`<br />-   `none`<br /><br /> 如果指定了 `prompt`，且发生内部编译器错误，则会提示用户选择是否将错误数据发送给 Microsoft。<br /><br /> 如果指定了 `send`，且发生内部编译器错误，则该任务会向 Microsoft 发送错误数据。<br /><br /> 默认值是 `none`，它仅在文本输出中报告错误。<br /><br /> 此参数对应于 vbc.exe 编译器的 [/errorreport](https://msdn.microsoft.com/library/a7fe83a2-a6d8-460c-8dad-79a8f433f501) 开关。|  
|`FileAlignment`|可选 `Int32` 参数。<br /><br /> 指定输出文件各部分的对齐位置，以字节为单位。 此参数可以具有下列值：<br /><br /> -   `512`<br />-   `1024`<br />-   `2048`<br />-   `4096`<br />-   `8192`<br /><br /> 此参数对应于 vbc.exe 编译器的 [/filealign](https://msdn.microsoft.com/library/cc61ec3d-ad38-4b28-9659-099d73cad099) 开关。|  
|`GenerateDocumentation`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则会生成文档信息，并将此信息与任务创建的可执行文件或库的名称一同放置在 XML 文件中。 有关详细信息，请参阅 [/doc](https://msdn.microsoft.com/library/5fc32ec9-a149-4648-994c-a8d0cccd0a65)。|  
|`Imports`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 从指定项集合导入命名空间。 此参数对应于 vbc.exe 编译器的 [/imports](https://msdn.microsoft.com/library/9a93fb53-c080-497b-bf9b-441022dbbc39) 开关。|  
|`KeyContainer`|可选 `String` 参数。<br /><br /> 指定加密密钥容器的名称。 此参数对应于 vbc.exe 编译器的 [/keycontainer](https://msdn.microsoft.com/library/6a9bc861-1752-4db1-9f64-b5252f0482cc) 开关。|  
|`KeyFile`|可选 `String` 参数。<br /><br /> 指定含有加密密钥的文件名。 有关详细信息，请参阅 [/keyfile](https://msdn.microsoft.com/library/ffa82a4b-517a-4c6c-9889-5bae7b534bb8)。|  
|`LangVersion`|可选 [String](<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) 参数。<br /><br /> 指定语言版本，“9”或“10”。|  
|`LinkResources`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 创建指向输出文件中的 .NET Framework 资源的链接；资源文件不会放入输出文件中。 此参数对应于 vbc.exe 编译器的 [/linkresource](https://msdn.microsoft.com/library/cf4dcad8-17b7-404c-9184-29358aa05b15) 开关。|  
|`MainEntryPoint`|可选 `String` 参数。<br /><br /> 指定包含 `Sub Main` 过程的类或模块。 此参数对应于 vbc.exe 编译器的 [/main](https://msdn.microsoft.com/library/83fc339d-6652-415d-b205-b5133319b5b0) 开关。|  
|`ModuleAssemblyName`|可选 `String` 参数。<br /><br /> 指定此模块所属程序集。|  
|`NoConfig`|可选 `Boolean` 参数。<br /><br /> 指定编译器不应使用 vbc.rsp 文件。 此参数对应于 vbc.exe 编译器的 [/noconfig](https://msdn.microsoft.com/library/a7405067-bd21-4171-adf4-a126fa3ad6c3) 参数。|  
|`NoLogo`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则禁止显示编译器横幅信息。 此参数对应于 vbc.exe 编译器的 [/nologo](https://msdn.microsoft.com/library/25ef54b6-d676-4639-a2d2-a747a158bc07) 开关。|  
|`NoStandardLib`|可选 `Boolean` 参数。<br /><br /> 导致编译器不引用标准库。 此参数对应于 vbc.exe 编译器的 [/nostdlib](https://msdn.microsoft.com/library/140381b8-dc96-4ad5-ae11-792c9ed0be4d) 开关。|  
|`NoVBRuntimeReference`|可选 `Boolean` 参数。<br /><br /> 仅限内部使用。 如果为 true，则会阻止自动引用 Microsoft.VisualBasic.dll.|  
|`NoWarnings`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，任务会禁止所有警告。 有关详细信息，请参阅 [/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83)。|  
|`Optimize`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则会启用编译器优化。 此参数对应于 vbc.exe 编译器的 [/optimize](https://msdn.microsoft.com/library/fcba4a97-3622-4b87-a891-0f77deab4998) 开关。|  
|`OptionCompare`|可选 `String` 参数。<br /><br /> 指定如何进行字符串比较。 此参数可以具有下列值：<br /><br /> -   `binary`<br />-   `text`<br /><br /> 值 `binary` 指定该任务使用二进制字符串比较。 值 `text` 指定该任务使用文本字符串比较。 此参数的默认值为 `binary`。 此参数对应于 vbc.exe 编译器的 [/optioncompare](https://msdn.microsoft.com/library/7237b766-b44d-4cc5-9a3c-885348a7d9e4) 开关。|  
|`OptionExplicit`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则要求显式声明变量。 此参数对应于 vbc.exe 编译器的 [/optionexplicit](https://msdn.microsoft.com/library/5d296ab3-bafe-4c4d-9887-78f162ed86c7) 开关。|  
|`OptionInfer`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则允许对变量进行类型推理。|  
|`OptionStrict`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则任务强制执行严格类型语义，限制隐式类型转换。 此参数对应于 vbc.exe 编译器的 [/optionstrict](https://msdn.microsoft.com/library/c7b10086-0fa4-49db-b3c8-4ae0db5957da) 开关。|  
|`OptionStrictType`|可选 `String` 参数。<br /><br /> 指定生成警告的严格类型语义。 当前仅支持“custom”。 此参数对应于 vbc.exe 编译器的 [/optionstrict](https://msdn.microsoft.com/library/c7b10086-0fa4-49db-b3c8-4ae0db5957da) 开关。|  
|`OutputAssembly`|可选 `String` 输出参数。<br /><br /> 指定输出文件的名称。 此参数对应于 vbc.exe 编译器的 [/out](https://msdn.microsoft.com/library/9f148c15-0909-4cb8-a2db-777f8a8b45ae) 开关。|  
|`Platform`|可选 `String` 参数。<br /><br /> 指定将作为输出文件目标的处理器平台。 此参数可以具有 `x86`、 `x64``Itanium` 或 `anycpu` 的值。 默认值为 `anycpu`。 此参数对应于 vbc.exe 编译器的 [/platform](https://msdn.microsoft.com/library/f9bc61e6-e854-4ae1-87b9-d6244de23fd1) 开关。|  
|`References`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 促使该任务将公共类型信息从指定项导入到当前项目中。 此参数对应于 vbc.exe 编译器的 [/reference](https://msdn.microsoft.com/library/66bdfced-bbf6-43d1-a554-bc0990315737) 开关。|  
|`RemoveIntegerChecks`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则禁用整数溢出错误检查。 默认值为 `false`。 此参数对应于 vbc.exe 编译器的 [/removeintchecks](https://msdn.microsoft.com/library/c1835bd5-1e38-4fba-bd2f-6984774765d4) 开关。|  
|`Resources`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 将 .NET Framework 资源嵌入到输出文件。 此参数对应于 vbc.exe 编译器的 [/resource](https://msdn.microsoft.com/library/eee2f227-91f2-4f2b-a9d6-1c51c5320858) 开关。|  
|`ResponseFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定包含此任务命令的响应文件。 此参数对应于 vbc.exe 编译器的 [@ (指定响应文件)](https://msdn.microsoft.com/library/a6847eaa-e5f9-4303-9421-45b55484b9ca)选项  。|  
|`RootNamespace`|可选 `String` 参数。<br /><br /> 指定所有类型声明的根命名空间。 此参数对应于 vbc.exe 编译器的 [/rootnamespace](https://msdn.microsoft.com/library/e9245edf-6bef-420d-a7c7-324117752783) 开关。|  
|`SdkPath`|可选 `String` 参数。<br /><br /> 指定 mscorlib.dll 和 microsoft.visualbasic.dll 的位置。 此参数对应于 vbc.exe 编译器的 [/sdkpath](https://msdn.microsoft.com/library/fec8a3f1-b791-4a37-8af7-344859f8212d) 开关。|  
|`Sources`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定一个或多个 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 源文件。|  
|`TargetCompactFramework`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则任务面向 [!INCLUDE[Compact](../includes/compact-md.md)]。 此开关对应于 vbc.exe 编译器的 [/netcf](https://msdn.microsoft.com/library/db7cfa59-c315-401c-a59b-0daf355343d6) 开关。|  
|`TargetType`|可选 `String` 参数。<br /><br /> 指定输出文件的文件格式。 此参数可以具有 `library` 或 `winexe` 的值，前者将创建代码库 `exe`，代码库将创建控制台应用程序 `module`，应用程序将创建一个模块，后者将创建 Windows 程序。 默认值为 `library`。 此参数对应于 vbc.exe 编译器的 [/target](https://msdn.microsoft.com/library/e0954147-548b-461f-9c4b-a8f88845616c) 开关。|  
|`Timeout`|可选 `Int32` 参数。<br /><br /> 指定终止任务可执行文件之前的时间量（以毫秒为单位）。 默认值是 `Int.MaxValue`，指示没有超时期限。|  
|`ToolPath`|可选 `String` 参数。<br /><br /> 指定任务从中加载基础可执行文件 (vbc.exe) 的位置。 如果未指定此参数，则任务会使用与运行 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 的框架版本对应的 SDK 安装路径。|  
|`TreatWarningsAsErrors`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则会将所有警告视为错误。 有关详细信息，请参阅 [/warnaserror (Visual Basic) ](https://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1)。|  
|`UseHostCompilerIfAvailable`|可选 `Boolean` 参数。<br /><br /> 指示该任务使用进程内编译器对象（如果可用）。 仅由 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 使用。|  
|`Utf8Output`|可选 `Boolean` 参数。<br /><br /> 记录使用 UTF-8 编码的编译器输出。 此参数对应于 vbc.exe 编译器的 [/utf8output](https://msdn.microsoft.com/library/8ab36b1e-027a-49ac-85b4-f48997d9e4d6) 开关。|  
|`Verbosity`|可选 `String` 参数。<br /><br /> 指定编译器输出的详细级别。 详细级别可以为 `Quiet`、`Normal`（默认）或 `Verbose`。|  
|`WarningsAsErrors`|可选 `String` 参数。<br /><br /> 指定将被视为错误的警告的列表。 有关详细信息，请参阅 [/warnaserror (Visual Basic) ](https://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1)。<br /><br /> 此参数替代 `TreatWarningsAsErrors` 参数。|  
|`WarningsNotAsErrors`|可选 `String` 参数。<br /><br /> 指定不被视为错误的警告的列表。 有关详细信息，请参阅 [/warnaserror (Visual Basic) ](https://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1)。<br /><br /> 只有 `TreatWarningsAsErrors` 参数设置为 `true` 时，此参数才有用。|  
|`Win32Icon`|可选 `String` 参数。<br /><br /> 在程序集中插入 .ico 文件，为输出文件赋予其在文件资源管理器中所需的外观。 此参数对应于 vbc.exe 编译器的 [/win32icon](https://msdn.microsoft.com/library/aecaab01-9353-46c5-941c-6edabd4eff92) 开关。|  
|`Win32Resources`|可选 `String` 参数。<br /><br /> 在输出文件中插入 Win32 资源 (.res) 文件。 此参数对应于 vbc.exe 编译器的 [/win32resource](https://msdn.microsoft.com/library/e226946d-19ce-4cc9-91f5-aed24f77aa2b) 开关。|  
  
## <a name="remarks"></a>备注  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.ToolTask> 类。 有关这些其他参数及其说明的列表，请参阅 [ToolTaskExtension 基类](../msbuild/tooltaskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 以下示例编译 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 项目。  
  
```  
<VBC  
   Sources="@(sources)"  
   Resources="strings.resources"  
   Optimize="true"  
   OutputAssembly="out.exe"/>  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](https://msdn.microsoft.com/library/6b57c444-50c7-4b88-8f59-ed65cff5e05c)   
 [操作](../msbuild/msbuild-tasks.md)   
 [任务引用](../msbuild/msbuild-task-reference.md)

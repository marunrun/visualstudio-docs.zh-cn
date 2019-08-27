---
title: Csc 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Csc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Csc task [MSBuild]
- MSBuild, Csc task
ms.assetid: d8c19b36-f5ca-484b-afa6-8ff3b90e103a
caps.latest.revision: 30
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e0dd27fe64982e77872e37ec01dbdb71a0a141ae
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694105"
---
# <a name="csc-task"></a>Csc 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包装 CSC.exe，生成可执行 (.exe) 文件、动态链接库（.dll文件）或者代码模块（.netmodule文件）。 有关 CSC.exe 的详细信息，请参阅 [C# 编译器选项](https://msdn.microsoft.com/library/d3403556-1816-4546-a782-e8223a772e44)。  
  
## <a name="parameters"></a>参数  
 下表描述了 `Csc` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`AdditionalLibPaths`|可选 `String[]` 参数。<br /><br /> 指定要在其中搜索引用的其他目录。 有关详细信息，请参阅 [/lib（C# 编译器选项）](https://msdn.microsoft.com/library/b0efcc88-e8aa-4df4-a00b-8bdef70b7673)。|  
|`AddModules`|可选 `String` 参数。<br /><br /> 指定将构成程序集一部分的一个或多个模块。 有关详细信息，请参阅 [/addmodule（C# 编译器选项）](https://msdn.microsoft.com/library/ed604546-0dc2-4bd4-9a3e-610a8d973e58)。|  
|`AllowUnsafeBlocks`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则编译使用 [unsafe](https://msdn.microsoft.com/library/7e818009-1c6e-4b9e-b769-3728a01586a0) 关键字的代码。 有关详细信息，请参阅 [/unsafe（C# 编译器选项）](https://msdn.microsoft.com/library/fdb77ed9-da03-45bd-bb7f-250704da1bcc)。|  
|`ApplicationConfiguration`|可选 `String` 参数。<br /><br /> 指定包含程序集绑定设置的应用程序配置文件。|  
|`BaseAddress`|可选 `String` 参数。<br /><br /> 指定要加载 DLL 的首选基址。 DLL 的默认基址由 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 公共语言运行时设置。 有关详细信息，请参阅 [/baseaddress（C# 编译器选项）](https://msdn.microsoft.com/library/ce13c965-dfe4-4433-94f5-63b476e3a608)。|  
|`CheckForOverflowUnderflow`|可选 `Boolean` 参数。<br /><br /> 指定溢出数据类型边界的整数算法是否导致运行时异常。 有关详细信息，请参阅 [/checked（C# 编译器选项）](https://msdn.microsoft.com/library/fb7475d3-e6a6-4e6d-b86c-69e7a74c854b)。|  
|`CodePage`|可选 `Int32` 参数。<br /><br /> 指定要用于编译中所有源代码文件的代码页。 有关详细信息，请参阅 [/codepage（C# 编译器选项）](https://msdn.microsoft.com/library/75942989-b69a-4308-90a0-840c73d2c478)。|  
|`DebugType`|可选 `String` 参数。<br /><br /> 指定调试类型。 `DebugType` 可以是 `full` 或 `pdbonly`。 默认值是 `full`，这使得调试程序能够附加到正在运行的程序中。 指定在调试程序中启动该程序时，`pdbonly` 启用源代码调试，但正在运行的程序附加到调试程序时，只显示汇编程序。<br /><br /> 此参数替代 `EmitDebugInformation` 参数。<br /><br /> 有关详细信息，请参阅 [/debug (C# 编译器选项)](https://msdn.microsoft.com/library/e2b48c07-01bc-45cc-a52c-92e9085eb969)。|  
|`DefineConstants`|可选 `String` 参数。<br /><br /> 定义预处理器符号。 有关详细信息，请参阅 [/define（C# 编译器选项）](https://msdn.microsoft.com/library/f17d7b4d-82d0-4133-8563-68cced1cac6e)。|  
|`DelaySign`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则指定需要完全签名的程序集。 如果为 `false`，则指定仅需要将公钥放在程序集中。<br /><br /> 此参数无任何效果，除非与 `KeyFile` 或 `KeyContainer` 参数配合使用。<br /><br /> 有关详细信息，请参阅 [/delaysign（C# 编译器选项）](https://msdn.microsoft.com/library/bcb058eb-2933-4e7f-b356-5c941db4de75)。|  
|`DisabledWarnings`|可选 `String` 参数。<br /><br /> 指定要禁用的警告的列表。 有关详细信息，请参阅 [/nowarn（C# 编译器选项）](https://msdn.microsoft.com/library/6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4)。|  
|`DocumentationFile`|可选 `String` 参数。<br /><br /> 将文档注释处理到一个 XML 文件中。 有关详细信息，请参阅 [/doc（C# 编译器选项）](https://msdn.microsoft.com/library/849eea59-c936-4311-bad8-d07404480f2a)。|  
|`EmitDebugInformation`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则该任务生成调试信息并将它放置在程序数据库 (pdb) 文件中。 如果为 `false`，则此任务不发出任何调试信息。 默认值为 `false`。 有关详细信息，请参阅 [/debug (C# 编译器选项)](https://msdn.microsoft.com/library/e2b48c07-01bc-45cc-a52c-92e9085eb969)。|  
|`ErrorReport`|可选 `String` 参数。<br /><br /> 提供向 Microsoft 报告 C# 内部错误的简便方法。 此参数可以具有 `prompt`、`send` 或 `none` 的值。 如果该参数设置为 `prompt`，则内部编译器错误发生时，你将收到一条提示。 该提示让你将一个 Bug 报告以电子方式发送给 Microsoft。 如果该参数设置为 `send`，则系统将自动发送 Bug 报告。 如果该参数设置为 `none`，则仅在编译器的文本输出中报告错误。 默认值为 `none`。 有关详细信息，请参阅 [/errorreport（C# 编译器选项）](https://msdn.microsoft.com/library/bd0e7493-b79d-4369-9c3f-ba26ebdfbedf)。|  
|`FileAlignment`|可选 `Int32` 参数。<br /><br /> 指定输出文件中各节的大小。 有关详细信息，请参阅 [/filealign（C# 编译器选项）](https://msdn.microsoft.com/library/15cf1c98-3798-4ced-9f08-60619308a073)。|  
|`GenerateFullPaths`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则指定编译器输出中文件的绝对路径。 如果为 `false`，则指定文件的名称。 默认值为 `false`。 有关详细信息，请参阅 [/fullpaths（C# 编译器选项）](https://msdn.microsoft.com/library/d2a5f857-cbb2-430b-879c-d648aaf0b8c4)。|  
|`KeyContainer`|可选 `String` 参数。<br /><br /> 指定加密密钥容器的名称。 有关详细信息，请参阅 [/keycontainer（C# 编译器选项）](https://msdn.microsoft.com/library/b3982b6d-2382-4f7e-bebd-ce98eaa30763)。|  
|`KeyFile`|可选 `String` 参数。<br /><br /> 指定含有加密密钥的文件名。 有关详细信息，请参阅 [/keyfile（C# 编译器选项）](https://msdn.microsoft.com/library/0815f9de-ace4-4e98-b4c6-13c55dea40c2)。|  
|`LangVersion`|可选 `String` 参数。<br /><br /> 指定要使用的语言版本。 有关详细信息，请参阅 [/langversion（C# 编译器选项）](https://msdn.microsoft.com/library/3fb00b05-a0ff-4782-b313-13a4c0f62d94)。|  
|`LinkResources`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 创建指向输出文件中的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 资源的链接；资源文件不会放入输出文件中。<br /><br /> 传递到此参数的项可以具有名为 `LogicalName` 和 `Access` 的可选元数据条目。 `LogicalName` 对应于 `/linkresource` 开关的 `identifier` 参数，`Access` 对应于 `accessibility-modifier` 参数。 有关详细信息，请参阅 [/linkresource (C# 编译器选项)](https://msdn.microsoft.com/library/440c26c2-77c1-4811-a0a3-57cce3f5fc96)。|  
|`MainEntryPoint`|可选 `String` 参数。<br /><br /> 指定 `Main` 方法的位置。 有关详细信息，请参阅 [/main（C# 编译器选项）](https://msdn.microsoft.com/library/975cf4d5-36ac-4530-826c-4aad0c7f2049)。|  
|`ModuleAssemblyName`|可选 `String` 参数。<br /><br /> 指定此模块所属程序集的名称。|  
|`NoConfig`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则告知编译器不使用 csc.rsp 文件进行编译。 有关详细信息，请参阅 [/noconfig (C# 编译器选项)](https://msdn.microsoft.com/library/cd26967e-e494-4c8c-b5c9-af13b2f78b2e)。|  
|`NoLogo`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则禁止显示编译器横幅信息。 有关详细信息，请参阅 [/nologo (C# 编译器选项)](https://msdn.microsoft.com/library/426afb36-a8fb-469d-9c45-a35d9512557c)。|  
|`NoStandardLib`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则防止导入 mscorlib.dll，这定义了整个 System 命名空间。 如果你想要定义或创建自己的 System 命名空间和对象，请使用此参数。 有关详细信息，请参阅 [/nostdlib（C# 编译器选项）](https://msdn.microsoft.com/library/ec197989-fa49-4725-a455-e06b551eb65f)。|  
|`NoWin32Manifest`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则不包括默认的 Win32 清单。|  
|`Optimize`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则启用优化。 如果为 `false`，则禁用优化。 有关详细信息，请参阅 [/optimize（C# 编译器选项）](https://msdn.microsoft.com/library/6dd5b6f2-cd1d-4593-a9f4-1c2ed9404ca0)。|  
|`OutputAssembly`|可选 `String` 输出参数。<br /><br /> 指定输出文件的名称。 有关详细信息，请参阅 [/out（C# 编译器选项）](https://msdn.microsoft.com/library/70d91d01-7bd2-4aea-ba8b-4e9807e9caa5)。|  
|`PdbFile`|可选 `String` 参数。<br /><br /> 指定调试信息文件名。 默认名称是扩展名为 .pdb 的输出文件名。|  
|`Platform`|可选 `String` 参数。<br /><br /> 指定将作为输出文件目标的处理器平台。 此参数可以具有 `x86`、`x64` 或 `anycpu` 的值。 默认值为 `anycpu`。 有关详细信息，请参阅 [/platform（C# 编译器选项）](https://msdn.microsoft.com/library/c290ff5e-47f4-4a85-9bb3-9c2525b0be04)。|  
|`References`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 促使该任务将公共类型信息从指定项导入到当前项目中。 有关详细信息，请参阅 [/reference（C# 编译器选项）](https://msdn.microsoft.com/library/8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4)。<br /><br /> 你可以通过将元数据 `Aliases` 添加到原始的“参考”项，在 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 文件中指定 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 引用别名。 例如，在以下 CSC 命令行中设置别名“LS1”：<br /><br /> `csc /r:LS1=MyCodeLibrary.dll /r:LS2=MyCodeLibrary2.dll *.cs`<br /><br /> 将使用：<br /><br /> `<Reference Include="MyCodeLibrary"> <Aliases>LS1</Aliases> </Reference>`|  
|`Resources`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 将 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 资源嵌入到输出文件中。<br /><br /> 传递到此参数的项可以具有名为 `LogicalName` 和 `Access` 的可选元数据条目。 `LogicalName` 对应于 `/resource` 开关的 `identifier` 参数，`Access` 对应于 `accessibility-modifier` 参数。 有关详细信息，请参阅 [/resource (C# 编译器选项)](https://msdn.microsoft.com/library/5212666e-98ab-47e4-a497-b5545ab15c7f)。|  
|`ResponseFiles`|可选 `String` 参数。<br /><br /> 指定包含此任务命令的响应文件。 有关详细信息，请参阅 [@（指定响应文件）](https://msdn.microsoft.com/library/dda4fa9f-a02c-400f-8b6a-d58834e13d7f)。|  
|`Sources`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定一个或多个 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 源文件。|  
|`TargetType`|可选 `String` 参数。<br /><br /> 指定输出文件的文件格式。 此参数可以具有 `library` 或 `winexe` 的值，前者将创建代码库 `exe`，代码库将创建控制台应用程序 `module`，应用程序将创建一个模块，后者将创建 Windows 程序。 默认值为 `library`。 有关详细信息，请参阅 [/target（C# 编译器选项）](https://msdn.microsoft.com/library/a18bbd8e-bbf7-49e7-992c-717d0eb1f76f)。|  
|`TreatWarningsAsErrors`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则将所有警告视为错误。 有关详细信息，请参阅 [/warnaserror（C# 编译器选项）](https://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c)。|  
|`UseHostCompilerIfAvailable`|可选 `Boolean` 参数。<br /><br /> 指示该任务使用进程内编译器对象（如果可用）。 仅由 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 使用。|  
|`Utf8Output`|可选 `Boolean` 参数。<br /><br /> 记录使用 UTF-8 编码的编译器输出。 有关详细信息，请参阅 [/utf8output（C# 编译器选项）](https://msdn.microsoft.com/library/27ff7381-c281-45d7-b2eb-1ad644b1354e)。|  
|`WarningLevel`|可选 `Int32` 参数。<br /><br /> 指定编译器显示的警告级别。 有关详细信息，请参阅 [/warn（C# 编译器选项）](https://msdn.microsoft.com/library/5f80ff59-4991-4382-9f9a-77da18446e71)。|  
|`WarningsAsErrors`|可选 `String` 参数。<br /><br /> 指定将被视为错误的警告的列表。 有关详细信息，请参阅 [/warnaserror（C# 编译器选项）](https://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c)。<br /><br /> 此参数替代 `TreatWarningsAsErrors` 参数。|  
|`WarningsNotAsErrors`|可选 `String` 参数。<br /><br /> 指定不被视为错误的警告的列表。 有关详细信息，请参阅 [/warnaserror（C# 编译器选项）](https://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c)。<br /><br /> 只有 `TreatWarningsAsErrors` 参数设置为 `true` 时，此参数才有用。|  
|`Win32Icon`|可选 `String` 参数。<br /><br /> 在程序集中插入 .ico 文件，为输出文件赋予其在文件资源管理器中所需的外观。 有关详细信息，请参阅 [/win32icon (C# 编译器选项)](https://msdn.microsoft.com/library/756d9b6d-ab07-41b7-ba58-5bd88f711138)。|  
|`Win32Manifest`|可选 `String` 参数。<br /><br /> 指定要包含的 Win32 清单。|  
|`Win32Resource`|可选 `String` 参数。<br /><br /> 在输出文件中插入 Win32 资源 (.res) 文件。 有关详细信息，请参阅 [/win32res（C# 编译器选项）](https://msdn.microsoft.com/library/3c33f750-6948-4c7e-a27e-bef98f77255b)。|  
  
## <a name="remarks"></a>备注  
 除上面列出的参数外，此任务还从 `Microsoft.Build.Tasks.ManagedCompiler` 类继承参数，该类继承自 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类（它自身继承自 <xref:Microsoft.Build.Utilities.ToolTask> 类）。 有关这些其他参数及其说明的列表，请参阅 [ToolTaskExtension 基类](../msbuild/tooltaskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 以下示例使用 `Csc` 任务来编译 `Compile` 项集合的源文件中的可执行文件。  
  
```  
<CSC  
    Sources="@(Compile)"  
    OutputAssembly="$(AppName).exe"  
    EmitDebugInformation="true" />  
```  
  
## <a name="see-also"></a>请参阅  
 [任务参考](../msbuild/msbuild-task-reference.md)   
 [任务](../msbuild/msbuild-tasks.md)

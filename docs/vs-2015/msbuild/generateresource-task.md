---
title: GenerateResource 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateResource
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateResource task
- GenerateResource task [MSBuild]
ms.assetid: c0aff32f-f2cc-46f6-9c3e-a5c9f8f912b1
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 712d0de957ff7f780567c927fb1b18b100f8f6ca
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703517"
---
# <a name="generateresource-task"></a>GenerateResource 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

将文本 .txt 和 .resx（基于 XML 的资源格式）文件转换为公共语言运行时二进制 .resources 文件，这些 .resources 文件可嵌入到运行时二进制可执行文件中或编译到附属程序集中。 此任务通常用于将 .txt 或 .resx 文件转换为 .resource 文件。 `GenerateResource` 任务在功能上类似于 [resgen.exe](https://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4)。  
  
## <a name="parameters"></a>参数  
 下表描述了 `GenerateResource` 任务的参数。  
  
|参数|描述|  
|---------------|-----------------|  
|`AdditionalInputs`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 包含此任务完成的依赖项检查的其他输入。 例如，项目和目标通常应该为输入，以便在对它们进行更新时，所有资源都重新生成。|  
|`EnvironmentVariables`|可选 `String[]` 参数。<br /><br /> 除（或选择性替代）常规环境块外，还指定应传递到生成的 resgen.exe 中的环境变量的名称/值对数组。|  
|`ExcludedInputPaths`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定项的数组，这些项指定在更新检查期间将从中忽略跟踪输入的路径。|  
|`ExecuteAsTool`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，请于进程外从适当的目标框架运行 tlbimp.exe 和 aximp.exe 来生成所需的包装器程序集。 此参数允许多目标的 `ResolveComReferences`。|  
|`FilesWritten`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含写入磁盘的所有文件的名称。 其中包含缓存文件（如果存在）。 此参数对实现 Clean 非常有用。|  
|`MinimalRebuildFromTracking`|可选 `Boolean` 参数。<br /><br /> 获取或设置一个开关，用于指定是否使用跟踪的增量生成。 如果为 `true`，则启用增量生成；否则，将强制执行重新生成。|  
|`NeverLockTypeAssemblies`|可选 `Boolean` 参数。<br /><br /> 指定生成的文件（如 .resources 文件）的名称。 如果不指定名称，则会使用匹配输入文件的名称，且创建的 .resources 文件会放在包含此输入文件的目录之中。|  
|`OutputResources`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定生成的文件（如 .resources 文件）的名称。 如果不指定名称，则会使用匹配输入文件的名称，且创建的 .resources 文件会放在包含此输入文件的目录之中。|  
|`PublicClass`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则会将强类型的资源类创建为公共类。|  
|`References`|可选 `String[]` 参数。<br /><br /> 要从中加载 .resx 文件中的类型的引用。 Resx 文件数据元素可能具有 .NET 类型。 读取 .resx 文件时，必须对此进行解析。 通常，使用标准类型加载规则可成功解析。 如果在 `References` 中提供程序集，则它们具有优先级。<br /><br /> 强类型资源不要求此参数。|  
|`SdkToolsPath`|可选 `String` 参数。<br /><br /> 指定 SDK 工具（例如 resgen.exe）的路径。|  
|`Sources`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要转换的项。 传递到此参数的项必须具有以下文件扩展名之一：<br /><br /> -   `.txt`：指定要转换的文本文件的扩展名。 文本文件只能包含字符串资源。<br />-   `.resx`：指定要转换的基于 XML 的资源文件的扩展名。<br />-   `.restext`：指定相同的格式为.txt。 如果要在生成过程中明确区分包含资源的源文件与其他源文件，则这个不相同的扩展名非常有用。<br />-   `.resources`：指定要转换的资源文件的扩展名。|  
|`StateFile`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定用于加速 .resx 输入文件中链接的依赖项检查的可选缓存文件的路径。|  
|`StronglyTypedClassName`|可选 `String` 参数。<br /><br /> 指定强类型资源类的类名。 如果未指定此参数，则使用资源文件的基名称。|  
|`StronglyTypedFilename`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定源文件的文件名。 如果未指定此参数，则会将类的名称用作基文件名，其扩展名取决于语言。 例如：`MyClass.cs`。|  
|`StronglyTypedLanguage`|可选 `String` 参数。<br /><br /> 指定在为强类型资源生成类源时要使用的语言。 此参数必须与 CodeDomProvider 所使用的其中一种语言完全匹配。 例如 `VB` 或 `C#`。<br /><br /> 通过将值传递给此参数来指示任务生成强类型资源。|  
|`StronglyTypedManifestPrefix`|可选 `String` 参数。<br /><br /> 指定要在强类型资源的生成类源中使用的资源命名空间或清单前缀。|  
|`StronglyTypedNamespace`|可选 `String` 参数。<br /><br /> 指定要用于强类型资源的生成类源的命名空间。 如果未指定此参数，则任何强类型资源都会位于全局命名空间中。|  
|`TLogReadFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读参数。<br /><br /> 获取表示读取跟踪日志的项的数组。|  
|`TLogWriteFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读参数。<br /><br /> 获取表示写入跟踪日志的项的数组。|  
|`ToolArchitecture`|可选 [String](<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) 参数。<br /><br /> 用于确定是否需要使用 Tracker.exe 来生成 ResGen.exe。<br /><br /> 应解析为 <xref:Microsoft.Build.Utilities.ExecutableType> 枚举的成员。 如果为 `String.Empty`，请使用启发式方法来确定默认体系结构。 应对 Microsoft.Build.Utilities.ExecutableType 枚举的成员可解析。|  
|`TrackerFrameworkPath`|Optional <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> 参数。<br /><br /> 指定其中包含 FileTracker.dll 的适当 .NET Framework 位置的路径。<br /><br /> 如果设置此参数，则用户应负责确保其传递的 FileTracker.dll 的位数与其要使用的 ResGen.exe 的位数相匹配。 如果未设置，则任务会基于当前的 .NET Framework 版本决定合适的位置。|  
|`TrackerLogDirectory`|Optional <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> 参数。<br /><br /> 指定用于放置运行此任务生成的跟踪日志的中间目录。|  
|`TrackerSdkPath`|Optional <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> 参数。<br /><br /> 指定包含 Tracker.exe 的适当 Windows SDK 位置的路径。<br /><br /> 如果设置此参数，则用户应负责确保其传递的 Tracker.exe 的位数与其要使用的 ResGen.exe 的位数相匹配。 如果未设置，则任务会基于当前的 Windows SDK 决定合适的位置。|  
|`TrackFileAccess`|可选 [Boolean](<!-- TODO: review code entity reference <xref:assetId:///Boolean?qualifyHint=False&amp;autoUpgrade=True>  -->) 参数。<br /><br /> 如果为 true，则使用输入文件的目录来解析相对文件路径。|  
|`UseSourcePath`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则指定使用输入文件的目录来解析相对文件路径。|  
  
## <a name="remarks"></a>备注  
 由于 .resx 文件可能包含其他资源文件的链接，因此仅通过比较 .resx 和 .resource 文件时间戳的方式来查看是否为最新输出并不可靠。 相反，`GenerateResource` 任务会跟踪 .resx 文件中的链接，同时也检查链接文件的时间戳。 这意味着通常不应对包含 `GenerateResource` 任务的目标使用 `Inputs` 和 `Outputs` 属性，因为这样会导致在实际上应运行该任务时跳过此任务。  
  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)。  
  
 使用 MSBuild 4.0 生成 .NET 3.5 项目时，x86 资源生成可能会失败。 若要解决此问题，可将目标生成为 AnyCPU 程序集。  
  
## <a name="example"></a>示例  
 以下示例使用 `GenerateResource` 任务从 `Resx` 项集合指定的文件中生成 .resources 文件。  
  
```  
<GenerateResource  
    Sources="@(Resx)"  
    OutputResources="@(Resx->'$(IntermediateOutputPath)%(Identity).resources')">  
    <Output  
        TaskParameter="OutputResources"  
        ItemName="Resources"/>  
</GenerateResource>  
```  
  
 `GenerateResource` 任务使用 \<EmbeddedResource> 项的 \<LogicalName> 元数据来命名嵌入程序集中的资源。  
  
 假定程序集命名为 myAssembly，则以下代码会生成一个名为 someQualifier.someResource.resources 的嵌入资源：  
  
```  
<ItemGroup>   <EmbeddedResource Include="myResource.resx">       <LogicalName>someQualifier.someResource.resources</LogicalName>   </EmbeddedResource></ItemGroup>  
```  
  
 如果没有 \<LogicalName> 元数据，则资源会被命名为 myAssembly.myResource.resources。  此示例仅适用于 Visual Basic 和 Visual C# 生成过程。  
  
## <a name="see-also"></a>请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)

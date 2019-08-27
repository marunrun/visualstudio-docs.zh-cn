---
title: MSBuild 任务参考 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tasks
ms.assetid: b3144b27-a426-4259-b8ae-5f7991b202b6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ed0f396613cea4ec2b6d9869e3ef1b121cac236b
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66747375"
---
# <a name="msbuild-task-reference"></a>MSBuild 任务参考

任务提供在生成过程中运行的代码。 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 提供以下列表中的任务。 安装 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 时，可使用其他任务来生成 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 项目。 有关详细信息，请参阅 [Visual C++ 任务](../msbuild/msbuild-tasks-specific-to-visual-cpp.md)。

除了此部分各主题中列出的参数外，每项任务还有下列参数：

| 参数 | 说明 |
|-------------------| - |
| `Condition` | 可选 `String` 参数。<br /><br /> [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 引擎使用 `Boolean` 表达式来确定是否执行此任务。 有关 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 支持的条件的信息，请参阅[条件](../msbuild/msbuild-conditions.md)。 |
| `ContinueOnError` | 可选参数。 可以包含下列值之一：<br /><br /> -   **WarnAndContinue** 或 **true**。 当任务失败时，[Target](../msbuild/target-element-msbuild.md) 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为警告。<br />-   **ErrorAndContinue**。 当任务失败时，`Target` 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为错误。<br />-   **ErrorAndStop** 或 **false**（默认值）。 当任务失败时，将不会执行 `Target` 元素中的剩余任务和生成，并且整个 `Target` 元素和生成都被视为已失败。<br /><br /> 4\.5 之前的 .NET Framework 版本仅支持 `true` 和 `false` 值。<br /><br /> 有关详细信息，请参阅[如何：忽略任务中的错误](../msbuild/how-to-ignore-errors-in-tasks.md)。 |

## <a name="in-this-section"></a>本节内容

- [任务基类](../msbuild/task-base-class.md)

 向派生自 <xref:Microsoft.Build.Utilities.Task> 类的任务添加几个参数。

- [TaskExtension 基类](../msbuild/taskextension-base-class.md)

 向派生自 <xref:Microsoft.Build.Tasks.TaskExtension> 类的任务添加几个参数。

- [ToolTaskExtension 基类](../msbuild/tooltaskextension-base-class.md)

 向派生自 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类的任务添加几个参数。

- [AL（程序集链接器）任务](../msbuild/al-assembly-linker-task.md)

 从一个或多个文件（可以是模块，也可以是资源文件）创建一个具有清单的程序集。

- [AspNetCompiler 任务](../msbuild/aspnetcompiler-task.md)

 包装 aspnet_compiler.exe，它是预编译 ASP.NET 应用程序的实用工具。 

- [AssignCulture 任务](../msbuild/assignculture-task.md)

 为项分配区域性标识符。

- [AssignProjectConfiguration 任务](../msbuild/assignprojectconfiguration-task.md)

 接受配置字符串列表，并将其分配给指定的项目。

- [AssignTargetPath 任务](../msbuild/assigntargetpath-task.md)

 接受文件列表，并添加 `<TargetPath>` 属性（如果尚未指定）。

- [CallTarget 任务](../msbuild/calltarget-task.md)

 调用项目文件中的目标。

- [CombinePath 任务](../msbuild/combinepath-task.md)

 将指定路径合并到单个路径。

- [ConvertToAbsolutePath 任务](../msbuild/converttoabsolutepath-task.md)

 将相对路径或引用转换为绝对路径。

- [Copy 任务](../msbuild/copy-task.md)

 将文件复制到一个新位置。

- [CreateCSharpManifestResourceName 任务](../msbuild/createcsharpmanifestresourcename-task.md)

 根据给定的 .resx 文件名或其他资源创建 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 样式的清单名称  。

- [CreateItem 任务](../msbuild/createitem-task.md)

 填充输入项中的项集合，允许从一个列表向另一个列表复制项。

- [CreateProperty 任务](../msbuild/createproperty-task.md)

 填充输入值中的属性，允许从一个属性或字符串向另一个属性或字符串复制值。

- [CreateVisualBasicManifestResourceName 任务](../msbuild/createvisualbasicmanifestresourcename-task.md)

 根据给定的 .resx 文件名或其他资源创建 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 样式的清单名称  。

- [Csc 任务](../msbuild/csc-task.md)

 调用 Visual C# 编译器以生成可执行文件、动态链接库或代码模块。

- [Delete 任务](../msbuild/delete-task.md)

 删除指定的文件。

- [DownloadFile 任务](../msbuild/downloadfile-task.md)

 将文件下载到指定位置。

- [Error 任务](../msbuild/error-task.md)

 基于评估的条件语句，停止生成操作并记录错误。

- [Exec 任务](../msbuild/exec-task.md)

 使用指定参数运行指定程序或命令。

- [FindAppConfigFile 任务](../msbuild/findappconfigfile-task.md)

 在提供的列表中查找 app.config 文件（若有）  。

- [FindInList 任务](../msbuild/findinlist-task.md)

 在指定的列表中查找具有匹配的 itemspec 的项。

- [FindUnderPath 任务](../msbuild/findunderpath-task.md)

 确定指定项集合中的哪些项存在于指定的文件夹及其所有子文件夹中。

- [FormatUrl 任务](../msbuild/formaturl-task.md)

 将 URL 转换为正确的 URL 格式。

- [FormatVersion 任务](../msbuild/formatversion-task.md)

 将修订号追加到版本号。

- [GenerateApplicationManifest 任务](../msbuild/generateapplicationmanifest-task.md)

 生成 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单或本机清单。

- [GenerateBootstrapper 任务](../msbuild/generatebootstrapper-task.md)

 提供自动化方式来检测、下载和安装应用程序及其必备组件。

- [GenerateDeploymentManifest 任务](../msbuild/generatedeploymentmanifest-task.md)

 生成 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署清单。

- [GenerateResource 任务](../msbuild/generateresource-task.md)

 将 .txt 和 .resx 文件转换为公共语言运行时二进制 .resources 文件。   

- [GenerateTrustInfo 任务](../msbuild/generatetrustinfo-task.md)

 从基本清单以及从 `TargetZone` 和 `ExcludedPermissions` 属性生成应用程序信任。

- [GetAssemblyIdentity 任务](../msbuild/getassemblyidentity-task.md)

 从指定的文件检索程序集标识并输出标识信息。

- [GetFileHash 任务](../msbuild/getfilehash-task.md)

 计算文件或文件集的内容的校验和。

- [GetFrameworkPath 任务](../msbuild/getframeworkpath-task.md)

 检索 .NET Framework 程序集的路径。

- [GetFrameworkSdkPath 任务](../msbuild/getframeworksdkpath-task.md)

 检索 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 的路径。

- [GetReferenceAssemblyPaths 任务](../msbuild/getreferenceassemblypaths-task.md)

 返回各种框架的引用程序集路径。

- [LC 任务](../msbuild/lc-task.md)

 从 .licx 文件生成 .license 文件。  

- [MakeDir 任务](../msbuild/makedir-task.md)

 创建目录，并在必要时创建任何父目录。

- [Message 任务](../msbuild/message-task.md)

 在生成期间记录消息。

- [Move 任务](../msbuild/move-task.md)

 将文件移至新位置。

- [MSBuild 任务](../msbuild/msbuild-task.md)

 从另一 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 项目生成 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 项目。

- [ReadLinesFromFile 任务](../msbuild/readlinesfromfile-task.md)

 从文本文件读取项列表。

- [RegisterAssembly 任务](../msbuild/registerassembly-task.md)

 读取指定程序集中的元数据，并在注册表中添加必要的项。

- [RemoveDir 任务](../msbuild/removedir-task.md)

 删除指定的目录及其所有文件和子目录。

- [RemoveDuplicates 任务](../msbuild/removeduplicates-task.md)

 从指定的项集合中删除重复的项。

- [RequiresFramework35SP1Assembly 任务](../msbuild/requiresframework35sp1assembly-task.md)

 确定应用程序是否需要 .NET Framework 3.5 SP1。

- ResGen 任务

 已过时。 使用 [GenerateResource 任务](../msbuild/generateresource-task.md)可以将 .txt 和 .resx 文件转换成公共语言运行时二进制 .resources 文件，反之亦然。   

- [ResolveAssemblyReference 任务](../msbuild/resolveassemblyreference-task.md)

 确定依赖指定程序集的所有程序集。

- [ResolveComReference 任务](../msbuild/resolvecomreference-task.md)

 获取一个或多个类型库名称或 .tlb 文件的列表，将这些类型库解析为磁盘上的位置。 

- [ResolveKeySource 任务](../msbuild/resolvekeysource-task.md)

 确定强名称密钥源

- [ResolveManifestFiles 任务](../msbuild/resolvemanifestfiles-task.md)

 在生成过程中，将以下各项解析为文件以便生成清单：生成项、依赖项、附属项、内容、调试符号和文档。

- [ResolveNativeReference 任务](../msbuild/resolvenativereference-task.md)

 解析本机引用。

- [ResolveNonMSBuildProjectOutput 任务](../msbuild/resolvenonmsbuildprojectoutput-task.md)

 确定非 MSBuild 项目引用的输出文件。

- [SGen 任务](../msbuild/sgen-task.md)

 创建指定程序集中的类型的 XML 序列化程序集。

- [SignFile 任务](../msbuild/signfile-task.md)

 使用指定证书签署指定文件。

- [Touch 任务](../msbuild/touch-task.md)

 设置文件的访问和修改时间。

- [UnregisterAssembly 任务](../msbuild/unregisterassembly-task.md)

 注销用于 COM 互操作的指定程序集。

- [Unzip 任务](../msbuild/unzip-task.md)

 将 .zip 存档解压缩到指定位置。 

- [UpdateManifest 任务](../msbuild/updatemanifest-task.md)

 更新清单中所选的属性并重新签名。

- [Vbc 任务](../msbuild/vbc-task.md)

 调用 Visual Basic 编译器以生成可执行文件、动态链接库或代码模块。

- [VerifyFileHash 任务](../msbuild/verifyfilehash-task.md)

 验证文件是否与预期的文件哈希匹配。

- [Warning 任务](../msbuild/warning-task.md)

 基于评估的条件语句，在生成期间记录警告。

- [WriteCodeFragment 任务](../msbuild/writecodefragment-task.md)

 使用指定的生成代码片段，生成临时代码文件。 不会删除该文件。

- [WriteLinesToFile 任务](../msbuild/writelinestofile-task.md)

 将指定项写入指定的文本文件。

- [XmlPeek 任务](../msbuild/xmlpeek-task.md)

 从 XML 文件返回 XPath 查询指定的值。

- [XmlPoke 任务](../msbuild/xmlpoke-task.md)

 将 XPath 查询指定的值设置为 XML 文件。

- [XslTransformation 任务](../msbuild/xsltransformation-task.md)

 使用可扩展样式表语言转换 (XSLT)  或编译的 XSLT 转换 XML 输入，并将其输出到一台输出设备或一个文件。

- [ZipDirectory 任务](../msbuild/zipdirectory-task.md)

 根据目录内容创建 .zip 存档。 

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [任务写入](../msbuild/task-writing.md)
- [任务](../msbuild/msbuild-tasks.md)
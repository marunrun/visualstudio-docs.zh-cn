---
title: MT 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VC.Project.VCManifestTool.ResourceOutputFileName
- VC.Project.VCManifestTool.SuppressDependencyElement
- VC.Project.VCManifestTool.ManifestFromManagedAssembly
- VC.Project.VCManifestTool.GenerateCategoryTags
- VC.Project.VCManifestTool.EnableDPIAwareness
- vc.task.mt
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBUILD (C++), MT task
- MT task (MSBuild (C++))
ms.assetid: bb94913c-1042-4968-9f08-b394518e899f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3fad0b3ddf57167c6721371ae5f8e11f5b7a4c13
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911231"
---
# <a name="mt-task"></a>MT 任务
包装 Microsoft 清单工具 mt.exe  。 有关详细信息，请参见 [Mt.exe](/windows/desktop/SbsCs/mt-exe)。

## <a name="parameters"></a>参数
 下表描述了 MT  任务的参数。 大多数任务参数和若干组参数都对应于命令行选项。

> [!NOTE]
> mt.exe  文档使用连字符 (-  ) 作为前缀，用于命令行选项，但本主题使用斜杠 (/  )。 以上任意一种前缀都是可接受的。

|参数|说明|
|---------------|-----------------|
|**AdditionalManifestFiles**|可选 **String []** 参数。<br /><br /> 指定一个或多个清单文件的名称。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/manifest”  选项。|
|**AdditionalOptions**|可选 **String** 参数。<br /><br /> 命令行选项列表。 例如，/\<option1> /\<option2> /\<option#>。 使用此参数可指定未由任何其他 MT  任务参数表示的命令行选项。<br /><br /> 有关详细信息，请参见 [Mt.exe](/windows/desktop/SbsCs/mt-exe)。|
|**AssemblyIdentity**|可选 **String** 参数。<br /><br /> 指定清单的 assemblyIdentity  元素的特性值。 指定一个逗号分隔的列表，其中第一个组件是 `name` 特性的值，后跟以下格式的一个或多个名称/值对：\<attribute name>=<attribute_value>  。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/identity”  选项。|
|**ComponentFileName**|可选 **String** 参数。<br /><br /> 指定要从 .rgs  或 .tlb  文件生成的动态链接库的名称。 如果指定 RegistrarScriptFile  或 TypeLibraryFile  MT 任务参数，则此参数为必需。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/dll”  选项。|
|**DependencyInformationFile**|可选 **String** 参数。<br /><br /> 指定 Visual Studio 用来跟踪清单工具的生成依赖项信息的依赖项信息文件。|
|**EmbedManifest**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则在程序集中嵌入清单文件。 如果为 `false`，则会创建为独立的清单文件。|
|**EnableDPIAwareness**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则添加到将应用程序标记为 DPI 的清单信息。 编写可识别 DPI 的应用程序，可使用户界面通过各种高 DPI 显示设置显得美观一致。<br /><br /> 有关详细信息，请参见[高 DPI](/windows/desktop/win7devguide/high-dpi)。|
|**GenerateCatalogFiles**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则生成目录定义 (.cdf  ) 文件。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/makecdfs”  选项。|
|**GenerateCategoryTags**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则会导致生成类型标记。 如果此参数为 `true`，还必须指定 ManifestFromManagedAssemblyMT  任务参数。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/category”  选项。|
|**InputResourceManifests**|可选 **String** 参数。<br /><br /> 从具有指定标识符的 RT_MANIFEST 类型的资源输入清单。 指定格式为 \<file>[;[#]\<resource_id>] 的资源，其中可选 \<resource_id> 参数是一个非负 16 位数字。<br /><br /> 如果没有指定 `resource_id`，则会使用 CREATEPROCESS_MANIFEST_RESOURCE 默认值 (1)。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/inputresource”  选项。|
|**ManifestFromManagedAssembly**|可选 **String** 参数。<br /><br /> 从指定的托管程序集生成清单。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/managedassemblyname”  选项。|
|**ManifestToIgnore**|可选 **String** 参数。<br /><br /> （未使用。）|
|**OutputManifestFile**|可选 **String** 参数。<br /><br /> 指定输出清单的名称。 如果省略了此参数，并且只有一个清单正在进行操作，则会就地修改该清单。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/out”  选项。|
|**OutputResourceManifests**|可选 **String** 参数。<br /><br /> 将清单输出到具有指定标识符的 RT_MANIFEST 类型的资源。 此资源格式为 \<file>[;[#]\<resource_id>]，其中可选 \<resource_id> 参数是一个非负 16 位数字。<br /><br /> 如果没有指定 `resource_id`，则会使用 CREATEPROCESS_MANIFEST_RESOURCE 默认值 (1)。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/outputresource”  选项。|
|**RegistrarScriptFile**|可选 **String** 参数。<br /><br /> 指定要用于免注册 COM 清单支持的注册器脚本 (.rgs  ) 文件。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/rgs”  选项。|
|**ReplacementsFile**|可选 **String** 参数。<br /><br /> 指定注册器脚本 (.rgs  ) 文件中包含可替换字符串的值的文件。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/replacements”  选项。|
|**ResourceOutputFileName**|可选 **String** 参数。<br /><br /> 指定用于将清单嵌入项目输出的输出资源文件。|
|**Sources**|可选 `ITaskItem[]` 参数。<br /><br /> 指定用空格分隔的清单源文件列表。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/manifest”  选项。|
|**SuppressDependencyElement**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则生成无依赖项元素的清单。 如果此参数为 `true`，还需指定 ManifestFromManagedAssemblyMT  任务参数。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/nodependency”  选项。|
|**SuppressStartupBanner**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则在任务开始时阻止显示版权和版本号消息。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/nologo”  选项。|
|**TrackerLogDirectory**|可选 `String` 参数。<br /><br /> 指定存储此任务跟踪日志的中间目录。|
|**TypeLibraryFile**|可选 **String** 参数。<br /><br /> 指定类型库 (.tlb  ) 文件的名称。 如果指定此参数，还要指定 ComponentFileNameMT  任务参数。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/tlb”  选项。|
|**UpdateFileHashes**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，将在 UpdateFileHashesSearchPathMT  任务参数指定的路径计算文件的哈希值，然后使用计算的值更新清单 file  元素的 hash  特性的值。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/hashupdate”  选项。 另请参阅此表中的 UpdateFileHashesSearchPath  参数。|
|**UpdateFileHashesSearchPath**|可选 `String` 参数。<br /><br /> 指定更新文件哈希时要使用的搜索路径。 将此参数与 UpdateFileHashesMT  任务参数一起使用。<br /><br /> 有关详细信息，请参阅此表中的 UpdateFileHashes  参数。|
|**VerboseOutput**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则显示详细调试信息。<br /><br /> 有关详细信息，请参阅 [Mt.exe](/windows/desktop/SbsCs/mt-exe) 中的“/verbose”  选项。|

## <a name="see-also"></a>请参阅
- [任务参考](../msbuild/msbuild-task-reference.md)
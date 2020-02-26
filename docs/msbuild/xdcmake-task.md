---
title: XDCMake 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vc.task.xdcmake
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- XDCMake task (MSBuild (C++))
- MSBuild (C++), XDCMake task
ms.assetid: a7de9c64-903a-4a02-85f3-f37672270f25
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 797a2f80c4e634b3dcb3b0fa32c46476e32cc334
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578128"
---
# <a name="xdcmake-task"></a>XDCMake 任务
包装 XML 文档工具 (xdcmake.exe  )，它将 XML 文档注释 (.xdc  ) 文件合并到一个 .xml  文件中。

 如果在 C++ 源代码中提供文档注释，并使用 [/doc](/cpp/build/reference/doc-process-documentation-comments-c-cpp) 编译器选项进行编译，就会创建“.xdc”  文件。 有关详细信息，请参阅 [XDCMake 参考](/cpp/build/reference/xdcmake-reference)、[XML 文档生成器工具属性页](/cpp/build/reference/xml-document-generator-tool-property-pages)和 xdcmake.exe  的命令行帮助选项 (/?  )。

## <a name="remarks"></a>备注
 默认情况下，xdcmake.exe  工具支持几个命令行选项。 如果你指定 **/old** 命令行选项，此工具还支持其他选项。

## <a name="parameters"></a>参数
 下表介绍了 **XDCMake** 任务的参数。

|参数|描述|
|---------------|-----------------|
|**AdditionalDocumentFile**|可选 **String []** 参数。<br /><br /> 指定还要合并的一个或多个 .xdc  文件。<br /><br /> 有关详细信息，请参阅 [XML 文档生成器工具属性页](/cpp/build/reference/xml-document-generator-tool-property-pages)中的**附加文档文件**说明。 另请参阅 xdcmake.exe  的“/old”  和“/Fs”  命令行选项。|
|**AdditionalOptions**|可选 **String** 参数。<br /><br /> 在命令行上指定的选项列表。 例如，/\<option1> /\<option2> /\<option#>。 此参数用于指定无法由其他任何 **XDCMake** 任务参数表示的选项。<br /><br /> 有关详细信息，请参阅 [XDCMake 参考](/cpp/build/reference/xdcmake-reference)、[XML 文档生成器工具属性页](/cpp/build/reference/xml-document-generator-tool-property-pages)和 xdcmake.exe  的命令行帮助 (/?  )。|
|**DocumentLibraryDependencies**|可选 **Boolean** 参数。<br /><br /> 若为 `true` 且当前项目与解决方案中的静态库 (.lib  ) 项目有依赖关系，那么当前项目的 .xml  文件输出中就会包含此库项目的 .xdc  文件。<br /><br /> 有关详细信息，请参阅 [XML 文档生成器工具属性页](/cpp/build/reference/xml-document-generator-tool-property-pages)中的**文档库依赖项**说明。|
|**OutputFile**|可选 **String** 参数。<br /><br /> 替代默认输出文件名。 默认名称派生自处理的第一个 .xdc  文件的名称。<br /><br /> 有关详细信息，请参阅 [XDCMake 参考](/cpp/build/reference/xdcmake-reference)中的“/out:\<filename>”  选项。 另请参阅 xdcmake.exe  的“/old”  和“/Fo”  命令行选项。|
|**ProjectName**|可选 **String** 参数。<br /><br /> 当前项目的名称。|
|**SlashOld**|可选 **Boolean** 参数。<br /><br /> 若为 `true`，将启用其他 xdcmake.exe  选项。<br /><br /> 有关详细信息，请参阅 xdcmake.exe  的“/old”  命令行选项。|
|**Sources**|必选 `ITaskItem[]` 参数。<br /><br /> 定义可以被任务使用和发出的 MSBuild 源文件项的数组。|
|**SuppressStartupBanner**|可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则在任务开始时阻止显示版权和版本号消息。<br /><br /> 有关详细信息，请参阅 [XDCMake 参考](/cpp/build/reference/xdcmake-reference)中的“/nologo”  选项。|
|**TrackerLogDirectory**|可选 **String** 参数。<br /><br /> 指定跟踪器日志目录。|

## <a name="see-also"></a>请参阅
- [任务参考](../msbuild/msbuild-task-reference.md)
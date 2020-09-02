---
title: XDCMake 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
- XDCMake task (MSBuild (Visual C++))
- MSBuild (Visual C++), XDCMake task
ms.assetid: a7de9c64-903a-4a02-85f3-f37672270f25
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c16c92b41aa0635ecb24d83e30e2c347620b2c75
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675540"
---
# <a name="xdcmake-task"></a>XDCMake 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包装 XML 文档工具 (xdcmake.exe)，它将 XML 文档注释 (.xdc) 文件合并到一个 .xml 文件中。  
  
 如果在 Visual C++ 源代码中提供文档注释，并使用 [/doc](https://msdn.microsoft.com/library/b54f7e2c-f28f-4f46-9ed6-0db09be2cc63)编译器选项进行编译，就会创建“.xdc”文件。 有关详细信息，请参阅 " [XDCMake 参考](https://msdn.microsoft.com/library/14e65747-d000-4343-854b-8393bf01cbac)"、" [XML 文档生成器工具" 属性页](https://msdn.microsoft.com/library/645912b5-197a-4c36-ba58-64df09444ca0)和 "xdcmake.exe 的命令行帮助选项 (**/？**) 。  
  
## <a name="remarks"></a>备注  
 默认情况下，xdcmake.exe 工具支持几个命令行选项。 如果你指定 **/old** 命令行选项，此工具还支持其他选项。  
  
## <a name="parameters"></a>参数  
 下表介绍了 **XDCMake** 任务的参数。  
  
|参数|描述|  
|---------------|-----------------|  
|**AdditionalDocumentFile**|可选 **String []** 参数。<br /><br /> 指定还要合并的一个或多个 .xdc 文件。<br /><br /> 有关详细信息，请参阅 " [XML 文档生成器工具" 属性页](https://msdn.microsoft.com/library/645912b5-197a-4c36-ba58-64df09444ca0)中的**附加文档文件**说明。 另请参阅 xdcmake.exe 的 **/old** 和 **/Fs** 命令行选项。|  
|**AdditionalOptions**|可选 **String** 参数。<br /><br /> 在命令行上指定的选项列表。 例如，/option1 /option2 /option#。** 此参数用于指定无法由其他任何 **XDCMake** 任务参数表示的选项。<br /><br /> 有关详细信息，请参阅 [XDCMake 参考](https://msdn.microsoft.com/library/14e65747-d000-4343-854b-8393bf01cbac)、[“XML 文档生成器工具”属性页](https://msdn.microsoft.com/library/645912b5-197a-4c36-ba58-64df09444ca0)和 xdcmake.exe 的命令行帮助 (**/?**)。|  
|**DocumentLibraryDependencies**|可选 **Boolean** 参数。<br /><br /> 若为 `true` 且当前项目与解决方案中的静态库 (.lib) 项目有依赖关系，那么当前项目的 .xml 文件输出中就会包含此库项目的 .xdc 文件。<br /><br /> 有关详细信息，请参阅 " [XML 文档生成器工具" 属性页](https://msdn.microsoft.com/library/645912b5-197a-4c36-ba58-64df09444ca0)中的**文档库依赖项**说明。|  
|**OutputFile**|可选 **String** 参数。<br /><br /> 替代默认输出文件名。 默认名称派生自处理的第一个 .xdc 文件的名称。<br /><br /> 有关详细信息，请参阅 **/out:** `filename` [XDCMake 引用](https://msdn.microsoft.com/library/14e65747-d000-4343-854b-8393bf01cbac)中的/out：选项。 另请参阅 xdcmake.exe 的 **/old** 和 **/fo** 命令行选项。|  
|**ProjectName**|可选 **String** 参数。<br /><br /> 当前项目的名称。|  
|**SlashOld**|可选 **Boolean** 参数。<br /><br /> 若为 `true`，将启用其他 xdcmake.exe 选项。<br /><br /> 有关详细信息，请参阅 **/old** 命令行选项 xdcmake.exe。|  
|**Sources**|必选 `ITaskItem[]` 参数。<br /><br /> 定义可以被任务使用和发出的 MSBuild 源文件项的数组。|  
|**SuppressStartupBanner**|可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则在任务开始时阻止显示版权和版本号消息。<br /><br /> 有关详细信息，请参阅[XDCMake Reference](https://msdn.microsoft.com/library/14e65747-d000-4343-854b-8393bf01cbac)中的 **/nologo**选项。|  
|**TrackerLogDirectory**|可选 **String** 参数。<br /><br /> 指定跟踪器日志目录。|  
  
## <a name="see-also"></a>另请参阅  
 [任务引用](../msbuild/msbuild-task-reference.md)

---
title: BscMake 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vc.task.bscmake
- VC.Project.VCBscMakeTool.PreserveSBR
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), tasks
- BscMake task (MSBuild (C++))
ms.assetid: bb98fc67-cad8-43a7-9598-60df6d734db2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff0c95c37e24f8c51453a849159073baff8dca0d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593416"
---
# <a name="bscmake-task"></a>BscMake 任务
> [!IMPORTANT]
> Visual Studio IDE 不再使用 BscMake。 自 Visual Studio 2008 起，浏览信息自动存储在解决方案文件夹的 .sdf 文件中   。

 包装 Microsoft 浏览信息维护实用工具 (bscmake.exe)  。  Bscmake.exe 工具从在编译期间创建的源浏览器文件 (.sbr) 生成浏览信息文件 (.bsc)    。 可使用对象浏览器查看 .bsc 文件   。 有关详细信息，请参阅 [BSCMAKE 参考](/cpp/build/reference/bscmake-reference)。

## <a name="parameters"></a>参数
 下表介绍了 **BscMake** 任务的参数。 大多数任务参数都对应于命令行选项。

|参数|描述|
|---------------|-----------------|
|**AdditionalOptions**|可选 **String** 参数。<br /><br /> 在命令行上指定的选项列表。 例如，/\<option1> /\<option2> /\<option#>。 此参数用于指定无法由其他任何 **BscMake** 任务参数表示的选项。<br /><br /> 有关详细信息，请参阅 [BSCMAKE 选项](/cpp/build/reference/bscmake-options)中的选项。|
|**OutputFile**|可选 **String** 参数。<br /><br /> 指定重写默认输出文件名的文件名。<br /><br /> 有关详细信息，请参阅 [BSCMAKE 选项](/cpp/build/reference/bscmake-options)中的 /o 选项  。|
|**PreserveSBR**|可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则会强制非增量生成。 无论 .bsc 文件是否存在，都会发生完整的非增量生成，并防止 .sbr 文件被截断   。<br /><br /> 有关详细信息，请参阅 [BSCMAKE 选项](/cpp/build/reference/bscmake-options)中的 /n 选项  。|
|**Sources**|可选的 **ITaskItem[]** 参数。<br /><br /> 定义可以被任务使用和发出的 MSBuild 源文件项的数组。|
|**SuppressStartupBanner**|可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则在任务开始时阻止显示版权和版本号消息。<br /><br /> 有关详细信息，请参阅 [BSCMAKE 选项](/cpp/build/reference/bscmake-options)中的 /NOLOGO 选项  。|
|**TrackerLogDirectory**|可选 **String** 参数。<br /><br /> 指定跟踪器日志目录。|

## <a name="see-also"></a>请参阅
- [任务参考](../msbuild/msbuild-task-reference.md)

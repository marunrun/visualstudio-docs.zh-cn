---
title: BscMake 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
- MSBuild (Visual C++), tasks
- BscMake task (MSBuild (Visual C++))
ms.assetid: bb98fc67-cad8-43a7-9598-60df6d734db2
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7ed246255fc20b9660d24f234767fdeb451102f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684550"
---
# <a name="bscmake-task"></a>BscMake 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

重要提示
> Visual Studio IDE 不再使用 bscmake。 自 Visual Studio 2008 起，浏览信息自动存储在解决方案文件夹的 .sdf 文件中。  
  
 包装 Microsoft 浏览信息维护实用工具 (bscmake.exe)。  Bscmake.exe 工具从在编译期间创建的源浏览器文件 (.sbr) 生成浏览信息文件 (.bsc)。 可使用对象浏览器查看 .bsc 文件****。 有关详细信息，请参阅 [BSCMAKE 参考](https://msdn.microsoft.com/library/b97ad994-1355-4809-98db-6abc12c6fb13)。  
  
## <a name="parameters"></a>参数  
 下表介绍了 **BscMake** 任务的参数。 大多数任务参数都对应于命令行选项。  
  
|参数|说明|  
|---------------|-----------------|  
|**其他**|可选的 **字符串** 参数。<br /><br /> 在命令行上指定的选项列表。 例如，"/*选项 1*  / *选项 2*  / *选项 #*"。 此参数用于指定无法由其他任何 **BscMake** 任务参数表示的选项。<br /><br /> 有关详细信息，请参阅 [BSCMAKE 选项](https://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2)中的选项。|  
|**OutputFile**|可选的 **字符串** 参数。<br /><br /> 指定重写默认输出文件名的文件名。<br /><br /> 有关详细信息，请参阅[BSCMAKE 选项](https://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2)中的 **/o**选项。|  
|**PreserveSBR**|可选的 **布尔** 参数。<br /><br /> 如果为 `true`，则会强制非增量生成。 无论 .bsc 文件是否存在，都会发生完整的非增量生成，并防止 .sbr 文件被截断。<br /><br /> 有关详细信息，请参阅 [BSCMAKE 选项](https://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2)中的 **/n** 选项。|  
|**源**|可选的 **ITaskItem[]** 参数。<br /><br /> 定义可以被任务使用和发出的 MSBuild 源文件项的数组。|  
|**SuppressStartupBanner**|可选的 **布尔** 参数。<br /><br /> 如果为 `true`，则在任务开始时阻止显示版权和版本号消息。<br /><br /> 有关详细信息，请参阅 [BSCMAKE 选项](https://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2)中的 **/NOLOGO** 选项。|  
|**TrackerLogDirectory**|可选的 **字符串** 参数。<br /><br /> 指定跟踪器日志目录。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [任务引用](../msbuild/msbuild-task-reference.md)

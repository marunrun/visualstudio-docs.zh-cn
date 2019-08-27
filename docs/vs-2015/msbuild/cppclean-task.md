---
title: CPPClean 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- vc.task.cppclean
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), CPPClean task
- CPPClean task (MSBuild (Visual C++))
ms.assetid: b62a482e-8fb5-4999-b50b-6605a078e291
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bddba1170cf675b5bde7ab8deed8cce1e7eb57dd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196580"
---
# <a name="cppclean-task"></a>CPPClean 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

删除生成 Visual C++ 项目时 MSBuild 创建的临时文件。 删除生成文件的过程称为“清除”  。  

## <a name="parameters"></a>参数  
 下表描述了 CPPClean 任务的参数  。  

|            参数            |                                                                                                描述                                                                                                 |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        DeletedFiles          |                               可选 `ITaskItem[]` 输出参数。<br /><br /> 定义可由任务使用和发出的 MSBuild 输出文件项的数组。                                |
|          DoDelete            |                                                            可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则清除临时生成文件。                                                             |
| FilePatternsToDeleteOnClean  |                                            必选 `String` 参数。<br /><br /> 指定要清除的文件的文件扩展名列表（以分号分隔）。                                             |
|   FilesExcludedFromClean     |                                                    可选 `String` 参数。<br /><br /> 指定不会清除的文件的列表（以分号分隔）。                                                    |
|       FoldersToClean         | 必选 `String` 参数。<br /><br /> 指定要清除的目录的列表（以分号分隔）。 可指定完整路径或相对路径，并且路径可包含通配符 (\\\*)  。 |

## <a name="remarks"></a>备注  

## <a name="see-also"></a>请参阅  
 [任务参考](../msbuild/msbuild-task-reference.md)

---
title: CPPClean 任务 | Microsoft Docs
ms.date: 11/04/2016
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
- MSBuild (C++), CPPClean task
- CPPClean task (MSBuild (C++))
ms.assetid: b62a482e-8fb5-4999-b50b-6605a078e291
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 827014e04c23239274e31b994fd0178cbe8e5883
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596068"
---
# <a name="cppclean-task"></a>CPPClean 任务
删除生成 C++ 项目时 MSBuild 创建的临时文件。 删除生成文件的过程称为“清除”  。

## <a name="parameters"></a>参数
 下表描述了 CPPClean 任务的参数  。

|参数|描述|
|---------------|-----------------|
|DeletedFiles |可选 `ITaskItem[]` 输出参数。<br /><br /> 定义可由任务使用和发出的 MSBuild 输出文件项的数组。|
|DoDelete |可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则清除临时生成文件。|
|FilePatternsToDeleteOnClean |必选 `String` 参数。<br /><br /> 指定要清除的文件的文件扩展名列表（以分号分隔）。|
|FilesExcludedFromClean |可选 `String` 参数。<br /><br /> 指定不会清除的文件的列表（以分号分隔）。|
|FoldersToClean |必选 `String` 参数。<br /><br /> 指定要清除的目录的列表（以分号分隔）。 可指定完整路径或相对路径，并且路径可包含通配符 (*)。|

## <a name="see-also"></a>请参阅
- [任务参考](../msbuild/msbuild-task-reference.md)

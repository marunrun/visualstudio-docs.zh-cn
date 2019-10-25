---
title: GetOutputFileName 任务 | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.getoutputfilename
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), GetOutputFileName task
- GetOutputFileName task (MSBuild (C++))
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: 9733aae5e53948cdf07d62f62cd7ca5f930d08a3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747305"
---
# <a name="getoutputfilename-task"></a>GetOutputFileName 任务

用于获取有关 cl 和其他工具（只允许指定输出目录或完整文件名或不允许指定任何内容）的输出文件名的帮助程序任务。

## <a name="parameters"></a>参数

下表显示 GetOutputFileName  任务的参数。

|参数|说明|
|---------------|-----------------|
|**OutputExtension**|必需的 **String** 参数。|
|**OutputFile**|可选的 string  输出参数。|
|**OutputPath**|可选的 string  参数。|
|SourceFile |必需的 **String** 参数。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)
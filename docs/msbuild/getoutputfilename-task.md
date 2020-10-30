---
title: GetOutputFileName 任务 | Microsoft Docs
description: 使用 MSBuild GetOutputFileName 帮助程序任务可指定 cl.exe 和其他工具的输出文件名选项。
ms.custom: SEO-VS-2020
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
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: cb4670bb84b151332951608f7b20ef5ea44e59a3
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436784"
---
# <a name="getoutputfilename-task"></a>GetOutputFileName 任务

用于获取有关 cl 和其他工具（只允许指定输出目录或完整文件名或不允许指定任何内容）的输出文件名的帮助程序任务。

## <a name="parameters"></a>参数

下表显示 GetOutputFileName  任务的参数。

|参数|说明|
|---------------|-----------------|
|**OutputExtension**|必需的 **String** 参数。|
|**OutputFile**|可选的 string 输出参数。|
|**OutputPath**|可选的 string  参数。|
|SourceFile|必需的 **String** 参数。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)

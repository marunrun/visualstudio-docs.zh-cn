---
title: -Diff | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 5377fedb-632a-4e86-a947-7c11c86451e7
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fd76b0803f43a7694ec0d689eeb8489f491f8464
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657755"
---
# <a name="diff"></a>/Diff
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

比较两个文件。 差异将在特殊 Visual Studio 窗口中显示。

## <a name="syntax"></a>语法

```
devenv /Diff SourceFile, TargetFile, [SourceDisplayName],[TargetDisplayName]
```

## <a name="arguments"></a>参数
 `SourceFile`（必需）。 要比较的第一个文件的完整路径和名称。

 `TargetFile`（必需）。 要比较的第二个文件的完整路径和名称

 `SourceDisplayName`（可选）。 第一个文件的显示名称。

 `TargetDisplayName`（可选）。 第二个文件的显示名称。

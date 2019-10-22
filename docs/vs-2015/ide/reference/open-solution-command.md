---
title: “打开解决方案”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.opensolution
helpviewer_keywords:
- Open Solution command
- File.OpenSolution command
ms.assetid: 61de76c8-69d7-4cdb-b605-e132f45d05d9
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b9c9ab66d2885137e9c470f577996ab861b554d5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671912"
---
# <a name="open-solution-command"></a>“打开解决方案”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

打开一个现有解决方案，关闭其他所有打开的解决方案。

## <a name="syntax"></a>语法

```
File.OpenSolution filename
```

## <a name="arguments"></a>自变量
 `Filename`（必需）。 要打开的解决方案的完整路径和文件名。

 `filename` 参数的语法要求用引号将包含空格的路径括起来。

## <a name="remarks"></a>备注
 键入内容时，自动完成功能会尝试查找正确的路径和文件名。

## <a name="example"></a>示例
 此示例打开解决方案 Test1.sln。

```
>File.OpenSolution "c:\MySolutions\Test1\Test1.sln"
```

## <a name="see-also"></a>另请参阅
 [Visual studio](../../ide/reference/visual-studio-commands.md) "[命令" 窗口](../../ide/reference/command-window.md)中的["查找/命令" 框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)

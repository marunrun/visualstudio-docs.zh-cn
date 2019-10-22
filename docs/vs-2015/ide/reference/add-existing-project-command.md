---
title: “添加现有项目”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.addexistingproject
helpviewer_keywords:
- Add Existing Project command
- File.AddExistingProject
ms.assetid: 71cf3e31-c76b-405b-ad6a-1b1bc654bd40
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 73d8e54938659920227b3614046b8a8f933023ff
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670217"
---
# <a name="add-existing-project-command"></a>“添加现有项目”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将现有项目添加到当前解决方案中。

## <a name="syntax"></a>语法

```
File.AddExistingProject filename
```

## <a name="arguments"></a>自变量
 `filename`（可选）。 待添加到解决方案的项目的完整路径、项目名称和扩展名。

 如果 `filename` 参数包含空格，则必须将其放在引号内。

 如果未指定文件名，该命令将打开文件对话框，以便用户可以选取一个项目。

## <a name="remarks"></a>备注
 键入内容时，自动完成功能会尝试查找正确的路径和文件名。

## <a name="example"></a>示例
 此示例向当前解决方案中添加 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 项目 - TestProject1。

```
>File.AddExistingProject "c:\visual studio projects\TestProject1.vbproj"
```

## <a name="see-also"></a>另请参阅
 [Visual studio](../../ide/reference/visual-studio-commands.md) "[命令" 窗口](../../ide/reference/command-window.md)中的["查找/命令" 框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)

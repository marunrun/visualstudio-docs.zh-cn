---
title: “添加现有项目”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- file.addexistingproject
helpviewer_keywords:
- Add Existing Project command
- File.AddExistingProject
ms.assetid: 71cf3e31-c76b-405b-ad6a-1b1bc654bd40
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 05d57024c52e0a35d7e387f5ba3cccf0697fe44a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748852"
---
# <a name="add-existing-project-command"></a>“添加现有项目”命令
将现有项目添加到当前解决方案中。

## <a name="syntax"></a>语法

```cmd
File.AddExistingProject filename
```

## <a name="arguments"></a>自变量
`filename`\
可选。 待添加到解决方案的项目的完整路径、项目名称和扩展名。

如果 `filename` 参数包含空格，则必须将其放在引号内。

如果未指定文件名，该命令将打开文件对话框，以便用户可以选取一个项目。

## <a name="remarks"></a>备注
键入内容时，自动完成功能会尝试查找正确的路径和文件名。

## <a name="example"></a>示例
此示例向当前解决方案中添加 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目 - TestProject1。

```cmd
>File.AddExistingProject "c:\visual studio projects\TestProject1.vbproj"
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
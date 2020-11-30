---
title: “添加现有项目”命令
description: 了解“添加现有项目”命令以及该命令如何将现有项目添加到当前解决方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- file.addexistingproject
helpviewer_keywords:
- Add Existing Project command
- File.AddExistingProject
ms.assetid: 71cf3e31-c76b-405b-ad6a-1b1bc654bd40
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2c12106621599d428e9a701de9ba5e468b5e312a
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "95870997"
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

## <a name="remarks"></a>注解
键入内容时，自动完成功能会尝试查找正确的路径和文件名。

## <a name="example"></a>示例
此示例向当前解决方案中添加 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目 - TestProject1。

```cmd
>File.AddExistingProject "c:\visual studio projects\TestProject1.vbproj"
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)

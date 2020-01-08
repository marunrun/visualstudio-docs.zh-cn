---
title: “打开项目”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- file.openproject
- file.opensolution
helpviewer_keywords:
- op command
- File.OpenProject command
- Open Project command
ms.assetid: baa85f86-041b-49f4-9ced-0c397dc180e1
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 97c1034fbbafa04af2d62526fdbb48812d64e050
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75565807"
---
# <a name="open-project-command"></a>打开项目命令

打开现有项目或解决方案。

## <a name="syntax"></a>语法

```cmd
File.OpenProject filename
```

## <a name="arguments"></a>自变量

`filename`

必需。 要打开的项目或解决方案的完整路径和文件名。

> [!NOTE]
> `filename` 参数的语法要求用引号将包含空格的路径括起来。

## <a name="remarks"></a>备注

键入内容时，自动完成功能会尝试查找正确的路径和文件名。

调试时此命令不可用。

## <a name="example"></a>示例

以下示例打开 Visual Basic 项目 Test1  ：

```cmd
>File.OpenProject "C:\My Projects\Test1\Test1.vbproj"
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)

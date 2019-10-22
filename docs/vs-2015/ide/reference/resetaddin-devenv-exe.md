---
title: -ResetAddin (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- disable addin
- addin state
- reset addin
ms.assetid: 9e339c8d-d768-4d86-8f45-2f479fc8255b
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9958e6e9a540dce1a405df8991780600b8f4a702
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665605"
---
# <a name="resetaddin-devenvexe"></a>/ResetAddin (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

移除与指定外接程序关联的命令和命令用户界面。

## <a name="syntax"></a>语法

```
Devenv /ResetAddin AddIn
```

## <a name="arguments"></a>自变量
 `AddIn`（可选）。 外接程序的命令名称。

## <a name="remarks"></a>备注
 默认情况下，外接程序的命令名称等于 *\<AddInSolutionName>* .Connect<em>.\<AddInSolutionName></em>，并在 Connect.cs 中显示为 `Exec` 方法的 `commandName` 参数。 还可以通过开始在 Visual Studio 的“命令”窗口中键入外接程序的名称并使用 Intellisense 填充其余部分来验证命令名称。

## <a name="example"></a>示例
 以下示例启动 Visual Studio 并阻止 `MyAddin` 外接程序在启动时运行。

```
Devenv.exe /ResetAddin MyAddin.Connect.MyAddin
```

## <a name="see-also"></a>另请参阅
 在 Visual Studio [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)[中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)

---
title: -RunExit (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- RunExit Devenv switch
- Devenv, /RunExit switch
- /RunExit Devenv switch
ms.assetid: bfc94875-5fc0-4110-b961-d59c0b403790
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3fa010e72267dadfb1974f7ce8be3b6b9a3e1cff
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935039"
---
# <a name="runexit-devenvexe"></a>/RunExit (devenv.exe)

编译和运行指定的项目或解决方案，然后关闭集成开发环境 (IDE)。

## <a name="syntax"></a>语法

```shell
devenv /RunExit {SolutionName|ProjectName} [/Out OutputFilename]
```

## <a name="arguments"></a>自变量

- *SolutionName*

  解决方案文件的完整路径和名称。

- *ProjectName*

  项目文件的完整路径和名称。

- `/Out` OutputFilename

  可选。 要将工具输出发送到的文件的文件名。 如果文件已有，工具将输出追加到文件末尾。

## <a name="remarks"></a>备注

根据为活动解决方案配置指定的设置编译并运行指定项目或解决方案。 此开关在项目或解决方案运行时最小化 IDE。 它在项目或解决方案完成运行后关闭 IDE。

- 用双引号将含有空格的字符串引起来。

- “命令”窗口或使用 `/Out` 开关指定的任何日志文件中都可显示摘要信息（包括错误）。

## <a name="example"></a>示例

此示例会在最小化的 IDE 中使用活动部署配置运行解决方案 `MySolution`，然后关闭 IDE。

```
devenv /runexit "%USERPROFILE%\source\repos\MySolution\MySolution.sln"
```

## <a name="see-also"></a>请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [/Run (devenv.exe)](../../ide/reference/run-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
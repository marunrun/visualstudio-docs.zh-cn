---
title: -Run (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /Run Devenv
- Run Devenv switch
- applications [Visual Studio], running
- /R Devenv switch
- Devenv, /Run switch
- R Devenv switch (/R)
ms.assetid: b1f22f9d-39a5-4918-8a2a-4b5c1e872665
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 051462339ea25dde9c2b55394e1854c60a71dc7e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747763"
---
# <a name="run-devenvexe"></a>/Run (devenv.exe)

编译并运行指定的项目或解决方案。

## <a name="syntax"></a>语法

```shell
devenv {/Run|/R} {SolutionName|ProjectName} [/Out OutputFilename]
```

## <a name="arguments"></a>自变量

- *SolutionName*

  解决方案文件的完整路径和名称。

- *ProjectName*

  项目文件的完整路径和名称。

- `/Out` OutputFilename 

  可选。 要将工具输出发送到的文件的文件名。 如果文件已有，工具将输出追加到文件末尾。

## <a name="remarks"></a>备注

根据为活动解决方案配置指定的设置编译并运行指定项目或解决方案。 此开关启动 IDE，并在项目或解决方案已完成运行后让它一直处于活动状态。

- 用双引号将含有空格的字符串引起来。

- “命令”窗口或使用 `/Out` 开关指定的任何日志文件中都可显示摘要信息（包括错误）  。

## <a name="example"></a>示例

该示例使用活动部署配置运行解决方案 `MySolution`。

```shell
devenv /run "%USERPROFILE%\source\repos\MySolution\MySolution.sln"
```

## <a name="see-also"></a>请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [/Runexit (devenv.exe)](../../ide/reference/runexit-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
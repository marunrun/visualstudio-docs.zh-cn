---
title: -Out (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio], builds
- Devenv, /Out switch
- builds [Visual Studio], logs
- error logs [Visual Studio], command-line build errors
- error logs [Visual Studio]
- /Out Devenv switch
- Out Devenv switch
- builds [Visual Studio], errors
- output files, build errors
ms.assetid: 9002d8c2-36d4-451c-b489-8f01932f31f7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cda81d37be0246c1181b4d82cbd17c3119b94437
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75568006"
---
# <a name="out-devenvexe"></a>/Out (devenv.exe)

指定用于在[运行](run-devenv-exe.md)、[运行和退出](runexit-devenv-exe.md)、[升级](upgrade-devenv-exe.md)、[生成](build-devenv-exe.md)、[重新生成](rebuild-devenv-exe.md)、[清理](clean-devenv-exe.md)或[部署](deploy-devenv-exe.md)解决方案时存储和显示错误的文件。

## <a name="syntax"></a>语法

```shell
devenv /Out FileName
```

## <a name="arguments"></a>参数

- *FileName*

  必需。 用于在生成可执行文件时接收输出的文件的路径和文件名。

## <a name="remarks"></a>备注

如果指定的文件名不存在，便会自动创建文件。 否则，如果已有文件，结果会追加到文件的现有内容中。

命令行生成错误显示在“命令”  窗口中，以及“输出”  窗口的“解决方案生成器”视图中。 此开关可用于查看无人参与生成的结果。

## <a name="example"></a>示例

此示例会运行 `MySolution`，并将错误写入文件 `MyErrorLog.txt` 中。

```shell
devenv /run "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /out "C:\MyErrorLog.txt"
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [/Run (devenv.exe)](../../ide/reference/run-devenv-exe.md)
- [/RunExit (devenv.exe)](runexit-devenv-exe.md)
- [/Upgrade (devenv.exe)](upgrade-devenv-exe.md)
- [/Clean (devenv.exe)](clean-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)

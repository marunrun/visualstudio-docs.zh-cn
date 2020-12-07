---
title: -Command (devenv.exe)
description: 了解如何使用 Command devenv 命令行开关在启动 Visual Studio IDE 后执行指定的命令。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /Command switch
- /Command Devenv switch
- Command Devenv switch
ms.assetid: 13c20cd6-f09d-400a-8b7b-ecc266a32cef
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bcfff93ac9cb4903c534c0d4d57387a5143b6b40
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040870"
---
# <a name="command-devenvexe"></a>/Command (devenv.exe)

在启动 Visual Studio IDE 后执行指定命令。

## <a name="syntax"></a>语法

```shell
devenv /Command CommandName
```

## <a name="arguments"></a>参数

CommandName

必需。 Visual Studio 命令或其别名的完整名称（放在双引号中）。 有关命令和别名语法的详细信息，请参阅 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)。

## <a name="remarks"></a>备注

启动完成后，IDE 将执行已命名的命令。

::: moniker range="vs-2017"

如果使用此开关，IDE 将不会在启动时显示起始页。

::: moniker-end

如果外接程序公开了某个命令，则可以使用此开关从命令行启动此外接程序。 有关详细信息，请参阅[如何：使用加载项管理器控制加载项](/previous-versions/xwdatdwh(v=vs.140))。

## <a name="example"></a>示例

第一个示例启动 Visual Studio，并自动运行宏“打开收藏夹文件”。

第二个示例在 IDE 内打开 Web 浏览选项卡，并转到 Microsoft Docs 站点。

第三个示例新建名为 `some_file.cs` 的文件，并在代码编辑器中打开它。

```shell
devenv /command "Macros.MyMacros.Module1.OpenFavoriteFiles"

devenv /command "navigate https://docs.microsoft.com/"

devenv /command "nf some_file.cs"
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
- [“命令”窗口](command-window.md)

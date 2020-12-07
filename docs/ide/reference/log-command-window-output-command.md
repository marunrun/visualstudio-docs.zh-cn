---
title: “日志命令窗口输出”命令
description: 了解 Log Command Window Output 命令，以及它如何将所有所有输入和输出从“命令”窗口复制到文件中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- tools.logcommandwindowoutput
helpviewer_keywords:
- log Command window output command
- View.LogCommandWindowOutput command
ms.assetid: d4ecec35-5af4-4954-8d60-2cd24583fbb4
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cab4f102832e8dfa6ce51b61abed8e3bfd672c40
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305267"
---
# <a name="log-command-window-output-command"></a>“日志命令窗口输出”命令

将“命令”窗口的所有输入和输出复制到文件中。

## <a name="syntax"></a>语法

```cmd
Tools.LogCommandWindowOutput [filename] [/on|/off] [/overwrite]
```

## <a name="arguments"></a>自变量

`filename`\
可选。 日志文件名。 默认情况下，该文件在用户的配置文件文件夹中创建。 如果该文件名已存在，将在该现有文件的末尾追加日志。 如果未指定文件，则使用上次指定的文件。 如果不存在以前的文件，则创建名称为 cmdline.log 的默认日志文件。

> [!TIP]
> 要更改日志文件的保存位置，请输入该文件的完整路径，如果该路径包含任何空格，请使用引号将路径引起。

## <a name="switches"></a>交换机

/on\
可选。 在指定文件中启动“命令”窗口的日志，并在文件中追加新信息。

/off\
可选。 停止“命令”窗口的日志。

/overwrite\
可选。 如果 `filename` 参数中指定的文件与现有文件匹配，该文件将会被覆盖。

## <a name="remarks"></a>备注

如果未指定任何文件，则默认创建文件 cmdline.log。 默认情况下，此命令的别名为 Log。

## <a name="examples"></a>示例

此示例创建新的日志文件 cmdlog 并启动命令日志。

```cmd
>Tools.LogCommandWindowOutput cmdlog
```

此示例停止日志记录命令。

```cmd
>Tools.LogCommandWindowOutput /off
```

此示例继续在以前使用的日志文件中记录命令。

```cmd
>Tools.LogCommandWindowOutput /on
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)

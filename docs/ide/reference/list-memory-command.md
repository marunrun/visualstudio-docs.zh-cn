---
title: “列出内存”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listmemory
helpviewer_keywords:
- Debug.ListMemory command
- ListMemory command
- list memory command
ms.assetid: a84de361-a6a6-4f6d-96aa-a0d4a424371e
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7bb92f3ac3420f146fdcd39b5925f7b3a517959a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748706"
---
# <a name="list-memory-command"></a>“列出内存”命令
显示指定范围内内存的内容。

## <a name="syntax"></a>语法

```cmd
Debug.ListMemory [/ANSI|Unicode] [/Count:number] [/Format:formattype]
[/Hex|Signed|Unsigned] [expression]
```

## <a name="arguments"></a>自变量
`expression`

可选。 从此处开始显示内存的内存地址。

## <a name="switches"></a>开关
/ANSI&#124;Unicode

可选。 将内存显示为对应于内存的字节的 ANSI 或 Unicode 字符。

/Count:`number`

可选。 确定要显示的内存的字节数，从 `expression` 开始。

/Format:`formattype`

可选。 查看“内存”窗口中的内存信息时使用的格式类型；可以为 OneByte、TwoBytes、FourBytes、EightBytes、Float（32 位）或 Double（64 位）  。 如果使用 OneByte，则 `/Unicode` 不可用。

/Hex&#124;Signed&#124;Unsigned

可选。 指定查看数字时使用的格式：有符号、无符号的或十六进制。

## <a name="remarks"></a>备注
不必写出带所有开关的完整“Debug.ListMemory”命令，可以使用某些开关预设为指定值的预定义别名调用该命令  。 例如，不必输入：

```cmd
>Debug.ListMemory /Format:float /Count:30 /Unicode
```

可写入：

```cmd
>df /Count:30 /Unicode
```

下面是 Debug.ListMemory 命令的可用别名列表  ：

|Alias|命令和开关|
|-----------| - |
|**d**|Debug.ListMemory|
|**da**|Debug.ListMemory /Ansi|
|**db**|Debug.ListMemory /Format:OneByte|
|**dc**|Debug.ListMemory /Format:FourBytes /Ansi|
|**dd**|Debug.ListMemory /Format:FourBytes|
|**df**|Debug.ListMemory /Format:Float|
|**dq**|Debug.ListMemory /Format:EightBytes|
|**du**|Debug.ListMemory /Unicode|

## <a name="example"></a>示例

```cmd
>Debug.ListMemory /Format:float /Count:30 /Unicode
```

## <a name="see-also"></a>请参阅

- [“列出调用堆栈”命令](../../ide/reference/list-call-stack-command.md)
- [“列出线程”命令](../../ide/reference/list-threads-command.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
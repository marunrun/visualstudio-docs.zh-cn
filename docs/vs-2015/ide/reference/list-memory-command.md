---
title: “列出内存”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listmemory
helpviewer_keywords:
- Debug.ListMemory command
- ListMemory command
- list memory command
ms.assetid: a84de361-a6a6-4f6d-96aa-a0d4a424371e
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2630402e03d1256f63e542818a9066745206d2c5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672751"
---
# <a name="list-memory-command"></a>“列出内存”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

显示指定范围内内存的内容。

## <a name="syntax"></a>语法

```
Debug.ListMemory [/ANSI|Unicode] [/Count:number] [/Format:formattype]
[/Hex|Signed|Unsigned] [expression]
```

## <a name="arguments"></a>自变量
 `expression`（可选）。 从此处开始显示内存的内存地址。

## <a name="switches"></a>开关
 /ANSI&#124;Unicode 可选。 将内存显示为对应于内存的字节的 ANSI 或 Unicode 字符。

 /Count： `number` 可选。 确定要显示的内存的字节数，从 `expression` 开始。

 /Format： `formattype` 可选。 查看“内存”窗口中的内存信息时使用的格式类型；可以为 OneByte、TwoBytes、FourBytes、EightBytes、Float（32 位）或 Double（64 位）  。 如果使用 OneByte，则 `/Unicode` 不可用。

 /Hex&#124;有&#124;符号无符号可选。 指定查看数字时使用的格式：有符号、无符号的或十六进制。

## <a name="remarks"></a>备注
 不必写出带所有开关的完整“Debug.ListMemory”命令，可以使用某些开关预设为指定值的预定义别名调用该命令  。 例如，不必输入：

```
>Debug.ListMemory /Format:float /Count:30 /Unicode
```

 可写入：

```
>df /Count:30 /Unicode
```

 下面是 Debug.ListMemory 命令的可用别名列表  ：

|Alias|命令和开关|
|-----------|--------------------------|
|**d**|Debug.ListMemory|
|**da**|Debug.ListMemory /Ansi|
|**db**|Debug.ListMemory /Format:OneByte|
|**dc**|Debug.ListMemory /Format:FourBytes /Ansi|
|**dd**|Debug.ListMemory /Format:FourBytes|
|**df**|Debug.ListMemory /Format:Float|
|**dq**|Debug.ListMemory /Format:EightBytes|
|**du**|Debug.ListMemory /Unicode|

## <a name="example"></a>示例

```
>Debug.ListMemory /Format:float /Count:30 /Unicode
```

## <a name="see-also"></a>另请参阅
 [列出调用堆栈命令](../../ide/reference/list-call-stack-command.md)[列表线程命令](../../ide/reference/list-threads-command.md) [visual studio 命令](../../ide/reference/visual-studio-commands.md)[命令窗口](../../ide/reference/command-window.md)[查找/命令框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)

---
title: “列出反汇编”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listdisassembly
helpviewer_keywords:
- Debug.ListDisassembly command
- list disassembly command
ms.assetid: eb363e35-e86a-4121-966f-991210c27e2a
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8ff5e620d4c53889afe17274364d6f92936025d3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672742"
---
# <a name="list-disassembly-command"></a>“列出反汇编”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

开始调试进程，并允许指定如何处理错误。

## <a name="syntax"></a>语法

```
Debug.ListDisassembly [/count:number] [/endaddress:expression]
[/codebytes:yes|no] [/source:yes|no] [/symbolnames:yes|no]
[/linenumbers:yes|no]
```

## <a name="switches"></a>开关
 每个开关都可以使用其完整形式或缩写形式来调用。

 /count： `number` [或]/c： `number` [或]/length： `number` [或]/l： `number` 可选。 要显示的指令数。 默认值为 8。

 /endaddress： `expression` [或]/e： `expression` 可选。 停止反汇编的地址。

 /codebytes： `yes`&#124; `no` [或]/bytes： `yes`&#124; `no` [或]/B： `yes`&#124; `no` Optional。 指示是否显示代码字节。 默认值是 `no`。

 /source： `yes`&#124; `no` [或]/s： `yes`&#124; `no` 可选。 指示是否显示源代码。 默认值是 `no`。

 /symbolnames： `yes`&#124; `no` [或]/names： `yes`&#124; `no` [或]/N： `yes`&#124; `no` Optional。 指示是否显示符号名称。 默认值是 `yes`。

 [/linenumbers： `yes`&#124; `no`]可有可无. 启用查看与源代码关联的行号。 /source 开关必须具有 `yes` 的值来使用 /linenumbers 开关。

## <a name="example"></a>示例

```
>Debug.ListDisassembly
```

## <a name="see-also"></a>另请参阅
 [列出调用堆栈命令](../../ide/reference/list-call-stack-command.md)[列表线程命令](../../ide/reference/list-threads-command.md) [visual studio 命令](../../ide/reference/visual-studio-commands.md)[命令窗口](../../ide/reference/command-window.md)[查找/命令框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)

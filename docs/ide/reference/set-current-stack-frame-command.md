---
title: “设置当前堆栈帧”命令
description: 了解“设置当前堆栈帧”命令以及如何通过它设置特定堆栈帧。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setcurrentstackframe
helpviewer_keywords:
- Set Current Stack Frame command
- Debug.SetCurrentStackFrame command
ms.assetid: 3dcf52c0-6781-4598-bac2-0094dce67c20
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 032602744247ded5cb38d8a3ae3e1157ccbc5cee
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2020
ms.locfileid: "96616598"
---
# <a name="set-current-stack-frame-command"></a>“设置当前堆栈帧”命令
允许设置特定堆栈帧。

## <a name="syntax"></a>语法

```cmd
Debug.SetCurrentStackFrame index
```

## <a name="arguments"></a>自变量
`index`

必需。 通过其索引选择堆栈帧。

## <a name="example"></a>示例

```cmd
>Debug.SetCurrentStackFrame 1
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
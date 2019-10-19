---
title: “监视”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.watch
helpviewer_keywords:
- Watch command
- Debug.Watch command
ms.assetid: aa02e647-d9f5-4905-a651-52a8df595795
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 18e585064bb50db7a0497c6b96e428a662e953ab
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72604836"
---
# <a name="watch-command"></a>“监视”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建并打开指定“监视”  窗口的实例。 可使用“监视”窗口计算变量、表达式或寄存器的值，然后编辑这些值并保存结果  。

## <a name="syntax"></a>语法

```
Debug.Watch[index]
```

## <a name="arguments"></a>自变量
 `index`（必需）。 监视窗口的实例数。

## <a name="remarks"></a>备注
 `index` 必须为整数。 有效值为 1、2、3 或 4。

## <a name="example"></a>示例

```
>Debug.Watch1
```

## <a name="see-also"></a>另请参阅
 "自动"[和 "局部变量](../../debugger/autos-and-locals-windows.md) [" 窗口如何：在变量窗口中编辑值](https://msdn.microsoft.com/library/36f464ab-c900-4c0b-9ab3-557b3d9cdab5)[如何：使用 "快速监视" 对话框](https://msdn.microsoft.com/library/ffaee1dd-e5ce-4ef2-9401-d28329398867) [visual studio 命令](../../ide/reference/visual-studio-commands.md)"[命令窗口](../../ide/reference/command-window.md)" "[查找/命令" 框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)

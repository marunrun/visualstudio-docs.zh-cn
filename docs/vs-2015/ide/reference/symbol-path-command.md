---
title: “符号路径”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.symbolpath
helpviewer_keywords:
- symbol path command
- Debug.SymbolPath command
- SymbolPath command
ms.assetid: b697ef2d-3f5d-40df-b113-7068a5bec0d4
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9d02d4cfede6ed3499d09ff58e4454c1ef9cbe0d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651008"
---
# <a name="symbol-path-command"></a>“符号路径”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置调试器的目录列表，以搜索符号。

## <a name="syntax"></a>语法

```
Debug.SymbolPath pathname1;pathname2;... pathnameN
```

## <a name="arguments"></a>参数
 `pathname`（可选）。 调试器路径列表的分号分隔列表，用于搜索符号。

## <a name="remarks"></a>备注
 如果没有指定 `pathname`，该命令将列出当前符号路径。

## <a name="example"></a>示例
 该示例向符号目录的列表添加两条路径。

```
Debug.SymbolPath C:\Symbol Path 1;C:\Symbol Path 2
```

## <a name="example"></a>示例
 该示例显示当前符号路径的分号分隔列表。

```
Debug.SymbolPath
```

## <a name="see-also"></a>另请参阅
 [命令窗口](../../ide/reference/command-window.md) [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)

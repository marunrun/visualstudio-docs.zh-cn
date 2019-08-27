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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 27c4c8ac23e2524245107d9052642350e9db09d2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163270"
---
# <a name="symbol-path-command"></a>“符号路径”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置调试器的目录列表，以搜索符号。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.SymbolPath pathname1;pathname2;... pathnameN  
```  
  
## <a name="arguments"></a>自变量  
 `pathname`  
 可选。 调试器路径列表的分号分隔列表，用于搜索符号。  
  
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
 [“命令”窗口](../../ide/reference/command-window.md)   
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)

---
title: “列出线程”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listthreads
helpviewer_keywords:
- ListThreads command
- list threads command
- Debug.ListThreads command
ms.assetid: 34b665c0-d46f-4c1a-a066-b678eba5ac54
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 90aff3fb3d3cbb596708bde1db8ff171198a5a60
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199106"
---
# <a name="list-threads-command"></a>“列出线程”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

显示当前程序中线程的列表。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.ListThreads [index]  
```  
  
## <a name="arguments"></a>自变量  
 `index`  
 可选。 通过索引来选择要用作当前线程的线程。  
  
## <a name="remarks"></a>备注  
 如果已指定，`index` 实际参数将指示的线程标记为当前线程。 星号 (*) 显示在当前线程旁边的列表中。  
  
## <a name="example"></a>示例  
  
```  
>Debug.ListThreads   
```  
  
## <a name="see-also"></a>另请参阅  
 [“列出调用堆栈”命令](../../ide/reference/list-call-stack-command.md)   
 [“列出反汇编”命令](../../ide/reference/list-disassembly-command.md)   
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

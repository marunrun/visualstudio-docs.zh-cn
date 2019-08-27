---
title: 设置当前进程 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Debug.SetCurrentProcess command
- Set Current Process command
ms.assetid: 1e016ebd-aadd-411f-a606-03bf69d3f8aa
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ed19c5b95351f8e9c34255a915fc6a446800f761
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163345"
---
# <a name="set-current-process"></a>设置当前进程
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将指定的进程设置为调试器中的活动进程。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.SetCurrentProcess index  
```  
  
## <a name="arguments"></a>自变量  
 `index`  
 必需。 进程的索引。  
  
## <a name="remarks"></a>备注  
 调试时可以附加到多个进程，但在任何给定时间，调试器中只有一个进程处于活动状态。 可以使用 `SetCurrentProcess` 命令设置活动进程。  
  
## <a name="example"></a>示例  
  
```  
>Debug.SetCurrentProcess 1  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

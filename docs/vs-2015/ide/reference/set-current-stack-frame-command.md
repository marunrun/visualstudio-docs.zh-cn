---
title: “设置当前堆栈帧”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.setcurrentstackframe
helpviewer_keywords:
- Set Current Stack Frame command
- Debug.SetCurrentStackFrame command
ms.assetid: 3dcf52c0-6781-4598-bac2-0094dce67c20
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 87d830e492420844de72a2cd34dbea336e365dfd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163356"
---
# <a name="set-current-stack-frame-command"></a>“设置当前堆栈帧”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

允许设置特定堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.SetCurrentStackFrame index  
```  
  
## <a name="arguments"></a>自变量  
 `index`  
 必需。 通过其索引选择堆栈帧。  
  
## <a name="example"></a>示例  
  
```  
>Debug.SetCurrentStackFrame 1  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

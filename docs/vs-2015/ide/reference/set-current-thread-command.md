---
title: “设置当前线程”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.setcurrentthread
helpviewer_keywords:
- Set Current Thread command
- Debug.SetCurrentThread command
ms.assetid: 9917ed1d-6c30-4d94-b2f0-69acce74f1b2
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 107303082202cb1dbb162ef9dfb845c2f6564df4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163335"
---
# <a name="set-current-thread-command"></a>“设置当前线程”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将指定的线程设置为当前线程。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.SetCurrentThread index  
```  
  
## <a name="arguments"></a>自变量  
 `index`  
 必需。 按线程的索引选择线程。  
  
## <a name="example"></a>示例  
  
```  
>Debug.SetCurrentThread 1  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

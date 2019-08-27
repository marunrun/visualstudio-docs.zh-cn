---
title: “转到”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- edit.goto
helpviewer_keywords:
- Debug.Goto command
- Go To command
ms.assetid: 201e1dd2-6701-467d-8cc1-faec2ef20511
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 010d2c395d77be590b3d8d3bc26fc83aaa63adfa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199263"
---
# <a name="go-to-command"></a>“转到”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将光标移到指定的行。  
  
## <a name="syntax"></a>语法  
  
```  
Edit.GoTo [linenumber]  
```  
  
## <a name="arguments"></a>自变量  
 `linenumber`  
 可选。 一个表示要转到的行号的整数。  
  
## <a name="remarks"></a>备注  
 行号从 1 开始。 如果 `linenumber` 的值小于 1，则显示第一行。 如果 `linenumber` 的值大于最后一行的行号，则显示最后一行。  
  
 如果未指定 `linenumber` 的值，则显示“转到行”对话框  。  
  
 此命令的别名为 GoToLn。  
  
## <a name="example"></a>示例  
  
```  
>Edit.GoTo 125  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

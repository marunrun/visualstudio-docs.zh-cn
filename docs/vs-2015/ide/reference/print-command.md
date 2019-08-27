---
title: Print 命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.print
helpviewer_keywords:
- Debug.Print command
- Print method
- Print command
ms.assetid: 0412d381-590a-483f-bab4-6e1cca095645
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 65d78387c6d60d0b432db9aab175fbfe8dc2869b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203564"
---
# <a name="print-command"></a>Print 命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

计算表达式或显示指定文本。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.Print text  
```  
  
## <a name="arguments"></a>自变量  
 `text`  
 必需。 要计算的表达式或要显示的文本。  
  
## <a name="remarks"></a>备注  
 可使用问号 (?) 作为此命令的别名。 例如，命令  
  
```  
>Debug.Print expA  
```  
  
 也可写作  
  
```  
>? expA  
```  
  
 此命令的这两个版本都将返回表达式 `expA` 的当前值。  
  
## <a name="example"></a>示例  
  
```  
>Debug.Print varA  
```  
  
## <a name="see-also"></a>另请参阅  
 [计算机语句命令](../../ide/reference/evaluate-statement-command.md)   
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

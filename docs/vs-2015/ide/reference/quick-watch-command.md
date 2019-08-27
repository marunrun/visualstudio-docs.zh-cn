---
title: “快速监视”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.quickwatch
helpviewer_keywords:
- Quick Watch command
- Debug.Quickwatch command
ms.assetid: 9670ac3a-8f2f-4874-974d-cb87d3b0cde1
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c9ac805ebea19604343d561bf553448fff2ca575
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701749"
---
# <a name="quick-watch-command"></a>“快速监视”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在[“快速监视”](https://msdn.microsoft.com/library/ffaee1dd-e5ce-4ef2-9401-d28329398867)对话框的“表达式”字段中显示选定或指定的文本。 可使用此对话框计算调试器所识别的变量或表达式的当前值或计算寄存器的内容。 此外，可更改任何非常量变量的值或任何寄存器的内容。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.QuickWatchq [text]  
```  
  
## <a name="arguments"></a>自变量  
 `text`  
 可选。 要添加到“快速监视”对话框的文本。  
  
## <a name="remarks"></a>备注  
 如果忽略了 `text`，则光标处当前选中的文本或字词将添加到“监视”窗口。  
  
## <a name="example"></a>示例  
  
```  
>Debug.QuickWatch  
```  
  
## <a name="see-also"></a>请参阅  
 [如何：使用“快速监视”对话框](https://msdn.microsoft.com/library/ffaee1dd-e5ce-4ef2-9401-d28329398867)   
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

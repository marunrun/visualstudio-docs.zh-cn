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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 537b3f45dcf22dcc766b9902d20bf97af24b3c9d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65675514"
---
# <a name="watch-command"></a>“监视”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建并打开指定“监视”  窗口的实例。 可使用“监视”窗口计算变量、表达式或寄存器的值，然后编辑这些值并保存结果。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.Watch[index]  
```  
  
## <a name="arguments"></a>自变量  
 `index`  
 必需。 监视窗口的实例数。  
  
## <a name="remarks"></a>备注  
 `index` 必须为整数。 有效值为 1、2、3 或 4。  
  
## <a name="example"></a>示例  
  
```  
>Debug.Watch1  
```  
  
## <a name="see-also"></a>请参阅  
 [“自动”和“局部变量”窗口](../../debugger/autos-and-locals-windows.md)   
 [如何：在“变量”窗口中编辑值](https://msdn.microsoft.com/library/36f464ab-c900-4c0b-9ab3-557b3d9cdab5)   
 [如何：使用“快速监视”对话框](https://msdn.microsoft.com/library/ffaee1dd-e5ce-4ef2-9401-d28329398867)   
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

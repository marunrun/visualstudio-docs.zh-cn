---
title: “列出源”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- Debug.ListSource
helpviewer_keywords:
- Debug.ListSource command
- list source command
- ListSource command
ms.assetid: e45f08d2-f4a3-49c3-9452-aa60508e2f74
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e0a4a8482dc1c2c66a45902f2f3382b179b46b13
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199127"
---
# <a name="list-source-command"></a>“列出源”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

显示源代码的指定行。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.ListSource [/Count:number] [/Current] [/File:filename]  
[/Line:number] [/ShowLineNumbers:yes|no]  
```  
  
## <a name="switches"></a>开关  
 /Count:`number`  
 可选。 指定要显示的行的编号。  
  
 /Current  
 可选。 显示当前行。  
  
 /File:`filename`  
 可选。 要显示的文件的路径。 如果未指定文件名，该命令会显示当前语句所在行的源代码。  
  
 /Line:`number`  
 可选。 显示特定行号。  
  
 /ShowLineNumbers:`yes|no`  
 可选。 指定是否显示行号。  
  
## <a name="remarks"></a>备注  
  
## <a name="example"></a>示例  
 此示例列出文件 Form1.vb 第 4 行的源代码，并显示行号。  
  
```  
Debug.ListSource /File:"C:\Visual Studio Projects\Form1.vb" /Line:4 /ShowLineNumbers:yes  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)

---
title: “列出模块”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listmodules
helpviewer_keywords:
- Debug.ListModules command
- ListModules command
- list modules command
ms.assetid: 3cb73774-6ac0-43b2-b781-75ed47175bfd
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7d24b081c20b5874d6daa57832136023ac678c0f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199149"
---
# <a name="list-modules-command"></a>“列出模块”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

列出当前进程的模块。  
  
## <a name="syntax"></a>语法  
  
```  
Debug.ListModules [/Address:yes|no] [/Name:yes|no] [/Order:yes|no]  
[/Path:yes|no] [/Process:yes|no] [/SymbolFile:yes|no]  
[/SymbolStatus:yes|no] [/Timestamp:yes|no] [/Version:yes|no]  
```  
  
#### <a name="parameters"></a>参数  
 /Address:`yes|no`  
 可选。 指定是否显示模块的内存地址。 默认值是 `yes`。  
  
 /Name:`yes|no`  
 可选。 指定是否显示模块的名称。 默认值是 `yes`。  
  
 /Order:`yes|no`  
 可选。 指定是否显示模块的顺序。 默认值是 `no`。  
  
 /Path:`yes|no`  
 可选。 指定是否显示模块的路径。 默认值是 `yes`。  
  
 /Process:`yes|no`  
 可选。 指定是否显示模块的进程。 默认值是 `no`。  
  
 /SymbolFile:`yes|no`  
 可选。 指定是否显示模块的符号文件。 默认值是 `no`。  
  
 /SymbolStatus:`yes|no`  
 可选。 指定是否显示模块的符号状态。 默认值是 `yes`。  
  
 /Timestamp:`yes|no`  
 可选。 指定是否显示模块的时间戳。 默认值是 `no`。  
  
 /Version:`yes|no`  
 可选。 指定是否显示模块的版本。 默认值是 `no`。  
  
## <a name="remarks"></a>备注  
  
## <a name="example"></a>示例  
 此示例列出模块名称、地址和当前进程的时间戳。  
  
```  
Debug.ListModules /Address:yes /Name:yes /Order:no /Path:no /Process:no /SymbolFile:no /SymbolStatus:no /Timestamp:yes /Version:no  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [如何：使用“模块”窗口](../../debugger/how-to-use-the-modules-window.md)

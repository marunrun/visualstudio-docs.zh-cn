---
title: “日志命令窗口输出”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- tools.logcommandwindowoutput
helpviewer_keywords:
- log Command window output command
- View.LogCommandWindowOutput command
ms.assetid: d4ecec35-5af4-4954-8d60-2cd24583fbb4
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a05fe75aabaf2ce04010fe0c985a3cc1645ee696
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446027"
---
# <a name="log-command-window-output-command"></a>“日志命令窗口输出”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将“命令”窗口的所有输入和输出复制到文件中。  
  
## <a name="syntax"></a>语法  
  
```  
Tools.LogCommandWindowOutput [filename] [/on|/off] [/overwrite]  
```  
  
## <a name="arguments"></a>自变量  
 `filename`  
 可选。 日志文件的名称。 默认情况下，该文件在用户的配置文件文件夹中创建。 如果该文件名已存在，将在该现有文件的末尾追加日志。 如果未指定文件，则使用上次指定的文件。 如果不存在以前的文件，则创建名称为 cmdline.log 的默认日志文件。  
  
> [!TIP]
> 要更改日志文件的保存位置，请输入该文件的完整路径，如果该路径包含任何空格，请使用引号将路径引起。  
  
## <a name="switches"></a>开关  
 /on  
 可选。 在指定文件中启动“命令”窗口的日志，并在文件中追加新信息。  
  
 /off  
 可选。 停止“命令”窗口的日志。  
  
 /overwrite  
 可选。 如果 `filename` 参数中指定的文件与现有文件匹配，该文件将会被覆盖。  
  
## <a name="remarks"></a>备注  
 如果未指定任何文件，则默认创建文件 cmdline.log。 默认情况下，此命令的别名为 Log。  
  
## <a name="examples"></a>示例  
 此示例创建新的日志文件 cmdlog 并启动命令日志。  
  
```  
>Tools.LogCommandWindowOutput cmdlog  
```  
  
 此示例停止日志记录命令。  
  
```  
>Tools.LogCommandWindowOutput /off  
```  
  
 此示例继续在以前使用的日志文件中记录命令。  
  
```  
>Tools.LogCommandWindowOutput /on  
```  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

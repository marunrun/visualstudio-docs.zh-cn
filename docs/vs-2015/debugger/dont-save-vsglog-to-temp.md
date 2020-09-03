---
title: DONT_SAVE_VSGLOG_TO_TEMP | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: f27ab0e6-9575-4ca0-9901-37d3e5c3a2f5
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 449c6c1ecdb0644b9b52b6ec12ce867dc34d66c4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156102"
---
# <a name="dont_save_vsglog_to_temp"></a>DONT_SAVE_VSGLOG_TO_TEMP
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过其存在定义图形日志文件是否保存到用户的临时文件目录。  
  
## <a name="syntax"></a>语法  
  
```cpp  
#define DONT_SAVE_VSGLOG_TO_TEMP  
```  
  
## <a name="value"></a>“值”  
 一个预处理器符号，根据其是否存在来确定是否将图形日志文件保存到用户的临时文件目录中。 如果定义了此符号，则 `VSG_DEFAULT_RUN_FILENAME` 定义的文件名相对于捕获的应用的当前目录，或为绝对路径；否则，`VSG_DEFAULT_RUN_FILENAME` 定义的文件名相对于用户的临时文件目录，且不能是绝对路径。  
  
## <a name="remarks"></a>备注  
 根据用户权限的不同，可能无法将图形日志文件保存到任意位置。 如果不确定用户是否可以写入到你选择的位置，建议你最好将图形日志保存到用户的临时文件目录或其他已知良好的位置。  
  
 若要防止将图形日志文件保存到临时文件目录，必须在包含 `vsgcapture.h` 之前定义 `DONT_SAVE_VSGLOG_TO_TEMP`。  
  
## <a name="example"></a>示例  
 此示例展示如何将图形日志文件保存到主机计算机上的绝对路径。  
  
```  
// Define DONT_SAVE_VSGLOG_TO_TEMP and VSG_DEFAULT_RUN_FILENAME before including vsgcapture.h  
#define DONT_SAVE_VSGLOG_TO_TEMP  
#define VSG_DEFAULT_RUN_FILENAME L"C:\\Graphics Diagnostics Captures\\default.vsglog"  
  
#include <vsgcapture.h>  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSG_DEFAULT_RUN_FILENAME](../debugger/vsg-default-run-filename.md)

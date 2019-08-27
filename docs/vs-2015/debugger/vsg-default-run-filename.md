---
title: VSG_DEFAULT_RUN_FILENAME | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: ea549d2f-c857-458c-93c7-bc5a2d11d15d
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2980d34028c58a6abadb2df21bf22c8d37cda6e0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160763"
---
# <a name="vsgdefaultrunfilename"></a>VSG_DEFAULT_RUN_FILENAME
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

定义图形日志文件的默认文件名。  
  
## <a name="syntax"></a>语法  
  
```cpp  
#define VSG_DEFAULT_FILENAME filename  
```  
  
#### <a name="parameters"></a>参数  
 `filename`  
 以编程方式捕获图形信息时默认为图形日志文件指定的文件名。  
  
## <a name="value"></a>值  
 表示图形日志文件的文件名的字符串。 默认情况下为 L"default.vsglog"。  
  
```cpp  
#define VSG_DEFAULT_FILENAME L"default.vsglog"  
```  
  
## <a name="remarks"></a>备注  
 如果定义预处理器符号 `DONT_SAVE_VSGLOG_TO_TEMP`，则文件名与捕获的应用的当前目录相关，或为绝对路径；否则，它与用户的临时文件目录相关，且不能是绝对路径。  
  
 若要更改定义的文件名称，则必须重新定义其包括在内之前`vsgcapture.h`在程序中。  
  
## <a name="example"></a>示例  
 此示例说明如何更改捕获文件的默认文件名：  
  
```cpp  
// Redefine the default capture filename before including vsgcapture.h  
#define VSG_DEFAULT_FILENAME L"capture.vsglog"  
  
#include <vsgcapture.h>  
```  
  
## <a name="see-also"></a>请参阅  
 [DONT_SAVE_VSGLOG_TO_TEMP](../debugger/dont-save-vsglog-to-temp.md)
